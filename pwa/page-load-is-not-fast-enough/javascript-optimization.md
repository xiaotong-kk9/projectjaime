# JS优化

* [使用 Preload 优先加载重要资源](javascript-optimization.md#preload-critical-assets)
* [去掉未使用的 JS 代码](javascript-optimization.md#remove-unused-javascript)
* [削减及压缩 JS 资源](javascript-optimization.md#compress-javascript)

## 使用 Preload 优先加载重要资源 <a id="preload-critical-assets"></a>

Preload 是一种声明式的 fetch 请求，它会告诉浏览器有重要的资源需要尽快加载。浏览器会为该资源分配最高的优先级，并且在未推迟 window.onload 事件的时候尝试下载。
```
<link rel="preload" as="script" href="critical_js.js">
<link rel="preload" as="style" href="critical_style.css">
<link rel="preload" as="video" href="critical_video.mp4" type="video/mp4">
<link rel="preload" as="font" href="fonts/critical_webfont.woff2" type="font/woff2">
<link rel="preload" as="image" href="critical_image.png" media="(max-width: 600px)">
```

Prefetch 是另一种告诉浏览器资源很重要的标记。标记 Prefetch 的资源的优先级较低，会在当浏览器结束了所有页面需要的网络请求之后再去请求。
如果需要提升下一个页面的加载速度，使用 prefetch 来请求资源。
```
<link rel="prefetch" as="script" href="important-for-next-page.js">
```

## 去掉未使用的 JS 代码 <a id="remove-unused-javascript"></a>
在使用 npm 来管理 js 包的时候，我们经常会添加我们可能并不会充分利用的库。针对这个问题，我们需要分析 bundle 来检测没有使用的代码，然后去掉未使用和不需要的库。

要分析 bundle，最简单的方式就是在 DevTools 的 Network 中勾选 Disable Cache，然后重新加载页面。
在 Coverage 中可以查看 CSS 资源和 JS 资源中有多少代码是未使用的。

如果你在使用 webpack，可以使用 [Webpack Bundle Analyzer](https://github.com/webpack-contrib/webpack-bundle-analyzer) 来查看 bundle 的组成。如果你在使用其他 bundler 比如说 [Parcel](https://parceljs.org/) 或者 [Rollup](https://rollupjs.org/guide/en/)， 也有可视化工具可以分析bundle。

要去掉未使用的库，可以在 Webpack Bundle Analyzer 的图表中看到有一些 package 在同一个 domain 下。
比如说 <strike>import firebase from 'firebase';</strike>
```
import firebase from 'firebase/app';
import 'firebase/database';
```

要去掉不需要的代码，可以在现有库的基础上，优化出一个轻量版本。


## 削减及压缩 JS 资源 <a id="compress-javascript"></a>

削减及压缩 JS 可以减少资源大小，提升网页加载效率。

其中削减指的是去掉空格和非必要代码，在不影响代码功能的情况下，创建一份更小的代码。
[terser](https://github.com/terser-js/terser)就是一个很受欢迎的削减压缩工具，webpack v4已经默认导入了这个插件来创建压缩过的构建文件。

压缩指的是通过压缩算法来修改数据达到压缩效果。
[Gzip](https://www.youtube.com/watch?v=whGwm0Lky2s&feature=youtu.be&t=14m11s)是现在服务端和客户端交互中最广泛使用的压缩格式。
[Brotli](https://opensource.googleblog.com/2015/09/introducing-brotli-new-compression.html)是一种比较新的压缩算法，可以提供比Gzip更好的压缩效果。

压缩分为两种形式，一种是动态压缩，一种是静态压缩。

动态压缩可以使用 [Express](https://expressjs.com/) 和 [compression](https://github.com/expressjs/compression) 当资源被请求的时候才进行压缩。
```
const express = require('express');
const compression = require('compression');

const app = express();

app.use(compression());

app.use(express.static('public'));

const listener = app.listen(process.env.PORT, function() {
	console.log('Your app is listening on port ' + listener.address().port);
});
```
这种压缩方式用的是gzip。如果服务器支持，可以使用像是 [shrink-ray](https://github.com/aickin/shrink-ray#readme) 模块来通过 Brotli 达到更好的压缩效果。

静态压缩可以使用 [BrotliWebpackPlugin](https://github.com/mynameiswhm/brotli-webpack-plugin) 或者 [CompressionPlugin](https://github.com/webpack-contrib/compression-webpack-plugin)。压缩插件可以像其他插件一样直接放在 webpack 的配置文件中：
```
module.exports = {
	//...
	plugins: [
		//...
		new CompressionPlugin()
	]
}
```
当压缩资源存在 build 文件夹中，在服务器中创建一个路由来处理所有的 JS 端点来提供压缩的资源。
```
const express = require('express');
const app = express();

app.get('*.js', (req, res, next) => {
	req.url = req.url + '.gz';
	res.set('Content-Encoding', 'gzip');
	next();
});

app.use(express.static('public'));
```