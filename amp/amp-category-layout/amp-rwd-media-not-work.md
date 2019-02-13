# 响应式页面AMP组件media不生效

## 解决方案

### 为AMP组件添加media属性，控制组件在不同屏幕大小下是否展示

可能导致问题原因：media格式出错

解决方案：media属性如果使用and连接两个条件左右要有空格

```css
<amp-img
    media="(min-width: 650px)"
    src="wide.jpg"
    width=466
    height=355
    layout="responsive">
</amp-img>
```

```css
<amp-img
    media="(max-width: 650px) and (min-width: 100px)"
    src="medium.jpg"
    width=466
    height=355
    layout="responsive">
</amp-img>
```

```css
<amp-img
    media="(max-width: 100px)"
    src="narrow.jpg"
    width=466
    height=355
    layout="responsive">
</amp-img>
```

文档参考： [Layout & media queries官方文档](https://www.ampproject.org/docs/design/responsive/control_layout#using-media-queries)

