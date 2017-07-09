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

 ![](img/find_class_in_jar.png)

//mkdir -p: 创建目录, -p(parent)创建目录，若无父目录，则创建;



### Linux配置JDK, MAVEN

习惯通过FileZilla或者M哦吧XTerm把本地下载的OpenJDK，即zulu-linux-x64.tar.gz导入Linux开发坏境，然后命令```tar zxvf zulu-linux-x64.tar.gz```, 编辑Linux下的环境变量文件，即profile文件，```vim /etc/profile```，Ctrl + End，去文件末尾，添加：

```JAVA_HOME=/root/JDK/zulu-linux-x64

export PATH=$PATH:${JAVA_HOME}/bin:${MAVEN_HOME}/bin:```

MAVE配置同次。生效：```source /etc/profile```

### 
