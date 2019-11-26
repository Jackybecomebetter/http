[TOC]



### 一、什么是http协议

（1）超文本传输协议（hypertext transfer protocol）是一种用于分布式、协作式和超媒体信息系统的应用层协议。http是万维网（word wide web）的基础。

（2）http构建与tcp/ip协议来传输数据（html文件、图片、其他文件、查询结果等），其中服务器默认端口是80。

（3）http是无连接无状态的

（4）http协议使用客户端-服务器的架构。浏览器作为http客户端通过URL向http服务端发送请求。web服务器收到请求之后，向客户端发送相应信息。

![](./picture/1.jpg)

### 二、http协议中核心的几个概念

**1、http特点**

（1）简单快速：客户端向服务器发送请求的时候，只需要传送请求方法和路径。请求方法有GET、HEAD、POST等，因为协议简单，是的http服务器程序规模小，因而通信速度很快。

（2）灵活：可以传输任意类型的数据对象，由content-type加以标记

（3）无连接：每次连接只处理一个请求，处理完成之后断开。

（4）无状态：对于事物处理没有记忆能力。处理一个事务的时候，它并不会记录事物的信息，所以如果后续需要用到之前的信息的时候，需要重传。当然现在很多浏览器加了cookie缓存功能，保存一些非常常用的数据信息，减少需要重传的次数。

（5）支持b/s和c/s模式。

**2、URI（uniform resource identifier）统一资源标识符**

​	URI统一资源标识符是一种抽象的概念。web上面的每种资源例如HTML文档、图像、视频片段、程序都可以用一个URI来进行定位，URI可以由三个部分组成：

（1）访问资源的命名机制

（2）存放资源的主机名

（3）资源本身的名称，由路径表示

**3、URL（uniform rescource locator）统一资源定位符**

​	URL是一种具体的URI，它不仅标识了一个web上的资源，还指名了如何locate该资源。采用URI可以使用一种统一的格式来描述各种信息资源，包括文件、服务器地址和目录。

一般 由三部分组成：

（1）协议

（2）存有该资源的主机ip地址，有时需要端口号

（3）资源在主机的具体路径

**4、URL具体例子**

https://www.google.com/search?q=http%E5%8D%8F%E8%AE%AE&source=lmns&bih=774&biw=1536&sfr=vfe&hl=zh-CN&ved=2ahUKEwiql8SHzYXmAhVO4JQKHXSiAnIQ_AUoAHoECAEQAA

​	http://www.aspxfans.com:8080/news/index.asp?boardID=5&ID=24618&page=1#name

（1）协议部分：“http：”，这里表示网页使用的是http协议。在因特网中可以使用多种协议，例如http或者ftp等等，http后面用//分开

（2）域名：域名这里对应ip地址

（3）端口部分：如果省略端口部分，则用默认端口。

（4）虚拟目录部分：从第一个/到最后一个/，这里的虚拟目录就是“/news/”。虚拟目录不是必须的

（5）文件名：从域名之后的第一个/开始到？结束，这里是"/news/index.asp?"，如果没有没有？，则是从/开始到#结束。文件名也不是必须的，如果省略，则用默认文件名

（6）锚部分：从#开始到最后，这里的锚是name

（7）参数部分：从？开始到#结束为参数部分，又称搜索部分、查询部分。本例中参数部分是“boardID=5&ID=24618&page=1”，可以有多个参数，参数与参数之间用&隔开。

**5、URN，uniform resource name，统一资源命名，通过名字来标识资源**，例如：mailto:java-net@java.sun.com

​	URI是一种抽象的、高层次概念定义统一资源标识。而URL和URN则是具体的资源标识的方式。URL和URN都是一种URI。

**6、HTML，hypertext makeup language,超文本标记语言**

（1）html是一种用于创建网页的标准标记语言。

（2）html常与css、js用于设计网页、网页应用程序以及移动应用程序的用户界面，网页浏览器可以读取html文件，并把其渲染为可视化网页。

