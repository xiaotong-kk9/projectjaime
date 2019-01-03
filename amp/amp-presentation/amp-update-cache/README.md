# AMP缓存更新\(AMP update cache\)

有时候我们会遇到页面需要及时更新或者删除，例如新闻发布，节日活动这样的实时性相对较高的页面，AMP Cache服务器不一定能够相对及时地进行页面更新或者删除，那么，我们就需要使用到缓存更新\(update-cache\)这样来处理一些问题了。

PS: AMP使用AMP Cache进行内容的缓存，在搜索页面时我们可以看到有[AMP标志](https://developers.google.com/search/docs/guides/about-amp)的页面一般来源于AMP Cache预先缓存的页面\(注:有一定几率是来自Publisher的服务器的页面\)。AMP Cache是一个具有代理功能的内容分发网络\(CND\),可以把[验证通过的AMP页面](https://github.com/ampproject/amphtml/blob/master/spec/amp-html-format.md)通过缓存放置到遍布全世界的Google AMP Cache服务器，这保证了从搜索结果进去相应的AMP页面时打开的速度。

* AMP Cache缓存的[内容](https://developers.google.com/amp/cache/overview#amp-cache-url-format)不仅仅是AMP HTML，还包括image, font等引用文件。
* AMP Cache采用的是stale-while-revalidate的缓存策略，这个缓存策略意思是当用户请求资源的时候，先会返回当前版本的资源，然后会去服务器请求资源是否有更新，如果有则更新当前的资源并Cache到AMP Cache服务器，那么如果用户再次请求，拿到的资源就是最新的了。
* AMP Cache更新机制，页面为15秒更新一次，其他资源为1分钟更新一次，这可能会变更，请注意。

## 基本步骤如下:

1. 生成一对公钥以及私钥。\(Generate a pair of RSA keys\)
2. 将公钥\(public-key.pem\)改名为apikey.pub, 放到服务器中例如以下的结构中: [https://example.com/.well-known/amphtml/apikey.pub](https://example.com/.well-known/amphtml/apikey.pub), 并且response type为"text/plain;charset=UTF-8"。（Rename the public key as apikey.pub, and post the public key on the domain to be refreshed at the following location: "\[[https://example.com/.well-known/amphtml/apikey.pub"）\]\(https://example.com/.well-known/amphtml/apikey.pub"）](https://example.com/.well-known/amphtml/apikey.pub"）]%28https://example.com/.well-known/amphtml/apikey.pub"）)\)
3. 使用私钥对想要更新的页面进行签名加密并且发送http请求AMP Cache服务器进行AMP页面的更新.\(Sign the AMP url and send the request using http to make a update on AMP Cache Server.\)

## 了解基本步骤之后，我们就可以进行实践了，选择你熟悉的编程语言进行AMP update-cache代码的编码。

* [使用PHP进行AMP内容更新\(Update AMP Content using PHP\)](amp-update-cache-php.md).
* [使用Linux Shell进行AMP内容更新\(Update AMP Content using Linux Shell\)](amp-update-cache-linux-shell.md).
* [使用Python进行AMP内容更新\(Update AMP Content using Python\)](amp-update-cache-python.md)
* 如果需要Node版的，可以参考AMP官网的[AMP update-cache Demo](https://github.com/ampproject/samples/tree/master/amp-update-cache)

