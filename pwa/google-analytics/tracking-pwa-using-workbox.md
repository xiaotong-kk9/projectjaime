##基于workbox开发的PWA如何在离线状态控制GA的数据追踪?

[Workbox](https://developers.google.com/web/tools/workbox/)是Google为了降低开发PWA开发成本提供的一个JS库，使用这个库追踪GA请求非常简单，只需要调用workbox.googleAnalytics.initialize()就ok了，可参考[Workbox Google Analytics](https://developers.google.com/web/tools/workbox/modules/workbox-google-analytics).

PS: Workbox Google Analytics是基于[Background Sync](https://wicg.github.io/BackgroundSync/spec/)的，因此能确保GA的hit在网络恢复时能即时恢复请求。