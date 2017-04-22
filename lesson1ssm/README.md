#使用IntelliJ IDEA 2017开发基于Maven+Spring MVC的入门Java项目

项目源码：https://github.com/dayu-teacher/dayu-java-ssm.git

###开发环境搭建

>开发环境：IntelliJ IDEA 2017 + GIT + MAVEN + Spring MVC 4.3.7 + Tomcat8

1、下载安装JDK1.8

2、下载安装Tomcat8

3、下载安装Intellij IDEA


##一、修改pom.xml文件，加载 Spring MVC相关的依赖Jar包

<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <jdk.version>1.8</jdk.version>
    <!-- spring版本号 -->
    <spring.version>4.3.7.RELEASE</spring.version>
    <!-- log4j日志文件管理包版本 -->
    <slf4j.version>1.7.25</slf4j.version>
    <log4j.version>1.2.17</log4j.version>
  </properties>
  

 <!-- springframework start -->
    <!-- spring mvc -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <!-- spring核心包 -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-core</artifactId>
      <version>${spring.version}</version>
    </dependency>

    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-web</artifactId>
      <version>${spring.version}</version>
    </dependency>

    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-oxm</artifactId>
      <version>${spring.version}</version>
    </dependency>

    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-tx</artifactId>
      <version>${spring.version}</version>
    </dependency>

    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context-support</artifactId>
      <version>${spring.version}</version>
    </dependency>

    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-orm</artifactId>
      <version>${spring.version}</version>
    </dependency>

    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-test</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <!-- springframework end -->


##二、添加 HelloWorldController 控制器

前端通过 @RequestMapping 中匹配的URL地址请求，执行注解 @RequestMapping 在类级别和方法级别的业务逻辑处理后返回ModelAndView。

##三、添加静态文件夹、项目入口文件index.jsp

1、在webapp目录下建立index.jsp作为项目默认入口文件。

2、在webapp目录下建立3个文件夹用于放静态的文件：images[用于放图片]，js[用于放js文件]，style[用于放css文件]。

##四、添加视图控制器HelloWorldController对应的展示页面 getHello.jsp

在WEB-INF下面建立一个文件夹views，用于放jsp文件。 我们这里先建立一个HelloWorldController中需要引用的jsp文件：getHello.jsp。

##五、在 resources 目录下添加 Spring Config 文件 spring-content.xml

在本项目中spring-content.xml的主要作用：1、配置自动扫描的包，2、配置视图解析器，把handler方法返回值解析为实际的物理视图

<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
      http://www.springframework.org/schema/beans/spring-beans-4.3.xsd
      http://www.springframework.org/schema/context
      http://www.springframework.org/schema/context/spring-context-4.3.xsd
      http://www.springframework.org/schema/mvc
      http://www.springframework.org/schema/mvc/spring-mvc-4.3.xsd">
    <!-- 配置自动扫描的包 -->
    <context:component-scan base-package="com.dayu.controller" />
    <!-- 视图解释类 配置视图解析器 如何把handler 方法返回值解析为实际的物理视图 -->
    <bean id="viewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/views/" />
        <!--可为空,方便实现自已的依据扩展名来选择视图解释类的逻辑 -->
        <property name="suffix" value=".jsp" />
    </bean>
</beans>


##六、配置WEB-INF下的web.xml文件

web.xml文件声明了一个Servlet（即dispatcher servlet）来接收所有类型的请求。Dispatcher servlet在这里充当前端控制器的角色。

<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns="http://java.sun.com/xml/ns/javaee"
         xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd"
         id="WebApp_ID" version="2.5">
  <display-name>Archetype Created Web Application</display-name>

  <!-- 配置DispatchcerServlet -->
  <servlet>
    <servlet-name>springDispatcherServlet</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <!-- 配置Spring mvc下的配置文件的位置和名称 -->
    <init-param>
      <param-name>contextConfigLocation</param-name>
      <param-value>classpath:spring-content.xml</param-value>
    </init-param>
    <load-on-startup>1</load-on-startup>
  </servlet>

  <servlet-mapping>
    <servlet-name>springDispatcherServlet</servlet-name>
    <url-pattern>/</url-pattern>
  </servlet-mapping>
</web-app>

##七、运行测试
