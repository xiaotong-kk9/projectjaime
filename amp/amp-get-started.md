# AMP入门指南

####关于AMP，我们可以理解为AMP实际是上自己实现了一套构建页面的方式，AMP页面由三大核心组件 AMP HTML, AMP JS, AMP Cache组成:
* AMP HTML其实有一系列带有AMP标记的属性或者组件组成，例如 amp-img, amp-list等等。
* AMP JS实际上就是我们引入这些组件的基础依赖，同时也包括了一系列的资源管理，[最佳性能做法](https://www.ampproject.org/zh_cn/learn/about-how/)的控制。AMP可以动态控制资源的加载顺序，同时控制所有外部内容均为异步加载，这一定程度上保证了用户的浏览体验，AMP也能够保证资源请求必须是优先级较大的才会优先请求。举个栗子，某些图片或者广告，当用户可能会查看到或快速滚动到他们时，AMP才会进行资源的请求，这样能减少带宽的压力，同时也能保证用户的体验。
* AMP Cache是一个具有代理功能的内容分发网络(CND),可以把[验证通过的AMP页面](https://github.com/ampproject/amphtml/blob/master/spec/amp-html-format.md)通过缓存放置到遍布全世界的Google AMP Cache服务器.
  * AMP Cache缓存的[内容](https://developers.google.com/amp/cache/overview#amp-cache-url-format)不仅仅是AMP HTML，还包括image, font等引用文件。
  * AMP Cache采用的是stale-while-revalidate的缓存策略，这个缓存策略意思是当用户请求资源的时候，先会返回当前版本的资源，然后会去服务器请求资源是否有更新，如果有则更新当前的资源并Cache到AMP Cache服务器，那么如果用户再次请求，拿到的资源就是最新的了。
  * AMP Cache更新机制，页面为15秒更新一次，其他资源为1分钟更新一次，这可能会变更，请注意。
  * 如果想要控制AMP页面内容的更新，例如您是从事新闻且对时效性较高的发布者，那么你可能需要这个。亲测删除或者更新时间一般为2-30分钟不等，如果想要及时更新自己的页面，那么请参考如何使用[使用update-cache进行AMP内容更新](./amp-update-cache.md)教程。

####那么，了解了AMP的实现方式之后，我们可能就想要知道怎么去做一个AMP，我们可以通过两个代码实验来了解一下AMP页面的实现方式。
* [AMP基础入门代码实验](https://codelabs.developers.google.com/codelabs/accelerated-mobile-pages-foundations/#0)
* [AMP进阶代码实验](https://codelabs.developers.google.com/codelabs/accelerated-mobile-pages-foundations/#0)
* [AMP交互代码实验](https://codelabs.developers.google.com/codelabs/advanced-interactivity-in-amp/index.html?index=..%2F..%2Findex#0)
* [AMP体验优化代码实验](https://codelabs.developers.google.com/codelabs/amp-beautiful-interactive-canonical/index.html?index=..%2F..%2Findex#7)

####通过上面的代码实验我们大致了解了AMP实现方式，那么接下来我们完整了解一下AMP的开发流程
1. 开发AMP页面(可以参考上面的教程学习)
2. 加入第三方服务(广告或者统计分析工具, 可参考[支持的合作平台，代理商，合作伙伴](https://www.ampproject.org/support/faqs/supported-platforms))
3. 对AMP页面进行[验证](https://www.ampproject.org/docs/fundamentals/validate),例如使用[AMP Test Too](https://search.google.com/test/amp)以及[结构化数据测试工具](https://search.google.com/structured-data/testing-tool/u/0/)进行验证。关于结构化数据，可以参考[AMP与结构化数据](https://developers.google.com/search/docs/data-types/article#amp-sd)
4. 验证通过后AMP Cache服务器会自动缓存AMP页面。开发流程到此基本完成，但是请在上线前确保下面的注意事项你都已经看了。


####注意事项: 
1. 发布前确保Canonical页面以及AMP页面是互相指向的状态，具体请参考[使你的AMP页面可被呈现](https://www.ampproject.org/docs/fundamentals/discovery#linking-pages-with-link)。
2. 发布前，确定 Schema.org 的 snippet 有正确地被加在 AMP 页面, 这可以让大多数的搜索引擎更了解这篇文章的 metadata，使用[结构化数据测试工具](https://search.google.com/structured-data/testing-tool/u/0/)进行验证，可以参考: [集成第三方平台metadata到AMP页面中](https://www.ampproject.org/docs/fundamentals/discovery#integrate-with-third-party-platforms-through-additional-metadata)
3. AMP页面跟Canonical页面的UI以及UX要确保基本一致，避免降低用户的体验。



