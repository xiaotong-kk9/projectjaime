# 图片优化

* [使用 Imagemin 来压缩图片](image-optimization.md#compress-image-with-imagemin)
* [使用懒加载来加载图片](image-optimization.md#use-lazyload)
* [使用响应式图片](image-optimization.md#responsive-image)
* [使用合适尺寸及格式的图片](image-optimization.md#image-with-correct-dimensions)
* [使用 webP](image-optimization.md#use-webp)

## 使用 Imagemin 来压缩图片 <a id="compress-image-with-imagemin"></a>

在很多情况下移动端的图片在合理压缩后仍然能保证高质量的展示效果。
Imagemin 可以通过 [CLI](https://github.com/imagemin/imagemin-cli) 和 [npm module](https://www.npmjs.com/package/imagemin) 使用。
参考文档: https://web.dev/use-imagemin-to-compress-images/

## 使用懒加载来加载图片 <a id="use-lazyload"></a>

使用 [lazysizes](https://github.com/aFarkas/lazysizes)。
lazysizes 应用非常简单，只要在页面引入 js ，再在需要懒加载的标签上添加 class="lazyload" 。
```
  <img data-src="flower.jpg" class="lazyload" alt="">

  <picture>
    <source type="image/webp" data-srcset="flower.webp">
    <source type="image/jpeg" data-srcset="flower.jpg">
    <img data-src="flower.jpg" class="lazyload" alt="">
  </picture>
```

## 使用响应式图片 <a id="responsive-image"></a>
使用 [sharp npm package](https://www.npmjs.com/package/sharp) 或者 [the ImageMagick CLI tool](https://www.imagemagick.org/script/index.php) 来调整图片。
使用 srcset 来提供不同尺寸图片。
```
  <img src="flower-large.jpg" srcset="flower-small.jpg 480w, flower-large.jpg 1080w" sizes="50vw">
```

## 使用合适尺寸及格式的图片 <a id="image-with-correct-dimensions"></a>
很多网站会为了方便在桌面端和移动端使用同一套图片，这是非常不推荐的。加载过大的图片会造成加载速度变慢以及流量浪费，同时又不会提升视觉效果。
更好的做法就是为移动端提供合适尺寸的图片，同时根据图片内容比较 PNG/JPEG/GIF 等格式，平衡视觉效果和图片大小选用最佳适用格式。

## 使用webP <a id="use-webp"></a>
webP 格式比 JPEG 和 PNG 都更小，是一种非常好的压缩格式，同时提供无损压缩及有损压缩。
webP 格式转换可以使用 [cwebp command-line tool](https://developers.google.com/speed/webp/docs/using) 或者 the[Imagemin WebP plugin](https://github.com/imagemin/imagemin-webp) (npm package)。
使用 webP 图片：
```
  <picture>
    <source type="image/webp" srcset="flower.webp">
    <source type="image/jpeg" srcset="flower.jpg">
    <img src="flower.jpg" alt="">
  </picture>
```