# Servlet





******

## 1. Servlet简介



### 1.1 认识Servlet

Java Servlet 是运行在 Web 服务器或应用服务器上的程序，它是作为来自 Web 浏览器或其他 HTTP 客户端的请求和 HTTP 服务器上的数据库或应用程序之间的中间层。

使用 Servlet，您可以收集来自网页表单的用户输入，呈现来自数据库或者其他源的记录，还可以动态创建网页。

Java Servlet 通常情况下与使用 CGI（Common Gateway Interface，公共网关接口）实现的程序可以达到异曲同工的效果。但是相比于 CGI，Servlet 有以下几点优势：

- 性能明显更好。
- Servlet 在 Web 服务器的地址空间内执行。这样它就没有必要再创建一个单独的进程来处理每个客户端请求。
- Servlet 是独立于平台的，因为它们是用 Java 编写的。
- 服务器上的 Java 安全管理器执行了一系列限制，以保护服务器计算机上的资源。因此，Servlet 是可信的。
- Java 类库的全部功能对 Servlet 来说都是可用的。它可以通过 sockets 和 RMI 机制与 applets、数据库或其他软件进行交互。



### 1.2 Servlet优势

Servlet 执行以下主要任务：

- 读取客户端（浏览器）发送的显式的数据。这包括网页上的 HTML 表单，或者也可以是来自 applet 或自定义的 HTTP 客户端程序的表单。
- 读取客户端（浏览器）发送的隐式的 HTTP 请求数据。这包括 cookies、媒体类型和浏览器能理解的压缩格式等等。
- 处理数据并生成结果。这个过程可能需要访问数据库，执行 RMI 或 CORBA 调用，调用 Web 服务，或者直接计算得出对应的响应。
- 发送显式的数据（即文档）到客户端（浏览器）。该文档的格式可以是多种多样的，包括文本文件（HTML 或 XML）、二进制文件（GIF 图像）、Excel 等。
- 发送隐式的 HTTP 响应到客户端（浏览器）。这包括告诉浏览器或其他客户端被返回的文档类型（例如 HTML），设置 cookies 和缓存参数，以及其他类似的任务。



### 1.3 Servlet架构

<img src="./img/1.jpg" alt="Servlet 架构"  />



## 2. Servlet生命周期

Servlet 生命周期可被定义为从创建直到毁灭的整个过程。以下是 Servlet 遵循的过程：

- Servlet 通过调用 **init ()** 方法进行初始化。

- Servlet 调用 **service()** 方法来处理客户端的请求。

- Servlet 通过调用 **destroy()** 方法终止（结束）。

- 最后，Servlet 是由 JVM 的垃圾回收器进行垃圾回收的。

  

### 2.1 生命周期架构图

下图显示了一个典型的 Servlet 生命周期方案。

- 第一个到达服务器的 HTTP 请求被委派到 Servlet 容器。
- Servlet 容器在调用 service() 方法之前加载 Servlet。
- 然后 Servlet 容器处理由多个线程产生的多个请求，每个线程执行一个单一的 Servlet 实例的 service() 方法。



![Servlet 生命周期](./img/2.jpg)



### 2.2 init() 方法

init 方法被设计成只调用一次。它在第一次创建 Servlet 时被调用，在后续每次用户请求时不再调用。因此，它是用于一次性初始化，就像 Applet 的 init 方法一样。

Servlet 创建于用户第一次调用对应于该 Servlet 的 URL 时，但是您也可以指定 Servlet 在服务器第一次启动时被加载。

当用户调用一个 Servlet 时，就会创建一个 Servlet 实例，每一个用户请求都会产生一个新的线程，适当的时候移交给 doGet 或 doPost 方法。

**init() 方法简单地创建或加载一些数据，这些数据将被用于 Servlet 的整个生命周期。**

init 方法的定义如下：

```java
public void init() throws ServletException {
  // 初始化代码...
}
```



### 2.3 service() 方法

service() 方法是执行实际任务的主要方法。Servlet 容器（即 Web 服务器）调用 service() 方法来处理来自客户端（浏览器）的请求，并把格式化的响应写回给客户端。

每次服务器接收到一个 Servlet 请求时，服务器会产生一个新的线程并调用服务。service() 方法检查 HTTP 请求类型（GET、POST、PUT、DELETE 等），并在适当的时候调用 doGet、doPost、doPut，doDelete 等方法。

下面是该方法的特征：

```java
public void service(ServletRequest request, 
                    ServletResponse response) 
      throws ServletException, IOException{
}
```

service() 方法由容器调用，service 方法在适当的时候调用 doGet、doPost、doPut、doDelete 等方法。所以，您不用对 service() 方法做任何动作，您只需要根据来自客户端的请求类型来重载 doGet() 或 doPost() 即可。

doGet() 和 doPost() 方法是每次服务请求中最常用的方法。下面是这两种方法的特征。



### 2.4 doGet() 方法

GET 请求来自于一个 URL 的正常请求，或者来自于一个未指定 METHOD 的 HTML 表单，它由 doGet() 方法处理。

```java
public void doGet(HttpServletRequest request,
                  HttpServletResponse response)
    throws ServletException, IOException {
    // Servlet 代码
}
```



### 2.5 doPost() 方法

POST 请求来自于一个特别指定了 METHOD 为 POST 的 HTML 表单，它由 doPost() 方法处理。

```java
public void doPost(HttpServletRequest request,
                   HttpServletResponse response)
    throws ServletException, IOException {
    // Servlet 代码
}
```



### 2.6 destroy() 方法

**destroy() 方法只会被调用一次，在 Servlet 生命周期结束时被调用**

destroy() 方法可以让您的 Servlet 关闭数据库连接、停止后台线程、把 Cookie 列表或点击计数器写入到磁盘，并执行其他类似的清理活动。

在调用 destroy() 方法之后，servlet 对象被标记为垃圾回收。destroy 方法定义如下所示：

```java
  public void destroy() {
    // 终止化代码...
  }
```



## 3. 表单提交数据



### 3.1 使用表单的 GET 方法实例

下面是一个简单的实例，使用 HTML 表单和提交按钮传递两个值。我们将使用相同的 Servlet HelloForm 来处理输入。

```html
<html>
<body>
<form action="HelloForm" method="GET">
名字：<input type="text" name="first_name">
<br />
姓氏：<input type="text" name="last_name" />
<input type="submit" value="提交" />
</form>
</body>
</html>
```

**action：对应的Servlet名字**

**method：处理的方法名**

**name：对应表单组件的名字，用来Servlet识别**

保存这个 HTML 到 hello.htm 文件中。当您访问 *http://localhost:8080/Hello.html* 时，下面是上面表单的实际输出。

![img](./img/3.png)

尝试输入名字和姓氏，然后点击"提交"按钮，在您本机上查看输出结果。基于所提供的输入，它会产生与上一个实例类似的结果。



### 3.2 使用表单的 POST 方法实例

让我们对上面的 Servlet 做小小的修改，以便它可以处理 GET 和 POST 方法。下面的 **HelloForm.java** Servlet 程序使用 GET 和 POST 方法处理由 Web 浏览器给出的输入。

```java
// 导入必需的 java 库
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

// 扩展 HttpServlet 类
public class HelloForm extends HttpServlet {
 
  // 处理 GET 方法请求的方法
  public void doGet(HttpServletRequest request,
                    HttpServletResponse response)
            throws ServletException, IOException
  {
      // 设置响应内容类型
      response.setContentType("text/html");

      PrintWriter out = response.getWriter();
      String title = "Using GET Method to Read Form Data";
      String docType =
      "<!doctype html public \"-//w3c//dtd html 4.0 " +       "transitional//en\">\n";
      out.println(docType +
                "<html>\n" +
                "<head><title>" + title + "</title></head>\n" +
                "<body bgcolor=\"#f0f0f0\">\n" +
                "<h1 align=\"center\">" + title + "</h1>\n" +
                "<ul>\n" +
                "  <li><b>名字</b>："
                + request.getParameter("first_name") + "\n" +
                "  <li><b>姓氏</b>："
                + request.getParameter("last_name") + "\n" +
                "</ul>\n" +
                "</body></html>");
  }
  // 处理 POST 方法请求的方法
  public void doPost(HttpServletRequest request,
                     HttpServletResponse response)
      throws ServletException, IOException {
     doGet(request, response);
  }
}
```

现在，编译部署上述的 Servlet，并使用带有 POST 方法的 Hello.htm 进行测试，如下所示：

```java
<html>
<body>
<form action="HelloForm" method="POST">
名字：<input type="text" name="first_name">
<br />
姓氏：<input type="text" name="last_name" />
<input type="submit" value="提交" />
</form>
</body>
</html>
```

