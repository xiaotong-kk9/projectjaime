# 通过参数 enabled 控制是否发送追踪请求

功能实现方式：使用amp-analytics的triggers。

## 解决方案

### 在amp-analytics的triggers中为trigger-object添加参数 enabled 并设置为 true/false 或通过表达式赋值

true/false 示例：

```
  <amp-analytics id="analytics1">
    <script type="application/json">
    {
      "requests": {
        "pageview": "https://foo.com/pixel?account=${account}"
      },
      "triggers": {
        "trackPageview": {
          "on": "visible",
          "request": "pageview",
          "enabled": false,
          "vars": {
            "account": "aaa"
          }
        }
      }
    }
    </script>
  </amp-analytics>
```

表达式示例：

```
  <amp-analytics id="analytics1">
    <script type="application/json">
    {
      "requests": {
        "pageview": "https://foo.com/pixel?account=${account}"
      },
      "triggers": {
        "trackPageview": {
          "on": "visible",
          "request": "pageview",
          "enabled": QUERY_PARAM('key'),
          "vars": {
            "account": "aaa"
          }
        }
      }
    }
    </script>
  </amp-analytics>
```

文档参考： [amp-analytics官方文档](https://www.ampproject.org/docs/reference/components/amp-analytics)