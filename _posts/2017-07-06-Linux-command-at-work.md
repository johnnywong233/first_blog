### frequently used command
//多台主机之间scp文件/夹

```
scp <user>@<ip>:/path/ /<des_path>

scp root:iso*help@15.119.82.70:/var/opt/kubernetes/offline/suite_images/1.0.tar .

scp root:iso*help@15.119.82.70:/var/opt/* /usr/
```

//生成tar.gz格式的压缩包

```
tar czf hpas-7.4.3.tar.gz hpas-7.4.3/
```

//使用wget从远程主机copy/download文件

```
wget ftp://cmfshare:cmfshare@16.155.193.1/home/README.md
```

//查找目录下面的所有jar包是否含有某个特定的class类*.class
```
find . -name "*.jar"|awk '{print "jar -tvf "$1}'|sh|grep XMLInputFactory

find . -name "*.jar"|awk '{print "jar -tvf "$1}'|sh|grep JsonStreamFactory
```
实例图片：

 ![](https://github.com/johnnywong233/first_blog/raw/gh-pages/_posts/img/find_class_in_jar.png)

//mkdir -p: 创建目录, -p(parent)创建目录，若无父目录，则创建;

//sed文本替换

sed -i 's/src/des/g' some.file

sed -i 's/@ADMIN@/admin/g' demo-postgres.yaml

//在具体行号前加一行内容

sed -i 'N;4addpdf' a.txt

//在具体行号前或后加一行内容，值得注意的是，"eepdf"添加到第三行
sed -i 'N;4ieepdf' a.txt

即，```sed -i 'N;1ieepdf' a.txt```是不起作用的。

//在具体行号前或后加一行内容，值得注意的是，"abc"添加到第四行
sed -i '4iabc' demo.txt


//echo追加
```
echo "append content" >> demo.txt
echo "overwriten content" > demo.txt
```
一个问题，单纯的echo命令是不是不能实现文本的指定行追加内容？



### Linux配置JDK, MAVEN
习惯通过FileZilla或者MobaXTerm把本地下载的OpenJDK，即zulu-linux-x64.tar.gz导入Linux开发坏境，然后命令```tar zxvf zulu-linux-x64.tar.gz```, 编辑Linux下的环境变量文件，即profile文件，```vim /etc/profile```，Ctrl + End，去文件末尾，添加：
```
JAVA_HOME=/root/JDK/zulu-linux-x64
export PATH=$PATH:${JAVA_HOME}/bin:${MAVEN_HOME}/bin:
```

MAVEN配置同次。生效：```source /etc/profile```

### FTP权限账户
在使用wget命令去下载ftp的资源时，用户名密码都没有错，路径也没有问题，但是一直报错找不到文件。
后来才知道，使用的是不同的一套用户名/密码，从而看到不一样的目录以及文件，具备不同的权限：
```wget ftp://cmfshare:cmfshare@16.155.193.1/home/README.md```  
![](https://github.com/johnnywong233/first_blog/raw/gh-pages/_posts/img/ftp_permission.png)  
并且wget不能下载带空格的文件.否则报错。

