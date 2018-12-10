#GA系列

##问题列表: 

* [没有使用任何第三方框架下，原生代码实现的PWA如何实现GA数据的跟踪？](#tracking-pwa-using-native-code)
* [基于workbox开发的PWA如何在离线状态控制GA的数据追踪？](#tracking-pwa-using-workbox)


##没有使用任何第三方框架下原生代码实现的PWA如何实现GA数据的跟踪? {#tracking-pwa-using-native-code}

PWA即使在离线情况也能提供良好的用户体验，那么，我们这里有两个问题要解决。

A.PWA中生命周期中发生的事件怎么追踪，如notificationclose等事件，可以参考[怎么集成GA在PWA](https://developers.google.com/web/ilt/pwa/integrating-analytics)。

B.离线状态下网站也会有GA的数据追踪请求，那么可以参考[PWA离线数据追踪](https://developers.google.com/web/ilt/pwa/integrating-analytics#offline_analytics), 教程里面用到了[sw-offline-google-analytics](https://developers.google.com/web/updates/2016/07/offline-google-analytics.https://www.npmjs.com/package/sw-offline-google-analytics)这个库，非常简单易用。 


##基于workbox开发的PWA如何在离线状态控制GA的数据追踪? {#tracking-pwa-using-workbox}

[Workbox](https://developers.google.com/web/tools/workbox/)是Google为了降低开发PWA开发成本提供的一个JS库，使用这个库追踪GA请求非常简单，只需要调用workbox.googleAnalytics.initialize()就ok了，可参考[Workbox Google Analytics](https://developers.google.com/web/tools/workbox/modules/workbox-google-analytics).

PS: Workbox Google Analytics是基于[Background Sync](https://wicg.github.io/BackgroundSync/spec/)的，因此能确保GA的hit在网络恢复时能即时恢复请求。