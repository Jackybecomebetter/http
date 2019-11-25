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

​	http定义了与服务器交互的不同方法，最基本的请求方法有四种，分别是GET、POST、PUT、DELETE。我们可以这样理解，URL定义了网络上的某个资源，而请求方法GET、POST、PUT、DELETE则对应了资源的查、增、改、查。