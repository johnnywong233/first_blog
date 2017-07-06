#### 1. Eclipse 启动错误 java-was-started-but-returned-exit-code-1
参考[解决方案](http://stackoverflow.com/questions/18609160/eclipse-returns-error-message-java-was-started-but-returned-exit-code-1).

在eclipse.ini文件添加jre下面的jvm.dll文件：
```
-vm
C:\Program Files\Java\jdk1.8.0_77\jre\bin\server\jvm.dll
```

值得一提的是，我在工作中主要使用的一款开源数据库连接、管理....（很强大的，有时间可以另写一篇blog）工具Dbeaver，在某一次启动时候报类似的错误：

![这里写图片描述](http://img.blog.csdn.net/20170623010734864?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbG9uZWx5bWFub250aGV3YXk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

又因为Dbeaver是基于Eclipse项目开发的，其界面和Eclipse也是如出一辙。类似地，在dbeaver.ini文件添加：

```
-vm
C:\Program Files\Java\jdk1.8.0_77\jre\bin\server\jvm.dll
```

问题解决。