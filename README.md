# ueditor
springboot整合ueditor实现 主要解决了图片及视频上传及数据回显的问题
虽然说不是很难，但是觉着思考与解决问题的过程比问题本身更重要，所以把整个过程记录下来:)
公司的一个项目  后端是springboot，用的是技术部自己的框架，无非就是整合了ssm，spring security，flowable工作流等等东西。前端一开始准备用react，后来因为不知道啥原因，还是改用的bootstrap和jquery。
由于百度的ueditor只提供了后端jsp的源码，对于使用纯html或前后端分离的生产环境，需要开发者自己修改源码来整合项目

首先将主要的jar包引入 之前在网上找的demo是使用的thymyleaf做模板引擎，这里没有使用（使用模板引擎的具体例子:https://juejin.im/entry/58ec6da7ac502e006badd7c0）

1.将ueditor自带的静态资源文件导入
2.写ueditor跳转的controller方法，默认的mapping是/config
3.加载json资源文件是在ConfigManager类的getConfigPath方法。在这里有一个问题，用阿里的代码规范检查插件扫描源码时，调用JsonObject的方法时，会出现未抛出异常的错误，JsonObject的原方法抛出了异常，按理来说在使用他的方法时也应该抛出异常，但是源码中没有抛出，并且能够编译通过。。。到现在也没有找到是什么原因。
4.更改BinaryUploader类，获取字节流
5.修改json文件，更改上传文件的路径
6.最后上传视频时出现了错误，debug发现是tomcat上传文件大小的限制，springboot可以在入口函数中及配置文件中更改文件大小的设置。

