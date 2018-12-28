# 我想添加把我的Web添加到主屏幕有什么要求吗？

条件如下：

A. Web应用没被添加到主屏幕

B. 用户至少在跟Web应用中浏览30秒或以上。

C. 拥有[web app manifest](https://developers.google.com/web/fundamentals/web-app-manifest/).而且满足以下条件：

```text
short_name(主屏幕名称)
name(弹出安装横幅时名称)
至少包含192x192像素大小的icon图标
display模式，必须从fullscreen, standalog, minial-ui选一种。
```

D. Web应用必须使用https协议。

E. 已经注册了service worker.

具体可参考[添加到主屏幕的条件](https://developers.google.com/web/fundamentals/app-install-banners/#criteria).

