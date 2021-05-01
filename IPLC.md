# 专线
* 严格意义上应该是经认证企业通过公有云平台或运营商平台申请，硬件施工专线光缆至申请企业的办公场所，另一端直接接入运营商的专线POP，网络流量从出企业就是全程走专线内网，不受公网影响。
* **目前机场常用的专线其实并不是严格意义上的专线，更侧重于内网这一概念。也就是虽然从用户到节点接入点是走公网，但到达节点后经内网中转到下一个墙外的服务器，所以无需担心被封杀审查。**

* **机场应用的专线，少数是两个地区端对端的专线（比如花卷莞港/苏日专线），更多的是利用公有云不同区域的VPC之间内网互通机制，组建的内网。最经典的就是阿里云的经典网络内网，可惜已经作古了。以下的各厂商专线内网名称选用的是跨VPC互通的品牌名，不代表机场采用的一定是跨VPC内网互通的方法。**

# 常见的专线（内网）线路
**按照公有云规模排列**

## 1、[AWS Direct Connect](https://aws.amazon.com/cn/directconnect/?nc1=h_ls)
* 官方简介：AWS Direct Connect 是一种云服务解决方案，让您可以轻松建立从本地通往 AWS 的专用网络连接。使用 AWS Direct Connect，您可以在 AWS 和数据中心、办公室或租用环境之间建立私有连接。这样可以提高带宽吞吐量并能提供一个比基于 Internet 的连接更为一致的网络体验。

* 点评：据大佬说是需要特别申请的业务，目前没看到哪个机场有这类节点。至于很多机场用的月抛AWS、AGA作为BGP入口，和这个并不等同，那是公网中转，存在被墙可能。

* 相关机场：暂无

## 2、[Azure ExpressRoute](https://azure.microsoft.com/zh-cn/services/expressroute/)
* 官方简介：使用 Azure ExpressRoute 以在 Azure 数据中心与位于本地或共置环境中的基础结构之间创建专用连接。ExpressRoute 连接并不经过公共 Internet，并且与典型的 Internet 连接相比，它们提供更高的可靠性、更快的速度以及更低的延迟

* 点评：据说北京/上海的世纪互联（Azure国内代理商）可与海外Azure节点组建MPLS内网。

* 相关机场：
  * Qcrane --号称微软内网，原来入口确实是北京/上海的世纪互联入口，但最近变成AWS宁夏入口，暂时不知线路怎么走。据场主介绍azure内网开销太大，准备仅部分节点保留。

## 3、[阿里云企业网CEN](https://help.aliyun.com/document_detail/59870.html)
* 官方简介：云企业网（Cloud Enterprise Network，CEN)帮助您在VPC间，VPC与本地数据中心间搭建私网通信通道，通过路由自动分发及学习，提高网络的快速收敛和跨网络通信的质量及安全性，实现全网资源的互通，帮助您打造一张具有企业级规模和通信能力的互联网络。

* 点评：最早的阿里云经典内网被无数机场用作专线节点使用，直至2020年寿终正寝。之后陆续有阿里云CEN货源流入机场圈，但是因为价格昂贵，仅有conair，厘米云，w8ves，墙洞，海豚湾等部分机场上线。3月份的一次剧变，再次让cen线路从机场圈短期销声匿迹，同时也导致部分机场跑路倒台。当然野火烧不尽，春风吹又生，慢慢的总会有的

* 相关机场：
  * 魅影极速：作为最早靠阿里云内网成名奠定江湖地位的机场大佬，这几年走得很坎坷。。。现在据说部分节点是阿里云CEN线路。
  * EXFLUX：十余个游戏节点线路是CEN，限速3-5M


## 4、[腾讯云AIA](https://cloud.tencent.com/product/aia)
* 官方简介：Anycast 公网加速（Anycast Internet Acceleration，AIA）是一个覆盖多地的动态加速网络，可以大幅提升您业务的公网访问体验。不同于其他应用层加速服务，AIA 能实现 IP 传输的质量优化和多入口就近接入，减少网络传输的抖动、丢包，最终提升云上应用的服务质量，扩大服务范围，精简后端部署。

