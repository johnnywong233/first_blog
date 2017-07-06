## frequently used command
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

//
