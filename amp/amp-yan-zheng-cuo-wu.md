# AMP 验证错误

## 文档

[AMP 验证错误官方文档（中文）](https://www.ampproject.org/zh_cn/docs/troubleshooting/validation_errors)

[解决验证错误（中文）](https://www.ampproject.org/zh_cn/docs/fundamentals/converting/resolving-errors)

[AMP 验证错误完整概述（英文）](https://github.com/ampproject/amphtml/blob/master/validator/validator-main.protoascii)

* [Origin of &lt;amp-iframe&gt; must not be equal to container.](amp-yan-zheng-cuo-wu.md#origin-of-amp-iframe)
* [The author stylesheet specified in tag 'style amp-custom' is too long.](amp-yan-zheng-cuo-wu.md#stylesheet-too-long)
* [The author stylesheet specified in tag 'style amp-custom' and the combined inline styles is too long.](amp-yan-zheng-cuo-wu.md#stylesheet-custom-and-inline-too-long)

### Origin of &lt;amp-iframe&gt; must not be equal to container. <a id="origin-of-amp-iframe"></a>

amp-iframe 的 sandbox 属性如果添加了 allow-same-origin ，引入的内嵌页面不能和父级页面在同一个域名，要放在二级域名或者其他域名。 文档参考（[Iframe origin policy](https://github.com/ampproject/amphtml/blob/master/spec/amp-iframe-origin-policy.md)）

### The author stylesheet specified in tag 'style amp-custom' is too long. <a id="stylesheet-too-long"></a>

style amp-custom 中的css太多，超过50kb，需要减少css代码。

### The author stylesheet specified in tag 'style amp-custom' and the combined inline styles is too long. <a id="stylesheet-custom-and-inline-too-long"></a>

style amp-custom 和 HTML标签上的行内 css 加起来太多，超过50kb，需要减少css代码。

