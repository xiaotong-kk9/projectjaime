# 在列表(amp-list)中无法完成每两个或每多个为整体循环渲染

功能实现方式：修改返回数据结构，分为两层数组，在amp-list的template中直接渲染。

## 解决方案

### 在返回数据中，提供两层数组

这里的示例功能为在carousel中每个slide

返回数据结构示例：
```
{  
   "items":[  
      {  
         "parentEle":[ //外层循环数组
            {  
               "childEle":[ //内层循环数组
                 {
                    "img":"urltoimg1.png"
                 },
                 {  
                    "img":"urltoimg2.png"
                 }
               ]
            },
            {  
               "childEle":[{
                  "img":"urltoimg1.png"
               },
               {  
                  "img":"urltoimg2.png"
               }]
            },
            {  
               "childEle":[{
                  "img":"urltoimg1.png"
               },
               {  
                  "img":"urltoimg2.png"
               }]
            }
         ]
      }
   ]
}
```

template示例：
```
<amp-list src="../json/data.json" width="auto" height="200" layout="fixed-height">
  <template type="amp-mustache">
    <amp-carousel type="slides" width="auto" height="200" layout="fixed-height">
    {{#parentEle}}
    <ul>
      {{#childEle}}
      <li>
        <amp-img src="{{img}}" width="100" height="100" layout="responsive"></amp-img>
      </li>
      {{/childEle}}
    </ul>
    {{/parentEle}}
    </amp-carousel>
  </template>
</amp-list> 
```