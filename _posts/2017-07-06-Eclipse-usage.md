#### Eclipse 启动错误 java-was-started-but-returned-exit-code-1
参考[解决方案](http://stackoverflow.com/questions/18609160/eclipse-returns-error-message-java-was-started-but-returned-exit-code-1).

在eclipse.ini文件添加jre下面的jvm.dll文件：
```
-vm
C:\Program Files\Java\jdk1.8.0_77\jre\bin\server\jvm.dll
```
值得一提的是，我在工作中主要使用的一款开源数据库连接、管理....（很强大的，有时间可以另写一篇blog）工具Dbeaver，在某一次启动时候报类似的错误：

![](http://img.blog.csdn.net/20170623010734864?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbG9uZWx5bWFub250aGV3YXk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

又因为Dbeaver是基于Eclipse项目开发的，其界面和Eclipse也是如出一辙。类似地，在dbeaver.ini文件添加：

```
-vm
C:\Program Files\Java\jdk1.8.0_77\jre\bin\server\jvm.dll
```
问题解决。

#### Eclipse安装插件的几种方式
Eclipse魅力之一就是支持可扩展的插件来丰富自身的功能。有以下几种插件安装方式：
- 拿到的是一串URL，步骤：Help-->Install new software-->Add，给插件起个名字，然后输入链接，OK之后，等待Eclipse自动检索，这种方式要建立在网速良好的情况下，检索完成后，选择需要的组件，Next-->Finish，重启Eclipse，插件安装完成。
- 拿到的是一个jar包或者是类似包名的文件夹，如 http://download.eclipse.org/eclipse/updates/4.3-P-builds/，把jar包或者文件夹直接放到eclipse\plugins下，重启Eclipse，插件安装完成。（注意如果有两个文件夹plugins和features，则分别copy到Eclipse对应的文件夹下面）
- Help, marketplace, 搜索想要安装的插件，注意不一定有你想要的，因为这个是官方的插件库，而很多时候我们想要安装的插件没有放在官方的插件库里面。
- 使用link的方式安装步骤，在硬盘任意目录建立一个文件夹，用来存储link插件，如：D:\myPlugins，将plugin和feature放到D:\myPlugins\你的插件名称\eclipse下，注意，这个eclipse文件夹是必须的。然后在Eclipse安装目录下，新建links文件夹，在里面新建一个txt，内容为path=D:\\myPlugins\\你的插件名称，路径为\\或/，最后将txt重命名为你的插件名称.link，重启Eclipse，插件安装完成。这种方式可以更好的管理自己的插件，随时插拔，某个插件不想用时，将对应link文件删除即可。

插件列表：
[1](http://www.open-open.com/04.htm)
[2](http://www.csdn.net/article/2013-06-17/2815779-Eclipse)
[3](http://www.csdn.net/article/2012-09-12/2809862-6-java-to-uml-tools)
[4](http://marketplace.eclipse.org/)

#### 