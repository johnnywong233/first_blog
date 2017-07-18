### 1. 破解beyond compare 4的register key
官网下载的Beyond Compare 4，在使用一个月之后，需要输入注册密钥才能使用，可是注册密钥要花钱购买。BC3，不清楚；我使用的是BC4，小版本号应该不影响同样的破解方式。访问[网站](https://onhax.me/beyond-compare-pro-serial-key-is-herelatest)粘帖里面的serial key，即可。

### 2. beyond compare 4安装java反编译插件
工作中遇到一个需求，比较jar包的差异；更有甚者，需要比较两个war包的不同。记得好像是公司的一个软件产品的hot-fix（我司以jar包或者war包形式提供hot-fix），但是后来发现这个hot-fix有点问题，故而需要对jar/war做分析；可能这个处理思路有点问题。不过我当时是这么处理的。如果有更好的处理思路，还请不吝留言。

总而言之，要比较jar/war包里面的编译后的class文件的不同。百度/google之后，可供参考的解决方案是安装反编译插件，可以把.class文件反编译成.java文件。

一．下载beyond compare插件

下载地址：

windows下的[官网下载地址](http://www.scootersoftware.com/download.php?z=kb_moreformats_win)

linux 扩展的[官网下载地址](http://www.scootersoftware.com/download.php?zz=kb_moreformats_nix)

二：选择中文版的下载导入

![](http://img.blog.csdn.net/20170628220719898?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbG9uZWx5bWFub250aGV3YXk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

类似这样以bcpkg为文件后缀名的。
进入页面点 Download All就行（但有时候点Download All下载的是空的扩展文件，这时候需要勾选想要使用的扩展再点Download Marked才可以）。

三、打开beyond comare，选择工具->导入设置->导入WindowsFormats.bcpkg

四、重新打开beyond comare。

这个反编译工具默认对中文的反编译不支持，需要做以下修改： 

1. 找到这个目录：BeyondCompare\Helpers\Java； 
2. 编辑该目录下的 CLASS_to_JAVA.bat 文件，修改其内容为“Helpers\Java\jad.exe -8 -p %1 > %2”，其中的-8参数就是将Unicode字符转换为ANSI字符串的关键参数；
3. 打开beyondcompare，工具->文件格式，按下图修改：
![](http://img.blog.csdn.net/20170628220852057?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbG9uZWx5bWFub250aGV3YXk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast) 
4. 重启beyondcompare即可。

### 3. BC比较远程服务器文件
不同机器之间如何比较文件？

BC工具支持ftp，sftp协议的。因此只需要在路径输入远程机器的路径就可以。
例如我现在需要增量发布代码，但是很多时候容易漏掉文件什么的。左侧的路径选择本机的编译好的类目录，右侧远程主机。
![](http://img.blog.csdn.net/20170628215018821?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbG9uZWx5bWFub250aGV3YXk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
关于远程主机的路径写法：
```sftp://root@<ip>//app/tomcat-7.0.70/webapps/ROOT/WEB-INF/classes```
路径分为3个部分：

1. 使用的协议，例如sftp，或者ftp协议。格式与http一样都是后面跟上://
2. 主机定位信息，就是用户名@主机ip的形式。
3. 要比较的目录全路径。这样该工具就会将windows与linux的这两个目录比较。

一些说明：

1. 差异比较的时候不要选择比较时间，规则 -> 比较选项卡中时间戳不参与比较，否则每个文件都不一样。
2. 该工具添加一个插件可以直接将class文件反编译成java文件的，装上插件之后class也是可以比较的。
3. 发布增量代码的时候选择需要同步的文件，右键选择复制到右边，或者复制到左边，具体看你想更新那边的文件。


### 4. 在Eclipse中外挂使用BC
Eclipse自带的文本比较工具太差劲，在代码提交的时候的一个噩梦就是冲突；很多时候git diff显得心有余而力不足（也很有可能是我的使用/打开方式不对！）。而我对于Beyond Compare简直是逢人就推荐的。

那Eclipse能不能使用Beyond Compare呢？即BC有没有针对Eclipse的插件呢？
网上一搜，还真有。Beyond Compare的[插件下载地址](http://beyondcvs.sourceforge.net/)
下载最新版org.eclipse.externaltools-Update-0.8.9.v201003051612.zip
然后就是老生常谈的Eclipse安装插件了；不清楚的话，上面的[下载网站](http://beyondcvs.sourceforge.net/)也有说明。

装好之后，打开Eclipse，选择菜单 Window -> Preferences，弹出窗口，在左边External Tools下面就会多出Beyond Compare，在右边直接按Browse...按钮，选择Beyond Compare的安装位置：
![](http://img.blog.csdn.net/20170628221322125?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbG9uZWx5bWFub250aGV3YXk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
之后，比较的时候就可以用Beyond Compare。

### 5. BC实用发布功能
参考：
增量发布有的时候真的是场噩梦。首先要了解开发版本和服务端的版本，各种文件比对。对我来说，更多时候面对的是各种jar包。之前都是解包替换再压包，好不麻烦。Beyond Compare可以让你解放出来。
  ● 文件比较和替换 
比如，Maven工程下有个target目录，默认情况下里面包含最新编译好的class文件。如图： 
![](http://img.blog.csdn.net/20170628212725134?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbG9uZWx5bWFub250aGV3YXk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
上图的classes目录和被打成jar包的结构是一致的。*.jar为线上服务器版本的jar。 
这时候要对工程做增量发布，则选中两个文件，右键点击比较。
![](http://img.blog.csdn.net/20170628212951053?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbG9uZWx5bWFub250aGV3YXk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
关注红色部分，即是差异所在。
![](http://img.blog.csdn.net/20170628213133336?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbG9uZWx5bWFub250aGV3YXk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
选中要更新文件，在右键菜单里选择”复制到左侧”。完成更新。
![](http://img.blog.csdn.net/20170628213227858?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbG9uZWx5bWFub250aGV3YXk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
再回过头看看jar包，已经修改日期已经改变，可以确认jar包已更新。剩下的就是重新发布到服务器。
![](http://img.blog.csdn.net/20170628213314229?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbG9uZWx5bWFub250aGV3YXk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
上面的操作不仅对jar包生效，对war包和zip包也是有效的。
