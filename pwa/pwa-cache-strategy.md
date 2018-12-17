#缓存策略の选择

[PWA](https://developers.google.com/web/progressive-web-apps/)基于Service Worker（以下简称SW）以及Cache API的结合，离线情况下也能提供良好的用户体验。但是，我们有多种业务场景的情况下，该如何抉择缓存策略呢？

内容列表:
* [APP Shell（应用外壳）如何选择缓存策略？](./cache-strategy/precache-app-shell.md)
* [不常变动的文件但常用的CSS或者JS文件，该怎么选择缓存策略？](./cache-strategy/cache-first.md)
* [资源实时更新，但是我也想在网络不好的时候能够读返回一个旧点的页面？](./cache-strategy/network-first.md)
* [想先从Cache返回旧的资源，同时我也想要把Cache中的资源更新一遍，怎么做？](./cache-strategy/stale-while-revalidate.md)
* [只想从Cache返回资源，其他不需要，怎么做？](./cache-strategy/cache-only.md)
* [只想从请求并拿取网络中的最新资源，怎么做？](./cache-strategy/network-only.md)