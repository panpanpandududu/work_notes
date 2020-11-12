## fiddler

### 简介

1. ##### 是位于客户端和服务器端的HTTP代理

2. ##### 目前最常用的HTTP抓包工具之一

3. ##### 功能非常强大，是web调试的利器：

- 监控浏览器所有的HTTP/HTTPS流量
- 查看，分析请求内容细节
- 伪造客户端请求和服务器响应
- 测试网站的性能
- 解密HTTPS的web会话
- 全局，局部断点功能
- 第三方插件

##### 使用场景

- 接口调试，接口测试，线上环境调试，web性能分析
- 判断前后端bug,开发环境hosts配置，mock，弱网断网测试

### B/S架构

编写程序部署到web服务器

web服务器运行在服务器上，绑定IP地址并监听某端口，接收和处理http请求

客户端通过http协议获取服务器上的网页，文档等资源

[http ://test.lemonban.com/ningmengban/images/logo.png]()

```python
http:// ：协议
test.lemonban.com ：域名 --》协助找到主机
```

### http协议概述

HTTP（Hyper  Text   Transfer    Protocol）（超文本传输协议）

HTTP请求报文组成：

请求行，请求头部，空一行，请求正文（请求体）4部分组成

![image-20201012180055483](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201012180055483.png)

#### URL（uniform resource locator）:统一资源定位符

格式：<u>scheme(协议)://host（主机）[:port#]（端口）/path（路径）/.../[?query-string]（参数）</u>

- scheme:协议，如http，https.ftp等
- host：域名或者ip地址
- port：端口号
- path：资源路径
- query-string：发送的参数

### fiddler原理

the  free web debugging proxy for any browser,system or platform

![image-20201012162435186](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201012162435186.png)

##### 能够监听到客户端向服务器端发送请求以及服务器端向客户端发送响应

因为fiddler默认设置为系统代理，而谷歌，ie等浏览器默认读的就是系统代理，所以能够被fiddler监听

![image-20201012163118981](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201012163118981.png)

### fiddler工具栏

保留想要请求，删除其他请求 选择需要保留的，再按shift+delete

重复请求：选择某个请求R，shift+R 可设置循环次数

删除所有请求：ctrl+x

查找：ctrl+f

![image-20201013164914533](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201013164914533.png)

![image-20201013165615408](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201013165615408.png)

### fiddler之打断点

#### 1.fiddler可修改以下请求

- fiddler设置断点，可修改http请求头信息，如修改cookie，user-agent
- 可以修改请求数据，突破表单限制，提交任意数字
- 拦截响应数据，修改响应体，如修改服务端返回的页面数据

#### 2.断点的两种方式

##### before requests:这个是打在request请求的时候，未达到服务器之前

![img](https://images2015.cnblogs.com/blog/1070438/201704/1070438-20170427231400147-1640451671.png)

##### after  responses：也就是服务器响应之后，在fiddler将响应传回给客户端之前

![img](https://images2015.cnblogs.com/blog/1070438/201704/1070438-20170427231652897-1951650044.png)

#### 3.全局断点：

##### rules  ->  automatic breakpoint  -> before requests

#### 4.单个断点

已经知道了某个接口的请求地址，这时候只需要针对这一条请求打断点调试，在命令行输入指令就可以

##### 请求前断点： bpu 关键字/地址   回车

这样请求接口时，只会拦截这个接口，此处可以修改任意请求参数

取消断点：命令行输入 bpu+回车

##### 响应后断点：bpafter  网址  回车

#### 5.拦截来自某个网站所有请求

1. 在命令行输入：bpu +[https://blog.csdn.net/](https://blog.csdn.net/Rao_Juan/)
2. 打开该网址任意网页，均被拦截
3. 打开其他网站，其他网站可正常请求
4. 说明只拦截了来自CSDN(https://blog.csdn.net)的请求
5. 清除输入bpu 回车

### Inspectors(检查器）

作用：主要是对请求和响应进行查看和分享，监听请求的响应内容

#### 一.请求信息

##### 1.headers

显示头信息，上半部分显示请求的头信息

##### 2.TextView,syntaxView,imageView,HexView,Json,xml

不同的显示方式,需要根据请求的不同格式进行选择，一个请求不可能同时可以用所有的方式进行显示

##### 3.auth

认证信息

##### 4.cookies

cookies信息

##### 5.raw

请求的完整信息，包括：请求的方法、地址、路径、协议版本、头信息和参数等

![image-20201015181621775](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201015181621775.png)

#### 二.响应信息

##### 1.headers

显示响应的头信息，包括协议版本，响应code，响应结果和头信息

##### 2.TextView,syntaxView,imageView,HexView,Json,xml

不同的显示方式

##### 3.auth

认证信息

##### 4.cookies

cookies信息

##### 5.raw

响应的完整信息，包括：协议版本，响应code，响应结果，响应的头信息和响应体

##### 6.caching

缓存信息

### AutoResponder(自动响应器）

autoresponder可用于拦截某一请求，进行如下操作：

- 重定向到本地的资源
- 使用fiddler的内置响应
- 自定义响应 

### composer(设计者)

可用于接口测试

![img](http://images2015.cnblogs.com/blog/1070438/201704/1070438-20170423222605226-1716047535.png)

#### 1.模拟get请求

- 在composer区域输入地址，或者直接从左侧session会话框中的某个请求直接拖到右面，点击execute执行，请求就可以发送成功了
- 请求发送成功后，左边会话框会生成一个会话记录，可以查看抓包详情，选中此会话，点中inspectors,查看相关信息
- 右侧history区域会多一个历史请求记录

![image-20201016170738522](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201016170738522.png)

#### 2.模拟post请求

请求类型勾选post

url地址栏输入对应的请求地址

body区域写相关json参数

header请求头区域，可以把前面抓包的数据copy过来

### filter过滤器

##### 1.user  filters启用，Action运行

![image-20201027155540523](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201027155540523.png)

![image-20201027155316417](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201027155316417.png)

##### 2.Hosts过滤

Zone:指定只显示内网（intranet）或互联网（Internet）的内容H

Host:指定显示某个域名下的会话

——No  Host  Filter : 无host过滤

—hide  the  following  hosts :只显示如下host

—flag  the   following   hosts : 加粗显示如下host

输入多个host，多个之前用半角逗号或者回车分隔；

支持通配符：*，baidu.com;

![image-20201028110452403](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201028110452403.png)

![image-20201028110703020](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201028110703020.png)

步骤：选择hosts——>输入过滤条件单条件（xx.xx.com）或多条件（xx.xx.com，ss.ss.com或xx.xx.com+enter+ss.ss.com）或通配符（*.xx.com）——>changes  not  yet  saved  ——>选择Action中Run  Filterset  now;

![image-20201028114042321](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201028114042321.png)

##### 3.client  process过滤

客户端进程过滤规则：

show  only  traffic  from :你可以指定只捕获哪个windows进程中的请求；

show  only internet  explorer  traffic:只显示IE发出的请求；

hide  Windows RSS  platform  traffic：隐藏windows  RSS平台发出的请求；

![image-20201028120047476](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201028120047476.png)

![image-20201028120414290](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201028120414290.png)

##### 4.request  headers过滤

请求header过滤规则：

show  only  if  url  contains：只展示url中包含某字符的请求；

flag  requests  with  headers：标记带有特定header的请求；

delete request  header：删除请求的header；

set request  header：设置请求的header，即在所有请求里加上某字段

![image-20201028135113247](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201028135113247.png)

##### 5.Breakpoints过滤

断点设置规则：

break   request   on  http  post：给所有post请求设置断点；

break   request   on  http  GET  with  queryString：给所有带参数的get请求设置断点；

break  request  on  Content-type：给特定的Content-type设置断点

##### 6.request  status  code过滤

 