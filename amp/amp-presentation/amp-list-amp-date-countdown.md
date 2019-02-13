# 在列表（amp-list）中使用倒计时（amp-date-countdown）出现模版报错

报错信息：The tag 'template' may not appear as a descendant of tag 'template'.

报错原因：模版不能够嵌套使用。

解决方案：将倒计时组件的模板拿到列表（amp-list）外面。


```
  <template type="amp-mustache" id="foo">
    {{d}}, {{h}} hours, {{m}} minutes and {{s}} seconds
  </template>

  <amp-list id="bar" src="/getList" layout="fixed-height" height="1000">
    <template type="amp-mustache">
      <amp-date-countdown timestamp-seconds="{{timestamp}}" layout="fixed-height" height="100" template="foo"></amp-date-countdown>
    </template>
  </amp-list>
```

参考文档: [[amp-date-countdown inside amp-list] - 'template' may not appear as a descendant of tag 'template'](https://github.com/ampproject/amphtml/issues/18385)