下面是上面表单的实际输出，尝试输入名字和姓氏，然后点击"提交"按钮，在您本机上查看输出结果。



![img](./img/4.png)

基于所提供的输入，它会产生与上一个实例类似的结果。



### 3.3 将复选框数据传递到 Servlet 程序

当需要选择一个以上的选项时，则使用复选框。

下面是一个 HTML 代码实例 CheckBox.htm，一个带有两个复选框的表单。

```html
<html>
<body>
<form action="CheckBox" method="POST" target="_blank">
<input type="checkbox" name="maths" checked="checked" /> 数学
<input type="checkbox" name="physics"  /> 物理
<input type="checkbox" name="chemistry" checked="checked" /> 
                                                化学
<input type="submit" value="选择学科" />
</form>
</body>
</html>
```

这段代码的结果是下面的表单：

![img](./img/5.png)

下面是 CheckBox.java Servlet 程序，处理 Web 浏览器给出的复选框输入。

```java
// 导入必需的 java 库
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

// 扩展 HttpServlet 类
public class CheckBox extends HttpServlet {
 
  // 处理 GET 方法请求的方法
  public void doGet(HttpServletRequest request,
                    HttpServletResponse response)
            throws ServletException, IOException
  {
      // 设置响应内容类型
      response.setContentType("text/html");

      PrintWriter out = response.getWriter();
     String title = "读取复选框数据";
      String docType =
      "<!doctype html public \"-//w3c//dtd html 4.0 " +       "transitional//en\">\n";
      out.println(docType +
                "<html>\n" +
                "<head><title>" + title + "</title></head>\n" +
                "<body bgcolor=\"#f0f0f0\">\n" +
                "<h1 align=\"center\">" + title + "</h1>\n" +
                "<ul>\n" +
                "  <li><b>数学标识：</b>: "
                + request.getParameter("maths") + "\n" +
                "  <li><b>物理标识：</b>: "
                + request.getParameter("physics") + "\n" +
                "  <li><b>化学标识：</b>: "
                + request.getParameter("chemistry") + "\n" +
                "</ul>\n" +
                "</body></html>");
  }
  // 处理 POST 方法请求的方法
  public void doPost(HttpServletRequest request,
                     HttpServletResponse response)
      throws ServletException, IOException {
     doGet(request, response);
  }
}
```

上面的实例将显示下面的结果：

读取复选框数据**数学标识：**on**物理标识：**null**化学标识：**on



### 3.4 读取所有的表单参数

以下是通用的实例，使用 HttpServletRequest 的 **getParameterNames()** 方法读取所有可用的表单参数。该方法返回一个枚举，其中包含未指定顺序的参数名。

一旦我们有一个枚举，我们可以以标准方式循环枚举，使用 *hasMoreElements()* 方法来确定何时停止，使用 *nextElement()* 方法来获取每个参数的名称。

```java
// 导入必需的 java 库
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;
import java.util.*;

// 扩展 HttpServlet 类
public class ReadParams extends HttpServlet {
 
  // 处理 GET 方法请求的方法
  public void doGet(HttpServletRequest request,
                    HttpServletResponse response)
            throws ServletException, IOException
  {
      // 设置响应内容类型
      response.setContentType("text/html");

      PrintWriter out = response.getWriter();
     String title = "读取所有的表单数据";
      String docType =
      "<!doctype html public \"-//w3c//dtd html 4.0 " +       "transitional//en\">\n";
      out.println(docType +
        "<html>\n" +
        "<head><title>" + title + "</title></head>\n" +
        "<body bgcolor=\"#f0f0f0\">\n" +
        "<h1 align=\"center\">" + title + "</h1>\n" +
        "<table width=\"100%\" border=\"1\" align=\"center\">\n" +
        "<tr bgcolor=\"#949494\">\n" +
        "<th>参数名称</th><th>参数值</th>\n"+
        "</tr>\n");

      Enumeration paramNames = request.getParameterNames();
      
      while(paramNames.hasMoreElements()) {
         String paramName = (String)paramNames.nextElement();
         out.print("<tr><td>" + paramName + "</td>\n<td>");
         String[] paramValues =
                request.getParameterValues(paramName);
         // 读取单个值的数据
         if (paramValues.length == 1) {
           String paramValue = paramValues[0];
           if (paramValue.length() == 0)
             out.println("<i>No Value</i>");
           else
             out.println(paramValue);
         } else {
             // 读取多个值的数据
             out.println("<ul>");
             for(int i=0; i < paramValues.length; i++) {                 out.println("<li>" + paramValues[i]);
             }
             out.println("</ul>");
         }
      }
      out.println("</tr>\n</table>\n</body></html>");
  }
  // 处理 POST 方法请求的方法
  public void doPost(HttpServletRequest request,
                     HttpServletResponse response)
      throws ServletException, IOException {
     doGet(request, response);
  }
}
```

现在，通过下面的表单尝试上面的 Servlet：

```java
<html>
<body>
<form action="ReadParams" method="POST" target="_blank">
<input type="checkbox" name="maths" checked="checked" /> 数学
<input type="checkbox" name="physics"  /> 物理
<input type="checkbox" name="chemistry" checked="checked" /> 化学
<input type="submit" value="选择学科" />
</form>
</body>
</html>
```

现在使用上面的表单调用 Servlet，将产生以下结果：

​												**读取所有的表单数据**

| 参数名称  | 参数值 |
| --------- | ------ |
| maths     | on     |
| chemistry | on     |

您可以尝试使用上面的 Servlet 来读取其他的表单数据，比如文本框、单选按钮或下拉框等。





## 4. 请求与响应



### 4.1 理解

![img](./img/6.png)



### 4.2 Request



HttpServletRequest对象方法

| 序号 | 方法 & 描述                                                  |
| :--- | :----------------------------------------------------------- |
| 1    | **Cookie[] getCookies()** 返回一个数组，包含客户端发送该请求的所有的 Cookie 对象。 |
| 2    | **Enumeration getAttributeNames()** 返回一个枚举，包含提供给该请求可用的属性名称。 |
| 3    | **Enumeration getHeaderNames()** 返回一个枚举，包含在该请求中包含的所有的头名。 |
| 4    | **Enumeration getParameterNames()** 返回一个 String 对象的枚举，包含在该请求中包含的参数的名称。 |
| 5    | **HttpSession getSession()** 返回与该请求关联的当前 session 会话，或者如果请求没有 session 会话，则创建一个。 |
| 6    | **HttpSession getSession(boolean create)** 返回与该请求关联的当前 HttpSession，或者如果没有当前会话，且创建是真的，则返回一个新的 session 会话。 |
| 7    | **Locale getLocale()** 基于 Accept-Language 头，返回客户端接受内容的首选的区域设置。 |
| 8    | **Object getAttribute(String name)** 以对象形式返回已命名属性的值，如果没有给定名称的属性存在，则返回 null。 |
| 9    | **ServletInputStream getInputStream()** 使用 ServletInputStream，以二进制数据形式检索请求的主体。 |
| 10   | **String getAuthType()** 返回用于保护 Servlet 的身份验证方案的名称，例如，"BASIC" 或 "SSL"，如果JSP没有受到保护则返回 null。 |
| 11   | **String getCharacterEncoding()** 返回请求主体中使用的字符编码的名称。 |
| 12   | **String getContentType()** 返回请求主体的 MIME 类型，如果不知道类型则返回 null。 |
| 13   | **String getContextPath()** 返回指示请求上下文的请求 URI 部分。 |
| 14   | **String getHeader(String name)** 以字符串形式返回指定的请求头的值。 |
| 15   | **String getMethod()** 返回请求的 HTTP 方法的名称，例如，GET、POST 或 PUT。 |
| 16   | **String getParameter(String name)** 以字符串形式返回请求参数的值，或者如果参数不存在则返回 null。 |
| 17   | **String getPathInfo()** 当请求发出时，返回与客户端发送的 URL 相关的任何额外的路径信息。 |
| 18   | **String getProtocol()** 返回请求协议的名称和版本。          |
| 19   | **String getQueryString()** 返回包含在路径后的请求 URL 中的查询字符串。 |
| 20   | **String getRemoteAddr()** 返回发送请求的客户端的互联网协议（IP）地址。 |
| 21   | **String getRemoteHost()** 返回发送请求的客户端的完全限定名称。 |
| 22   | **String getRemoteUser()** 如果用户已通过身份验证，则返回发出请求的登录用户，或者如果用户未通过身份验证，则返回 null。 |
| 23   | **String getRequestURI()** 从协议名称直到 HTTP 请求的第一行的查询字符串中，返回该请求的 URL 的一部分。 |
| 24   | **String getRequestedSessionId()** 返回由客户端指定的 session 会话 ID。 |
| 25   | **String getServletPath()** 返回调用 JSP 的请求的 URL 的一部分。 |
| 26   | **String[] getParameterValues(String name)** 返回一个字符串对象的数组，包含所有给定的请求参数的值，如果参数不存在则返回 null。 |
| 27   | **boolean isSecure()** 返回一个布尔值，指示请求是否使用安全通道，如 HTTPS。 |
| 28   | **int getContentLength()** 以字节为单位返回请求主体的长度，并提供输入流，或者如果长度未知则返回 -1。 |
| 29   | **int getIntHeader(String name)** 返回指定的请求头的值为一个 int 值。 |
| 30   | **int getServerPort()** 返回接收到这个请求的端口号。         |
| 31   | **setCharacterEncoding()** 设置被发送到服务端的响应的字符编码。例如，UTF-8。 |



