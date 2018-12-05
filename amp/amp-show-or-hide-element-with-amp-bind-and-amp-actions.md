# 隐藏的元素无法通过触发事件展示

请首先在开发者工具中检查目标元素是否被页面其他元素遮挡，检查目标元素CSS设置，是否存在颜色与背景色一致，透明度设置为0，位置在viewport以外的情况。

## 功能实现方式

* [使用amp-bind组件和show/hide方法](#amp-bind-show-hide)
* [使用amp-bind组件和setState更新元素hidden属性](#amp-bind-amp-setState)

## 解决方案

#### 使用amp-bind组件和show/hide方法 {#amp-bind-show-hide}

可能导致问题原因：show/hide方法原理是切换元素属性上的hidden，无法覆盖通过css设置的display:none。

解决方案：去掉元素上的display:none，使用hidden来设置默认隐藏。

```javascript
<p id="foo" hidden>content...</p>
<button type="button" on="tap:foo.show">show</button>
```

文档参考：
[amp-bind官方文档](https://www.ampproject.org/docs/reference/components/amp-bind)
[actions-and-events官方文档](https://www.ampproject.org/docs/interaction_dynamic/amp-actions-and-events#globally-defined-events-and-actions)



#### 使用amp-bind组件和setState更新元素hidden属性 {#amp-bind-amp-setState}

可能导致问题原因：为元素更新hidden的值，无法覆盖通过css设置的display:none。hidden的值需为boolean，不能够为false添加引号。

解决方案：去掉元素上的display:none，去掉setState中引号。

```javascript
<p hidden [hidden]="fooStatus">content...</p>
<button type="button" on="tap:AMP.setState({fooStatus:false})">show</button>
```

文档参考：
[amp-bind官方文档](https://www.ampproject.org/docs/reference/components/amp-bind)