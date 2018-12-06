# AMP 验证错误

## 文档

[AMP 验证错误官方文档（中文）](https://www.ampproject.org/zh_cn/docs/troubleshooting/validation_errors)

[解决验证错误（中文）](https://www.ampproject.org/zh_cn/docs/fundamentals/converting/resolving-errors)

https://www.ampproject.org/zh_cn/docs/fundamentals/converting/resolving-errors

[AMP 验证错误完整概述（英文）](https://github.com/ampproject/amphtml/blob/master/validator/validator-main.protoascii)

* [Origin of &lt;amp-iframe&gt; must not be equal to container](#origin-of-amp-iframe)

---

#### Origin of &lt;amp-iframe&gt; must not be equal to container {#origin-of-amp-iframe}

amp-iframe的sandbox属性如果添加了allow-same-origin，引入的内嵌页面不能和父级页面在同一个域名，要放在二级域名或者其他域名。
文档参考（[Iframe origin policy](https://github.com/ampproject/amphtml/blob/master/spec/amp-iframe-origin-policy.md)）