（3）html是一种标记语言而不是编程语言。

![](./picture/2.jpg)

### 三、http报文

**1、请求报文**

​	http协议以ASCII码进行传输，是建立在TCP/IP协议的应用层协议。该协议把http请求分为三个部分：状态行、请求头、消息主题。

![](./picture/3.jpg)

>```http
>GET /562f25980001b1b106000338.jpg HTTP/1.1
>Host    img.mukewang.com
>User-Agent  Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/51.0.2704.106 Safari/537.36
>Accept  image/webp,image/*,*/*;q=0.8
>Referer http://www.imooc.com/
>Accept-Encoding gzip, deflate, sdch
>Accept-Language zh-CN,zh;q=0.8
>
>```

**第一部分：请求行，用来说明请求类型,要访问的资源以及所使用的HTTP版本.**

GET说明请求类型为GET,[/562f25980001b1b106000338.jpg]为要访问的资源，该行的最后一部分说明使用的是HTTP1.1版本。

**第二部分：请求头部，紧接着请求行（即第一行）之后的部分，用来说明服务器要使用的附加信息**

从第二行起为请求头部，HOST将指出请求的目的地.User-Agent,服务器端和客户端脚本都能访问它,它是浏览器类型检测逻辑的重要基础.该信息由你的浏览器来定义,并且在每个请求中自动发送等等

**第三部分：空行，请求头部后面的空行是必须的**

即使第四部分的请求数据为空，也必须有空行。

**第四部分：请求数据也叫主体，可以添加任意的其他数据。**

这个例子的请求数据为空。



​	http定义了与服务器交互的不同方法，最基本的请求方法有四种，分别是GET、POST、PUT、DELETE。我们可以这样理解，URL定义了网络上的某个资源，而请求方法GET、POST、PUT、DELETE则对应了资源的查、增、改、查。

**（1）GET用于数据获取，并且应该是安全和幂等的**

​	所谓安全的意味着该操作用于获取信息而非修改信息。所谓幂等意味着对于同一URL的多个请求，应该返回相同的相应。

Get报文示例

>```http
> GET /books/?sex=man&name=Professional HTTP/1.1
> Host: www.example.com
> User-Agent: Mozilla/5.0 (Windows; U; Windows NT 5.1; en-US; rv:1.7.6)
> Gecko/20050225 Firefox/1.0.1
> Connection: Keep-Alive
> 
>```

**（2）POST：表示可能修改服务器上资源的请求**

>```http
> POST / HTTP/1.1
> Host: www.example.com
> User-Agent: Mozilla/5.0 (Windows; U; Windows NT 5.1; en-US; rv:1.7.6)
> Gecko/20050225 Firefox/1.0.1
> Content-Type: application/x-www-form-urlencoded
> Content-Length: 40
> Connection: Keep-Alive
>
> sex=man&name=Professional 
>```
>
>

**注意：**

- GET 可提交的数据量受到URL长度的限制，HTTP 协议规范没有对 URL 长度进行限制。这个限制是特定的浏览器及服务器对它的限制
- 理论上讲，POST 是没有大小限制的，HTTP 协议规范也没有进行大小限制，出于安全考虑，服务器软件在实现时会做一定限制
- 参考上面的报文示例，可以发现 GET 和 POST 数据内容是一模一样的，只是位置不同，一个在 URL 里，一个在 HTTP 包的包体里



**（3）POST提交数据的方式**

​	HTTP 协议中规定 **POST 提交的数据必须在 body 部分中**，但是协议中没有规定数据使用哪种编码方式或者数据格式。**实际上，开发者完全可以自己决定消息主体的格式，只要最后发送的 HTTP 请求满足上面的格式就可以。**

