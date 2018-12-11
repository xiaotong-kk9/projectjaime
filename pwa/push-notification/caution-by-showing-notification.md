##如果想要展示Notification需要注意些什么?

如果想要展示Notification需要获取权限，同时需要用户点击同意后调用回调函数处理即可。但是一定要注意的一点是，请求Notification只有一次机会， 如果用户点击了不同意的按钮，那么将永久没有办法进行Notification。建议根据[权限请求设计建议](https://developers.google.com/web/fundamentals/push-notifications/permission-ux)设计来控制自己的请求权限的时间还有条件。

可参考[Notification如何请求通知权限](https://developers.google.com/web/fundamentals/push-notifications/subscribing-a-user#requesting_permission)。