#使用Linux Shell进行AMP内容更新(Update AMP Content using Linux Shell)

1. 生成一对公钥以及私钥。(Generate a pair of RSA keys)
2. 将公钥改名为apikey.pub, 放到服务器中例如以下的结构中: https://example.com/.well-known/amphtml/apikey.pub, 并且response type为"text/plain;charset=UTF-8"。（Rename the public key as apikey.pub, and post the public key on the domain to be refreshed at the following location: "https://example.com/.well-known/amphtml/apikey.pub"）
3. 使用私钥对想要更新的页面进行签名加密并且发送http请求AMP Cache服务器进行AMP页面的更新.(Sign the AMP url and send the request using http to make a update on AMP Cache Server.)

##1. 生成一对公钥以及私钥

````
// 生成私钥
openssl genrsa 2048 > private-key.pem

// 生成公钥
openssl rsa -in private-key.pem -pubout >public-key.pem
````

应该会得出来一对公钥和私钥，如图：

![Image](../../resource/img/publickey.png)
![Image](../../resource/img/privatekey.png)


##2. 将公钥(public-key.pem)改名为apikey.pub, 放到服务器中例如以下的结构中


````
// 对公钥(public-key.pem)进行重命名
mv public-key.pem apikey.pub
````

将apikey.pub放到服务器上面的文件夹下(/.well-known/amphtml/apikey.pub)，在浏览器端访问后得到如图的结果: 

![Image](../../resource/img/publickey-on-server.png)

##3. 使用私钥对想要更新的页面进行加密并且发送http请求AMP Cache服务器进行AMP页面的更新

举个栗子: 假如我们要更新的页面是: amptest-58188.appspot.com/delete.html,那么可以根据下面的教程来进行。

* **第一步**: 
 
````
// 说明: 使用私钥(private key)对amp url进行签名，最后拼接成可以携带所需字段的url。
echo -n >url.txt '/update-cache/c/s/amptest-58188.appspot.com/delete.html?amp_action=flush&amp_ts='`date +%s` && cat url.txt | openssl dgst -sha256 -sign private-key.pem>signature.bin | openssl base64 | tr -- '+/=' '-_ '  >> sign.txt && echo "&amp_url_signature=" >> url.txt && cat sign.txt >> url.txt && rm sign.txt && cat  url.txt

// 参数说明: amp_action一般为flush，代表我们需要对AMP页面进行更新, amp_ts是当前系统的时间戳， amp_url_signature为使用private key对amp url进行签名后的websafe base64编码,想要了解更多可参考[缓存参数(update cache parameters)](https://developers.google.com/amp/cache/update-cache#parameters)
````

结果如下图: 

![Image](../../resource/img/update-cache-linux-shell.png)


* **第二步**: 接着我们就去查询需要更新的AMP Cache服务器，这个步骤是用来了解我们要更新哪个服务器上面的缓存，可以用[caches.json](https://cdn.ampproject.org/caches.json)进行查询，一般我们都选下图的第一个服务器。

![Image](../../resource/img/update-cahce-json.png)

* **第三步**: 一般我们会选择上图第一个AMP Cache服务器进行拼接url, 拼接后请求如下图：
![Image](../../resource/img/amp-update-cache-linux-request.png)

如果服务器返回如图中ok的相应，那么证明我们请求update cache成功了。

附: 

测试地址以及测试地址的公私钥:

1. 测试地址: https://amptest-58188.appspot.com/delete.html
 
2. 公钥: https://amptest-58188.appspot.com/.well-known/amphtml/apikey.pub

3. 私钥: https://amptest-58188.appspot.com/.well-known/amphtml/privatekey.pem

假如你不想做那么多步骤，那么你可以直接拿着私钥到[AMP update-cache request](https://amp-cache-refresh.appspot.com/)直接生成想要更新AMP页面的地址，并且请求即可。