### 4.3 response



**HttpServletResponse对象方法**

| 序号 | 方法 & 描述                                                  |
| :--- | :----------------------------------------------------------- |
| 1    | **String encodeRedirectURL(String url)** 为 sendRedirect 方法中使用的指定的 URL 进行编码，或者如果编码不是必需的，则返回 URL 未改变。 |
| 2    | **String encodeURL(String url)** 对包含 session 会话 ID 的指定 URL 进行编码，或者如果编码不是必需的，则返回 URL 未改变。 |
| 3    | **boolean containsHeader(String name)** 返回一个布尔值，指示是否已经设置已命名的响应报头。 |
| 4    | **boolean isCommitted()** 返回一个布尔值，指示响应是否已经提交。 |
| 5    | **void addCookie(Cookie cookie)** 把指定的 cookie 添加到响应。 |
| 6    | **void addDateHeader(String name, long date)** 添加一个带有给定的名称和日期值的响应报头。 |
| 7    | **void addHeader(String name, String value)** 添加一个带有给定的名称和值的响应报头。 |
| 8    | **void addIntHeader(String name, int value)** 添加一个带有给定的名称和整数值的响应报头。 |
| 9    | **void flushBuffer()** 强制任何在缓冲区中的内容被写入到客户端。 |
| 10   | **void reset()** 清除缓冲区中存在的任何数据，包括状态码和头。 |
| 11   | **void resetBuffer()** 清除响应中基础缓冲区的内容，不清除状态码和头。 |
| 12   | **void sendError(int sc)** 使用指定的状态码发送错误响应到客户端，并清除缓冲区。 |
| 13   | **void sendError(int sc, String msg)** 使用指定的状态发送错误响应到客户端。 |
| 14   | **void sendRedirect(String location)** 使用指定的重定向位置 URL 发送临时重定向响应到客户端。 |
| 15   | **void setBufferSize(int size)** 为响应主体设置首选的缓冲区大小。 |
| 16   | **void setCharacterEncoding(String charset)** 设置被发送到客户端的响应的字符编码（MIME 字符集）例如，UTF-8。 |
| 17   | **void setContentLength(int len)** 设置在 HTTP Servlet 响应中的内容主体的长度，该方法设置 HTTP Content-Length 头。 |
| 18   | **void setContentType(String type)** 如果响应还未被提交，设置被发送到客户端的响应的内容类型。 |
| 19   | **void setDateHeader(String name, long date)** 设置一个带有给定的名称和日期值的响应报头。 |
| 20   | **void setHeader(String name, String value)** 设置一个带有给定的名称和值的响应报头。 |
| 21   | **void setIntHeader(String name, int value)** 设置一个带有给定的名称和整数值的响应报头。 |
| 22   | **void setLocale(Locale loc)** 如果响应还未被提交，设置响应的区域。 |
| 23   | **void setStatus(int sc)** 为该响应设置状态码。              |



### 4.4 http状态码



#### 4.4.1 状态码

| 代码 | 消息                          | 描述                                                         |
| :--- | :---------------------------- | :----------------------------------------------------------- |
| 100  | Continue                      | 只有请求的一部分已经被服务器接收，但只要它没有被拒绝，客户端应继续该请求。 |
| 101  | Switching Protocols           | 服务器切换协议。                                             |
| 200  | OK                            | 请求成功。                                                   |
| 201  | Created                       | 该请求是完整的，并创建一个新的资源。                         |
| 202  | Accepted                      | 该请求被接受处理，但是该处理是不完整的。                     |
| 203  | Non-authoritative Information |                                                              |
| 204  | No Content                    |                                                              |
| 205  | Reset Content                 |                                                              |
| 206  | Partial Content               |                                                              |
| 300  | Multiple Choices              | 链接列表。用户可以选择一个链接，进入到该位置。最多五个地址。 |
| 301  | Moved Permanently             | 所请求的页面已经转移到一个新的 URL。                         |
| 302  | Found                         | 所请求的页面已经临时转移到一个新的 URL。                     |
| 303  | See Other                     | 所请求的页面可以在另一个不同的 URL 下被找到。                |
| 304  | Not Modified                  |                                                              |
| 305  | Use Proxy                     |                                                              |
| 306  | *Unused*                      | 在以前的版本中使用该代码。现在已不再使用它，但代码仍被保留。 |
| 307  | Temporary Redirect            | 所请求的页面已经临时转移到一个新的 URL。                     |
| 400  | Bad Request                   | 服务器不理解请求。                                           |
| 401  | Unauthorized                  | 所请求的页面需要用户名和密码。                               |
| 402  | Payment Required              | *您还不能使用该代码。*                                       |
| 403  | Forbidden                     | 禁止访问所请求的页面。                                       |
| 404  | Not Found                     | 服务器无法找到所请求的页面。.                                |
| 405  | Method Not Allowed            | 在请求中指定的方法是不允许的。                               |
| 406  | Not Acceptable                | 服务器只生成一个不被客户端接受的响应。                       |
| 407  | Proxy Authentication Required | 在请求送达之前，您必须使用代理服务器的验证。                 |
| 408  | Request Timeout               | 请求需要的时间比服务器能够等待的时间长，超时。               |
| 409  | Conflict                      | 请求因为冲突无法完成。                                       |
| 410  | Gone                          | 所请求的页面不再可用。                                       |
| 411  | Length Required               | "Content-Length" 未定义。服务器无法处理客户端发送的不带 Content-Length 的请求信息。 |
| 412  | Precondition Failed           | 请求中给出的先决条件被服务器评估为 false。                   |
| 413  | Request Entity Too Large      | 服务器不接受该请求，因为请求实体过大。                       |
| 414  | Request-url Too Long          | 服务器不接受该请求，因为 URL 太长。当您转换一个 "post" 请求为一个带有长的查询信息的 "get" 请求时发生。 |
| 415  | Unsupported Media Type        | 服务器不接受该请求，因为媒体类型不被支持。                   |
| 417  | Expectation Failed            |                                                              |
| 500  | Internal Server Error         | 未完成的请求。服务器遇到了一个意外的情况。                   |
| 501  | Not Implemented               | 未完成的请求。服务器不支持所需的功能。                       |
| 502  | Bad Gateway                   | 未完成的请求。服务器从上游服务器收到无效响应。               |
| 503  | Service Unavailable           | 未完成的请求。服务器暂时超载或死机。                         |
| 504  | Gateway Timeout               | 网关超时。                                                   |
| 505  | HTTP Version Not Supported    | 服务器不支持"HTTP协议"版本。                                 |

#### 4.4.2 设置 HTTP 状态代码的方法

下面的方法可用于在 Servlet 程序中设置 HTTP 状态码。这些方法通过 *HttpServletResponse* 对象可用。

| 序号 | 方法 & 描述                                                  |
| :--- | :----------------------------------------------------------- |
| 1    | **public void setStatus ( int statusCode )** 该方法设置一个任意的状态码。setStatus 方法接受一个 int（状态码）作为参数。如果您的反应包含了一个特殊的状态码和文档，请确保在使用 *PrintWriter* 实际返回任何内容之前调用 setStatus。 |
| 2    | **public void sendRedirect(String url)** 该方法生成一个 302 响应，连同一个带有新文档 URL 的 *Location* 头。 |
| 3    | **public void sendError(int code, String message)** 该方法发送一个状态码（通常为 404），连同一个在 HTML 文档内部自动格式化并发送到客户端的短消息。 |



**HTTP 状态码实例**

下面的例子把 407 错误代码发送到客户端浏览器，浏览器会显示 "Need authentication!!!" 消息。

