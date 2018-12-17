#使用update-cache进行AMP内容更新(Update AMP Content with update-cache request)

有时候我们会遇到页面需要及时更新或者删除，例如新闻发布，节日活动这样的实时性相对较高的页面，AMP Cache服务器不一定能够相对及时地进行页面更新或者删除，那么，我们就需要使用到缓存更新(update-cache)这样来处理一些问题了。

####基本步骤如下: 

1. 生成一对公钥以及私钥。(Generate a pair of RSA keys)
2. 将公钥(public-key.pem)改名为apikey.pub, 放到服务器中例如以下的结构中: https://example.com/.well-known/amphtml/apikey.pub, 并且response type为"text/plain;charset=UTF-8"。（Rename the public key as apikey.pub, and post the public key on the domain to be refreshed at the following location: "https://example.com/.well-known/amphtml/apikey.pub"）
3. 使用私钥对想要更新的页面进行签名加密并且发送http请求AMP Cache服务器进行AMP页面的更新.(Sign the AMP url and send the request using http to make a update on AMP Cache Server.)


####了解基本步骤之后，我们就可以进行实践了，选择你熟悉的编程语言进行AMP update-cache代码的编码。
* [使用PHP进行AMP内容更新(Update AMP Content using PHP)](./amp-update-cache-php.md).
* [使用Linux Shell进行AMP内容更新(Update AMP Content using Linux Shell)](./amp-update-cache-linux-shell.md).
* [使用Python进行AMP内容更新(Update AMP Content using Python)](./amp-update-cache-python.md)
* 如果需要Node版的，可以参考AMP官网的[AMP update-cache Demo](https://github.com/ampproject/samples/tree/master/amp-update-cache)