但是，数据发送出去，还要服务端解析成功才有意义。一般服务端语言如 PHP、Python 等，以及它们的 framework，都内置了自动解析常见数据格式的功能。服务端通常是根据请求头（headers）中的 Content-Type 字段来获知请求中的消息主体是用何种方式编码，再对主体进行解析。所以说到 POST 提交数据方案，包含了 Content-Type 和消息主体编码方式两部分。下面就正式开始介绍它们：

- `application/x-www-form-urlencoded`

这是最常见的 POST 数据提交方式。浏览器的原生 `<form>` 表单，如果不设置 enctype 属性，那么最终就会以 `application/x-www-form-urlencoded` 方式提交数据。上个小节当中的例子便是使用了这种提交方式。可以看到 body 当中的内容和 GET 请求是完全相同的。

- `multipart/form-data`

这又是一个常见的 POST 数据提交的方式。我们使用表单上传文件时，必须让 `<form>` 表单的 enctype 等于 `multipart/form-data`。直接来看一个请求示例：

>```http
>POST http://www.example.com HTTP/1.1
>Content-Type:multipart/form-data; boundary=----WebKitFormBoundaryrGKCBY7qhFd3TrwA
>
>------WebKitFormBoundaryrGKCBY7qhFd3TrwA
>Content-Disposition: form-data; name="text"
>
>title
>------WebKitFormBoundaryrGKCBY7qhFd3TrwA
>Content-Disposition: form-data; name="file"; filename="chrome.png"
>Content-Type: image/png
>
>PNG ... content of chrome.png ...
>------WebKitFormBoundaryrGKCBY7qhFd3TrwA--
>```