```java
// 导入必需的 java 库
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;
import java.util.*;

// 扩展 HttpServlet 类
public class showError extends HttpServlet {
 
  // 处理 GET 方法请求的方法
  public void doGet(HttpServletRequest request,
                    HttpServletResponse response)
            throws ServletException, IOException
  {
      // 设置错误代码和原因
      response.sendError(407, "Need authentication!!!" );
  }
  // 处理 POST 方法请求的方法
  public void doPost(HttpServletRequest request,
                     HttpServletResponse response)
      throws ServletException, IOException {
     doGet(request, response);
  }
}
```

现在，调用上面的 Servlet 将显示以下结果：

HTTP Status 407 - Need authentication!!!**type** Status report**message** Need authentication!!!**description** The client must first authenticate itself with the proxy (Need authentication!!!).Apache Tomcat/5.5.29



## 5. 文件上传



### 5.1 创建一个文件上传表单

下面的 HTML 代码创建了一个文件上传表单。以下几点需要注意：

- **表单 method属性应该设置为 POST 方法，不能使用 GET 方法。**
- **表单 enctype 属性应该设置为 multipart/form-data.（关键，必须设置）**
- 表单 **action** 属性应该设置为在后端服务器上处理文件上传的 Servlet 文件。下面的实例使用了 **FileUpload** Servlet 来上传文件。
- 上传单个文件，您应该使用单个带有属性 type="file" 的 <input .../> 标签。为了允许多个文件上传，请包含多个 name 属性值不同的 input 标签。输入标签具有不同的名称属性的值。浏览器会为每个 input 标签关联一个浏览按钮。

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<form action="FileUpload" method="post" enctype="multipart/form-data">
		<input type="file" name="upload" value="">
		<input type="submit" value="Submit">
	</form>
</body>
</html>
```



### 5.2 编写后台 Servlet

```java
package Servlet;

import java.io.IOException;
import javax.servlet.ServletException;
import javax.servlet.annotation.MultipartConfig;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.Part;

import org.apache.catalina.valves.rewrite.Substitution.RewriteRuleBackReferenceElement;

/**
 * Servlet implementation class FileUpload
 */
// 必须设置这个
@MultipartConfig
@WebServlet("/FileUpload")
public class FileUpload extends HttpServlet {
	private static final long serialVersionUID = 1L;
       
    /**
     * @see HttpServlet#HttpServlet()
     */
    public FileUpload() {
        super();
        // TODO Auto-generated constructor stub
    }

	/**
	 * @see HttpServlet#doGet(HttpServletRequest request, HttpServletResponse response)
	 */
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		// TODO Auto-generated method stub
		response.setCharacterEncoding("UTF-8");
		request.setCharacterEncoding("UTF-8");
		response.setContentType("text/html; charset=UTF-8");
		
		// 创建一个Part对象，通过请求的方法寻找对应name
		Part part = request.getPart("upload");
		response.getWriter().println(part.getSubmittedFileName());
	}

	/**
	 * @see HttpServlet#doPost(HttpServletRequest request, HttpServletResponse response)
	 */
	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		// TODO Auto-generated method stub
		doGet(request, response);
	}

}
```



### 5.3 Part API

|        **方法**         |                  描述                  |        返回值        |
| :---------------------: | :------------------------------------: | :------------------: |
| write(String fileName)  |      将文件内容写入指定的磁盘位置      |         void         |
|        getSize()        |           获取上传文件的大小           |         long         |
|        getName()        |         获取file控件的name属性         |        String        |
| getHeader(String name)  |             获取指定请求头             |        String        |
|    getHeaderNames()     |          获取所有请求头的名称          |        String        |
| getHeaders(String name) |      获取指定header名称的集合数据      | Collection< String > |
|    getContentType()     |            获取文件MIME类型            |        String        |
|    getInputStream()     |      获取输入流用于检索文件的内容      |     InputStream      |
|        delete()         | 删除Part数据和临时目录数据,默认会删除  |         void         |
| getSubmittedFileName()  | 获取上传文件名Servlet3.1 Tomcat8.0实现 |        String        |

结合 HttpServletRequest 对象和@MultipartConfig 注解来处理文件上传.
**指定缓存大小和临时目录**
@MutipartConfig 可以设置 相应参数限制条件，必须声明，否则会报错

|       参数        |  类型  |                             概述                             |
| :---------------: | :----: | :----------------------------------------------------------: |
|     location      | String |          指定上传文件的临时目录，默认为"",绝对路径           |
| fileSizeThreshold |  int   |           指定缓存大小,超过会先存入临时目录,默认0            |
|    maxFileSize    |  long  |    单个上传文件最大大小,默认是-1,表示没有限制，单位:bytes    |
|  maxRequestSize   |  long  | 限制该multipart/form-data请求中数据的大小,默认是-1，表示没有限制，单位:bytes |

FileSize表示上传的单个文件的大小，RequestSize表示一次上传的总的数据量，所以可以在一个表单中一次上传多个文件。



## 6. 网页跳转与重定向



### 6.1 跳转

request.getRequestDispatcher("你要跳转的页面").forward(request, response)

1. 属于转发，也是服务器跳转，相当于方法调用，在执行当前文件的过程中转向执行目标文件，**两个文件(当前文件和目标文件)属于同一次请求，前后页共用一个request，可以通过此来传递一些数据或者session信息，request.setAttribute()和request.getAttribute()。**

2. 在前后两次执行后，地址栏不变，仍是当前文件的地址。

3. **不能转向到本web应用之外的页面和网站，所以转向的速度要快。**

4. URL中所包含的“/”表示应用程序(项目)的路径。



### 6.2 重定向

当文档移动到新的位置，我们需要向客户端发送这个新位置时，我们需要用到网页重定向。当然，也可能是为了负载均衡，或者只是为了简单的随机，这些情况都有可能用到网页重定向。

重定向请求到另一个网页的最简单的方式是使用 response 对象的 **sendRedirect()** 方法。

下面是该方法的定义： 将请求重定向到另一页的最简单的方法是，用方法的sendRedirect()的响应对象。以下是这种方法的定义：

```java
public void HttpServletResponse.sendRedirect(String location)
throws IOException 
```

该方法把响应连同状态码和新的网页位置发送回浏览器。您也可以通过把 setStatus() 和 setHeader() 方法一起使用来达到同样的效果：

```java
....
String site = "http://www.newpage.com" ;
response.setStatus(response.SC_MOVED_TEMPORARILY);
response.setHeader("Location", site); 
....
```

注意：

1. 是客户端跳转，相当于客户端向服务端发送请求之后，服务器返回一个响应，客户端接收到响应之后又向服务端发送一次请求，一共是2次请求，前后页不共用一个request，不能读取转向前通过request.setAttribute()设置的属性值。

2. 在前后两次执行后，地址栏发生改变，是目标文件的地址。

3. 可以转向到本web应用之外的页面和网站，所以转向的速度相对要慢。

4. URL种所包含的"/"表示根目录的路径。

特殊的应用：对数据进行修改、删除、添加操作的时候，应该用response.sendRedirect()。如果是采用了request.getRequestDispatcher().forward(request,response)，那么操作前后的地址栏都不会发生改变，仍然是修改的控制器，如果此时再对当前页面刷新的话，就会重新发送一次请求对数据进行修改，这也就是有的人在刷新一次页面就增加一条数据的原因。





## 7. 会话管理



### 7.1 Cookie



#### 7.1.1 Servlet Cookie 方法

以下是在 Servlet 中操作 Cookie 时可使用的有用的方法列表。

| 序号 | 方法 & 描述                                                  |
| :--- | :----------------------------------------------------------- |
| 1    | **public void setDomain(String pattern)** 该方法设置 cookie 适用的域，例如 runoob.com。 |
| 2    | **public String getDomain()** 该方法获取 cookie 适用的域，例如 runoob.com。 |
| 3    | **public void setMaxAge(int expiry)** 该方法设置 cookie 过期的时间（以秒为单位）。如果不这样设置，cookie 只会在当前 session 会话中持续有效。 |
| 4    | **public int getMaxAge()** 该方法返回 cookie 的最大生存周期（以秒为单位），默认情况下，-1 表示 cookie 将持续下去，直到浏览器关闭。 |
| 5    | **public String getName()** 该方法返回 cookie 的名称。名称在创建后不能改变。 |
| 6    | **public void setValue(String newValue)** 该方法设置与 cookie 关联的值。 |
| 7    | **public String getValue()** 该方法获取与 cookie 关联的值。  |
| 8    | **public void setPath(String uri)** 该方法设置 cookie 适用的路径。如果您不指定路径，与当前页面相同目录下的（包括子目录下的）所有 URL 都会返回 cookie。 |
| 9    | **public String getPath()** 该方法获取 cookie 适用的路径。   |
| 10   | **public void setSecure(boolean flag)** 该方法设置布尔值，表示 cookie 是否应该只在加密的（即 SSL）连接上发送。 |
| 11   | **public void setComment(String purpose)** 设置cookie的注释。该注释在浏览器向用户呈现 cookie 时非常有用。 |
| 12   | **public String getComment()** 获取 cookie 的注释，如果 cookie 没有注释则返回 null。 |



#### 7.1.2 通过 Servlet 设置 Cookie

通过 Servlet 设置 Cookie 包括三个步骤：

**(1) 创建一个 Cookie 对象：**您可以调用带有 cookie 名称和 cookie 值的 Cookie 构造函数，cookie 名称和 cookie 值都是字符串。

```java
Cookie cookie = new Cookie("key","value");
```

请记住，无论是名字还是值，都不应该包含空格或以下任何字符：

```
[ ] ( ) = , " / ? @ : ;
```

**(2) 设置最大生存周期：**您可以使用 setMaxAge 方法来指定 cookie 能够保持有效的时间（以秒为单位）。下面将设置一个最长有效期为 24 小时的 cookie。

```java
cookie.setMaxAge(60*60*24); 
```

**(3) 发送 Cookie 到 HTTP 响应头：**您可以使用 **response.addCookie** 来添加 HTTP 响应头中的 Cookie，如下所示：

```java
response.addCookie(cookie);
```



#### 7.1.3 通过 Servlet 读取 Cookie

要读取 Cookie，您需要通过调用 *HttpServletRequest* 的 **getCookies( )** 方法创建一个 *javax.servlet.http.Cookie* **对象的数组**。然后循环遍历数组，并使用 getName() 和 getValue() 方法来访问每个 cookie 和关联的值。

一般通过循环来遍历cookie

```java
if (cookies != null) {
    for (Cookie cookie : cookies) {
    	// cookie的名字
    	cookie.getName();
    	// cookie的值
    	cookie.getValue();
    }
}
```



#### 7.1.4 通过 Servlet 删除 Cookie

删除 Cookie 是非常简单的。如果您想删除一个 cookie，那么您只需要按照以下三个步骤进行：

- 读取一个现有的 cookie，并把它存储在 Cookie 对象中。
- 使用 **setMaxAge()** 方法设置 cookie 的年龄为零，来删除现有的 cookie。
- 把这个 cookie 添加到响应头。



### 7.2 Session



#### 7.2.1 Seeion对象及其主要方法

Servlet 提供了 HttpSession 接口，该接口提供了一种跨多个页面请求或访问网站时识别用户以及存储有关用户信息的方式。

Servlet 容器使用这个接口来创建一个 HTTP 客户端和 HTTP 服务器之间的 session 会话。会话持续一个指定的时间段，跨多个连接或页面请求。

您会通过调用 HttpServletRequest 的公共方法 **getSession()** 来获取 HttpSession 对象，如下所示：

```java
HttpSession session = request.getSession();
```

你需要在向客户端发送任何文档内容之前调用 *request.getSession()*。下面总结了 HttpSession 对象中可用的几个重要的方法：

| 序号 | 方法 & 描述                                                  |
| :--- | :----------------------------------------------------------- |
| 1    | **public Object getAttribute(String name)** 该方法返回在该 session 会话中具有指定名称的对象，如果没有指定名称的对象，则返回 null。 |
| 2    | **public Enumeration getAttributeNames()** 该方法返回 String 对象的枚举，String 对象包含所有绑定到该 session 会话的对象的名称。 |
| 3    | **public long getCreationTime()** 该方法返回该 session 会话被创建的时间，自格林尼治标准时间 1970 年 1 月 1 日午夜算起，以毫秒为单位。 |
| 4    | **public String getId()** 该方法返回一个包含分配给该 session 会话的唯一标识符的字符串。 |
| 5    | **public long getLastAccessedTime()** 该方法返回客户端最后一次发送与该 session 会话相关的请求的时间自格林尼治标准时间 1970 年 1 月 1 日午夜算起，以毫秒为单位。 |
| 6    | **public int getMaxInactiveInterval()** 该方法返回 Servlet 容器在客户端访问时保持 session 会话打开的最大时间间隔，以秒为单位。 |
| 7    | **public void invalidate()** 该方法指示该 session 会话无效，并解除绑定到它上面的任何对象。 |
| 8    | **public boolean isNew()** 如果客户端还不知道该 session 会话，或者如果客户选择不参入该 session 会话，则该方法返回 true。 |
| 9    | **public void removeAttribute(String name)** 该方法将从该 session 会话移除指定名称的对象。 |
| 10   | **public void setAttribute(String name, Object value)** 该方法使用指定的名称绑定一个对象到该 session 会话。 |
| 11   | **public void setMaxInactiveInterval(int interval)** 该方法在 Servlet 容器指示该 session 会话无效之前，指定客户端请求之间的时间，以秒为单位。 |



#### 7.2.2 创建或读取Session会话

```java
// 有则返回有的，没有则创建新的
HttpSession session = request.getSession();

