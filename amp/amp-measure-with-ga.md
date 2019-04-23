# 使用 Google Analytics 查看 AMP 速度及表现

* [使用 Custom Reports 查看 AMP 作为自然搜索落地页速度及表现](amp-measure-with-ga.md#custom-report-organic-search)
* [使用 Custom Reports 查看 AMP 作为广告落地页速度及表现](amp-measure-with-ga.md#custom-report-google-cpc)
* [为什么报告结果显示有网页浏览量（Page View）但平均网页加载时间（Avg. Page Load Time）为0.00](amp-measure-with-ga.md#speed-equals-zero)
* [如何进行AMP缓存与非缓存分析](https://support.google.com/analytics/answer/6343176?hl=zh-Hans)
* [报告中速度数据的抽样率为1%导致样本过少怎么办](amp-measure-with-ga.md#adjust-sample-rate)

## 使用 Custom Reports 查看 AMP 作为自然搜索落地页速度及表现 <a id="custom-report-organic-search"></a>

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

## 使用 Custom Reports 查看 AMP 作为广告落地页速度及表现 <a id="custom-report-google-cpc"></a>

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

## 为什么报告结果显示有网页浏览量但速度为0.00 <a id="speed-equals-zero"></a>

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

## 报告中速度数据的抽样率为1%导致样本过少怎么办 <a id="adjust-sample-rate"></a>

记录速度的追踪hit，是有别于pageview单独发出的，GA免费版和GA360的hit均有上限。
如果增加了很多timing的hit，可能会影响到其他数据收集。[参考文档](https://support.google.com/analytics/answer/7367018?hl=zh-Hans)

如果觉得抽样率太低，可以通过设置参数进行提高，但不建议直接提升到100%以免达到上限影响其他追踪数据的收集。

AMP页面实施方式：

在triggers部分添加performanceTiming，将threshold修改为需要的抽样率。[参考文档](https://www.ampproject.org/docs/reference/components/amp-analytics#triggers)[参考代码](https://github.com/ampproject/amphtml/blob/master/extensions/amp-analytics/0.1/vendors/googleanalytics.js#L83)
```javascript
  'triggers': {
    'performanceTiming': {
      'on': 'visible',
      'request': 'timing',
      'sampleSpec': {
        'sampleOn': '${clientId}',
        'threshold': 5, // 抽样率 5%
      },
      'vars': {
        'timingRequestType': 'timing',
      },
    },
  }
```

analytics.js实施方式：

调整siteSpeedSampleRate。[参考文档](https://developers.google.com/analytics/devguides/collection/analyticsjs/field-reference#siteSpeedSampleRate)
```javascript
  ga('create', 'UA-XXXX-Y', {'siteSpeedSampleRate': 5}); // 抽样率 5%
```

