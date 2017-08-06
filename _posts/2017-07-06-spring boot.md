## 关于spring Boot的一些思考
- spring boot v.s. spring
- spring boot的优缺点

## 《JavaEE开发的颠覆者 Spring Boot实战》读书笔记

### 第一章
1.spring发展阶段

- xml配置；
- 注解配置（应用的基本配置，如数据库配置采用xml文件，业务配置有注解）；
- java配置。

2.每一个被spring管理的java对象都称之为bean；spring提供一个IoC容器用来初始化对象，解决对象之间的依赖管理和对象的使用。

3.Spring-Context：运行时Spring容器。

4.Spring生态：

- spring boot
- spring XD
- spring cload
- spring data
- spring integration
- spring batch
- spring security
- spring HATEOAS
- spring social
- spring AMQP
- spring mobile
- spring for android
- spring web flow
- spring web services
- spring LDAP
- spring session

5.安装jar包到本地repository：

	mvn install:install-file -DgroupId=com.oracle "-DartifactId=ojdbc14" "-Dversion=" "-Dpackaging=jar" "-Dfile=D:\*.jar"

6.spring框架四大原则：

- 使用POJO进行轻量级和最小侵入式开发；
- 通过依赖注入和基于接口编程实现松耦合；
- 通过AOP和默认习惯进行声明式编程；
- 使用AOP和模版减少模式化代码。

7.IoC和DI在spring下是等同的概念，IoC是通过DI来实现的。DI，即容器负责创建对象和维护对象间的依赖关系，而不是通过对象本身负责自己的创建和解决自己的依赖；目的是解耦，有“组合”的意味；IoC容器（SpringContext）负责创建bean。

推荐两者混用，一个较好的原则：全局配置使用java config（如数据库相关，MVC相关配置），业务bean的配置使用注解（@Service，@Component，@Controllor，@Repository）。java config实现方式：@Bean和@Configuration。

AOP，目的解耦，可以让一组类共享相同的行为；

8.注解本身没有功能，和xml类似，都是元数据（解释数据的数据，即配置）；元注解：可以注解到别的注解上的注解，被注解的注解称之为组合注解。

### 第二章

9.Bean的scope：

- Singleton；
- Prototype；
- Request；
- Session；
- GlobalSession；
- StepScope(Spring batch)。

10.注解@Value的参数中使用表达式：注入普通字符；操作系统属性；表达式运算结果；其他bean的属性；文件内容；网址内容；属性文件。

11.bean的生命周期：
- java config：使用@bean的initMethod和destoryMethod
- xml：配置文件里面的init-method和destory-method
- 注解：@PostConstruct和@PreDestroy

事件流程：1.自定义事件继承ApplicationEvent；2.自定义事件监听器，实现ApplicationListener；3.使用容器发布事件。

### 第三章



实际任务多是非阻碍，即异步；在配置类使用注解@EnableAsync开启对异步任务的支持。

@Scheduled支持多种类型的计划任务：cron、fixDay、fixDate.

条件注解：实现Condition接口，重写match方法来构造判断条件。@conditional根据满足某一个特定的条件来创建特定的bean


### 第四章

SSH=Structs 1.x+Spring+Hibernate；zetoturnaround,Jrebel厂商；

MVC：Model+View+Controller；

三层架构：Presentation tier+Application tier+Data tier（展现层+应用层+数据访问层）

两者的关系：MVC只存在三层架构的展现层，M实际上是数据模型，是包含数据的对象。spring MVC里，有一个类Model，用来和V之间的数据交互、传值；V是视图页面，包含JSP、FreeMarker、Velocity、Thymeleaf、Tile等；C是控制器（@Controller）。

服务端推送技术：Ajax是服务器轮询技术，使浏览器尽可能第一时间获得服务端的消息，轮询频率不好控制，加大服务端的压力；WebSocket双向通信技术；

jQuery的Ajax请求，没有浏览器兼容性问题；媒体类型text/event-stream，服务端SSE的支持；

<scope>test</scope>，存活期是test周期，发布时将不包含这些jar。


### 第五章

Spring boot提供基于http、ssh、telnet对运行时的项目进行监控;

spring-boot-devtools来进行开发热部署;

使用在线spring网站http://start.spring.io快速开发应用;

Spring Boot提供的控制台命令工具Spring Boot CLI, 下载并解压, 将CLI的bin目录配置到环境变量的path下面，即可使用:
```
spring init --build=maven --java-version=1.8 --dependencies=web --packaging=jar --boot-version=1.5.4 --groupId=com.johnny --artifactId=springboot_cli
```

