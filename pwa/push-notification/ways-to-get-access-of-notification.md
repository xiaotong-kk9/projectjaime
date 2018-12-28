# 想要获取Notification权限有什么比较可行的方式？

A. 如果是需要请求权限，可使用[RequestPermission](https://developer.mozilla.org/en-US/docs/Web/API/Notification/requestPermission)。

B. 如果仅仅是查询权限，可使用[Notification.permission](https://developer.mozilla.org/en-US/docs/Web/API/Notification/permission)和[navigator.permission.query\({name: 'notifications'}\).then\(\)](https://developer.mozilla.org/en-US/docs/Web/API/Permissions/query)。

