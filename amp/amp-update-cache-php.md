#使用PHP进行AMP内容更新(Update AMP Content using PHP)

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

举个栗子: 假如我们要更新的页面是: amptest-58188.appspot.com/delete.html,那么可以根据下面的教程来进行。如果需要Node版的，可以参考AMP官网的[AMP update-cache Demo](https://github.com/ampproject/samples/tree/master/amp-update-cache)

* **第一步**:将私钥粘贴到跟PHP文件同一个文件夹中，

![Image](../../resource/img/amp-cache-update-php-structure.png)


* **第二步**: 直接粘贴下面的代码，修改下面中的$ampBaseUrl还有signatureUrl为你自己的url地址即可进行AMP页面的更新或者删除。如果不知道怎么拼接，进入到[ampbyexample中输入url地址获取AMP页面地址](https://ampbyexample.com/advanced/using_the_google_amp_cache/)。


````
<?php

function urlsafe_b64encode($string) {
    return str_replace(array('+','/','='),array('-','_',''), base64_encode($string));
}
$timestamp=time();
$ampBaseUrl = "https://amptest--58188-appspot-com.cdn.ampproject.org";
$signatureUrl = '/update-cache/c/s/amptest-58188.appspot.com/delete.html?amp_action=flush&amp_ts='.$timestamp;

// 打开私钥(opening the private key)
$pkeyid = openssl_pkey_get_private("file://private-key.pem");
// 使用私钥（private key）进行签名(generating the signature)
openssl_sign($signatureUrl, $signature, $pkeyid, OPENSSL_ALGO_SHA256);
openssl_free_key($pkeyid);

// 对签名进行urlsafe base64编码(useurlsafe_b64encode to encode the signature)
$urlsafe_signature = urlsafe_b64encode($signature);
$ampUrl = $ampBaseUrl.$signatureUrl."&amp_url_signature=".$urlsafe_signature;

// 输出请求的地址
echo 'Update url: '.$ampUrl."\n";

//进行get请求AMP页面进行更新
$ch = curl_init();
$timeout = 5;
curl_setopt ($ch, CURLOPT_URL, $ampUrl);
curl_setopt ($ch, CURLOPT_RETURNTRANSFER, 1);
curl_setopt ($ch, CURLOPT_CONNECTTIMEOUT, $timeout);
$file_contents = curl_exec($ch);
curl_close($ch);
 
// 返回请求结果
echo 'Update result: '.$file_contents;
?>

````

* **第三步**: 请求PHP页面地址并且查看结果，如图: 

![Image](../../resource/img/amp-update-cache-php-result.png)

附: 

测试地址以及测试地址的公私钥:

1. 测试地址: https://amptest-58188.appspot.com/delete.html

2. 公钥: https://amptest-58188.appspot.com/.well-known/amphtml/apikey.pub

3. 私钥: https://amptest-58188.appspot.com/.well-known/amphtml/privatekey.pem

假如你不想做那么多步骤，那么你可以直接拿着私钥到[AMP update-cache request](https://amp-cache-refresh.appspot.com/)直接生成想要更新AMP页面的地址，并且请求即可。