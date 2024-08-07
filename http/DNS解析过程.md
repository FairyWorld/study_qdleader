# DNS解析过程
## 什么是DNS

DNS，就是Domain Name System的缩写，翻译过来就是域名系统，是互联网上作为域名和IP地址相互映射的一个分布式数据库。
DNS能够使用户更方便的访问互联网，而不用去记住能够被机器直接读取的IP数串。通过域名，最终得到该域名对应的IP地址的过程叫做域名解析（或主机名解析）。
#### 简单来说
DNS服务器是用来做URL与IP地址解析的，帮助用户找到要访问服务器的IP。


### DNS的结构
DNS解析是分布式存储的，从结构上来说最顶层是，根域名服务器(ROOT DNS Server)，存储260个顶级域名服务器的IP地址。对于Ipv4来说全球有13个根域名服务器，它储存了每个域(如.com .net .cn)的解析和域名服务器的地址信息。简单的说，根域名服务器就是存放顶级域名服务器地址的。

在根域名服务器下一级就是，顶级域名服务器。例如.com的域名服务器，存储的是一些一级域名的权威DNS服务器地址(如toutiao.com的DNS)。

顶级域名又称一级域名，顶级域名可以分为三类，即gTLD、ccTLD和New gTLD：

gTLD：国际顶级域名(generic top-level domains，gTLD)，例如：.com/.net/.org等都属于gTLD;
ccTLD：国家和地区顶级域名(country code top-level domains，简称ccTLD)，例如：中国是.cn域名，日本是.jp域名;
New gTLD：新顶级域名(New gTLD)，例如：.xyz/.top/.red/.help等新顶级域名。
顶级域名服务器就是根据上面三类保存域名IP对应数据的。

在顶级域名服务器下面一级就是，本地域名服务器(Local DNS)一般是运营商的DNS，主要作用就是代理用户进行域名分析的。

DNS域名服务器分为三级，从上到下分别是根域名服务器(Root DNS Server)、顶级域名服务器(gTLD、ccTLD、New gTLD)、本地域名服务器(Local DNS Server)。


## DNS域名解析的过程：


1、在浏览器中输入www  . qq  .com 域名，操作系统会先检查自己本地的hosts文件是否有这个网址映射关系，如果有，就先调用这个IP地址映射，完成域名解析。 
2、如果hosts里没有这个域名的映射，则查找本地DNS解析器缓存，是否有这个网址映射关系，如果有，直接返回，完成域名解析。 
3、如果hosts与本地DNS解析器缓存都没有相应的网址映射关系，首先会找TCP/ip参数中设置的首选DNS服务器，在此我们叫它本地DNS服务器，此服务器收到查询时，如果要查询的域名，包含在本地配置区域资源中，则返回解析结果给客户机，完成域名解析，此解析具有权威性。 

