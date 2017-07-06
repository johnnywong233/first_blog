# 简单
## 1. cannot resolve symbol Test（Junit）
以IntelliJ作为java 开发IDE，代码里写有一些方法，习惯是在当前类里面再写一个测试方法（因为并不是生产代码，习惯不好貌似不要紧），在测试方法上面添加注解@Test，但是报错cannot resolve symbol Test。感觉很莫名其妙，pom.xml文件里面已经添加JUnit的dependency啊，难道是我的IntelliJ的配置问题。智能IDE如IntelliJ，不是应该默认支持JUnit的么？后来明白，原来是在pom.xml中引入JUnit时，指定有```<scope>```，而我前面说过代码以及测试代码都是在src/main/java/下面。把scope去掉即可。

可是问题来的时候，一如蒙头苍蝇各种百度/google，问题的根源是什么都不知道，都没有分析一下，就去问百度/google。

总结：不要急着解决问题，要先冷静分析一下，这是不是问题。

## 2. mockito-core.jar & mockito-all.jar的选择问题
在写mockito的demo程序的时候，并不知道应该使用那个jar，于是把mockito-core以及mockito-all全部写入pom.xml文件中，一开始也没有什么问题。但是当用到静态方法argThat，就懵逼了，不知道应该导入哪一个jar包的类的哪个方法。

