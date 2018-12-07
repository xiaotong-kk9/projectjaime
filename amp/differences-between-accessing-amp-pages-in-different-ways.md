# 不同方式访问 AMP 页面的区别

#### 用户直接访问 AMP 页面

AMP 能够确保页面高效地加载资源，快速地渲染，只有进入 viewport 的元素才会加载展示。（[参考文档](https://www.ampproject.org/zh_cn/learn/about-how/)）


#### 用户直接访问 AMP Cache 页面

AMP 同样能够确保页面高效地加载资源，快速地渲染，只有进入 viewport 的元素才会加载展示。（[参考文档](https://www.ampproject.org/zh_cn/learn/about-how/)）

除此之外，AMP Cache 会对页面的HTML和资源进行处理优化。（[参考文档](https://developers.google.com/amp/cache/overview#cache-optimizations-and-modifications)）

如何修复 AMP Cache 页面问题？
https://www.ampproject.org/zh_cn/docs/troubleshooting/amp-cache-debugging


#### 用户通过 Google.com 和搜索广告（Search Ads）访问AMP页面（加载最快）

在搜索结果页或搜索广告落地页，AMP 可能会在 [Google AMP Viewer](https://support.google.com/websearch/answer/7220196?hl=zh-Hans) 中展示。（[参考文档](https://developers.google.com/search/docs/guides/about-amp)）

AMP 同样能够确保页面高效地加载资源，快速地渲染，只有进入 viewport 的元素才会加载展示。（[参考文档](https://www.ampproject.org/zh_cn/learn/about-how/)）

AMP Cache 会对页面的HTML和资源进行处理优化。（[参考文档](https://developers.google.com/amp/cache/overview#cache-optimizations-and-modifications)）

AMP 页面会在用户尚未点击的时候进行预加载，用户点击后立刻打开。

