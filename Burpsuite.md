# 抓包工具Burpsuite 使用分享
[官网下载链接](https://portswigger.net/burp/)
## 水货 ##
Burp Suite 是用于攻击web 应用程序的集成平台，包含了许多工具。Burp Suite为这些工具设计了许多接口，以加快攻击应用程序的过程。所有工具都共享一个请求，并能处理对应的HTTP 消息、持久性、认证、代理、日志、警报。

- Proxy——是一个拦截HTTP/S的代理服务器，作为一个在浏览器和目标应用程序之间的中间人，允许你拦截，查看，修改在两个方向上的原始数据流。
- Spider——是一个应用智能感应的网络爬虫，它能完整的枚举应用程序的内容和功能。
- Scanner[仅限专业版]——是一个高级的工具，执行后，它能自动地发现web 应用程序的安全漏洞。
- Intruder——是一个定制的高度可配置的工具，对web应用程序进行自动化攻击，如：枚举标识符，收集有用的数据，以及使用fuzzing 技术探测常规漏洞。
- Repeater——是一个靠手动操作来补发单独的HTTP 请求，并分析应用程序响应的工具。
- Sequencer——是一个用来分析那些不可预知的应用程序会话令牌和重要数据项的随机性的工具。
- Decoder——是一个进行手动执行或对应用程序数据者智能解码编码的工具。
- Comparer——是一个实用的工具，通常是通过一些相关的请求和响应得到两项数据的一个可视化的“差异”。

## 干货 ##
在安装好java环境(推荐JDK8)，运行burpsuite.jar

### 抓包 ###
点击Proxy找到Options查看代理设置,确保Running是√ ,默认是启动状态,如果不是可能存在端口冲突,关闭冲突软件或选中配置后点击Edit进行修改端口,设置浏览器代理地址

### 修改请求 ###
修改客户端发送到服务器的请求数据

修改请求之前先来配置一下拦截规则,在Proxy下的Options里面找到Intercept Client Requests 然后选择一条,点击Edit修改成入下配置,拦截所有请求
确保 Intercept requests based on the following rules前面有√,规则生效

- 拦截请求

在Proxy下的Intercept 查看 Intercept is按钮是否显示为on,如果不是点一下按钮(根据最上面的配置默认是off)

- 打开拦截器

用POSTMAN测试发送一个请求,然后Proxy Intercept都有高亮显示,此时这个请求正在被拦截然后修改请求主体内容,点击Forward放行请求

Forward是放行,通过请求

Drop 是丢弃请求,这条请求服务器不会收到

Action是对这条请求进行其他操作(和HTTP history中对请求右键可进行的操作类似)

- 修改请求

回到Proxy下的HTTP history选择修改的请求可以查看Original request和Edited request原生请求和修改后的请求

### 修改响应 ###

- 修改服务器发送到客户端的响应数据

在Proxy下的Options 关闭Intercept Client Requests的规则然后修改Intercept Server Responses

- 修改响应规则

使用POSTMAN发送请求以后,拦截器拦截响应

修改完成后同样点击Forward放行

- 修改响应数据

在HTTP history可以看到原生响应数据和修改后的响应数据