4、如果要查询的域名，不由本地DNS服务器区域解析，但该服务器已缓存了此网址映射关系，则调用这个IP地址映射，完成域名解析，此解析不具有权威性。 
5、如果本地DNS服务器本地区域文件与缓存解析都失效，则根据本地DNS服务器的设置（是否设置转发器）进行查询，如果未用转发模式，本地DNS就把请求发至13台根DNS，根DNS服务器收到请求后会判断这个域名(.com)是谁来授权管理，并会返回一个负责该顶级域名服务器的一个IP。本地DNS服务器收到IP信息后，将会联系负责.com域的这台服务器。这台负责.com域的服务器收到请求后，如果自己无法解析，它就会找一个管理.com域的下一级DNS服务器地址(http://qq.com)给本地DNS服务器。当本地DNS服务器收到这个地址后，就会找http://qq.com域服务器，重复上面的动作，进行查询，直至找到www.qq.com主机。 
6、如果用的是转发模式，此DNS服务器就会把请求转发至上一级DNS服务器，由上一级服务器进行解析，上一级服务器如果不能解析，或找根DNS或把转请求转至上上级，以此循环。不管是本地DNS服务器用是是转发，还是根提示，最后都是把结果返回给本地DNS服务器，由此DNS服务器再返回给客户机。

其完整的DNS解析过程有以下几个步骤：

（1）查看浏览器缓存

当用户通过浏览器访问某域名时，浏览器首先会在自己的缓存中查找是否有该域名对应的 IP 地址。

（2）查看系统缓存

当浏览器缓存中无域名对应 IP 则会自动检查用户计算机系统 Hosts 文件 DNS 缓存是否有该域名对应 IP。

（3）查看路由器缓存

当浏览器及系统缓存中均无域名对应 IP 则进入路由器缓存中检查，以上三步均为客服端的 DNS 缓存。

（4）查看ISP DNS 缓存

当在用户客服端查找不到域名对应 IP 地址，则将进入 ISP DNS 缓存中进行查询。比如你用的是电信的网络，则会进入电信的 DNS 缓存服务器中进行查找。

（5）询问根域名服务器

当以上均未完成，则进入根服务器进行查询。全球仅有 13 台根域名服务器，1 个主根域名服务器，其余 12 为辅根域名服务器。根域名收到请求后会查看区域文件记录，若无则将其管辖范围内顶级域名（如.com、.cn等）服务器 IP 告诉本地 DNS 服务器。

（6）询问顶级域名服务器

顶级域名服务器收到请求后查看区域文件记录，若无记录则将其管辖范围内权威域名服务器的 IP 地址告诉本地 DNS 服务器。

（7）询问权威域名（主域名）服务器

权威域名服务器接受到请求后查询自己的缓存，如果没有则进入下一级域名服务器进行查找，并重复该步骤直至找到正确记录。

（8）保存结果至缓存

本地域名服务器把返回的结果保存到缓存，以备下一次使用，同时将该结果反馈给客户端，客户端通过这个 IP 地址即可访问目标Web服务器。至此，DNS递归查询的整个过程结束。


网络客户端就是我们平常使用的电脑，打开浏览器，输入一个域名。比如输入www.baidu.com，这时，你使用的电脑会发出一个DNS请求到本地DNS服务器。本地DNS服务器一般都是你的网络接入服务器商提供，比如中国电信，中国移动。

查询入www.baidu.com的DNS请求到达本地DNS服务器之后，本地DNS服务器会首先查询它的缓存记录，如果缓存中有此条记录，就可以直接返回结果。如果没有，本地DNS服务器还要向DNS根服务器进行查询。

根DNS服务器没有记录具体的域名和IP地址的对应关系，而是告诉本地DNS服务器，你可以到域服务器上去继续查询，并给出域服务器的地址。

本地DNS服务器继续向域服务器发出请求，在这个例子中，请求的对象是.com域服务器。.com域服务器收到请求之后，也不会直接返回域名和IP地址的对应关系，而是告诉本地DNS服务器，你的域名的解析服务器的地址。

最后，本地DNS服务器向域名的解析服务器发出请求，这时就能收到一个域名和IP地址对应关系，本地DNS服务器不仅要把IP地址返回给用户电脑，还要把这个对应关系保存在缓存中，以备下次别的用户查询时，可以直接返回结果，加快网络访问。

 










### 关于DNS解析的TTL参数：

我们在配置DNS解析的时候，有一个参数常常容易忽略，就是DNS解析的TTL参数，Time To Live。TTL这个参数告诉本地DNS服务器，域名缓存的最长时间。用阿里云解析来举例，阿里云解析默认的TTL是10分钟，10分钟的含义是，本地DNS服务器对于域名的缓存时间是10分钟，10分钟之后，本地DNS服务器就会删除这条记录，删除之后，如果有用户访问这个域名，就要重复一遍上述复杂的流程。
其实，如果网站已经进入稳定发展的状态，不会轻易更换IP地址，我们完全可以将TTL设置到协议最大值，即24小时。带来的好处是，让域名解析记录能够更长时间的存放在本地DNS服务器中，以加快所有用户的访问。设置成24小时，其实，还解决了Googlebot在全球部署的服务器抓取网站可能带来的问题，这个问题麦新杰专门有一篇博文

 

阿里云之所以只将TTL设置成10分钟，是为了让域名解析更快生效而已。因为之前的解析会在最长10分钟之后失效（本地DNS服务器将对应的解析条目删除），然后新的解析生效。如果是24小时，这个生效的时间最长就是24小时，甚至更长（本地DNS服务器要有用户请求，才会发起查询）。