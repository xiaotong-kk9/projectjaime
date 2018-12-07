# 使用 Google Analytics 查看 AMP 速度及表现

* [使用 Custom Reports 查看 AMP 作为自然搜索落地页速度及表现](#custom-report-organic-search)
* [使用 Custom Reports 查看 AMP 作为广告落地页速度及表现](#custom-report-google-cpc)
* [为什么报告结果显示有网页浏览量（Page View）但平均网页加载时间（Avg. Page Load Time）为0.00](#speed-equals-zero)

#### 使用 Custom Reports 查看 AMP 作为自然搜索落地页速度及表现 {#custom-report-organic-search}

  1. 在 Custom Reports 中添加新的报告（[参考文档](https://support.google.com/analytics/answer/1151300)）

  2. 设置指标组（Metric Groups）（[参考文档](https://support.google.com/analytics/answer/6086087?hl=zh-Hans)）

      在指标组中添加想要查看的指标，比如Avg. Page Load Time、Page View等等。

  3. 设置纬度深入分析（Dimension Drilldowns）（[参考文档](https://support.google.com/analytics/answer/1033861?hl=zh-Hans)）

      添加着陆页（Landing Page），及其他需要查看的维度。

  4. 设置过滤器（Filters）（[参考文档](https://support.google.com/analytics/answer/1033162)）

      添加过滤条件：包含（Inlude）数据源（Data Source）完全（Exact），值为amp。

      添加过滤条件：包含（Inlude）来源/媒介（Source/Medium）完全（Exact），值为google / organic。

      添加其他所需要的过滤条件，比如地区、语言等等。

  5. 保存后调整日期查看



#### 使用 Custom Reports 查看 AMP 作为广告落地页速度及表现 {#custom-report-google-cpc}

  1. 在 Custom Reports 中添加新的报告（[参考文档](https://support.google.com/analytics/answer/1151300)）

  2. 设置指标组（Metric Groups）（[参考文档](https://support.google.com/analytics/answer/6086087?hl=zh-Hans)）

      在指标组中添加想要查看的指标，比如Avg. Page Load Time、Page View等等。

  3. 设置纬度深入分析（Dimension Drilldowns）（[参考文档](https://support.google.com/analytics/answer/1033861?hl=zh-Hans)）

      添加着陆页（Landing Page），及其他需要查看的维度。

  4. 设置过滤器（Filters）（[参考文档](https://support.google.com/analytics/answer/1033162)）

      添加过滤条件：包含（Inlude）数据源（Data Source）完全（Exact），值为amp。

      添加过滤条件：包含（Inlude）来源/媒介（Source/Medium）完全（Exact），值为google / cpc。

      添加其他所需要的过滤条件，比如地区、语言等等。

  5. 保存后调整日期查看



#### 为什么报告结果显示有网页浏览量但速度为0.00 {#speed-equals-zero}
  
  默认情况下，系统固定对 1% 的用户进行抽样，构成数据池，由此生成“网页计时”指标。（[参考文档](https://support.google.com/analytics/answer/1205784?hl=zh-Hans)）

  调整抽样率需要设置amp-analytics代码中的sampleSpec。（[参考文档](https://www.ampproject.org/docs/reference/components/amp-analytics#triggers)）

  ```javascript
  'triggers': {
    'sampledOnRandom': {
      'on': 'visible',
      'request': 'request',
      'sampleSpec': {
        'sampleOn': '${random}',
        'threshold': 50,
      },
    },
    'sampledOnClientId': {
      'on': 'visible',
      'request': 'request',
      'sampleSpec': {
        'sampleOn': '${clientId(cookieName)}',
        'threshold': 1,
      },
    },
  },
  ```
