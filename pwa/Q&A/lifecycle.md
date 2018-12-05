# PWA生命周期系列

问题列表：
* [我想用户打开网站的时候就预缓存首页index.htm以及常用的CSS和JS该怎么做？](#precache-app-shell)


##我想用户打开网站的时候就预缓存首页以及常用的CSS和JS该怎么做？{#precache-app-shell}

使用install事件，即SW首次安装发生的事件中进行Cache缓存，但是要注意的是，如果使用cache.addAll进行缓存的话，资源一定要保证正确的返回，否则SW将会安装失败。可参考开发[第一个服务工作线程](https://developers.google.com/web/fundamentals/primers/service-workers/lifecycle#_2)， [install事件如何缓存APP Shell及缓存说明](https://developers.google.com/web/ilt/pwa/caching-files-with-service-worker#storing_resources)