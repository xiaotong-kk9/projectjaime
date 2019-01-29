# 如何使用amp-app-banner在AMP中拉起原生应用(Native APP)或者跳转到应用安装界面

## 解决方案

### 
1. 通过meta和manifest定义IOS App和Android App的信息。
2. 定义一个AMP-app-banner的基本外观。(当浏览器环境没有自己的app install banner的时候会显示这个定义amp-app-banner的外观。在安卓上的Chrome和IOS上的Safari将不会显示这个定义的amp-app-banner，因为他们有自己的app install banner)
3. 在IOS Apps中和Android App中定义相应方法接收来自网页的url参数并且在APP进行相应的处理。




####1.通过meta和manifest定义IOS App和Android App的信息。
* 引入amp-app-banner组件

```
<script async custom-element="amp-app-banner" src="https://cdn.ampproject.org/v0/amp-app-banner-0.1.js"></script>
```

* 通过meta定义IOS App的信息
  
app-id是你的应用的唯一标识码（unique identifier), app-argument指传到Native APP进行处理的参数，AMP建议的格式是app-argument=app-name://link/to/app-content，可以参考下面medium这个应用的定义格式。关于IOS的更多meta信息可以参考：[Promoting Apps  with Smart App Banners](https://developer.apple.com/library/archive/documentation/AppleApplications/Reference/SafariWebContent/PromotingAppswithAppBanners/PromotingAppswithAppBanners.html)

```
<meta name="apple-itunes-app" content="app-id=828256236, app-argument=medium://p/9ea61abf530f">
```

* 通过amp-app-banner-manifest.json定义Android App的信息:
  
  ```
  <link rel="manifest" href="/amp-app-banner-manifest.json">
  ```

然后在amp-app-banner-manifest.json中原有的定义中添加上下面的代码。完整的栗子可以参考这个[链接](https://ampbyexample.com/amp-app-banner-manifest.json)

  ```
    {
        "prefer_related_applications": true, // This is not necessary for <amp-app-banner>, but signals a preference on non-AMP pages using the same manifest.json file for the native app over a web app if available
        "related_applications": [
            {
            "platform": "play",
            "id": "com.app.path",
            "url": "android-app://com.app.path/https/host.com/path/to/app-content"
            }
        ]
    }
  ```


####2.定义一个AMP-app-banner的基本外观。

```
<amp-app-banner layout="nodisplay"
  id="my-app-banner">
  <amp-img src="https://cdn-images-1.medium.com/max/50/1*JLegdtjFMNgqHgnxdd04fg.png"
    width="50"
    height="43"
    layout="fixed"></amp-img>
  <div class="banner-text">Learn more in the app.</div>
  <button open-button>View in app</button>
</amp-app-banner>
```

####3.在IOS Apps中和Android App中定义相应的方法接收来自网页的url参数并且在APP进行相应的处理

在Android App中你需要定义一个Activity来接收这个url参数,可以参考下面的栗子:

```
<activity
    android:name="com.example.android.GizmosActivity"
    android:label="@string/title_gizmos" >
    <intent-filter android:label="@string/view_article">
        <!-- This is important in order to allow browsers to launch your app. -->
        <category android:name="android.intent.category.BROWSABLE" />
        <!-- Accepts URIs that begin with "https://CANONICAL_HOST/gizmos” -->
        <data android:scheme="https"
              android:host="CANONICAL_HOST"
              android:pathPrefix="/" />
    </intent-filter>
</activity>
```

在IOS App中你需要定义一个方法来接收url参数, 例如下面的栗子:

```
- (BOOL)application:(UIApplication *)application openURL:(NSURL *)url sourceApplication:(NSString *)sourceApplication annotation:(id)annotation
{
    // in this example, the URL from which the user came is http://example.com/profile/?12345
    // determine if the user was viewing a profile
    if ([[url path] isEqualToString:@"/profile"]) {
        // switch to profile view controller
        [self.tabBarController setSelectedViewController:profileViewController];
        // pull the profile id number found in the query string
        NSString *profileID = [url query];
        // pass profileID to profile view controller
        [profileViewController loadProfile:profileID];
    }
    return YES;
}
```