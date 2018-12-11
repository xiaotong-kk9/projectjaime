##没有使用任何第三方框架下原生代码实现的PWA如何实现GA数据的跟踪?

PWA即使在离线情况也能提供良好的用户体验，那么，我们这里有两个问题要解决。

A.PWA中生命周期中发生的事件怎么追踪，如notificationclose等事件，可以参考[怎么集成GA在PWA](https://developers.google.com/web/ilt/pwa/integrating-analytics)。

B.离线状态下网站也会有GA的数据追踪请求，那么可以参考[PWA离线数据追踪](https://developers.google.com/web/ilt/pwa/integrating-analytics#offline_analytics), 教程里面用到了[sw-offline-google-analytics](https://developers.google.com/web/updates/2016/07/offline-google-analytics.https://www.npmjs.com/package/sw-offline-google-analytics)这个库，非常简单易用。 