// 读取Session保存一个名为code的数据值
String correctCode = (String)session.getAttribute("code");

// 给Session设置一个名为loginUser的数据值，值为userName
session.setAttribute("loginUser",userName);

```



#### 7.2.3 删除 Session 会话数据

当您完成了一个用户的 session 会话数据，您有以下几种选择：

- **移除一个特定的属性：**您可以调用 *public void removeAttribute(String name)* 方法来删除与特定的键相关联的值。
- **删除整个 session 会话：**您可以调用 *public void invalidate()* 方法来丢弃整个 session 会话。
- **设置 session 会话过期时间：**您可以调用 *public void setMaxInactiveInterval(int interval)* 方法来单独设置 session 会话超时。
- **注销用户：**如果使用的是支持 servlet 2.4 的服务器，您可以调用 **logout** 来注销 Web 服务器的客户端，并把属于所有用户的所有 session 会话设置为无效。
- **web.xml 配置：**如果您使用的是 Tomcat，除了上述方法，您还可以在 web.xml 文件中配置 session 会话超时，如下所示：

```xml
  <session-config>
    <session-timeout>15</session-timeout>
  </session-config>
```

上面实例中的超时时间是以分钟为单位，将覆盖 Tomcat 中默认的 30 分钟超时时间。

在一个 Servlet 中的 getMaxInactiveInterval() 方法会返回 session 会话的超时时间，以秒为单位。所以，如果在 web.xml 中配置 session 会话超时时间为 15 分钟，那么 getMaxInactiveInterval() 会返回 900。



## 8. ServletContext

### 8.1 概念

抽象表示Servlet的上下文环境，即当前Web应用，一个JVM中的每个Web应用都只有一个ServletContext对象与之对应

启动一个Web应用时会创建一个ServletContext对象，关闭时也会销毁此对象

### 8.2 方法

| setAttribute与getAttribute方法 | ServletContext对象的生命周期等同于Web服务器正常工作周期，需要长期保存的属性可保存在ServletContext对象中 |
| ------------------------------ | ------------------------------------------------------------ |
| **getRequestDispatcher**       | **路径参数必须以“/”作为开头，表示应用程序环境的根目录 （对比request对象的该方法**） |
| **getResourcePaths**           | **获取Web应用中的某个路径下有哪些文件，路径参数必须以“/”开始** |
| **getResourceAsStream**        | **读取Web应用中的某个文件，文件路径参数必须以“/”开始**       |



## 9. 过滤器

### 9.1 概念

Servlet 过滤器可以动态地拦截请求和响应，以变换或使用包含在请求或响应中的信息。

可以将一个或多个 Servlet 过滤器附加到一个 Servlet 或一组 Servlet。Servlet 过滤器也可以附加到 JavaServer Pages (JSP) 文件和 HTML 页面。调用 Servlet 前调用所有附加的 Servlet 过滤器。

Servlet 过滤器是可用于 Servlet 编程的 Java 类，可以实现以下目的：

- 在客户端的请求访问后端资源之前，拦截这些请求。
- 在服务器的响应发送回客户端之前，处理这些响应。

根据规范建议的各种类型的过滤器：

- 身份验证过滤器（Authentication Filters）。
- 数据压缩过滤器（Data compression Filters）。
- 加密过滤器（Encryption Filters）。
- 触发资源访问事件过滤器。
- 图像转换过滤器（Image Conversion Filters）。
- 日志记录和审核过滤器（Logging and Auditing Filters）。
- MIME-TYPE 链过滤器（MIME-TYPE Chain Filters）。
- 标记化过滤器（Tokenizing Filters）。
- XSL/T 过滤器（XSL/T Filters），转换 XML 内容。

过滤器通过 Web 部署描述符（web.xml）中的 XML 标签来声明，然后映射到您的应用程序的部署描述符中的 Servlet 名称或 URL 模式。

当 Web 容器启动 Web 应用程序时，它会为您在部署描述符中声明的每一个过滤器创建一个实例。

Filter的执行顺序与在web.xml配置文件中的配置顺序一致，一般把Filter配置在所有的Servlet之前。



### 9.2 使用

**编写Filter** 
编写java类实现Filter接口，并实现其doFilter方法。

**设置Filter**
使用注解：@WebFilter
在 web.xml 文件中使用<filter>和<filter-mapping>元素对编写的filter类进行注册，并设置它所能拦截的资源。



### 9.3 Servlet 过滤器方法

过滤器是一个实现了 javax.servlet.Filter 接口的 Java 类。javax.servlet.Filter 接口定义了三个方法：

| 序号 | 方法 & 描述                                                  |
| :--- | :----------------------------------------------------------- |
| 1    | **public void doFilter (ServletRequest, ServletResponse, FilterChain)** 该方法完成实际的过滤操作，当客户端请求方法与过滤器设置匹配的URL时，Servlet容器将先调用过滤器的doFilter方法。FilterChain用户访问后续过滤器。 |
| 2    | **public void init(FilterConfig filterConfig)** web 应用程序启动时，web 服务器将创建Filter 的实例对象，并调用其init方法，读取web.xml配置，完成对象的初始化功能，从而为后续的用户请求作好拦截的准备工作（filter对象只会创建一次，init方法也只会执行一次）。开发人员通过init方法的参数，可获得代表当前filter配置信息的FilterConfig对象。 |
| 3    | **public void destroy()** Servlet容器在销毁过滤器实例前调用该方法，在该方法中释放Servlet过滤器占用的资源。 |



## 10. JSP



### 10.1 JSP生命周期

理解JSP底层功能的关键就是去理解它们所遵守的生命周期。

JSP生命周期就是从创建到销毁的整个过程，类似于servlet生命周期，区别在于JSP生命周期还包括将JSP文件编译成servlet。

以下是JSP生命周期中所走过的几个阶段：

- **编译阶段：**

  servlet容器编译servlet源文件，生成servlet类

- 初始化阶段：

  加载与JSP对应的servlet类，创建其实例，并调用它的初始化方法

- 执行阶段：

  调用与JSP对应的servlet实例的服务方法

- 销毁阶段：

  调用与JSP对应的servlet实例的销毁方法，然后销毁servlet实例

很明显，JSP生命周期的四个主要阶段和servlet生命周期非常相似，下面给出图示：

![img](./img/7.jpg)

------

#### 10.1.1 JSP编译

当浏览器请求JSP页面时，JSP引擎会首先去检查是否需要编译这个文件。如果这个文件没有被编译过，或者在上次编译后被更改过，则编译这个JSP文件。

编译的过程包括三个步骤：

- 解析JSP文件。
- 将JSP文件转为servlet。
- 编译servlet。

------

#### 10.1.2 JSP初始化

容器载入JSP文件后，它会在为请求提供任何服务前调用jspInit()方法。如果您需要执行自定义的JSP初始化任务，复写jspInit()方法就行了，就像下面这样：

```java
public void jspInit(){
  // 初始化代码
}
```

一般来讲程序只初始化一次，servlet也是如此。通常情况下您可以在jspInit()方法中初始化数据库连接、打开文件和创建查询表。

------

#### 10.1.3 JSP执行

这一阶段描述了JSP生命周期中一切与请求相关的交互行为，直到被销毁。

当JSP网页完成初始化后，JSP引擎将会调用_jspService()方法。

_jspService()方法需要一个HttpServletRequest对象和一个HttpServletResponse对象作为它的参数，就像下面这样：

```java
void _jspService(HttpServletRequest request,
                 HttpServletResponse response)
{
   // 服务端处理代码
}
```

_jspService()方法在每个request中被调用一次并且负责产生与之相对应的response，并且它还负责产生所有7个HTTP方法的回应，比如GET、POST、DELETE等等。

------

#### 10.1.4 JSP清理

JSP生命周期的销毁阶段描述了当一个JSP网页从容器中被移除时所发生的一切。

jspDestroy()方法在JSP中等价于servlet中的销毁方法。当您需要执行任何清理工作时复写jspDestroy()方法，比如释放数据库连接或者关闭文件夹等等。

jspDestroy()方法的格式如下：

```java
public void jspDestroy()
{
   // 清理代码
}
```



### 10.2 JSP指令



#### 10.2.1 指令

JSP指令用来设置整个JSP页面相关的属性，如网页的编码方式和脚本语言。

语法格式如下：

```jsp
<%@ directive attribute="value" %>
```

指令可以有很多个属性，它们以键值对的形式存在，并用逗号隔开。

JSP中的三种指令标签：

| **指令**           | **描述**                                                |
| :----------------- | :------------------------------------------------------ |
| <%@ page ... %>    | 定义网页依赖属性，比如脚本语言、error页面、缓存需求等等 |
| <%@ include ... %> | 包含其他文件                                            |
| <%@ taglib ... %>  | 引入标签库的定义                                        |

------



#### 10.2.2 Page指令

Page指令为容器提供当前页面的使用说明。一个JSP页面可以包含多个page指令。

Page指令的语法格式：

```jsp
<%@ page attribute="value" %>
```

等价的XML格式：

```jsp
<jsp:directive.page attribute="value" />
```



**属性**

下表列出与Page指令相关的属性：说

| **属性**           | **描述**                                            |
| :----------------- | :-------------------------------------------------- |
| buffer             | 指定out对象使用缓冲区的大小                         |
| autoFlush          | 控制out对象的 缓存区                                |
| contentType        | 指定当前JSP页面的MIME类型和字符编码                 |
| errorPage          | 指定当JSP页面发生异常时需要转向的错误处理页面       |
| isErrorPage        | 指定当前页面是否可以作为另一个JSP页面的错误处理页面 |
| extends            | 指定servlet从哪一个类继承                           |
| import             | 导入要使用的Java类                                  |
| info               | 定义JSP页面的描述信息                               |
| isThreadSafe       | 指定对JSP页面的访问是否为线程安全                   |
| language           | 定义JSP页面所用的脚本语言，默认是Java               |
| session            | 指定JSP页面是否使用session                          |
| isELIgnored        | 指定是否执行EL表达式                                |
| isScriptingEnabled | 确定脚本元素能否被使用                              |



#### 10.2.3 Include指令

JSP可以通过include指令来包含其他文件。被包含的文件可以是JSP文件、HTML文件或文本文件。包含的文件就好像是该JSP文件的一部分，会被同时编译执行。

Include指令的语法格式如下：

```jsp
<%@ include file="relative url" %>
```

Include指令中的文件名实际上是一个相对的URL。如果您没有给文件关联一个路径，JSP编译器默认在当前路径下寻找。

等价的XML语法：

```jsp
<jsp:directive.include file="relative url" />
```



#### 10.2.4 Taglib指令

JSP API允许用户自定义标签，一个自定义标签库就是自定义标签的集合。

Taglib指令引入一个自定义标签集合的定义，包括库路径、自定义标签。

Taglib指令的语法：

```jsp
<%@ taglib uri="uri" prefix="prefixOfTag" %>
```

uri属性确定标签库的位置，prefix属性指定标签库的前缀。

等价的XML语法：

```jsp
<jsp:directive.taglib uri="uri" prefix="prefixOfTag" />
```



### 10.3 JSP 动作元素

与JSP指令元素不同的是，JSP动作元素在请求处理阶段起作用。JSP动作元素是用XML语法写成的。

利用JSP动作可以动态地插入文件、重用JavaBean组件、把用户重定向到另外的页面、为Java插件生成HTML代码。

动作元素只有一种语法，它符合XML标准：

```jsp
<jsp:action_name attribute="value" />
```

动作元素基本上都是预定义的函数，JSP规范定义了一系列的标准动作，它用JSP作为前缀，可用的标准动作元素如下：

| 语法            | 描述                                            |
| :-------------- | :---------------------------------------------- |
| jsp:include     | 在页面被请求的时候引入一个文件。                |
| jsp:useBean     | 寻找或者实例化一个JavaBean。                    |
| jsp:setProperty | 设置JavaBean的属性。                            |
| jsp:getProperty | 输出某个JavaBean的属性。                        |
| jsp:forward     | 把请求转到一个新的页面。                        |
| jsp:plugin      | 根据浏览器类型为Java插件生成OBJECT或EMBED标记。 |
| jsp:element     | 定义动态XML元素                                 |
| jsp:attribute   | 设置动态定义的XML元素属性。                     |
| jsp:body        | 设置动态定义的XML元素内容。                     |
| jsp:text        | 在JSP页面和文档中使用写入文本的模板             |

------

#### 10.3.1 常见的属性

所有的动作要素都有两个属性：id属性和scope属性。

- id属性：

  id属性是动作元素的唯一标识，可以在JSP页面中引用。动作元素创建的id值可以通过PageContext来调用。

  

- scope属性：

  该属性用于识别动作元素的生命周期。 id属性和scope属性有直接关系，scope属性定义了相关联id对象的寿命。 scope属性有四个可能的值： (a) page, (b)request, (c)session, 和 (d) application。

  

------

#### 10.3.2 <jsp:include>动作元素

<jsp:include>动作元素用来包含静态和动态的文件。该动作把指定文件插入正在生成的页面。语法格式如下：

```jsp
<jsp:include page="relative URL" flush="true" />
```

　前面已经介绍过include指令，它是在JSP文件被转换成Servlet的时候引入文件，而这里的jsp:include动作不同，插入文件的时间是在页面被请求的时候。

以下是include动作相关的属性列表。

| 属性  | 描述                                       |
| :---- | :----------------------------------------- |
| page  | 包含在页面中的相对URL地址。                |
| flush | 布尔属性，定义在包含资源前是否刷新缓存区。 |

#### 10.3.3 <jsp:useBean>动作元素

jsp:useBean动作用来装载一个将在JSP页面中使用的JavaBean。

这个功能非常有用，因为它使得我们既可以发挥Java组件重用的优势，同时也避免了损失JSP区别于Servlet的方便性。

jsp:useBean动作最简单的语法为：

```jsp
<jsp:useBean id="name" class="package.class" />
```

在类载入后，我们既可以通过 jsp:setProperty 和 jsp:getProperty 动作来修改和检索bean的属性。 

以下是useBean动作相关的属性列表。

| 属性     | 描述                                                        |
| :------- | :---------------------------------------------------------- |
| class    | 指定Bean的完整包名。                                        |
| type     | 指定将引用该对象变量的类型。                                |
| beanName | 通过 java.beans.Beans 的 instantiate() 方法指定Bean的名字。 |

在给出具体实例前，让我们先来看下 jsp:setProperty 和 jsp:getProperty 动作元素：

------

#### 10.3.4 <jsp:setProperty>动作元素

　jsp:setProperty用来设置已经实例化的Bean对象的属性，有两种用法。首先，你可以在jsp:useBean元素的外面（后面）使用jsp:setProperty，如下所示：

```jsp
<jsp:useBean id="myName" ... />
...
<jsp:setProperty name="myName" property="someProperty" .../>
```

　此时，不管jsp:useBean是找到了一个现有的Bean，还是新创建了一个Bean实例，jsp:setProperty都会执行。第二种用法是把jsp:setProperty放入jsp:useBean元素的内部，如下所示：

```jsp
<jsp:useBean id="myName" ... >
...
   <jsp:setProperty name="myName" property="someProperty" .../>
