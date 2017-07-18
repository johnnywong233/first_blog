### 1. 常用命令备忘
```
//调过UT的打包
mvn install -Dmaven.test.skip=true

//将下载或者从其他路径得到的，但是在maven repository找不到artifact ID信息的jar包安装到本地仓库的命令，然后就可以通过使用maven的pom文件来管理，而不是最传统的配置classpath的方法:
mvn install:install-file -Dfile=neuroph-2.6.jar -DgroupId=org.neuroph -DartifactId=neuroph -Dversion=2.6 -Dpackaging=jar
```

### 2. maven-assembly-plugin
在一个Linux环境下使用maven-assembly-plugin插件，前期使用得很正常，后来报错：
```
Failed to execute goal org.apache.maven.plugins:maven-assembly-plugin:2.6:single (make-assembly) on project suite-demo-config-web: Execution make-assembly of goal org.apache.maven.plugins:maven-assembly-plugin:2.6:single failed: user id '3518522' is too big ( > 2097151 ). -> [Help 1]
```
经过排查，发现问题是版本导致的，将目前使用的版本由2.6降到2.4，解决问题，深层原因暂时未知。
参考链接：https://stackoverflow.com/questions/33943565/error-with-maven-build-with-assembly-plugin

### 3.wagon-maven-plugin
在pom.xml文件里面的```<build>```里面配置：
```xml
<extensions>
    <extension>
        <groupId>org.apache.maven.wagon</groupId>
        <artifactId>wagon-ssh</artifactId>
        <version>2.8</version>
    </extension>
</extensions>
<plugin>
    <groupId>org.codehaus.mojo</groupId>
    <artifactId>wagon-maven-plugin</artifactId>
    <version>1.0</version>
    <configuration>
        <serverId>15.119.81.111</serverId>
        <fromFile>target/extractor-alm.jar</fromFile>
        <url>
            scp://hpba@15.119.81.111/home/hpba/HPBA-340-340-master-redhat-x64/ContentPacks/ALM/EXTRACTOR/extractor-alm/
        </url>
    </configuration>
</plugin>
```
同时在maven的setting.xml文件里面配置server信息（用户名和密码）
实现jar/war包自动上传到server，部署。

### 4. Maven安装json-lib错误
问题：
项目需要使用json-lib，mvn.repository.com查找它的dependency时结果如下：
```xml
<dependency>    
    <groupId>net.sf.json-lib</groupId>   
    <artifactId>json-lib</artifactId>    
    <version>2.4</version>    
</dependency>
```
然而import时提示无法找到这个jar。

解决办法：json-lib提供两个jdk版本的实现， json-lib-2.1-jdk13.jar和json-lib-2.1-jdk15.jar。把dependency的描述修改成下面的形式就就解决问题：
```xml
<dependency>    
    <groupId>net.sf.json-lib</groupId>   
    <artifactId>json-lib</artifactId>    
    <version>2.4</version>    
    <classifier>jdk15</classifier>  
</dependency>
```

### 5.docker-maven-plugin
在使用spotify的docker-maven-plugin遇到的一个问题。
Linux环境下配置好docker-maven-plugin插件的maven pom文件，前期使用完全没有问题，后来执行mvn clean install遇到报错：
```
Retrying request to {}->unix://localhost:80
...
Failed to execute goal com.spotify:docker-maven-plugin:0.4.13:build (build-image) on project demo-suite-data-image: Exception caught: java.util.concurrent.ExecutionException: com.spotify.docker.client.shaded.javax.ws.rs.ProcessingException: java.io.IOException: No such file or directory –
```
初始时，把报错信息的焦点定位于ProcessingException以及No such file or directory，当然google不懂任何有用的信息。
换个思路，google Retrying request to {}->unix://localhost:80。
找到参考：https://github.com/spotify/docker-maven-plugin/issues/105
总结起来就是，你现在的Linux坏境docker已经出问题，maven插件需要借助于docker环境（如docker daemon等）；docker verion或者docker info提示有错，maven当然会执行失败。

