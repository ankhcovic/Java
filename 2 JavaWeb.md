# JSP内置对象

* pageContext
* request
* session
* application
* page
* response
* out
* config
* exception

# MVC开发模式

## M: model 

通过JavaBean实现，完成具体的业务操作，如查询数据库、封装对象

## V: view

通过JSP展示数据

## C: controller

通过servlet实现控制器

* 获取用户的输入
* 控制模型
* 将数据交给视图展示

 

# Servlet

![img](C:\Users\94307\OneDrive - zju.edu.cn\learnbm\JAVA\学习笔记\2018120522281643.gif)

**Servlet 概述**

Servlet是sun公司提供的一门用于开发动态web资源的技术。
　　Sun公司在其API中提供了一个servlet接口，用户若想用发一个动态web资源(即开发一个Java程序向浏览器输出数据)，需要完成以下2个步骤：
　　1、编写一个Java类，实现servlet接口。
　　2、把开发好的Java类部署到web服务器中。
　　按照一种约定俗成的称呼习惯，通常我们也把实现了servlet接口的java程序，称之为servlet

ServletServlet程序无法单独运行，需要放在服务器中，由服务器调用。他是运行在服务器中的java程序，其作用是对服务器接收的请求进行处理。

![请求处理](C:\Users\94307\OneDrive - zju.edu.cn\learnbm\JAVA\学习笔记\20200810195414887.png)

```
Servlet	//接口
	GenericServlet	//抽象类
		HttpServlet 	//继承该类，重写doGet()、doPost()方法
```

**request和response**

request是Http请求信息的对象，response是Http响应信息的对象
浏览器发出请求访问服务器中的Servlet时，服务器会调用Servlet中的service方法处理请求，在这之前就会先创建request和response对象。
request对象封装了浏览器发给服务器的请求信息（请求头、请求行、请求实体等等）

response对象会封装服务器发送给浏览器的响应信息（状态行、响应头、响应实体等等）

在service方法执行完毕后，服务器再将response中的数据取出，按照HTTP协议的格式发送给浏览器。
服务器每次处理请求都会创建request和response对象，并在处理完请求，响应结束时，服务器会销毁request和response对象

##### 获取请求参数乱码

```java
request.setCharacterEncoding("utf-8");	//只对POST提交有效
```

**向客户端发送数据**

```java
/**
 *通知服务器响应和浏览器接收数据时采用 utf-8编码格式
 */
response.setContentType("text/html;charset=utf-8");
PrintWriter out = response.getWriter();
out.write("hello world");
```

##### 作用域对象

request在实现转发时，可以通过request.setAttribute方法和request.getAttribute方法，通过request对象中的map集合带数据，这个request对象的map集合和request对象作用的范围就是一个域对象。

```
request.setAttribute(String attrName,Object value);	
//往request域中存入域属性（属性名 和 属性值）

request.getAtrribute(String attrName);	
//根据属性名来获取 属性值

```

**request域对象**

**生命周期**：在服务器调用Servlet程序的service方法前创建，在请求处理完成，响应结束时，销毁request对象
**作用范围**：在一次请求的的范围内，都是同一个request对象
**主要功能**：和请求转发配合使用，从Servlet将数据带到 JSP 中



**请求转发**

**服务器内部资源的跳转方式**，浏览器发送请求访问服务器资源，该资源将请求转发给另一资源并由该资源做出响应的过程叫做请求转发
**请求转发的特点**

- 转发是一次请求，一次响应
- 请求转发后，浏览器地址不会改变
- 请求转发前后的request对象是同一个对象（所以转发才能带数据）
- 请求转发前后的两个资源必须是同一Web应用

**请求转发实现**:

```java
request.getRequestDispatcher(url).forward(req,res);
```

**重定向**

浏览器向服务器发送请求访问资源A，资源A在响应时通知浏览器进一步请求获取对应的资源，浏览器再次向服务器发送请求访问资源B，最终资源B响应浏览器的请求，这个过程就是重定向

**重定向的特点**：

- 重定向是两次请求，两次响应
- 重定向后浏览器地址会发生变化（两次请求都是浏览器发起）
- 重定向前后的request对象不是同一个（所以不能够写到数据到目的地）
- 重定向前后的两个资源可以来自不同的Web应用或者不同的服务器

**代码**：

```java
response.sendRedirect(url);
```