</jsp:useBean>
```

此时，jsp:setProperty只有在新建Bean实例时才会执行，如果是使用现有实例则不执行jsp:setProperty。

| 属性     | 描述                                                         |
| :------- | :----------------------------------------------------------- |
| name     | name属性是必需的。它表示要设置属性的是哪个Bean。             |
| property | property属性是必需的。它表示要设置哪个属性。有一个特殊用法：如果property的值是"*"，表示所有名字和Bean属性名字匹配的请求参数都将被传递给相应的属性set方法。 |
| value    | value 属性是可选的。该属性用来指定Bean属性的值。字符串数据会在目标类中通过标准的valueOf方法自动转换成数字、boolean、Boolean、 byte、Byte、char、Character。例如，boolean和Boolean类型的属性值（比如"true"）通过 Boolean.valueOf转换，int和Integer类型的属性值（比如"42"）通过Integer.valueOf转换。 　　value和param不能同时使用，但可以使用其中任意一个。 |
| param    | param 是可选的。它指定用哪个请求参数作为Bean属性的值。如果当前请求没有参数，则什么事情也不做，系统不会把null传递给Bean属性的set方法。因此，你可以让Bean自己提供默认属性值，只有当请求参数明确指定了新值时才修改默认属性值。 |

------

#### 10.3.5 <jsp:getProperty>动作元素

　jsp:getProperty动作提取指定Bean属性的值，转换成字符串，然后输出。语法格式如下：

```jsp
<jsp:useBean id="myName" ... />
...
<jsp:getProperty name="myName" property="someProperty" .../>
```

下表是与getProperty相关联的属性：

| 属性     | 描述                                   |
| :------- | :------------------------------------- |
| name     | 要检索的Bean属性名称。Bean必须已定义。 |
| property | 表示要提取Bean属性的值                 |

------

#### 10.3.6 <jsp:forward> 动作元素

　jsp:forward动作把请求转到另外的页面。jsp:forward标记只有一个属性page。语法格式如下所示：

```jsp
<jsp:forward page="Relative URL" />
```

以下是forward相关联的属性：

| 属性 | 描述                                                         |
| :--- | :----------------------------------------------------------- |
| page | page属性包含的是一个相对URL。page的值既可以直接给出，也可以在请求的时候动态计算，可以是一个JSP页面或者一个 Java Servlet. |

#### 10.3.7 <jsp:plugin>动作元素

jsp:plugin动作用来根据浏览器的类型，插入通过Java插件 运行Java Applet所必需的OBJECT或EMBED元素。

如果需要的插件不存在，它会下载插件，然后执行Java组件。 Java组件可以是一个applet或一个JavaBean。

plugin动作有多个对应HTML元素的属性用于格式化Java 组件。param元素可用于向Applet 或 Bean 传递参数。

以下是使用plugin 动作元素的典型实例:

```jsp
<jsp:plugin type="applet" codebase="dirname" code="MyApplet.class"                            width="60" height="80">
   <jsp:param name="fontcolor" value="red" />
   <jsp:param name="background" value="black" />
 
   <jsp:fallback>
      Unable to initialize Java Plugin
   </jsp:fallback>
 
