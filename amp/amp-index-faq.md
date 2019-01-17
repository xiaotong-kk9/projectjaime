# AMP 谷歌搜索收录常见问题

翻译自 [AMP Indexing FAQs by DongHwi Lee](https://productforums.google.com/forum/?hl=en#!category-topic/webmasters/Vrgj-a-gtm0)

Hello Webmasters!

我整理了一些 AMP 谷歌收录方面的 FAQ。

除了在本贴下方提问，你也同样可以参考以下文档：

* [谷歌搜索中的 AMP 开发者指南](https://developers.google.com/search/docs/guides/about-amp)

* [AMP 参考指南（中文）](https://www.ampproject.org/zh_cn/)


#### Q：AMP 页面一般需要多久会被收录并在搜索结果中展示？

爬虫爬取收录 AMP 页面和爬取收录普通页面是一样的。但是如果你有 AMP 错误，尤其是[ AMP 必需标记（中文）](https://www.ampproject.org/zh_cn/docs/getting_started/create/basic_markup)，这会影响爬虫是否能够成功爬取AMP页面。


以下参考文档可以帮助理解收录工作机制：

* [收录介绍](https://developers.google.com/search/docs/guides/intro-indexing)

* [爬虫的爬取预算](https://webmasters.googleblog.com/2017/01/what-crawl-budget-means-for-googlebot.html)

* [打造方便 Google 处理的网站的步骤（中文）](https://support.google.com/webmasters/answer/40349?hl=zh-Hans)


如何为了收录优化网站：

* [网站站长指南（中文）](https://support.google.com/webmasters/answer/35769?hl=zh-Hans)

* [优化你的爬取和收录](https://webmasters.googleblog.com/2009/08/optimize-your-crawling-indexing.html)

* [搜索引擎优化 (SEO) 新手指南（最佳实践）（中文）](https://support.google.com/webmasters/answer/7451184?vid=0-624057219926-1543423419632&hl=zh-Hans)

* [与 Google 搜索中的 AMP 网页相关的准则（中文）](https://support.google.com/webmasters/answer/6340290?hl=zh-Hans)


#### Q：如果我发布了 X 个 AMP 页面，收录需要多长时间？什么因素会影响爬虫对页面的选取？（假设规范页面（Canonical Page）已被爬取收录和未被爬取收录）

谷歌爬取收录 AMP 页面和常规页面的速度是一样的。请确保 AMP 有效来提升 AMP 页面的成功爬取，更多信息请参考[我的网站尚未编入索引（中文）](https://support.google.com/webmasters/answer/1050724?hl=zh-Hans&ref_topic=4558960)


#### Q：页面类型不同收录会不一样吗，比如说首页和商品详情页？

首页和商品详情页是同样的收录流程。谷歌通过多种因素，比如说页面的主要内容变更频率，来确定基于每个页面的最佳爬取频率。虽然通常情况下收录和排名需要页面被爬取，但迫使一个页面经常被重新爬取并不会影响收录或排名。谷歌通常不会为搜索区分类别页面或者商品详情页面，但举例来说，类别页面可以引导到新的商品详情页面。

请注意动态生成的商品列表页面会很容易变成死循环，这会使爬取更加困难。了解更多[帮助中心（中文）](https://support.google.com/webmasters/answer/76401?hl=zh-Hans)|[博文](https://webmasters.googleblog.com/2008/08/to-infinity-and-beyond-no.html)


#### Q: 如果一些页面可能会频繁地变更或下线，他们对收录来说仍然是好的候选吗？

是的，页面类型经常变更没有关系，比如说寿命有限的拍卖物品或者分类广告。网站可以使用[网站地图（中文）](https://support.google.com/webmasters/answer/183668?hl=zh-Hans)文件来提供页面新增和变更信息给谷歌。

参考资料：

* [如何从搜索中去掉 AMP](https://developers.google.com/search/docs/guides/remove-amp)

* [如果页面需要经常变更，使用谷歌 AMP 缓存更新请求（update-cache request）](https://developers.google.com/amp/cache/update-cache)


#### Q: 有什么办法可以加速收录（比如说，通过设置广告渠道）？

广告渠道不会影响页面在谷歌自然搜索结果收录或者排名。

网站管理员可以通过提供[网站地图（中文）](https://support.google.com/webmasters/answer/156184?hl=zh-Hans)来帮助谷歌爬虫，或者在 [Search Console（中文）](https://support.google.com/webmasters/answer/6065812?hl=zh-Hans)中提交单个URL。

如何为了收录优化网站：

* [网站站长指南（中文）](https://support.google.com/webmasters/answer/35769?hl=zh-Hans)

* [优化你的爬取和收录](https://webmasters.googleblog.com/2009/08/optimize-your-crawling-indexing.html)

* [搜索引擎优化 (SEO) 新手指南（最佳实践）（中文）](https://support.google.com/webmasters/answer/7451184?hl=zh-Hans)

* [与 Google 搜索中的 AMP 网页相关的准则（中文）](https://support.google.com/webmasters/answer/6340290?hl=zh-Hans)


#### Q: AMP对排名的影响是什么？

使用AMP不会改变排名。谷歌搜索将[页面速度](https://webmasters.googleblog.com/2018/01/using-page-speed-in-mobile-search.html)作为一个排名因素，但是网站可以通过包括AMP在内的多种技术加速。也就是说，谷歌搜索对所有页面应用同样的标准，不管应用什么技术来开发。

参考资料：

* [在移动端排名中使用页面速度](https://webmasters.googleblog.com/2018/01/using-page-speed-in-mobile-search.html)

* [移动端友好测试工具](https://search.google.com/test/mobile-friendly)


#### Q: 如果AMP页面中只有一小部分被收录出现在搜索中我应该担心吗？

一小部分本身不是问题。
* 请使用 Search Console 来查看网站中发现的AMP页面大致的统计数字。请查看“搜索曝光”下面的“[ Accelerated Mobile Pages ](https://www.google.com/webmasters/tools/accelerated-mobile-pages)”。
* 谷歌搜索可能没有发现网站中所有的 AMP 页面。这是正常情况，随着谷歌搜索发现 AMP 页面，会随时间推移而提升。我们建议使用[站点地图](https://support.google.com/webmasters/answer/156184?hl=zh-Hans)去提醒谷歌新增和更新的页面。
* 谷歌爬虫在努力不去引发网站服务基础架构问题。爬取会受到网站响应的限制。爬虫试图优先爬取和收录网站中最有用的页面。更多信息请参考[爬取的优先级](https://webmasters.googleblog.com/2017/01/what-crawl-budget-means-for-googlebot.html)

参考资料：

* [在 Google 上占有一席之地（中文）](https://support.google.com/webmasters/answer/6259634?hl=zh-Hans)


#### Q: 为什么我的搜索结果中同时出现了 AMP 和 non-AMP 的结果？

如果规范页面（Canonical Page）的 amphtml 链接或者从 AMP 页面到规范页面（Canonical Page）的链接断掉了，谷歌可能不会知道规范页面（Canonical Page）和 AMP 页面的串联。如果两个页面没有配对，它们可能会被认为是独立页面。


#### Q: 在这种情况下，我应该用不同方式标记 AMP 吗？桌面端网站（www），移动端网站（m.）和 AMP 页面。其中 AMP 指向 m.，m. 指向 AMP。

当桌面端网站和移动端网站同时存在的情况下，

* AMP应该通过 <link rel="canonical"> 指向桌面端

* 桌面端应该通过 <link rel="amphtml"> 指向 AMP

请参考[这个页面（中文）](https://www.ampproject.org/zh_cn/docs/getting_started/create/prepare_for_discovery)获得更多信息。


AMP同样可以作为独立的规范页面（Canonical）来承担所有流量。在很多例子中，没有必要存在单独的桌面端网站或者移动端网站（m.）。


如果因为某些原因，桌面端、移动端和 AMP 三个网站都存在：

* 桌面端：通过 <link rel="amphtml"> 指向AMP，通过 rel=alternate 指向移动端

* 移动端：通过 <link rel="canonical"> 指向桌面端，通过 rel=amphtml 指向AMP（移动端应该要和桌面端内容一致）

* AMP：通过 <link rel="canonical"> 指向桌面端

参考资料：

* [准备页面以供发现和分发（中文）](https://www.ampproject.org/zh_cn/docs/getting_started/create/prepare_for_discovery)


#### Q: 为什么我的AMP页面没有在热点新闻轮播（Top stories carousel）出现？

为页面添加结构化数据（Structured data）会使你的页面能够出现在轮播（Carousels）和富搜索结果展示（Rich results）中。但是能够使用一个搜索特性，并不能保证一定会以该特性的形式展示。

下面是一些可能导致页面没有出现在热点新闻轮播（Top stories carousel）的原因：

* 页面没有被收录：更多信息，请参考[我的网站尚未编入索引！（中文）](https://support.google.com/webmasters/answer/1050724?hl=zh-Hans&ref_topic=4558960)

* 页面没有显示在轮播中：没有办法保证页面一定会出现在具有特定特性的搜索结果中。这是因为搜索特性取决于多种因素，包括搜索设备类型，地点还有谷歌是否判断该特性可以为用户提供最好的搜索体验。更多信息，请参考[关于搜索特性](https://developers.google.com/search/docs/guides/search-features)

* 页面不是有效的 AMP 页面：更多信息，请参考[修复常见 AMP 错误](https://developers.google.com/search/docs/guides/validate-amp#fix-common-amp-errors)


#### Q: AMP 爬取来自爬取预算吗？

是的。谷歌爬虫需要在一个服务器的爬取预算中爬取包括 AMP 在内的所有文件，而避免引起网站的问题。一般来说，大部分网站不需要担心爬取预算，并且 AMP 内容对于爬取和收录来说非常高效。

当一个现代搜索引擎爬虫爬取一个页面，它同样需要抓取子资源，像是 JavaScript、CSS、图片等，来完整地理解页面。子资源的数量会远远比主文件多（根据 HTTP Archive 统计数据，[网站请求的平均数量](https://httparchive.org/reports/state-of-the-web#bytesTotal&reqTotal) 超过100）。AMP 通常需要更少的资源。
