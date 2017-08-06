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

Ctrl + F12: 相当于Eclipse的快捷键Ctrl + O, 打开方法；

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
IntelliJ IDea IDE 修复文件打开方式：settings --> Editor -->File Types
比如将.propertites文件用yml的方式打开，则会提示红点。

那要想去掉，回归默认方式，则

![](http://img.blog.csdn.net/20170624095134465?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbG9uZWx5bWFub250aGV3YXk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

去掉即可：

![](http://img.blog.csdn.net/20170624095230409?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbG9uZWx5bWFub250aGV3YXk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

### 3. IDEA目录
#### 安装目录介绍
如图：

![](https://github.com/johnnywong233/first_blog/raw/gh-pages/_posts/img/IDEA_bin.png)

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

![](https://github.com/johnnywong233/first_blog/raw/gh-pages/_posts/img/IDEA_user.png)

config目录是IDEA 个性化化配置目录，或者说是整个 IDE 设置目录。安装新版本的 IntelliJ IDEA 会自动扫描硬盘上的旧配置目录，指的就是该目录。这个目录主要记录：IDE 主要配置功能、自定义的代码模板、自定义的文件模板、自定义的快捷键、Project 的 tasks 记录等等个性化的设置。

system目录是IDEA 系统文件目录，是IDEA 与开发项目一个桥梁目录，里面主要有：缓存、索引、容器文件输出等等。

设置目录进行多台设置同步化处理，把上述config设置为云盘的自动备份目录，可以使得多态开发机器使用一套配置环境（前提是多套开发机的CPU，内存配置相近）；修改 idea.properties 属性文件中的 idea.config.path 值，我的机器为：idea.config.path=F:/360SycDir/idea_config/config

实际上针对IDEA的配置还有一个setting.jar文件，导出并共用这个jar即可。

### 4. 修改鼠标定位点
**不推荐**。默认情况下，鼠标点哪里，光标就定位到哪里；现在想要实现，鼠标点哪里，光标就定位到当前行的末尾；

配置：file - settings - Editor面板中的Virtual Space组中的 Allow placement of caret after end of line配置项勾掉即可;

### 5. Alt + Enter import出问题
问题描述，.java源文件需要引用import java.lang.reflect.Field;类，但是Alt + Enter快捷键不起作用，没有提示这个类。

重启IntelliJ、导入之前导出的设置文件setting.jar、更改import设置都不行，最后之后清缓存重启，问题解决。妈蛋。

### 6. 设置排除提示导入的包
打开settings > Editor > General > Auto Import, 可以在这里添加一些包，让这些包从自动导入的提示中排除出去，如com.sun。（每次要导入List时都会出来捣乱）

### 7. 设置取消导包时自动变成import .*
关于导入包，IntelliJ IDEA的默认设置是当同一个包下面的导入个数超过一个定值时，变成import java.util.*;，但是这并不是一个好的开发习惯。

取消设置：

打开settings > Editor > Code Style > Java > Scheme Default > Imports

- 将 Class count to use import with * 改为 99(导入同一个包的类超过这个数值自动变为*)

- 将 Names count to use static import with * 改为 99；(静态导入)

- 将 Package to Use import with * 删掉默认的这两个包(不管使用多少个类，只要在这个列表里都会变为 * )

PS：Scheme Default 是针对全局的，你也可以只修改某个Project的

### 8. 显示行号
Settings->Editor->Appearance标签项，勾选Show line numbers  

### 9. IntelliJ导入Gradle项目报错
报错信息:
```
Error:Could not GET 'http://134.32.32.219:8081/nexus/content/groups/public/org/springframework/boot/spring-boot-gradle-plugin/1.4.0.RELEASE/spring-boot-gradle-plugin-1.4.0.RELEASE.pom'. Received status code 503 from server: Service Unavailable
```

如图：

![](https://github.com/johnnywong233/first_blog/raw/gh-pages/_posts/img/IntelliJ_Gradle.png)

大意是需要设置 HTTP proxy. How？

在build.gradle同级目录touch gradle.properties文件，添加如下内容:
```
systemProp.http.proxyHost=web-proxy.atl.*.com
systemProp.http.proxyPort=8080
systemProp.http.proxyUser=userid
systemProp.http.proxyPassword=password
systemProp.http.nonProxyHosts=*.nonproxyrepos.com|localhost
```
类似地，如果需要设置HTTPS proxy，将上面的http改成https即可。

实际上，之前在build.gradle目录下执行命令```gradle clean build bootRun```，报错：

```
Error resolving plugin [id: 'cn.bestwu.propdeps', version: '0.0.10']
> Could not GET 'https://plugins.gradle.org/api/gradle/3.4/plugin/use/cn.bestwu.propdeps/0.0.10'.
> Connect to plugins.gradle.org:443 [plugins.gradle.org/104.16.174.166, plugins.gradle.org/104.16.171.166, plugins.gradle.org/104.16.172.166, plugins.gradle.
org/104.16.175.166, plugins.gradle.org/104.16.173.166] failed: Connection timed out: connect
```

也是同样的解决方法。

### 10. IntelliJ IDEA使用spring-boot-devtools热部署无效的解决方案

和Eclipse不同的是，Eclipse设置自动编译之后，修改类并保存会触发自动编译，而IDEA在非RUN或DEBUG情况下才会自动编译（前提是你已经设置Auto-Compile）。So how？

首先如图:

![](https://github.com/johnnywong233/first_blog/raw/gh-pages/_posts/img/IntelliJ_compiler_setting.png)

IDEA设置里面(Ctrl + Alt + S 快捷键打开settings——Build, Execution, Deployment——Compiler——Make project automatically)必须打勾.

然后快捷键 Shift+Ctrl+Alt+/，选择Registry，
找到```compiler.automake.allow.when.app.running```选项打勾; 然后以后修改css,js,java类文件，IDEA就会自动make。

### 11. nginx.conf文件编辑插件
因工作需要配置nginx.conf文件，使用notepad ++或者sublime来编辑，不好用；用IntelliJ IDEA打开也是，没有提示，不能快捷注释，格式化啥的都不行。

Google搜索"IntelliJ conf plugin"，发现开源的IntelliJ nginx 插件。 地址[nginx-support](https://plugins.jetbrains.com/plugin/4415-nginx-support)。安装过程与方式不多说。
怎么配置？参考如图：

![](https://github.com/johnnywong233/first_blog/raw/gh-pages/_posts/img/nginx_conf.png)

配置好之后，启动nginx，命令行打印：
```batch
D:/Java/tool/nginx-1.13.1/nginx.exe -c D:/Java/tool/nginx-1.13.1/conf/nginx.conf -g pid 'D:/Java/tool/nginx-1.13.1/logs/nginx.pid';
```
Ctrl + Shift + N搜索nginx打开nginx.conf文件，可以看到高亮显示；输入gz会看到提示；正则配置location可以看到英文提示说明。
更多功能有待研究。

题外话，一开始不知道使用什么文件打开方式打开.conf文件，所以选择默认的text。在这一步，如果选择取消cancel的话，会弹出一个选择安装插件的提示框：

![](https://github.com/johnnywong233/first_blog/raw/gh-pages/_posts/img/cong_file.png)

然后就可以选择下载，虽然提示的PHP以及Scala并不是自己想要的。

### 12.Ctrl + Atl + L
格式化代码的快捷键不可用，原因是这个快捷键被其他应用程序占用。
下载[Hotkey Commander](http://hkcmdr.anymania.com/),一款Windows Hotkey Explorer程序可以查看所有快捷键的程序和进程。

       
### 13. Ctrl + Shift + R
IDEA的全局搜索替换快捷键功能不支持多种类型文件的匹配？  
![](https://github.com/johnnywong233/first_blog/raw/gh-pages/_posts/img/file_type_filter.png)


