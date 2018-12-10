#Add to HomeScreen系列

##问题列表

* [我想添加把我的Web添加到主屏幕有什么要求吗？](#add-to-hs-demand)
* [如何追踪PWA正确安装到主屏幕上了？](#tracking-pwa-install)


##我想添加把我的Web添加到主屏幕有什么要求吗? {#add-to-hs-demand}

条件如下：

A. Web应用没被添加到主屏幕

B. 用户至少在跟Web应用中浏览30秒或以上。

C. 拥有[web app manifest](https://developers.google.com/web/fundamentals/web-app-manifest/).而且满足以下条件：

    short_name(主屏幕名称)
    name(弹出安装横幅时名称)
    至少包含192x192像素大小的icon图标
    display模式，必须从fullscreen, standalog, minial-ui选一种。

D. Web应用必须使用https协议。

E. 已经注册了service worker.

具体可参考[添加到主屏幕的条件](https://developers.google.com/web/fundamentals/app-install-banners/#criteria).

##如何追踪PWA已经正确安装到主屏幕上了? {#tracking-pwa-install}

A. [beforeinstallprompt](https://developer.mozilla.org/zh-CN/docs/Web/API/BeforeInstallPromptEvent)事件可以帮助我们追踪用户是否愿意添加到主屏幕, 可以参考[网网络应用横幅事件](https://developers.google.com/web/fundamentals/app-install-banners/?hl=zh-cn#_2)。

B. [appinstalled](https://developer.mozilla.org/en-US/docs/Web/Events/appinstalled)事件可以帮助我们追踪PWA是否正确安装到主屏幕中, 可以参考下图。
![Image](../resource/img/trackingAddToHomeScreen.png)

C. 附上一遍写的比较好的文章: [Tracking PWA events with Google Analytics](https://docs.google.com/document/d/15rTCnqWgzmvbjabY4uB_c9_Kox3QGRXs1xtR8Ghp1FE/edit)

DEMO link: https://webtest-12733.firebaseapp.com/index_a2hs.html

