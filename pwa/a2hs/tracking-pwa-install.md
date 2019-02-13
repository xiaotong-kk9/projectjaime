# 如何追踪PWA已经正确安装到主屏幕上了?

A. [beforeinstallprompt](https://developer.mozilla.org/zh-CN/docs/Web/API/BeforeInstallPromptEvent)事件可以帮助我们追踪用户是否愿意添加到主屏幕, 可以参考[网网络应用横幅事件](https://developers.google.com/web/fundamentals/app-install-banners/?hl=zh-cn#_2)。

B. [appinstalled](https://developer.mozilla.org/en-US/docs/Web/Events/appinstalled)事件可以帮助我们追踪PWA是否正确安装到主屏幕中, 可以参考下图。 ![Image](https://github.com/xiaotong-tj/projectjaime/tree/5b3ff9ddc93a74b60a5e89a0fd88df928d214a75/pwa/resource/img/trackingAddToHomeScreen.png)

C. 附上一遍写的比较好的文章: [Tracking PWA events with Google Analytics](https://docs.google.com/document/d/15rTCnqWgzmvbjabY4uB_c9_Kox3QGRXs1xtR8Ghp1FE/edit)

DEMO link: [https://webtest-12733.firebaseapp.com/index\_a2hs.html](https://webtest-12733.firebaseapp.com/index_a2hs.html)

