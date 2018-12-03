# 使用amp-bind和show/hide事件展示或隐藏元素

## 功能描述

页面元素需要通过点击或其他事件触发元素展示或隐藏。

---
## 解决方案

使用组件/方法：
amp-bind组件和show/hide方法。

文档参考：
[amp-bind官方文档](https://www.ampproject.org/docs/reference/components/amp-bind)
[actions-and-events官方文档](https://www.ampproject.org/docs/interaction_dynamic/amp-actions-and-events#globally-defined-events-and-actions)

实施方法：
为目标元素设置ID，通过为按钮绑定tap或其他事件，来执行show/hide方法。


展示元素：

```javascript
<p id="foo" hidden>content...</p>
<button type="button" on="tap:foo.show">show</button>
```


隐藏元素：

```javascript
<p id="foo">content...</p>
<button type="button" on="tap:foo.hide">hide</button>
```

---
## 相关问题

#### 默认隐藏的元素无法展示

show/hide方法原理是切换元素属性上的hidden，无法覆盖通过css设置的display:none。
