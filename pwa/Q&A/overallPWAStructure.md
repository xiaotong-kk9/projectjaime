# verall PWA Structure(总体PWA架构)

##问题列表：

* [构建PWA时使用什么架构比较好?](#which-structure-works-well-for-PWA)
* [现在PWA特性在浏览器中支持情况如何？](#PWA-feature-suppport-status)
* [我可以使用什么框架构建PWA吗？](#which-framework-workx-well-for-PWA)
* [我想用户打开网站的时候就预缓存首页index.htm以及常用的CSS和JS该怎么做？](#precache-app-shell)
* [如果我们使用了App Shell，那么我们需要通过AJAX/Fetch/xmlhttprequest获取内容，而且使用客户端渲染,这是可行的吗？](#how-to-use-app-shell)
* [我使用的是Angular或者是React构建的应用，也可以用来构建PWA吗?](#react-angular-for-PWA)


##构建PWA时用什么架构比较好？{#which-structure-works-well-for-PWA}
建议使用[Application Shell](https://developers.google.com/web/fundamentals/architecture/app-shell)，这样的话非常适合缓存优先的缓存策略，可以帮助PWA加载更快，而且独立于网络，即网络情况不好也能呈现一定内容给用户。


##现在PWA特性在浏览器中支持情况如何？{#PWA-feature-suppport-status}
可以参考[caniuse](https://caniuse.com/).

##我可以使用什么框架构建PWA吗？{#which-framework-workx-well-for-PWA}
嗯，怎么说呢？这完全取决于你。下面列举了一些可以快速帮助你构建PWA的框架：

* [Polymer App Toolbox](https://polymer-library.polymer-project.org/3.0/docs/devguide/feature-overview), 由谷歌的团队维护。

* [Create React App](https://github.com/facebookincubator/create-react-app)

* [Preact CLI](https://github.com/developit/preact-cli)

* [Vue PWA Template](https://github.com/developit/preact-cli)


##我想用户打开网站的时候就预缓存首页以及常用的CSS和JS该怎么做？{#precache-app-shell}

使用install事件，即SW首次安装发生的事件中进行Cache缓存，但是要注意的是，如果使用cache.addAll进行缓存的话，资源一定要保证正确的返回，否则SW将会安装失败。可参考开发[第一个服务工作线程](https://developers.google.com/web/fundamentals/primers/service-workers/lifecycle#_2)， [install事件如何缓存APP Shell及缓存说明](https://developers.google.com/web/ilt/pwa/caching-files-with-service-worker#storing_resources)

##如果我们使用了[App Shell](https://developers.google.com/web/fundamentals/architecture/app-shell)，那么我们需要通过AJAX/Fetch/xmlhttprequest获取内容，而且使用客户端渲染(Client side rendering),这是可行的吗？{#how-to-use-app-shell}

使用HTML/JS/CSS构建App Shell而且对fetch的内容使用客户端渲染是比较常见的方式。Fetch获取的动态内容可以是JSON也可以是服务端渲染好的HTML，是非常容易插入到页面中的。

其实还有其他方式，例如在页面加载时可以渲染App Shell其实可以充当一个占位符的作用，然后一旦页面渲染完成并且可用，便可以把App Shell替换掉。

##我使用的是Angular或者是React构建的应用，也可以用来构建PWA吗?{#react-angular-for-PWA}
当然可以，你可以使用任何框架来构建你想要的PWA，例如添加到主屏幕，增加启动屏幕，还有安装Service worker还有缓存我们想要的内容。

##如果我想要在PWA中开发infinite list, 按下返回按钮后能够回到原来的位置呢，有什么比较好的建议吗？
这取决于你使用的框架。

如果你使用的是React，可以使用[react-virtualized](https://github.com/bvaughn/react-virtualized).

如果使用的是Polymer，可以使用[iron-list](https://www.webcomponents.org/element/PolymerElements/iron-list)