* 点评：20年开始前rixcloud开始广泛使用AIA作为节点路线，获得一致好评。RIXCLOUD跑路后，yoyu/w8ves继承了这种线路理念，一度达到鼎盛，再后来不可抗力因素导致倒台。21年开始见证了AIA的大爆发，越来越多机场上了AIA节点或游戏节点。

* 相关机场：
  * Nexitally和AmyTelecom：4月开始改为全线AIA
  * ImmTelecom：4月开始改为全线AIA
  * Precision Cloud：韩国新加坡加拿大英国等部分节点AIA
  * Blinkload：BUSINESS套餐有香港，日本，美国AIA节点各两个。
  * FlowerCloud:高级节点过境段为AIA
  * YToo：除实验节点外的节点过境段为AIA
  * CNIX：香港韩国英国部分节点AIA
  * 海豚湾：IPLC节点为AIA
  * DlerCloud：据闻也要上AIA
  * TAG:近三十条AIA游戏节点线路。

## 5、[华为云云连接CC](https://www.huaweicloud.com/product/cc.html)
* 官方简介：云连接（Cloud Connect）能够提供一种快速构建跨区域VPC及云上多VPC与云下多数据中心之间的高速、优质、稳定的网络能力，帮助用户打造一张具有企业级规模和通信能力的全球云上网络。

* 点评：华为云的POP跟阿里云，腾讯云相比少了些，亚太地区只有香港，曼谷，新加坡，美国没POP

* 相关机场：
  * DlerCloud：1888以上套餐才有，CC节点。
  * FastLink：IPLC节点
  * 几鸡：IPLC节点
  * MDSS：V4等级的节点。
  * 跑路云：广港游戏节点，限速


## 6、[UCloud高速通道](https://docs.ucloud.cn/udpn/guide)
* 官方简介：高速通道 （UCloud Dedicated Private Network)，提供各个地域之间的，低延迟、高质量的内网数据传输服务。

* 点评：市面很多UCLOUD只是入口或落地是UCLOUD，薅羊毛的，中间过境传输并不是UDPN。

* 相关机场：
  * 几鸡：D+以上套餐才有，10倍率游戏专线，限速2M
  * EXFLUX:上海-韩国游戏节点,限速3M

## 7、[青云](https://docs.qingcloud.com/product/sd_wan/quick_start/vpc_connect_vpc)
* 官方简介：实现 VPC 私有网络主机与另一个区的 VPC 私有网络主机网络互通。

* 点评：最早据说Nexitally和CNIX用过青云内网，20年有过一家云际互联的机场也上过，后来恶意跑路了。。。

* 相关机场：
   sad，无。

## 9、[安畅云联网](https://www.anchnet.com/infrastructure/cloudlink)
* 官方简介：云联网（CloudLink）基于SDN和高质量传输网络构建的云交换平台，实现多服务商（公有云、ISP、IDC）与用户间的快速互联互通，为企业提供安全、中立、开放的网络连接服务及灵活搭建IT基础架构的能力。


* 点评：安畅的CN2机房很有名了。。。第一次知道到安畅专线业务被机场使用还是很新鲜的

* 相关机场：
  * EXFLUX：全线内网线路
  * Bywave：全线内网线路
  * WaveCloud：全线内网线路，最近被DDOS
  * 跑路云：DRL/BGP线路
  * 星梦数据：IEPL线路
  * NyanCAT：被DDOS了大半年，注册谨慎


## 10、[花卷](https://www.betaidc.com/index.html)

* 点评：CNIX自从用了花卷莞港线路后，一战成名，甚至因低廉价格和花卷线路被称为永远的神YYDS。Nexitally在华为云下架后，用过一段时间花卷，但是反响不佳，官方解释是线路未来得及扩容。

* 相关机场：
  * PrecisionCloud：香港、澳门为莞港，日本实验是苏日线路。
  * Nexitally：Premium会员的Hong Kong 21为莞港线路。
  * CNIX：香港线路基本为花卷，
  * Franxx：苏日花卷，限速20M
  * 跑路云：莞港、苏日花卷，限速5M



