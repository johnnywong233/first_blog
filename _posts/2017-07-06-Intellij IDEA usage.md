### 1. 常用快捷键

Ctrl + Alt + L：格式化代码，值得注意的是左侧project视图下选中多个文件夹也可以实现对多个文件进行格式化；

Ctrl + Alt + Z：撤销本地修改，打开Revert change窗口；

Ctrl + Alt + N：打开文件；

Ctrl + Alt + R：全局搜索替换；

F11：添加标签bookmark；

Shift + F11：查看标签bookmark；

Shift + F6：重命名（重构）文件；

Ctrl + Shift + U：大小写切换；

Ctrl + Shift + J：整合两行；

Ctrl + Shift + F：全局查找；

Ctrl + D：复制光标所在行；

Ctrl + X：删除某一行，同时具有剪切的功能，然后可以使用Ctrl + V；

Ctrl + E：定位导航到最近打开的文件；如果想减少列表中的候选项，则可以借助Speed Search 功能——输入目标文件名中的一部分，列表将仅显示匹配项。

Ctrl + Shift + E：定位导航到最近编辑的文件；

Ctrl + Shift + T：定位导航到对应的UT类，没有的话，则新建；

Ctrl + G：定位到某一行，支持行号：列号这种用法；

Ctrl + Shift + N：支持**通配符、驼峰式命名以及目录名前缀**等方法进行搜索；支持**文件名：行号**打开文件且直接定位到异常堆栈出错行，如App.java:23

Ctrl + Shift + V：来进行访问历史粘贴板；

通过以下快捷键打开窗口，在工具窗口获得焦点时再按一次快捷键，工具窗口将会隐藏，返回全屏编辑器上工作

Alt + 1：打开Project工具窗口

Alt + 9：Changes工具窗口

Alt + F12：Terminal工具窗口

在左边栏可以看到颜色的方块上面安装Ctrl/Shift，点击鼠标左键，快捷换色。


### 2. IDEA文件打开方式
Intellij IDea IDE 修复文件打开方式：settings --> Editor -->File Types
比如将.propertites文件用yml的方式打开，则会提示红点。

那要想去掉，回归默认方式，则

![这里写图片描述](http://img.blog.csdn.net/20170624095134465?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbG9uZWx5bWFub250aGV3YXk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

去掉即可：

![这里写图片描述](http://img.blog.csdn.net/20170624095230409?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbG9uZWx5bWFub250aGV3YXk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

###3. IDEA目录
#### 安装目录介绍
如图：

![](/img/IDEA_bin.png)

IDEA 的安装目录并不复杂，上图为最常改动的 bin 目录，经常会改动的文件或是必须介绍就是如图红色框中的几个。

idea.exe 文件是IDEA32 位的可行执行文件，IntelliJ IDEA 安装完**默认**发送到桌面的也就是这个执行文件的快捷方式。

idea.exe.vmoptions 文件是 IntelliJ IDEA 32 位的可执行文件的 VM 配置文件；由于32位系统内存一般都是 2G 左右的（固定死），所以也没有多大空间可以调整，所以一般无需调整的。

idea64.exe 文件是 IntelliJ IDEA 64 位的可行执行文件，要求必须电脑上装有 JDK 64 位版本。64 位的系统也是建议使用该文件。

idea64.exe.vmoptions 文件是 IntelliJ IDEA 64 位的可执行文件的 VM 配置文件.

idea.properties：属性配置文件，没有 32 位和 64 位之分，修改原则主要根据个人对 IntelliJ IDEA 的个性化配置情况来分析。常修改的就是下面 4 个参数：

- idea.config.path=${user.home}/.IntelliJIdea/config，该属性主要用于指向 IntelliJ IDEA 的个性化配置目录，默认是被注释，打开注释之后才算启用该属性，这里需要特别注意的是斜杠方向，这里用的是正斜杠。
- idea.system.path=${user.home}/.IntelliJIdea/system，该属性主要用于指向 IntelliJ IDEA 的系统文件目录，默认是被注释，打开注释之后才算启用该属性，这里需要特别注意的是斜杠方向，这里用的是正斜杠。如果你的项目很多，则该目录会很大，如果你的 C 盘空间不够的时候，还是建议把该目录转移到其他盘符下。
- idea.max.intellisense.filesize=2500，该属性主要用于提高在编辑大文件时候的代码帮助。IntelliJ IDEA 在编辑大文件的时候还是很容易卡顿的。
- idea.cycle.buffer.size=1024，该属性主要用于控制控制台输出缓存。有遇到一些项目开启很多输出，控制台很快就被刷满了没办法再自动输出后面内容，这种项目建议增大该值或是直接禁用掉，禁用语句 idea.cycle.buffer.size=disabled。

#### 配置目录介绍
如图：

![](/img/IDEA_user.png)

config目录是IDEA 个性化化配置目录，或者说是整个 IDE 设置目录。安装新版本的 IntelliJ IDEA 会自动扫描硬盘上的旧配置目录，指的就是该目录。这个目录主要记录：IDE 主要配置功能、自定义的代码模板、自定义的文件模板、自定义的快捷键、Project 的 tasks 记录等等个性化的设置。

system目录是IDEA 系统文件目录，是IDEA 与开发项目一个桥梁目录，里面主要有：缓存、索引、容器文件输出等等。

设置目录进行多台设置同步化处理，把上述config设置为云盘的自动备份目录，可以使得多态开发机器使用一套配置环境（前提是多套开发机的CPU，内存配置相近）；修改 idea.properties 属性文件中的 idea.config.path 值，我的机器为：idea.config.path=F:/360SycDir/idea_config/config

实际上针对IDEA的配置还有一个setting.jar文件，导出并共用这个jar即可。

### 4. 修改鼠标定位点
**不推荐**。默认情况下，鼠标点哪里，光标就定位到哪里；现在想要实现，鼠标点哪里，光标就定位到当前行的末尾；

配置：file - settings - Editor面板中的Virtual Space组中的 Allow placement of caret after end of line配置项勾掉即可;