### 6.maven-assembly-plugin
使用maven的assembly插件时遇到的一个问题。
需求场景是：把web工程mvn clean install生成的war包放置到下载之后的JBoss压缩包解压缩之后的文件夹deployment/standalone下面，替换里面的已有war包，重新打包成tar.gz格式的压缩包供后面的dockerfile使用。pom.xml及assembly.xml文件一切配置就绪。
前期使用也是正常，几次之后出问题，报错：
```
[WARNING] Entry: hpas-7.4.3/bundles/system/layers/base/javax/servlet/api/v25/jboss-servlet-api_2.5_spec-1.0.1.Final.jar longer than 100 characters.
```
网上有很多类似的故障如：http://stackoverflow.com/questions/9416511/tycho-shots-a-warning-when-my-entry-is-longer-than-100-chars
各种google之后，解决方法有两类：
1.不用这个assembly插件，换一个更强大的tycho-p2-director-plugin[http://git.eclipse.org/c/tycho/org.eclipse.tycho.git/] ,但是需要重新学习了解的成本。
2.更新maven的插件版本，从现有的2.6之后升级到3.0.0，但是：
![](http://img.blog.csdn.net/20170616020318935?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbG9uZWx5bWFub250aGV3YXk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
貌似很多时候，maven的插件报错不影响其功能使用。
但是，这都不是完美的解决方案。
终于找到一个更靠谱的解决方法：
https://github.com/downgoon/memcloud/issues/4
在```< plugin>——<execution>——<configuration>```下面配置
```
<tarLongFileMode>gnu</tarLongFileMode>
```
### 7. Eclipse导入maven项目报错：could not read pom.xml
如图，IDE是Eclipse，导入GitHub上面git clone的maven项目时，报错：
![](http://img.blog.csdn.net/20170626223645738?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbG9uZWx5bWFub250aGV3YXk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
参考：http://blog.csdn.net/t123012009065/article/details/17333773
意思是pom.xml有不能解析的配置项，把不能解析的配置修改过来即可。
与其他pom文件对比，发现多了这一行：
<?xml version="1.0" encoding="UTF-8"?>
去掉就行。wait but why？git clone的maven项目，怎么会有这种问题呢？还是一个高star的项目。

### 8. Eclipse解析pom.xml文件报错
报错信息如此：

Plugin execution not covered by lifecycle configuration with：org.jvnet.maven-antrun-extended-plugin:maven-antrun-extended-plugin:1.43:run(execution: unpack, phase: compile)
![](http://img.blog.csdn.net/20170626224914665?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbG9uZWx5bWFub250aGV3YXk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

具体是配置和GWT相关。参考：
[1](http://stackoverflow.com/questions/14886380/generated-project-with-gwt-maven-plugin-eclipse)
[2](http://stackoverflow.com/questions/8523737/why-am-i-receiving-a-plugin-execution-not-covered-by-lifecycle-configuration-wi)

如图所示，可得知大致解决方法：
1. 第一种会改变pom.xml文件，生产代码，不推荐提交更改；
2. 更改自己本地开发坏境的配置，即将修改置于settings directory，建议。

### 9.  maven-resources-plugin的使用
直入主题：
```xml
<build>
	<plugins>
	    <plugin>
	        <artifactId>maven-resources-plugin</artifactId>
	        <version>3.0.1</version>
	        <executions>
	            <execution>
	                <id>copy-resources</id>
	                <phase>package</phase>
	                <goals>
	                    <goal>copy-resources</goal>
	                </goals>
	                <configuration>
	                    <outputDirectory>docker</outputDirectory>
	                    <outputDirectory>kubernetes</outputDirectory>
	                    <resources>
	                        <resource>
	                            <directory>target</directory>
	                            <includes>
	                                <include>*.jar</include>
	                            </includes>
	                        </resource>
	                    </resources>
	                </configuration>
	            </execution>
	        </executions>
	    </plugin>
	</plugins>
</build>
```
如上配置，只有最后一个outputDirectory是有效的，即只把target下面的jar文件copy到kubernetes，并没有copy到上一个配置的outputDirectory，即docker。

那配置两个maven-resources-plugin？如下所示：
```xml
<plugin>
    <artifactId>maven-resources-plugin</artifactId>
    <version>3.0.1</version>
    <executions>
        <execution>
            <id>copy-resources</id>
            <phase>package</phase>
            <goals>
                <goal>copy-resources</goal>
            </goals>
            <configuration>
                <outputDirectory>kubernetes</outputDirectory>
                <resources>
                    <resource>
                        <directory>target</directory>
                        <includes>
                            <include>*.jar</include>
                        </includes>
                    </resource>
                </resources>
            </configuration>
        </execution>
    </executions>
</plugin>

<plugin>
    <artifactId>maven-resources-plugin</artifactId>
    <version>3.0.1</version>
    <executions>
        <execution>
            <id>copy-resources</id>
            <phase>package</phase>
            <goals>
                <goal>copy-resources</goal>
            </goals>
            <configuration>
                <outputDirectory>docker</outputDirectory>
                <resources>
                    <resource>
                        <directory>target</directory>
                        <includes>
                            <include>*.jar</include>
                        </includes>
                    </resource>
                </resources>
            </configuration>
        </execution>
    </executions>
</plugin>
```
也是只有下面一个配置项生效。

### 10.关于maven scope
1.Compile（编译）
compile是默认的范围.编译范围依赖在所有的classpath中可用，同时它们也会被打包.

2.Provided（已提供）
provided依赖只有在当JDK或者一个容器已提供该依赖之后才使用.例如，如果你开发一个web应用，你可能在编译classpath中需要可用的Servlet API来编译一个servlet，但是你不会想要在打包好的WAR中包含这个Servlet API；这个Servlet API JAR由你的应用服务器或者servlet容器提供.已提供范围的依赖在编译classpath（不是运行时）可用.它们不是传递性的，也不会被打包.

3.Runtime（运行时）
runtime依赖在运行和测试系统的时候需要，但在编译的时候不需要.比如，你可能在编译的时候只需要JDBC API JAR，而只有在运行的时候才需要JDBC驱动实现.

4.Test（测试）
Test范围依赖 在一般的 编译和运行时都不需要，它们只有在测试编译和测试运行阶段可用.

5.System（系统）
system范围依赖与provided类似，但是必须显式的提供一个对于本地系统中JAR文件的路径.这么做是为了允许基于本地对象编译，而这些对象是系统类库的一部分.这样的构件应该是一直可用的，Maven也不会在仓库中去寻找它.如果你将一个依赖范围设置成系统范围，你必须同时提供一个systemPath元素.注意该范围是不推荐使用的（你应该一直尽量去从公共或定制的Maven仓库中引用依赖）.

### 11.一方库、二方库、三方库
一方库：本工程中的相互依赖;

二方库：公司内部的依赖库，一般指公司内部的其他项目发布的jar包;

三方库：公司之外的开源库， 比如apache、ibm、google等发布的依赖.

### 12.mvn帮助插件
```help:active-profiles```
列出当前构建中活动的Profile（项目的，用户的，全局的）。

```help:effective-pom```
显示当前构建的实际POM，包含活动的Profile。

```help:effective-settings```
打印出项目的实际settings, 包括从全局的settings和用户级别settings继承的
配置。

```help:describe```
描述插件的属性。它不需要在项目目录下运行。但是你必须提供你想要描述插件
的 groupId 和 artifactId。
eg: ```mvn help:describe -Dplugin=assembly```

### 13. Maven中的依赖关系查看
```mvn dependency:resolve```

### 14.Pom文件配置忽略测试失败
当Maven遇到一个失败的单元测试/测试案例，它默认的行为是停止当前的构建。如果希望继续构建项目，即使Surefire插件遇到失败的单元测试，设置Surefire的**testFailureIgnore**这个配置属性为true。
```xml
<plugin>
	<groupId>org.apache.maven.plugins</groupId>
	<artifactId>maven-surefire-plugin</artifactId>
	<configuration>
		<testFailureIgnore>true</testFailureIgnore>
	</configuration>
</plugin>
```

### 15. 阿里云aliyun搭建的maven私服
```xml
<mirror>
	<id>aliyun</id>
	<mirrorOf>aliyun</mirrorOf>
	<name>Human Readable Name for this Mirror.</name>
	<url>http://maven.aliyun.com/nexus/content/groups/public</url>
</mirror>
```
### 16. Maven与Gradle项目的互相转化
Maven项目转Gradle项目, 也就是pom.xml文件转换为build.gradle文件。**前提条件**：radle项目目录结构保持跟Maven一样的约定，即/src/main/java。

方法,在maven根目录（也就是pom.xml所在目录）下运行，**前提条件**安装Gradle 2.0以上：
```batch
gradle init --type pom
```
Gradle项目转Maven项目稍显麻烦，在build.gradle中增加以下内容(group,version可自行修改，artifactId默认为目录名称):
```groovy
apply plugin: 'java'
apply plugin: 'maven'

group = 'com.101tec'
version = '0.7-dev'
sourceCompatibility = 1.8
```
然后执行gradle install，成功后将在build\poms目录下生成pom-default.xml文件，把它复制到根目录下，改名成pom.xml即可.

通过修改build.gradle也可以直接在根目录下生成pom.xml:
```groovy
task writeNewPom << {
    pom {
        project {
            inceptionYear '2008'
            licenses {
                license {
                    name 'The Apache Software License, Version 2.0'
                    url 'http://www.apache.org/licenses/LICENSE-2.0.txt'
                    distribution 'repo'
                }
            }
        }
    }.writeTo("$buildDir/pom.xml")
}
```






# [Maven scope](http://ee-dreamer.com/?p=320)

[Maven assembly插件使用](http://ee-dreamer.com/?p=1129)

[Maven插件详解](http://ee-dreamer.com/?p=401)

[maven用eclipse创建多模块项目](http://ee-dreamer.com/?p=250)

[将maven web项目部署到eclipse tomcat中](http://ee-dreamer.com/?p=41)

[maven blog](http://seanzhou.iteye.com/category/192769)

# 
