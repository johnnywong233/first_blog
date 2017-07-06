###1.Chrome浏览器http抓包
谷歌的 Chrome 浏览器自带一个功能强大的 HTTP 抓包工具，可以用于调试程序，监控 HTTP 信息交换。在浏览器地址栏输入 chrome://net-internals/#requests 即可进入。

示例：

chrome://net-internals/#dns

chrome://net-internals/#events&q=type:SPDY_SESSION%20is:active

### 2.我在用的Chrome 插件（extension）推荐
-  OneTab chrome的确好用，但是是内存大户，借助于OneTab 可以把需要留着待会儿看的标签页发送保存到onetab以节省内存，需要时再打开；另一方面，也可以当作收藏夹来使用，方便以后回来回顾干货网页，一定程度上可以理解为书签。
- Proxy SwitchSharp 代理切换工具，必备。
- adblock plus 广告屏蔽。
- postman rest api测试工具。可参考我的blog [postman使用](http://blog.csdn.net/lonelymanontheway/article/details/73320725)
- Octotree 借助于此插件，你可以直接在Chrome侧边栏向打开文件夹一样的查看GitHub上面的项目；还可以下载需要的单个文件、文件夹，而不必git clone整个项目。

###3.Chrome被劫持的解决方法
笔记本在使用一段时间后（可能是访问某些个不良网站之后），chrome被（毒霸，360，百度的hao123等等）劫持，桌面上的Chrome快捷方式以及任务栏的快速启动栏都被劫持：即打开Chrome之后，主页变成毒霸等的主页。看着恶心。右键快捷方式——属性——目标，尝试修改为正常的路径，失败：

![这里写图片描述](http://img.blog.csdn.net/20170623012937630?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbG9uZWx5bWFub250aGV3YXk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

笔记本上的唯一一款安全软件QQ管家启动也不能解决这个问题（是的，只有在需要的时候才打开QQ管家），最后的解决方法：

删除桌面的快捷方式以及解锁任务栏上面的Chrome，去Chrome的安装C:\Program Files (x86)\Google\Chrome\Application.exe，把快捷方式重新生成到桌面。

###4.extension安装
在较老版本Chrome（具体哪个版本号之前待考）安装后，在桌面的快捷图标，右键properties——shortcut，如果不是以**双引号**（现在是双引号，并且不允许修改其值）括起来的启动程序位置，则可以做如下修改。

C:\Users\wajian\AppData\Local\Google\Chrome\Application\chrome.exe **--enable-easy-off-store-extension-install**。

我当前的 Chrome版本58.0.3029.110 (64-bit)不可如此安装，估计是Chrome考虑到安全/权限问题。
同理，早先版本的Chrome如果被劫持，可以通过修改上面这种方法加以解决：把target里面的劫持商删除即可。

![这里写图片描述](http://img.blog.csdn.net/20170623014155443?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbG9uZWx5bWFub250aGV3YXk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

现在Chrome推荐的extension安装方式当然就是在线安装，因为可以实时校验？另一种安装方式是下载.crx后缀名的插件，拖到extension页面chrome://extensions/，这种方式可以离线安装，不安全，估计后期Chrome也会不支持。
