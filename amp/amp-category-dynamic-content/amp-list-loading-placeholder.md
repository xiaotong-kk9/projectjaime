# AMP-list切换src后，placeholder使用纯文字加载不明显，有什么更好的方法？

## 解决方案:

1. 如果AMP-list已有placerholder，那么可以直接使用amp-list的placeholder属性，在变更src的时候placeholder会自动显示，等数据加载成功后placeholder会自动隐藏。参考地址: https://ampbyexample.com/playground/#url=https://ampbyexample.com/components/amp-list/source/
2. 如果自身没有placeholder，我们推荐通过 http://tobiasahlin.com/spinkit/ 这里找寻合适placeholder，并添加到amplist中的placeholder中。关于placeholder的推荐来源，可以参考这篇自定义加载指针的文章: https://ampbyexample.com/advanced/custom_loading_indicators/
3. 附上Demo地址: https://webtest-12733.firebaseapp.com/AMP/ampList/loading.html