</jsp:plugin>
```

如果你有兴趣可以尝试使用applet来测试jsp:plugin动作元素，<fallback>元素是一个新元素，在组件出现故障的错误是发送给用户错误信息。

------

#### 10.3.8 <jsp:element> 、 <jsp:attribute>、 <jsp:body>动作元素

<jsp:element> 、 <jsp:attribute>、 <jsp:body>动作元素动态定义XML元素。动态是非常重要的，这就意味着XML元素在编译时是动态生成的而非静态。

以下实例动态定义了XML元素：

```jsp
<%@page language="java" contentType="text/html"%>
<html xmlns="http://www.w3c.org/1999/xhtml"       xmlns:jsp="http://java.sun.com/JSP/Page">

<head><title>Generate XML Element</title></head>
<body>
<jsp:element name="xmlElement">
<jsp:attribute name="xmlElementAttr">
   Value for the attribute
</jsp:attribute>
<jsp:body>
   Body for XML element
</jsp:body>
</jsp:element>
</body>
</html>
```

执行时生成HTML代码如下：

```jsp
<html xmlns="http://www.w3c.org/1999/xhtml"       xmlns:jsp="http://java.sun.com/JSP/Page">
 
<head><title>Generate XML Element</title></head>
<body>
<xmlElement xmlElementAttr="Value for the attribute">
   Body for XML element
</xmlElement>
</body>
</html>
```

------

#### 10.3.9 <jsp:text>动作元素

<jsp:text>动作元素允许在JSP页面和文档中使用写入文本的模板，语法格式如下：

```jsp
<jsp:text>Template data</jsp:text>
```

以上文本模板不能包含其他元素，只能只能包含文本和EL表达式（注：EL表达式将在后续章节中介绍）。请注 意，在XML文件中，您不能使用表达式如 ${whatever > 0}，因为>符号是非法的。 你可以使用 ${whatever gt 0}表达式或者嵌入在一个CDATA部分的值。

```jsp
<jsp:text><![CDATA[<br>]]></jsp:text>
```

如果你需要在 XHTML 中声明 DOCTYPE,必须使用到<jsp:text>动作元素，实例如下：

```jsp
<jsp:text><![CDATA[<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "DTD/xhtml1-strict.dtd">]]>
</jsp:text>
<head><title>jsp:text action</title></head>
<body>

