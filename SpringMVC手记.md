# SpringMVC�̳�
# ����
## ���Ŀ
### Maven ���
ʹ�� `Maven` ���Էǳ�����Ĵ `SpringMVC` ��Ŀ, ���ҿ����ڰ汾�䶯ʱ, ���ٸ��������� `jar`

**��ʾ** ����ʹ�õĻ�ֻ�� `eclipse` �����ϵ� `Maven`, һ���ڹ��������ص� `Eclipse JavaEE IDE` �ʹ����˸ò��

>
###### �½�һ�� Maven Project  
����Ϊ�����: 
* new һ���µ� `maven project`
* next ѡ�� `maven-archetype-webapp`

#### �����ļ� pom.xml
>��Ŀ¼ `pom.xml` ������Ҫ��Ҫ���õ�һ���ļ�

�������һ���������
```
<!--��������������Ŀ-->
<dependencies>
...
    <!--
         1. spring-web
    -->
 	<dependency>
    	<groupId>org.springframework</groupId>
    	<artifactId>spring-web</artifactId>
    	<version>${springVersion}</version>
    </dependency>
    
    <!--
        2. spring-webmvc 
        ���а�����Ҫ��DispatcherServlet 
        ��Ҫ©��
    -->
    <dependency>
    	<groupId>org.springframework</groupId>
    	<artifactId>spring-webmvc</artifactId>
    	<version>${springVersion}</version>
    </dependency>
...
</dependencies>
    
<properties>
    <!--
    �������õ�������${springVersion}
    ��߽���ͳһ����, �����ظ��޸�
    -->
    <springVersion>4.1.1.RELEASE</springVersion>
</properties>
```
֮��ѡ����Ŀ�е� `pom.xml` ִ�� `run as Maven install` 

**ע������**  
����֮�����Ŀ���ڱ��� 
* ע�� `Libraries` ������ `Apache Tomcat`  
> �������: �� `Properties` ��ѡ�� `Java Build Path` -> `Add Library` -> `Server Runtime` ѡ������һ���  

* ��һ����������maven������ 
> �������: ��Ȼ��`Properties` ��ѡ�� `Project  Facets` ���� `DynamicWebModule`, `Java`, `javaScript` ��Ҫ��ѡ, ���� `Java` ��İ汾����Ҫ�޸�Ϊ�ڵ�ǰ `JRE` �� `JDK` ��ͬ�İ汾��

����������ɺ��Ѿ������� `SpringMVC` ������

### ����SpringMVC
������� `SpringMVC` ���������  

`WEB-INF` �� `web.xml` ������������
```
<web-app xmlns="http://java.sun.com/xml/ns/javaee"  
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
      xsi:schemaLocation="http://java.sun.com/xml/ns/javaee 
      http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd"  
      version="3.0">  
    <servlet>
        <!--spring-mvc��������Լ�����-->
        <servlet-name>spring-mvc</servlet-name>  
        <init-param>
    		<param-name>contextConfigLocation</param-name>
    		<!--�������springmvc.xml������һ���Ҫ������ļ�-->
    		<param-value>classpath:springmvc.xml</param-value>
    	</init-param>
    	<load-on-startup>1</load-on-startup>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>  
    </servlet>  
    
    <servlet-mapping>  
        <!--spring-mvc�������������-->
        <servlet-name>spring-mvc</servlet-name>  
        <url-pattern>/</url-pattern>  
    </servlet-mapping>  
</web-app>  
```
�� `web.xml` ͬ���ļ��н��� `classpath:springmvc.xml` �ж���� `springmvc.xml`  
������������
```
<beans xmlns="http://www.springframework.org/schema/beans"  
    xmlns:context="http://www.springframework.org/schema/context"  
    xmlns:mvc="http://www.springframework.org/schema/mvc" 
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
    xsi:schemaLocation="  
        http://www.springframework.org/schema/beans       
        http://www.springframework.org/schema/beans/spring-beans-3.0.xsd  
        http://www.springframework.org/schema/context   
        http://www.springframework.org/schema/context/spring-context-3.0.xsd  
        http://www.springframework.org/schema/mvc  
        http://www.springframework.org/schema/mvc/spring-mvc-3.0.xsd">  
    <!--com.springmvc.controller ������¾������ǵ�controller �����Զ���-->
    <context:component-scan base-package="com.springmvc.controller" />  
    <bean id="viewResolver"  
        class="org.springframework.web.servlet.view.InternalResourceViewResolver">  
        <!--/WEB-INF/view/ ���·���������ǵ�view�ļ��� �����Զ���-->
        <property name="prefix" value="/WEB-INF/view/" />  
        <property name="suffix" value=".jsp" />  
    </bean>  
</beans>  
```
���϶������Կ��������ϲ鵽���� ���в���ȫ������

���˲��� `SpringMVC` ��Ŀ����

**��ʾ**
��װ�� `Spring` ��ӦIDE����������`<beans xmlns>` `<web-app xmlns>` �е����Կ�����Ӧ��ѡ����

## Hello World
֮ǰ�����Ѿ������� `view` ·�� `/WEB-INF/view/` �Լ� `controller` �� `com.springmvc.controller` ֮�����ǲ���׸��, �½�`controller` �Լ� `view` ��Ĭ��Ϊ�Դ�ΪĬ�ϰ�����Ĭ�ϸ�Ŀ¼

�� `controller` �����½� `Java` �ļ�, ����ȡ��  
�����ֱ�Ӹ�������
```
package com.springmvc.controller;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.RequestMapping;

@RequestMapping(value = "/Home")
@Controller
public class Home {
	@RequestMapping(value = "/Index")
	public String HelloWorld(Model model) {
		model.addAttribute("message", "Hello World!!!");
		return "index";
	}
}
```

ͬ�� `view` �ļ������½���ͼ ������ `controller` �е� `return "index"` һ��Ϊ `index.jsp`   
���а����ı�ǩͬ��ֱ�Ӹ���
```
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"  
    pageEncoding="ISO-8859-1"%>  
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"
 "http://www.w3.org/TR/html4/loose.dtd">  
<html>  
<head>  
<meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">  
<title>Insert title here</title>  
</head>  
<body>  
<h1>message:${message}</h1>  
</body>  
</html>  
```
����Ŀ����� `Tomcat` �м���ֱ�� `run as run on server`
������� `http://localhost:8080/VickOA/Home/Index` ���ɿ�����ػ�������Ϣ  

**��ʾ** `http://��ַ:�˿�/��Ŀ��/Home/Index`

���µ����������

## ��
Spring���� `spring-framework` ������: http://projects.spring.io/spring-framework/  
Eclipse����������: https://www.eclipse.org/

TODO
# RequestMapping
## ����URL
## ���󷽷�
## �������
## ����ͷ
## Ant���ͨ���
## PathVariable
֧��REST URL

## HiddenHttpMethodFilter
RequestMethod������ʽ GET POST PUT DELETE

## RequestParam

## RequestHeader

## POJO�����뼶������

## Controllerʹ��Servletԭ��API����
