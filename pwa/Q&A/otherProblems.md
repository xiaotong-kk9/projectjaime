#其他问题


#### [清空浏览器缓存是否代表service worker卸载？从此是不是不会收到push事件推送过来的消息了？](#清空浏览器缓存是否代表service worker卸载？从此是不是不会收到push事件推送过来的消息了？)
#### [遇到了DOMException: Quota exceeded这个错误，怎么破？](#遇到了DOMException: Quota exceeded这个错误，怎么破？)


##清空浏览器缓存是否代表service worker卸载？从此是不是不会收到[push](https://developers.google.com/web/ilt/pwa/introduction-to-push-notifications#push_api)事件推送过来的消息了？

清除浏览器设置(Clear browsing data)缓存是会删除service worker的，而一旦service worker被删除，那么push过来的消息也没有service worker去接收了，因此也不可能弹出notification了。

同时清空站点设置（Site settings）权限也会被重置，需要重新获取权限。

建议可以使用DevTools中的Remote-devices来进行查看，当你在浏览器设置中Clear browsing data的选项中选中 Cookies and site data的选项时，可以在DevTools中查看service-worker将会被移除 。可参考[如果我不想要Service worker怎么办](https://dev.chromium.org/Home/chromium-security/security-faq/service-worker-security-faq#TOC-What-if-I-don-t-want-any-SWs-), 同时还有[如何清除浏览数据](https://support.google.com/chrome/answer/2392709?hl=en&co=GENIE.Platform%3DDesktop&oco=1)。


## 遇到了DOMException: Quota exceeded这个错误，怎么破？

有以下几点建议：

1. 清除旧的缓存再进行新的缓存。
2. [注册Service worker](https://developers.google.com/web/ilt/pwa/introduction-to-service-worker#registration_and_scope)之前进行[quota的查询](https://developers.google.com/web/updates/2017/08/estimating-available-storage-space#the-present)，再决定是否安装Service worker。
3. 如果使用了workbox进行开发，那么可以[使用expiration插件进行quota控制](https://developers.google.com/web/tools/workbox/guides/storage-quota)。
4. 重启浏览器。

参考文档：

[DOM exception quotaExceed - MDN](https://developer.mozilla.org/en-US/docs/Web/API/DOMException#exception-QuotaExceededError)

[Managing quota - Chrome](https://developer.chrome.com/apps/offline_storage#managing_quota)

PS: navigator对象在Service worker中也可用(Safari下没有[NavigatorStorage](https://developer.mozilla.org/en-US/docs/Web/API/NavigatorStorage/storage)对象，望周知)。