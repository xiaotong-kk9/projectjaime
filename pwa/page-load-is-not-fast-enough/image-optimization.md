# 图片优化

* [使用 Imagemin 来压缩图片](image-optimization.md#compress-image-with-imagemin)
* [使用懒加载来加载图片](image-optimization.md#use-lazyload)
* [使用响应式图片](image-optimization.md#responsive-image)
* [使用合适尺寸及格式的图片](image-optimization.md#image-with-correct-dimensions)
* [使用 webP](image-optimization.md#use-webp)

## 使用 Imagemin 来压缩图片 <a id="compress-image-with-imagemin"></a>

在很多情况下移动端的图片在合理压缩后仍然能保证高质量的展示效果。

Imagemin 是一款很好的压缩工具，可以通过 [CLI](https://github.com/imagemin/imagemin-cli) 和 [npm module](https://www.npmjs.com/package/imagemin) 使用。通常来说，npm module 提供了更多的配置选项，所以更推荐使用。

Imagemin 提供有损压缩和无损压缩两种形式，不同图片格式的不同压缩形式需要使用相应的插件([插件列表](https://www.npmjs.com/search?q=imagemin))。使用前请确认插件是有损还是无损，是否满足压缩需求。

参考文档: https://web.dev/use-imagemin-to-compress-images/

## 使用懒加载来加载图片 <a id="use-lazyload"></a>

懒加载是一种提高页面访问速度的很有效的策略，当资源浏览到的时候再加载，从而减少访问页面时初始加载资源数量。

[lazysizes](https://github.com/aFarkas/lazysizes) 可以帮助开发者方便地进行懒加载的设置。

应用 lazysizes 非常简单，只要在页面引入 js，再在需要懒加载的标签上添加 class="lazyload"。

```
  <img data-src="flower.jpg" class="lazyload" alt="">

  <picture>
    <source type="image/webp" data-srcset="flower.webp">
    <source type="image/jpeg" data-srcset="flower.jpg">
    <img data-src="flower.jpg" class="lazyload" alt="">
  </picture>
```

想要验证懒加载是否生效可以打开浏览器的开发者工具，重新加载页面，会观察到只加载了一部分资源（首屏展示的资源及未添加class="lazyload"的资源）。
随着页面滚动，首屏下方的资源才会加载展示。

## 使用响应式图片 <a id="responsive-image"></a>

响应式图片是一种为不同设备提供不同图片来减少资源大小提升加载速度的策略。

调整图片尺寸可以使用 [sharp npm package](https://www.npmjs.com/package/sharp) 或者 [the ImageMagick CLI tool](https://www.imagemagick.org/script/index.php) 。

加载不同尺寸图片可以使用 srcset。
```
  <img src="flower-large.jpg" srcset="flower-small.jpg 480w, flower-large.jpg 1080w" sizes="50vw">
```

想要验证响应式图片是否生效可以打开浏览器的开发者工具，将浏览器窗口尺寸调整为不同大小，查看资源加载信息。

## 使用合适尺寸及格式的图片 <a id="image-with-correct-dimensions"></a>

很多网站会为了方便在桌面端和移动端使用同一套图片，这是非常不推荐的。加载过大的图片会造成加载速度变慢以及流量浪费，同时又不会提升视觉效果。

更好的做法就是为移动端提供合适尺寸的图片，同时根据图片内容比较 PNG/JPEG/GIF 等格式，平衡视觉效果和图片大小选用最佳适用格式。

调整图片尺寸可以使用 [the ImageMagick CLI tool](https://www.imagemagick.org/script/index.php)。

想要验证图片尺寸是否合适，可以使用 lighthouse 测试页面，如果Opportunities中出现Properly size images，说明仍然有图片尺寸不合适，请查看报错信息中列出的图片重新检查调整。

## 使用webP <a id="use-webp"></a>

webP 格式比 JPEG 和 PNG 都更小，通常可以减少25-35%，是一种非常好的图片格式，同时提供无损压缩及有损压缩。

webP 格式转换可以使用 [cwebp command-line tool](https://developers.google.com/speed/webp/docs/using) 或者 the[Imagemin WebP plugin](https://github.com/imagemin/imagemin-webp) (npm package)。

使用 webP 图片：
```
  <picture>
    <source type="image/webp" srcset="flower.webp">
    <source type="image/jpeg" srcset="flower.jpg">
    <img src="flower.jpg" alt="">
  </picture>
```
如果浏览器不支持 picture 标签，只会展示 img 标签的图片内容。

想要验证图片格式，可以在浏览器开发者工具中查看加载图片格式。