​	这个例子稍微复杂点。首先生成了一个 boundary 用于分割不同的字段，为了避免与正文内容重复，boundary 很长很复杂。然后 `Content-Type` 里指明了数据是以 `multipart/form-data` 来编码，本次请求的 boundary 是什么内容。消息主体里按照字段个数又分为多个结构类似的部分，每部分都是以 --boundary 开始，紧接着是内容描述信息，然后是回车，最后是字段具体内容（文本或二进制）。如果传输的是文件，还要包含文件名和文件类型信息。消息主体最后以 --boundary-- 标示结束。关于 `multipart/form-data` 的详细定义，请前往 [RFC1867](http://www.ietf.org/rfc/rfc1867.txt) 查看（或者相对友好一点的 [MDN 文档](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Disposition)）。

这种方式一般用来上传文件，各大服务端语言对它也有着良好的支持。

上面提到的这两种 POST 数据的方式，都是浏览器原生支持的，而且现阶段标准中原生 `<form>` 表单也只支持这两种方式（通过 `<form>` 元素的 enctype 属性指定，默认为 `application/x-www-form-urlencoded`。其实 enctype 还支持 text/plain，不过用得非常少）。

随着越来越多的 Web 站点，尤其是 WebApp，全部使用 Ajax 进行数据交互之后，我们完全可以定义新的数据提交方式，例如 `application/json`，`text/xml`，乃至 `application/x-protobuf` 这种二进制格式，只要服务器可以根据 `Content-Type` 和 `Content-Encoding` 正确地解析出请求，都是没有问题的。



**2、响应报文**

**（1）响应报文格式**

​	服务器接收到客户端发送过来的请求之后会返回一个HTTP的响应消息。响应报文主要由四个部分构成：状态行、消息报头、空行和相应正文。

![](./picture/4.jpg)

例子：

>```http
>HTTP/1.1 200 OK
>Date: Fri, 22 May 2009 06:07:21 GMT
>Content-Type: text/html; charset=UTF-8
>
><html>
>      <head></head>
>      <body>
>            <!--body goes here-->
>      </body>
></html>
>```

**第一部分：状态行，由HTTP协议版本号， 状态码， 状态消息 三部分组成。**

第一行为状态行，（HTTP/1.1）表明HTTP版本为1.1版本，状态码为200，状态消息为（ok）

**第二部分：消息报头，用来说明客户端要使用的一些附加信息**

第二行和第三行为消息报头，
 Date:生成响应的日期和时间；Content-Type:指定了MIME类型的HTML(text/html),编码类型是UTF-8

**第三部分：空行，消息报头后面的空行是必须的**

**第四部分：响应正文，服务器返回给客户端的文本信息。**

空行后面的html部分为响应正文。



**（2）常见状态码**

- `200 OK` 客户端请求成功
- `301 Moved Permanently` 请求永久重定向
- `302 Moved Temporarily` 请求临时重定向
- `304 Not Modified` 文件未修改，可以直接使用缓存的文件。
- `400 Bad Request` 由于客户端请求有语法错误，不能被服务器所理解。
- `401 Unauthorized` 请求未经授权。这个状态代码必须和WWW-Authenticate报头域一起使用
- `403 Forbidden` 服务器收到请求，但是拒绝提供服务。服务器通常会在响应正文中给出不提供服务的原因
- `404 Not Found` 请求的资源不存在，例如，输入了错误的URL
- `500 Internal Server Error` 服务器发生不可预期的错误，导致无法完成客户端的请求。
- `503 Service Unavailable` 服务器当前不能够处理客户端的请求，在一段时间之后，服务器可能会恢复正常。



**（3）transfer encoding**

​	**Transfer-Encoding 是一个用来标示 HTTP 报文传输格式的头部值**。尽管这个取值理论上可以有很多，但是当前的 HTTP 规范里实际上只定义了一种传输取值——chunked。

​	如果一个HTTP消息（请求消息或应答消息）的Transfer-Encoding消息头的值为chunked，那么，**消息体由数量未定的块组成，并以最后一个大小为0的块为结束。**

​	**每一个非空的块都以该块包含数据的字节数（字节数以十六进制表示）开始，跟随一个CRLF （回车及换行），然后是数据本身，最后块CRLF结束。在一些实现中，块大小和CRLF之间填充有白空格（0x20）。**

​	**最后一块是单行，由块大小（0），一些可选的填充白空格，以及CRLF。最后一块不再包含任何数据，但是可以发送可选的尾部，包括消息头字段。消息最后以CRLF结尾。**

示例

>```http
>HTTP/1.1 200 OK
>Content-Type: text/plain
>Transfer-Encoding: chunked
>
>25
>This is the data in the first chunk
>
>1A
>and this is the second one
>0
>```

**注意：**

- chunked 和 multipart 两个名词在意义上有类似的地方，不过在 HTTP 协议当中这两个概念则不是一个类别的。**multipart 是一种 Content-Type，标示 HTTP 报文内容的类型**，而 **chunked 是一种传输格式，标示报头将以何种方式进行传输**。
- **chunked 传输不能事先知道内容的长度，只能靠最后的空 chunk 块来判断**，因此对于下载请求来说，是没有办法实现进度的。在浏览器和下载工具中，偶尔我们也会看到有些文件是看不到下载进度的，即采用 chunked 方式进行下载。
- **chunked 的优势在于，服务器端可以边生成内容边发送，无需事先生成全部的内容。**HTTP/2 不支持 Transfer-Encoding: chunked，因为 HTTP/2 有自己的 streaming 传输方式（Source：[MDN - Transfer-Encoding](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Transfer-Encoding)）。

**4、条件GET**

​	条件GET用于减少不必要的带宽浪费。由客户端向服务器发出一个包询问，询问服务器自从上次访问网站的时间之后是否更改了页面，如果返回没有更改的话，那么客户端只使用本地缓存即可。如果发生了更改，就发送这个更新了的网页给用户。

示例：

（1）客户端发送请求

>```http
> GET / HTTP/1.1  
> Host: www.sina.com.cn:80  
> If-Modified-Since:Thu, 4 Feb 2010 20:39:13 GMT  
> Connection: Close  
>```

第一次发送请求的时候，服务器放回数据给客户端。后面的请求，服务器根据If-Modified-Since后面的时间判断该网址页面是否发生更改，如果没有更新返回一个`304 Not Modified`响应。告诉浏览器没有更新，可以使用已缓存的上次获取的文件。

>```http
> HTTP/1.0 304 Not Modified  
> Date: Thu, 04 Feb 2010 12:38:41 GMT  
> Content-Type: text/html  
> Expires: Thu, 04 Feb 2010 12:39:41 GMT  
> Last-Modified: Thu, 04 Feb 2010 12:29:04 GMT  
> Age: 28  
> X-Cache: HIT from sy32-21.sina.com.cn  
> Connection: close 
>```

如果服务器更新，就返回正常响应。

### 四、持久连接

​	我们知道 HTTP 协议采用“请求-应答”模式，当使用**普通模式**，即非 Keep-Alive 模式时，**每个请求/应答客户和服务器都要新建一个连接**，完成之后立即断开连接（HTTP 协议为无连接的协议）；**当使用 Keep-Alive 模式（又称持久连接、连接重用）时，Keep-Alive 功能使客户端到服务器端的连接持续有效，**当出现对服务器的后继请求时，Keep-Alive 功能避免了建立或者重新建立连接。

​	在 HTTP 1.0 版本中，并没有官方的标准来规定 Keep-Alive 如何工作，因此实际上它是被附加到 HTTP 1.0协议上，如果客户端浏览器支持 Keep-Alive ，那么就在HTTP请求头中添加一个字段 Connection: Keep-Alive，当服务器收到附带有 Connection: Keep-Alive 的请求时，它也会在响应头中添加一个同样的字段来使用 Keep-Alive 。这样一来，客户端和服务器之间的HTTP连接就会被保持，不会断开（超过 Keep-Alive 规定的时间，意外断电等情况除外），当客户端发送另外一个请求时，就使用这条已经建立的连接。

​	**在 HTTP 1.1 版本中，默认情况下所有连接都被保持**，**如果加入 "Connection: close" 才关闭。**目前大部分浏览器都使用 HTTP 1.1 协议，也就是说默认都会发起 Keep-Alive 的连接请求了，所以是否能完成一个完整的 Keep-Alive 连接就看服务器设置情况。

​	由于 HTTP 1.0 没有官方的 Keep-Alive 规范，并且也已经基本被淘汰，以下讨论均是针对 HTTP 1.1 标准中的 Keep-Alive 展开的。

**注意：**

- HTTP Keep-Alive 简单说就是保持当前的TCP连接，避免了重新建立连接。
- HTTP 长连接不可能一直保持，例如 `Keep-Alive: timeout=5, max=100`，表示这个TCP通道可以保持5秒，max=100，表示这个长连接最多接收100次请求就断开。
- HTTP 是一个无状态协议，这意味着每个请求都是独立的，Keep-Alive 没能改变这个结果。另外，Keep-Alive也不能保证客户端和服务器之间的连接一定是活跃的，在 HTTP1.1 版本中也如此。唯一能保证的就是当连接被关闭时你能得到一个通知，所以不应该让程序依赖于 Keep-Alive 的保持连接特性，否则会有意想不到的后果。
- 使用长连接之后，客户端、服务端怎么知道本次传输结束呢？两部分：1. 判断传输数据是否达到了Content-Length 指示的大小；2. 动态生成的文件没有 Content-Length ，它是分块传输（chunked），这时候就要根据 chunked 编码来判断，chunked 编码的数据在最后有一个空 chunked 块，表明本次传输数据结束，详见[这里](http://www.cnblogs.com/skynet/archive/2010/12/11/1903347.html)。什么是 chunked 分块传输呢？下面我们就来介绍一下。

### 五、相关博客链接

https://blog.csdn.net/mfe10714022/article/details/39692305

https://hit-alibaba.github.io/interview/basic/network/HTTP.html