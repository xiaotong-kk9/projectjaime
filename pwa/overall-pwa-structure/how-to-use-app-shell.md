# 如果我们使用了App Shell，那么我们需要通过AJAX/Fetch/xmlhttprequest获取内容，而且使用客户端渲染,这是可行的吗？

使用HTML/JS/CSS构建App Shell而且对fetch的内容使用客户端渲染是比较常见的方式。Fetch获取的动态内容可以是JSON也可以是服务端渲染好的HTML，是非常容易插入到页面中的。

其实还有其他方式，例如在页面加载时可以渲染App Shell其实可以充当一个占位符的作用，然后一旦页面渲染完成并且可用，便可以把App Shell替换掉。

