# iOS编译
部署完服务后就可以开始客户端的编译。客户端提供源码，从[Github](https://github.com/wildfirechat/ios-chat)或者[码云](https://gitee.com/wfchat/ios-chat)下载最新的源码。

## 修改配置
找到```config.m```文件，仔细阅读这个文件里面的注释，修改```IM_SERVER_HOST```为你的IM服务器地址，比如```192.168.1.100```. 修改```APP_SERVER_ADDRESS```为你的应用服务器地址，比如```http://192.168.1.100:8888```。
> IM服务需要分别配置host，注意没有HTTP头和端口；APP服务配置host与端口组成的完整http地址。

## 运行
编译运行，填入您的手机号码，验证码填写服务器部署时指定的```superCode```，默认是 ```66666```（五个6）。
