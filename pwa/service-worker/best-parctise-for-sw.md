##实现生产环境中最佳的SW的教程？

嗯，关于这个，我们有两点建议：
1. 可以使用[WorkboxJS](https://workboxjs.org/)，这个库是谷歌团队在维护的，致力于帮助开发者快速构建PWA。
2. 开发[kill switch(回退切换功能)](http://stackoverflow.com/questions/33986976/how-can-i-remove-a-buggy-service-worker-or-implement-a-kill-switch)，可以让你在某些错误发生的情况下能够及时删除PWA。