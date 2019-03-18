# 当使用的图片的宽高是不确定时，想要保证图片的比例正常显示，应该怎么处理？

## 解决思路

1.包含AMP-img的父元素宽高是确定的(或者高度是确定的)。
2.对AMP-img使用fill的layout以及使用CSS 3的属性Object-fit: contain或者Object-fit:cover属性 ，这样amp-img会直接继承父元素的宽高，图片将有可能被放大，并且部分内容会被裁剪，但是图片还能保持原来的比例，不会被拉伸。

####方案一：图片不会被放大，按照自身比例显示， 示例代码如下:

![Image](../../.gitbook/assets/amp-img-unknown-dimension-contain.png)

a.CSS部分

```
// 父元素
.fixed-height-container {
    position: relative;
    width: 100%;
    height: 300px;
}
// AMP-img元素
amp-img.contain img {
    object-fit: contain;
}
```

b.HTML部分

```
<div class="fixed-height-container">
    <amp-img class="contain" layout="fill" src="https://unsplash.it/400/300"></amp-img>
</div>
```


####方案二：图片会放大到能完全填充父元素的宽高，但部分内容会被裁剪, 示例代码如下：

![Image](../../.gitbook/assets/amp-img-unknown-dimension-cover.png)

a.CSS部分

```
// 父元素
.fixed-height-container {
    position: relative;
    width: 100%;
    height: 300px;
}
// AMP-img元素
amp-img.contain img {
    object-fit: cover;
}
```

b.HTML部分
```
<div class="fixed-height-container">
    <amp-img class="cover" layout="fill" src="https://unsplash.it/1920/480"></amp-img>
</div>
```