### 第六章
关闭特定的自动配置使用@SpringBootApplication注解的exclude参数：
@SpringBootApplication(exclude = {DataSourceAutoConfiguration.class})
 
自定义banner, [网站](http://patorjk.com/software/taag)

不推荐使用xml配置文件，但是提供注解@ImportResource来加载xml配置：
@ImportResource({"classpath:some-context.xml", "classpath:another-context.xml"})

常规Spring坏境下，注入properties文件里面的值的方式：通过@PropertySource指明properties文件位置，然后通过@value注入之;
Spring Boot坏境下，在application.properties/application.yaml文件里面定义key-value，直接使用@Value注入即可。

默认情况下,Spring Boot使用logback作为日志框架。（version 1.3.0）

### 第七章
内嵌Tomcat, Jetty不支持以jar形式运行JSP, Undertow不支持JSP;

Thymeleaf是一个xml/xhtml/html5的模板引擎，可以作为MVC的web应用的View层;

引入Bootstrap作为样式控制;

ContentNegotiatingViewResolver不是自己处理View，代理给不同的ViewResolver来处理不同的View，有最高的优先级。

BeanNameViewResolver

InternalResourcesViewResolver通过设置前缀、后缀以及控制器中的方法来返回视图名的字符串，以得到实际页面。

自动配置类的addResourceHanders方法定义静态资源的自动配置：类路径文件、webjar（将常用的脚本框架封装在jar包中的jar包，可以通过localhost:8080/webjar/**来访问）

### 附录A

JHipster是一个代码生成器，可以用来生成基于sb和AngularJS的项目：安装Node.js, git, Yeoman generator, JHipster, Bower, Grunt, 命令：yo jhipster


## 零碎知识点
启动jar包命令：
```batch
java -jar  target/*.jar
```
指定profile：
```batch
java -jar  target/*.jar spring.profiles.active=dev
java -jar target/*.jar --active.profile=prod
```
这种方式，只要控制台关闭，服务就不能访问。在后台运行的方式来启动：
```batch
nohup java -jar target/*.jar &
```
启动的时候设置jvm参数：
```batch
java -Xms10m -Xmx80m -jar app.jar &
```
spring boot内嵌tomcat的配置项：
- 设置内嵌Tomcat的最大线程数:
server.tomcat.max-threads=1000

- 设置内嵌Tomcat的编码
server.tomcat.uri-encoding = UTF-8

- 其他
```yaml
server.tomcat.accesslog.enabled=false # Enable access log.
server.tomcat.accesslog.pattern=common # Format pattern for access logs.
server.tomcat.accesslog.prefix=access_log # Log file name prefix.
server.tomcat.accesslog.rename-on-rotate=false # Defer inclusion of the date stamp in the file name until rotate time.
server.tomcat.accesslog.suffix=.log # Log file name suffix.
server.tomcat.background-processor-delay=30 # Delay in seconds between the invocation of backgroundProcess methods.
server.tomcat.basedir= # Tomcat base directory. If not specified a temporary directory will be used.
server.tomcat.internal-proxies=10\\.\\d{1,3}\\.\\d{1,3}\\.\\d{1,3}|\\
        192\\.168\\.\\d{1,3}\\.\\d{1,3}|\\
        169\\.254\\.\\d{1,3}\\.\\d{1,3}|\\
        127\\.\\d{1,3}\\.\\d{1,3}\\.\\d{1,3}|\\
        172\\.1[6-9]{1}\\.\\d{1,3}\\.\\d{1,3}|\\
        172\\.2[0-9]{1}\\.\\d{1,3}\\.\\d{1,3}|\\
        172\\.3[0-1]{1}\\.\\d{1,3}\\.\\d{1,3} # regular expression matching trusted IP addresses.
server.tomcat.max-threads=0 # Maximum amount of worker threads.
server.tomcat.min-spare-threads=0 # Minimum amount of worker threads.
server.tomcat.port-header=X-Forwarded-Port # Name of the HTTP header used to override the original port value.
server.tomcat.protocol-header= # Header that holds the incoming protocol, usually named "X-Forwarded-Proto".
server.tomcat.protocol-header-https-value=https # Value of the protocol header that indicates that the incoming request uses SSL.
server.tomcat.redirect-context-root= # Whether requests to the context root should be redirected by appending a / to the path.
server.tomcat.remote-ip-header= # Name of the http header from which the remote ip is extracted. For instance `X-FORWARDED-FOR`
server.tomcat.uri-encoding=UTF-8 # Character encoding to use to decode the URI.
```


学习参考blog：
- [1](https://github.com/lianggzone/springboot-action)
- [2](https://github.com/ityouknow/spring-boot-examples)
























