# AMP 检查列表

1. AMP Validator \([链接](https://validator.ampproject.org/)\)

   在 Chrome 上安装 AMP Validator 插件，需要确保所有 AMP 页面都没有报错。如果 AMP 页面有报错将不会被 AMP Cache 缓存，也不会被收录。

2. AMP Cache URL \([链接](https://developers.google.com/amp/cache/reference/acceleratedmobilepageurl/rest/v1/ampUrls/batchGet)\)

   使用链接中的 URL 转换工具将 AMP URL 转换为 AMP Cache URL 后访问查看页面展示是否有问题，开发者工具控制台是否有报错。

3. 检查 Canonical link 和 amphtml link \([链接](https://amp.dev/documentation/guides-and-tutorials/optimize-and-measure/discovery/)\)

   需要确认 AMP 页面和 non-AMP 页面一一对应，canonical link 和 amphtml link 设置正确。
   
   通常情况下为了SEO友好，建议AMP页面与desktop页面互相链接，mobile站页面与desktop页面互相链接。
   
   例如：
   
   首页PC版
  ```text
    <link rel="alternate" hreflang="en" href="https://m.foo.com/" media="only screen and (max-width: 640px)">【alternate指向m版首页】
    <link rel="amphtml" hreflang="en" href="https://m.foo.com/amp.html">【amphtml指向amp版首页】
  ```
   首页m版
  ```text
    <link rel="canonical" href="https://www.foo.com/">【canonical指向pc版首页】
  ```
   首页amp版
  ```text
    <link rel="canonical" href="https://www.foo.com/">【canonical指向pc版首页】
  ```

4. 检查跨域\([链接](https://amp.dev/documentation/guides-and-tutorials/learn/amp-caches-and-cors/amp-cors-requests/)\)

   跨域设置 access-control-allow-origin 的域名可以通过 AMP Cache URL 工具转换得到（格式类似：[https://ampbyexample-com.cdn.ampproject.org](https://ampbyexample-com.cdn.ampproject.org) ），请务必不要设置为 \*，并且不要漏掉文档中列出的 header。

   ```text
    HTTP/2 200
    access-control-allow-headers: Content-Type, Content-Length, Accept-Encoding, X-CSRF-Token
    access-control-allow-credentials: true
    access-control-allow-origin: https://ampbyexample-com.cdn.ampproject.org
    amp-access-control-allow-source-origin: https://ampbyexample.com
    access-control-allow-methods: POST, GET, OPTIONS
    access-control-expose-headers: AMP-Access-Control-Allow-Source-Origin
   ```

5. 使用 ampbench 检查页面\([链接](https://ampbench.appspot.com/)\)

   修复所有的报错，检查结构化数据（Structured Data）。

6. 使用 Search Console AMP 状态报告关注收录情况\([链接](https://support.google.com/webmasters/answer/7450883?hl=zh-Hans)\)

   有关 SEO 的疑问请参考[搜索引擎优化新手指南](https://support.google.com/webmasters/answer/7451184?hl=zh-Hans)。

7. 检查 Google AMP Client ID API 设置\([链接](https://support.google.com/analytics/answer/7486764?hl=zh-Hans)\)

   需要确认第一二三步都实施正确，使用文档中的设置验证步骤来进行实施验证。

