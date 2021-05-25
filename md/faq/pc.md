# PC 常见问题

## Q. 如何抓取日志
A. 协议栈会自己抓取最近5M的日志，将会对问题的解决提供非常大的帮助。协议栈日志在不同系统上存在不同的目录。在MAC上的目录是```~/Library/Application Support/{包名}/wildfirechat/{用户Id}/wfchat_{日期}.xlog```；在Linux上的目录是```~/.wildfirechat/data/{用户Id}/wfchat_{日期}.xlog```；在windows上的目录在```C:\Users\{登电脑登录用户名}\AppData\Roaming\wildfirechat\{用户Id}\wfchat_{日期}.xlog```。log是[mars](https://github.com/Tencent/mars)的```xlog```格式，没有密码。用户可以自己解压后分析，也可以发给我们分析问题。

## Q. 如何删掉截图依赖的QT
A. 有些客户自己有截图工具或者使用electron上的截图插件，就需要把官方PC版本所带的Qt依赖去掉。解决办法就是在pc工程目录下有{platform}-qt-denpendency，把其中除了```QtCore```以外的所有内容全部删掉。然后PC UI上截图按钮唤起自有的截图插件即可。
> ```QtCore```在不同平台有着不同的文件形式，windows下为```Qt5Core.dll```，mac下为```QtCore.framework```，linux下为```libQt5Core.so.5```。删除其他内容是需要保留```QtCore```的目录结构。

## Q. 手机端扫码提示会话不存在或者已过期？
A. 只有手机端和PC端所对应的APP、IM Server都相同时，才能扫码登录PC端。

    1. PC端需要购买```PC SDK```才能连接自己部署的服务，默认只能连接官方服务。确认是否想官方购买了```PC SDK```，如果未购买，可[申请试用](../quick_start/trial.md)
    2. 确认PC端```config.js```和手机端```Config.java```或```WFCConfig.m```所配置的```APP_SERVER```是否一致。

## Q. 扫码无法登录，如果让PC端连接自己部署的服务？
A. 请参考上一问题。

## Q. 二维码不显示
A. 控制台 -> 网络，看下pc_session请求是否正常访问你们部署的[app server](../quick_start/server.md)

## Q. 手机扫码，提示未登录或者错误
A. AppServer从0.40版本起引入了shiro，所有移动端的请求都需要进行认证，您需要把移动端升级到最新版本另外退出重新登录一下，具体原因请参考[这里](https://github.com/wildfirechat/im-app_server/blob/master/README.md#版本兼容)。如果还是无法解决问题，请自行DEBUG一下，相关部分所有代码都是开源的。

## Q. 开发者模式如何打开？发布版本如何关闭
A. 我们默认的快捷键Ctrl(mac下CMD)+G，可以在代码中搜索```toggleDevTools```找到如下代码，可以修改或者注释掉这个功能。但我们还是建议客户保留这个功能，如果出现问题可以进行调试。可以设置一个比较复杂的组合键防止客户误触。
```
globalShortcut.register('CommandOrControl+G', () => {
    mainWindow.webContents.toggleDevTools();
})
```

## Q. 如何更换icon等
A. 替换```build/icons```目录下的所有文件，此外，也需要替换```public/images```和```src/assets/images```下面的相应图片。

## Q. 如何将登录方式修改为账号密码登录？
A. IM本身只需要```userId```和```token```即可进行连接，故可以参考移动端的登录逻辑，去获取```userId```和```token```，其中需要注意的是：```token```和```clientId```、```platform```是绑定的，登录获取```token```时，这两个字段不能随便填写，需要分别通过```wfc.getClientId()```和```Config.getWFCPlatform()```获取。