一开始报错：**IncompatibleClassChangeError**
参考[stackoverflow](http://stackoverflow.com/questions/1980452/what-causes-java-lang-incompatibleclasschangeerror)

意思是changing non-static non-private fields/methods to be static or vice versa.
查看出错一行代码，argThat的原因。

应该导入下面这个静态方法，而不是上面的。

import static org.mockito.hamcrest.MockitoHamcrest.argThat;//来自mockito-core.jar
 
import static org.mockito.ArgumentMatchers.argThat;//来自mockito-core.jar
 
import static org.mockito.Matchers.argThat;//来自mockito-all.jar

通过反编译工具查看源码，mockito-all.jar基本上是由mockito-core.jar以及hamcrest-core（maven repository的介绍：This is the core API of hamcrest matcher framework to be used by third-party framework providers. This includes the a foundation set of matcher implementations for common operations.）以及另外一个没怎么听过，更没有用过的objenesis（maven repository的介绍：A library for instantiating Java objects）三个jar包组成。

使用第二个argThat则报错：

java.lang.NoSuchMethodError: org.mockito.internal.progress.ThreadSafeMockingProgress.mockingProgress()Lorg/mockito/internal/progress/MockingProgress;
以及java.lang.NoSuchMethodError: org.mockito.internal.matchers.InstanceOf.<init>(Ljava/lang/Class;Ljava/lang/String;)V
 http://stackoverflow.com/questions/31962003/mockito-test-gives-no-such-method-error-when-run-as-junit-test-but-when-jars-are

![这里写图片描述](http://img.blog.csdn.net/20170623010055831?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbG9uZWx5bWFub250aGV3YXk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

Eclipse快捷键Ctrl+ Shift +T, 发现当前classpath下面有太多jar包包含这个类ThreadSafeMockingProgress。由于生产项目使用的mockito是mockito-core，一开始在pom.xml文件中把mockito-all注释，发现导致很多unresolved symbol报错，意思是没有导入相应的jar依赖。于是转换方向，注释mockito-core，使用mockito-all。问题解决。

另外，从上面的截图，也验证mockito-all这个jar包包含mockito-core这个jar包。

## 3. apache poi jar包解析excel
在使用apache的poi这个jar包做excel表格的解析和生成的demo程序时。遇到报错信息：
java.lang.IllegalAccessError: tried to access method org.apache.poi.util.POILogger.log from class org.apache.poi.openxml4j.opc.ZipPackage
参考https://stackoverflow.com/questions/34630209/java-lang-illegalaccesserror-tried-to-access-method-org-apache-poi-util-poilogg
最开始pom文件只有两处使用到poi相关的dependency：

```
<dependency>
	<groupId>org.apache.poi</groupId>
	<artifactId>poi</artifactId>
	<version>3.15</version>
</dependency> 
<dependency>
	<groupId>fr.opensagres.xdocreport</groupId>
	<artifactId>org.apache.poi.xwpf.converter.core</artifactId>
	<version>1.0.6</version>
</dependency>
```

把下面这个不明所以的```<groupId>```的dependency注释掉，Eclipse报解析错误，意思是找不到类（cannot resolve symbol），即不能通过编译。这给我一种错觉，以为我的dependency没有搞错，需要添加org.apache.poi.xwpf.converter.core这个jar包。

因而上述答案看得不明所以。

但是多次Google以及百度给出的解释都是POI jar包版本的问题。比如[这里](http://blog.csdn.net/u013361445/article/details/50491815)和[这里](http://stackoverflow.com/questions/33415904/apache-poi-parsing-error)
 
把```<artifactId>org.apache.poi.xwpf.converter.core</artifactId>```注释掉，然后添加

```
<dependency>
    <groupId>org.apache.poi</groupId>
    <artifactId>poi-ooxml</artifactId>
    <version>3.15</version>
</dependency>

<dependency>
    <groupId>org.apache.poi</groupId>
    <artifactId>poi-ooxml-schemas</artifactId>
    <version>3.15</version>
</dependency>
```

发现没有错误，没有cannot resolve symbol，可以正常编译。
 
当然，上面两个poi个jar包有可能有冗余的情况，即有可能没有使用到某个jar；就比如使用spring时添加dependency一样，也是乱加一气。
 
但是运行代码之后还是报错：java.lang.NoClassDefFoundError: org/openxmlformats/schemas/wordprocessingml/x2006/main/impl/CTTcImpl$1PList.
 
多次百度才发现还需要添加一个jar的dependency：

```
<dependency>
    <groupId>org.apache.poi</groupId>
    <artifactId>ooxml-schemas</artifactId>
    <version>1.3</version>
</dependency>
```

ooxml-schemas和poi-ooxml-schemas是两个不同的jar包。

最后需要使用的apeche的poi jar包如下：

```
<dependency>
	<groupId>org.apache.poi</groupId>
	<artifactId>poi</artifactId>
	<version>3.15</version>
</dependency>

<dependency>
	<groupId>org.apache.poi</groupId>
	<artifactId>poi-ooxml</artifactId>
	<version>3.15</version>
</dependency>

<dependency>
	<groupId>org.apache.poi</groupId>
	<artifactId>poi-ooxml-schemas</artifactId>
	<version>3.15</version>
</dependency>

<dependency>
	<groupId>org.apache.poi</groupId>
	<artifactId>ooxml-schemas</artifactId>
	<version>1.3</version>
</dependency>
```

至此，问题得以解决。

##4.try……catch……finally的改进
相信你我一定写过很多次这种重复的“无意义”的代码：

```
BufferedOutputStream bos = null;
BufferedInputStream bis = null;
try {
    bos = new BufferedOutputStream(new FileOutputStream(storefile));
    bis = new BufferedInputStream(inputStream);
    int c;
    while((c= bis.read())!=-1){
        bos.write(c);
        bos.flush();
    }
} catch (IOException e) {
    e.printStackTrace();
}finally{
    bos.close();
    bis.close();
}
```

事实上，上面的代码还没有足够完善，即对异常的处理还不够。比如bos.close的方法调用也可能会出错，所以我们需要在finally字句里面做try{}catch{}判断。想想都要疯掉。

借助于IntelliJ IDEA智能IDE的提示：

![这里写图片描述](http://img.blog.csdn.net/20170626232235769?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbG9uZWx5bWFub250aGV3YXk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

敲下IDEA最强大的快捷键：Alt + Enter

变成这样：

```
try (BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream(storefile));
     BufferedInputStream bis = new BufferedInputStream(inputStream)) {
    int c;
    while ((c = bis.read()) != -1) {
        bos.write(c);
        bos.flush();
    }
} catch (IOException e) {
    e.printStackTrace();
}
```

看起来清爽许多。

## 5. 报错java.sql.SQLNonTransientConnectionException: CLIENT_PLUGIN_AUTH is required
在连接本地Mysql时候的一个报错：
```
Loading class `com.mysql.jdbc.Driver'. This is deprecated. The new driver class is `com.mysql.cj.jdbc.Driver'. The driver is automatically registered via the SPI and manual loading of the driver class is generally unnecessary.
2017-07-02 10:30:44.145 [main] ERROR sql.or.MysqlConnection - CLIENT_PLUGIN_AUTH is required
java.sql.SQLNonTransientConnectionException: CLIENT_PLUGIN_AUTH is required
	at com.mysql.cj.jdbc.exceptions.SQLError.createSQLException(SQLError.java:526)
	at com.mysql.cj.jdbc.exceptions.SQLError.createSQLException(SQLError.java:513)
	at com.mysql.cj.jdbc.exceptions.SQLError.createSQLException(SQLError.java:505)
	at com.mysql.cj.jdbc.exceptions.SQLError.createSQLException(SQLError.java:479)
	at com.mysql.cj.jdbc.exceptions.SQLError.createSQLException(SQLError.java:489)
	at com.mysql.cj.jdbc.exceptions.SQLExceptionsMapping.translateException(SQLExceptionsMapping.java:72)
	at com.mysql.cj.jdbc.ConnectionImpl.createNewIO(ConnectionImpl.java:1606)
	at com.mysql.cj.jdbc.ConnectionImpl.<init>(ConnectionImpl.java:633)
	at com.mysql.cj.jdbc.ConnectionImpl.getInstance(ConnectionImpl.java:347)
	at com.mysql.cj.jdbc.NonRegisteringDriver.connect(NonRegisteringDriver.java:219)
	at java.sql.DriverManager.getConnection(Unknown Source)
	at java.sql.DriverManager.getConnection(Unknown Source)
	at sql.or.MysqlConnection.setConnection(MysqlConnection.java:45)
	at sql.or.test.OpenReplicatorTest.main(OpenReplicatorTest.java:34)
Caused by: com.mysql.cj.core.exceptions.UnableToConnectException: CLIENT_PLUGIN_AUTH is required
...
context: AbstractTransport.Context[threadId=5,scramble=@hmiJr"L<'L**6oMt}<O,protocolVersion=10,serverHost=localhost,serverPort=3306,serverStatus=2,serverCollation=8,serverVersion=5.1.50-community,serverCapabilities=63487]
```

[参考](https://stackoverflow.com/questions/37348572/new-mysql-driver-causes-java-sql-sqlnontransientconnectionexception-client-plug)

大意是使用的mysql-jdbc的版本不对，本地安装的Mysql是5.1.50，在pom文件里面引用的mysql-jdbc版本是最新的6.0.6，换成5.1.41，报错消失。

### 6. IDEA提示web.xml文件listener-class is not allowed here
在使用IDEA开发web项目时，有时候web.xml文件中会有很多标签被标为红色的字体，提示listener-class is not allowed here。比如：

```
<init-param>
<param-name>contextConfigLocation</param-name>
<param-value>classpath:</param-value> （不是系统默认WEB-INF时，需用classpath*：）
</init-param>
```

替换```<web-app>```实例引用模板信息:

```
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
		 xmlns="http://java.sun.com/xml/ns/javaee"
         xmlns:web="http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd"
         xsi:schemaLocation="http://java.sun.com/xml/ns/javaee 
		 http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd"
         id="WebApp_ID" version="2.5">
```

然后不再报错，但我不晓得为什么version="3.1"就出校验出错；

解答：Servlet3.0是J2EE6.0规范的一部分，跟随J2EE6.0一起发布，并且Tomcat7.0已经完全支持Servlet3.0；

平时，一般使用tomcat6.0，是不能够使用servelt3.0的，tomcat6.0还不能支持那些规范；
至于为什么不能使用listener-class，是因为在web-app_3_0.xsd结构定义文件中，根本就不提倡这些配置，因为Servlet3.0已经支持注解形式；

解决方法：（不推荐换版本号，推荐使用3.0以上版本，然后使用注解形式，当然不用注解而是使用web.xml等配置文件也是没有问题的。）

将web.xml头部内容

```
<web-app version="2.4"
xmlns="htt://java.sun.com/xml/ns/j2ee" xmns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://java.sun.com/xml/ns/j2ee
    http://java.sun.com/xml/ns/j2ee/web-app_2_4.xsd">
```

替换为

```
<web-app xmlns="http://java.sun.com/xml/ns/javaee" version="2.5">
```



# 中级
## 