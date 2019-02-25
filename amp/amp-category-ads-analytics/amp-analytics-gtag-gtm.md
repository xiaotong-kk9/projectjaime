# 如何开启AMP Linker并验证


* [AMP Linker设置方法](amp-analytics-gtag-gtm.md#amp-linker-implementation)
* [AMP Linker验证方法](amp-analytics-gtag-gtm.md#amp-linker-validation)

## AMP Linker设置方法<a id="amp-linker-implementation"></a>

### 第一步：在AMP页面设置

#### 使用gtag：

* 确认header中有```<script async custom-element="amp-analytics" src="https://cdn.ampproject.org/v0/amp-analytics-0.1.js"></script>```。

* 设置&lt;amp-analytics&gt;的type为gtag，为标签添加data-credentials="include"。[参考文档](https://developers.google.com/gtagjs/devguide/amp#installation)
```
<amp-analytics type="gtag" data-credentials="include">
  <script type="application/json">
  {
    "vars" : {
      "gtag_id": "<TARGET_ID>",
      "config" : {
        "<TARGET_ID>": { "groups": "default" }
      }
    }
  }
  </script>
</amp-analytics>
```

* 如果AMP页面和其他页面在不同的domain或者subdomain上，需要声明linker的domains参数。[参考文档](https://developers.google.com/gtagjs/devguide/amp#link_domains)
```
<amp-analytics type="gtag" data-credentials="include">
  <script type="application/json">
  {
    "vars" : {
      "gtag_id": "<TARGET_ID>",
      "config" : {
        "<TARGET_ID>": {
          "groups": "default",
          "linker": { "domains": ["example.com", "example2.com", "foo.example.com"] }
        }
      }
    }
  }
  </script>
</amp-analytics>
```

* 如果在追踪中需要发送custom dimension，需要在extraUrlParams中声明。[参考文档](https://www.ampproject.org/docs/reference/components/amp-analytics#extra-url-params)
```
<amp-analytics type="gtag" data-credentials="include">
  <script type="application/json">
  {
    "vars" : {
      "gtag_id": "<TARGET_ID>",
      "config" : {
        "<TARGET_ID>": {
          "groups": "default",
          "linker": { "domains": ["example.com", "example2.com", "foo.example.com"] }
        }
      }
    },
    "extraUrlParams": {
      "cd1": "1"
    }
  }
  </script>
</amp-analytics>
```

* 如果在追踪中需要发送来自cookie的其他参数，请使用"CLIENT_ID(cookiename)"来取值。[参考文档](https://github.com/ampproject/amphtml/blob/master/spec/amp-var-substitutions.md)
```
<amp-analytics type="gtag" data-credentials="include">
  <script type="application/json">
  {
    "vars" : {
      "gtag_id": "<TARGET_ID>",
      "config" : {
        "<TARGET_ID>": {
          "groups": "default",
          "linker": { "domains": ["example.com", "example2.com", "foo.example.com"] }
        }
      }
    },
    "triggers": {
      "trackPageview": {
        "on": "visible",
        "request": "pageview",
        "vars": {
          "currency": "CLIENT_ID(cur)"
        }
      }
    }
  }
  </script>
</amp-analytics>
```

#### 使用GTM：

* 为代码添加linkers
```
<amp-analytics config="https://www.googletagmanager.com/amp.json?id=GTM-CONTAINER_ID" data-credentials="include">
 <script type="application/json">
   {
     "linkers": {
       "_gl": {
         "enabled": true,
         "destinationDomains": ["a.com","b.com"], //如果可能跳转至其他domain或subdomain
         "ids": {
           "_ga": "CLIENT_ID(AMP_ECID_GOOGLE,,_ga)"
         },
        "proxyOnly": false
       }
     }
   }
 </script>
</amp-analytics>
```


### 第二步：在non-AMP页面设置


#### 如果使用analytics.js：

添加 ga('create', 'UA-XXXXX-Y', 'auto', {'useAmpClientId': true});


#### 如果使用gtag.js：

添加 gtag('create', 'UA-XXXXX-Y', 'auto', {'use_amp_client_id': true});


#### 如果使用GTM：
为google analytics tag添加 Configuration useAmpClientId为true，请参考[文档](https://support.google.com/analytics/answer/7486764?hl=en)的If you use Google Tag Manager部分。


### 第三步：使用引荐排除

当 Google 向用户提供 AMP 内容时，它会使用 Google AMP 缓存。您必须使用以下网域添加单个引荐排除项目：cdn.ampproject.org。这样可以防止 Google 提供的所有缓存 AMP 子网域中断会话。

如果您使用多个子域提供 AMP 网页，则可能需要对 AMP 子域分别进行不同的处理。在这种情况下，请为您的网站输入在引荐排除中使用的任何现有子域的缓存版本，以便在 AMP 和非 AMP 网站之间维护特定的引荐排除项目。举例来说，如果您的子域 subdomain.example.com 已有现成的引荐排除项目，则应为 subdomain-example-com.cdn.ampproject.org 添加一个引荐排除项目。[详细了解](https://developers.google.com/amp/cache/overview#amp-cache-url-format) AMP 缓存网址格式。

您可以在 Google Analytics（分析）的“管理”部分输入与 AMP 相关的引荐排除项目以及您的其他所有引荐排除项目。[了解详情](https://support.google.com/analytics/answer/2795830?hl=zh-Hans)

[参考文档](https://support.google.com/analytics/answer/7486764?hl=zh-Hans)


## AMP Linker验证方法<a id="amp-linker-validation"></a>

1. 在无痕模式中打开 Google Chrome 浏览器。在 Chrome 开发者工具中启用移动设备模拟器。
2. 在 google.com 上输入一个会返回您网站上 AMP 页面的搜索查询。
3. 点击一个会前往 AMP 页面的搜索结果，该页面应是通过 Google AMP 缓存进行投放，并显示在 Google 搜索 AMP 查看工具中。
4. 转到 Chrome 开发者工具中的“Network”（网络）标签，输入字符串 collect 进行过滤，以查找与 AMP 网页浏览对应的 Google Analytics（分析）网络请求。
5. 选择转到 www.google-analytics.com 的网络请求。在请求的“Headers”（标头）标签上，滚动到“Query String Parameters”（查询字符串参数）以找到客户端 ID。请记下 cid 参数。
6. 点击 Clear（清除）以清除网络请求。
7. 要验证是否启用了非 AMP 网页，您需要确认在转到非 AMP 网页时，网页链接上携带key为_gl的加密参数，且仍然存在相同的 cid 参数。为此，请点击 AMP 网页上指向您的网域所提供的非 AMP 网页的任意链接。要找到客户端 ID，请再次针对字符串 collect 进行过滤。选择转到 www.google-analytics.com 的任意网络请求。检查 cid 查询参数值是否与您在第 5 步记下的值相符。
8. 如果 cid 值不相符，请根据上述设置方法重新检查。


