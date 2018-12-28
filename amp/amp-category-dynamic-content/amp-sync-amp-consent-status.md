# AMP页面关闭弹出提示在non-AMP页面仍然会出现

功能实现方式：

* [AMP页面使用amp-consent/amp-user-notification，non-AMP页面通过cookie判断状态](amp-sync-amp-consent-status.md#amp-consent-cookie)
* [AMP页面使用amp-consent/amp-user-notification，non-AMP页面通过服务端数据判断状态](amp-sync-amp-consent-status.md#amp-consent-server)

## 解决方案

### AMP页面使用amp-consent/amp-user-notification，non-AMP页面通过cookie判断状态 <a id="amp-consent-cookie"></a>

可能导致问题原因：使用amp-consent/amp-user-notification没有将状态发送至服务端，通过返回请求存cookie到浏览器。

解决方案：在amp-consent/amp-user-notification的接受\(accept\)和拒绝\(reject\)按钮上添加绑定事件，提交form到服务端，服务端通过返回请求将cookie存到浏览器。non-AMP页面通过js读取cookie，对相应内容进行展示或隐藏处理。

文档参考： [amp-user-notification发送状态至服务端官方示例](https://ampbyexample.com/components/amp-user-notification/#advanced-usage-with-a-server-endpoint) [amp-form官方文档](https://www.ampproject.org/docs/reference/components/amp-form)

### AMP页面使用amp-consent/amp-user-notification，non-AMP页面通过服务端数据判断状态 <a id="amp-bind-amp-setState"></a>

可能导致问题原因：使用amp-consent/amp-user-notification没有将状态发送至服务端保存到数据库。

解决方案：在amp-consent/amp-user-notification的接受\(accept\)和拒绝\(reject\)按钮上添加绑定事件，提交form至服务端保存到数据库。non-AMP页面通过数据库读取状态，对相应内容进行展示或隐藏处理。

文档参考： [amp-user-notification发送状态至服务端官方示例](https://ampbyexample.com/components/amp-user-notification/#advanced-usage-with-a-server-endpoint) [amp-form官方文档](https://www.ampproject.org/docs/reference/components/amp-form)