<books><book><jsp:text>  
    Welcome to JSP Programming
</jsp:text></book></books>

</body>
</html>
```

你可以对以上实例尝试使用<jsp:text>及不使用该动作元素执行结果的区别。



### 10.4 JSP 隐式对象

JSP隐式对象是JSP容器为每个页面提供的Java对象，开发者可以直接使用它们而不用显式声明。JSP隐式对象也被称为预定义变量。

JSP所支持的九大隐式对象：

| **对象**    | **描述**                                                     |
| :---------- | :----------------------------------------------------------- |
| request     | **HttpServletRequest**类的实例                               |
| response    | **HttpServletResponse**类的实例                              |
| out         | **PrintWriter**类的实例，用于把结果输出至网页上              |
| session     | **HttpSession**类的实例                                      |
| application | **ServletContext**类的实例，与应用上下文有关                 |
| config      | **ServletConfig**类的实例                                    |
| pageContext | **PageContext**类的实例，提供对JSP页面所有对象以及命名空间的访问 |
| page        | 类似于Java类中的this关键字                                   |
| Exception   | **Exception**类的对象，代表发生错误的JSP页面中对应的异常对象 |

------

#### 10.4.1 request对象

request对象是javax.servlet.http.HttpServletRequest 类的实例。每当客户端请求一个JSP页面时，JSP引擎就会制造一个新的request对象来代表这个请求。

request对象提供了一系列方法来获取HTTP头信息，cookies，HTTP方法等等。

------

#### 10.4.2 response对象

response对象是javax.servlet.http.HttpServletResponse类的实例。当服务器创建request对象时会同时创建用于响应这个客户端的response对象。

response对象也定义了处理HTTP头模块的接口。通过这个对象，开发者们可以添加新的cookies，时间戳，HTTP状态码等等。

------

#### 10.4.3 out对象

out对象是 javax.servlet.jsp.JspWriter 类的实例，用来在response对象中写入内容。

最初的JspWriter类对象根据页面是否有缓存来进行不同的实例化操作。可以在page指令中使用buffered='false'属性来轻松关闭缓存。

JspWriter类包含了大部分java.io.PrintWriter类中的方法。不过，JspWriter新增了一些专为处理缓存而设计的方法。还有就是，JspWriter类会抛出IOExceptions异常，而PrintWriter不会。

下表列出了我们将会用来输出boolean，char，int，double，Srtring，object等类型数据的重要方法：

| **方法**                     | **描述**                 |
| :--------------------------- | :----------------------- |
| **out.print(dataType dt)**   | 输出Type类型的值         |
| **out.println(dataType dt)** | 输出Type类型的值然后换行 |
| **out.flush()**              | 刷新输出流               |

------

#### 10.4.4 session对象

session对象是 javax.servlet.http.HttpSession 类的实例。和Java Servlets中的session对象有一样的行为。

session对象用来跟踪在各个客户端请求间的会话。

------

#### 10.4.5 application对象

application对象直接包装了servlet的ServletContext类的对象，是javax.servlet.ServletContext 类的实例。

这个对象在JSP页面的整个生命周期中都代表着这个JSP页面。这个对象在JSP页面初始化时被创建，随着jspDestroy()方法的调用而被移除。

通过向application中添加属性，则所有组成您web应用的JSP文件都能访问到这些属性。

------

#### 10.4.6 config对象

config对象是 javax.servlet.ServletConfig 类的实例，直接包装了servlet的ServletConfig类的对象。

这个对象允许开发者访问Servlet或者JSP引擎的初始化参数，比如文件路径等。

以下是config对象的使用方法，不是很重要，所以不常用：

```java
config.getServletName();
```

它返回包含在<servlet-name>元素中的servlet名字，注意，<servlet-name>元素在 WEB-INF\web.xml 文件中定义。

------

#### 10.4.7 pageContext 对象

pageContext对象是javax.servlet.jsp.PageContext 类的实例，用来代表整个JSP页面。

这个对象主要用来访问页面信息，同时过滤掉大部分实现细节。

这个对象存储了request对象和response对象的引用。application对象，config对象，session对象，out对象可以通过访问这个对象的属性来导出。

pageContext对象也包含了传给JSP页面的指令信息，包括缓存信息，ErrorPage URL,页面scope等。

PageContext类定义了一些字段，包括PAGE_SCOPE，REQUEST_SCOPE，SESSION_SCOPE， APPLICATION_SCOPE。它也提供了40余种方法，有一半继承自javax.servlet.jsp.JspContext 类。

其中一个重要的方法就是removeArribute()，它可接受一个或两个参数。比如，pageContext.removeArribute("attrName")移除四个scope中相关属性，但是下面这种方法只移除特定scope中的相关属性：

```java
pageContext.removeAttribute("attrName", PAGE_SCOPE);
```

------

#### 10.4.8 page 对象

这个对象就是页面实例的引用。它可以被看做是整个JSP页面的代表。

page 对象就是this对象的同义词。

------

#### 10.4.9 exception 对象

exception 对象包装了从先前页面中抛出的异常信息。它通常被用来产生对出错条件的适当响应。



### 10.5 EL语法

#### 10.5.1 语法格式

**${ expression }**

要在页面中输出，则可用\${}

{“Hello World”}

#### 10.5.2 EL隐含对象

![image-20200407211445131](./img/8.png)



### 10.6 JSTL

#### 10.6.1 引入

```jsp
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
```

#### 10.6.2 常用标签

<c:out>	用于在JSP中显示数据，就像<%= ... >
<c:set>	用于保存数据
<c:remove>	用于删除数据
<c:catch>	用来处理产生错误的异常状况，并且将错误信息储存起来
<c:if>	与我们在一般程序中用的if一样
<c:choose>	本身只当做<c:when>和<c:otherwise>的父标签
<c:when>	<c:choose>的子标签，用来判断条件是否成立
<c:otherwise>	<c:choose>的子标签，接在<c:when>标签后，当<c:when>标签判断为false时被执行
<c:import>	检索一个绝对或相对 URL，然后将其内容暴露给页面
<c:forEach>	基础迭代标签，接受多种集合类型
<c:forTokens>	根据指定的分隔符来分隔内容并迭代输出
<c:param>	用来给包含或重定向的页面传递参数
<c:redirect>	重定向至一个新的URL.
<c:url>	使用可选的查询参数来创造一个URL



## 11. JDBC

### 11.1 注册Driver类实现对象

加载实现了java.sql.Driver接口的类的实例对象

Class.forName(“驱动类的完整类名”);

用DriverManager类的registerDriver方法注册



加载驱动程序，不同的数据库系统有不同的加载代码：
MySQL数据库：
Class.forName(“com.mysql.jdbc.Driver");
Class.forName("org.gjt.mm.mysql.Driver");

MS SQL Server
Class.forName("com.microsoft.jdbc.sqlserver.SQLServerDriver")

Oracle
Class.forName(“oracle.jdbc.driver.OracleDriver”);

DB2
Class.forName(“com.ibm.db2.jdbc.app.DB2Driver”);

Access(使用ODBC)
Class.forName("sun.jdbc.odbc.JdbcOdbcDriver") ;

Derby
Class.forName("org.apache.derby.jdbc.ClientDriver")

### 11.2 获取Connection连接对象

用DriverManager类的getConection方法获取
方法需要三个参数：url、数据库访问用户名与密码
url具有相对固定的格式，获取后将返回Connection对象

### 11.3 关闭Connection连接对象

Connection对象close方法，注意处理异常



### 11.4 使用步骤

```java
public class HowToUseJDBC {
	public static void main(String[] args) throws SQLExceotion, ClassNotFoundException {
		// 步骤一：实现并注册一个Driver对象
		// DriverManager.registerDriver(new JBDC())
		Class.forName("org.sqlite.JDBC");

		// 步骤二：创建一个连接到数据库的Connection对象
		String url = "jdbc:sqlite:d:\\web.db";
		Connection connection = DriverManager.getConnection(url);

		// 步骤三：创建一个Statement对象
		Statement stmt = connection.createStatement();

		// 步骤四：执行需要的SQL语句
		String sql = "SELECT * FROM t_user";
		ResultSet rs = stmt.executeQuery(sql);

		// 步骤五： 处理结果集
		while (rs.next()) {
			System.out.println(rs.getString);
		}

		// 关闭
		rs.close();
		stmt.close();
		connection.close();
	}
} 
```

