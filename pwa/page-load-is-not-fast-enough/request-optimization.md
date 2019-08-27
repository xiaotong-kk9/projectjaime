# 网络请求优化

* [延迟首屏以下内容的加载请求](request-optimization.md#defer-request-below-the-fold)
* [使用Preconnect来与重要的域名建立连接](request-optimization.md#preconnect-required-origins)
* [使用 Network Information API 判断网络请求质量 ](request-optimization.md#adaptive-serving-based-on-network-quality)

## 延迟首屏以下内容的加载请求 <a id="defer-request-below-the-fold"></a>

并非所有的加载都需要在页面初始化时执行，可以将部分网络请求设置为用户操作或页面滚动至特定位置触发。


## 使用Preconnect来与重要的域名建立连接 <a id="preconnect-required-origins"></a>

评估所有第三方域名请求的优先级，将重要的域名使用preconnect优先建立连接。
```
<link rel="preconnect" href="https://example.com">
```
如果不希望优先建立连接，而又想要提升连接速度，可以使用dns-prefetch标签，该标签可以优先进行相应域名的dns解析而不建立连接。
```
<link rel="dns-prefetch" href="https://example.com">
```

## 使用 Network Information API 判断网络请求质量 <a id="adaptive-serving-based-on-network-quality"></a>

使用 Network Information API 判断网络类型。如果网络为4G或wifi可以考虑使用高质量图片，提供视频自动播放等等优化用户体验。
如果网络为3G或更差，请尽量使用压缩过的图片，减少动画视频加载。
通过navigator.connection来得到网络相关信息。
```
  {
    downlink: 7.7, //带宽7.7Mbps
    downlinkMax: Infinity, //带宽最大值无穷
    effectiveType: "4g", //连接有效类型，值一般为slow-2g，2g，3g或者4g
    onchange: null, //Event handler，当网络信息变化时触发
    ontypechange: null, //Event handler，当网络类型变化时触发
    rtt: 100, //连接的round-trip latency为100ms
    saveData: false, //用户是否为节省流量模式
    type: "wifi" //连接类型
  }
```