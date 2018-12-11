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