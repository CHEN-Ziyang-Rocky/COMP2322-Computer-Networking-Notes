# COMP 2322 Computer Networking

[TOC]

## <u>00. Introduction:</u>

![截屏2023-01-11 17.10.20](/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-11%2017.10.20.png)

![截屏2023-01-11 17.09.57](/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-11%2017.09.57.png)

![截屏2023-01-11 17.09.32](/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-11%2017.09.32.png)





## <u>01. Computer Networks and the Internet</u>

### 1.1 Internet

在本书中，我们使用一种特定的计算机网络，即公共因特网，作为讨论计算机网络及其协议的主要载体 。 

互联网 (Internet)，由计算机网络互联而成（即“网络的网络”）的庞大的系统，是以 TCP/IP 协议为主的一簇协议支撑工作的网络。

- 构成描述：**Internet = network edge + access nekwork + network core**

- 服务描述：互联网是为 **分布式的应用进程** 提供**通讯服务**的 **基础设施**，包括应用层以下的 **protocol**。互联网通过套接字接口 (API) 为进程提供服务，规定了接入网络核心的端系统数据交付的方式。分布式应用（distributed application）指的是应用程序分布在不同计算机上，通过网络来共同完成一项任务的工作方式。

  <img src="/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-14%2013.59.00.png" alt="截屏2023-01-14 13.59.00" style="zoom:33%;" />



#### "nuts and bolts" view

从因特网的**具体构成（结构上）来看**，Internet 就是一堆的网络，通过(几十亿)网络互联设备连在一起的一个巨型网络。其中有

- <u>**Network edge:** 和互联网连接的设备，称为:</u> **<u>hosts 主机 = end systems 端系统</u> (eg. iPad, iPhone, PC, MacBook) 来运行网络应用程序**

- <u>**Access networks (physical media):** 就是有线或者无线通信链路</u>，可以把边缘接入到网络核心, 可以将报文发给另外一个主机。**end systems** 通过 **communication links (通信链路)** 和 **packet switches (分组交换机)** 连接在一起，<u>**link 的 transmission rate = bandwidth 带宽(bit /s or bps)**</u>，发送数据形成的信息包称为 **packet (分组)**
  - **packet switches 分组交换机(forward packets 转发设备):**  作用是来了一个数据从哪个地方把它转走，不同的网络层工作的层次/支撑它运行的协议不一样， 根据**不同的协议**可以把它分成**链路层的交换机、网络层的路由器、防火墙等等**。eg. <u>routers 路由器 and switches 交换机</u>
  
  - **communication links (通信链路):** eg. fiber 光纤, copper 同轴电缆, radio 无线电, satellite 卫星
  - 当一台端系统要向另 一 台端系统发送数据时，发送端系统将数据分段，并为每段加上首部字节 。 由此形成的信息包用计算机网络的术语来说称为 **packet (分组)**。 这些分组通过网络发送到目的端系统，在那里被装配成初始数据 。
  
- <u>**network core 属于基础设施:** 就是**一堆互相连接的路由器(mesh of interconnected routers)**</u>，网络核心能够把所有的东西发给我所需要的目标主机，网络核心连接着所有端系统，从而我可以跟所有的端系统通信。作用：数据交换

![截屏2023-01-12 16.30.32](/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-12%2016.30.32.png)

#### Service view

**从服务角度**来看: 互联网是 **分布式的应用** 以及 **为分布式应用提供通讯的这个基础设施**

- Distributed application 是网络存在的理由，**为 分布式应用（distributed application）提供通讯服务的基础设施**(infrastructure, eg. PC)
- 通信基础设施为apps提供编程接口API (通信服务)，使设备之间可以进行连接。eg. 允许发送和接收应用程序 "连接" 到互联网的接口(API)

<img src="/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-12%2015.23.13.png" alt="截屏2023-01-12 15.23.13" style="zoom:35%;" />

<img src="/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-13%2020.44.10.png" alt="截屏2023-01-13 20.44.10" style="zoom:45%;" />

### 1.2 Protocol

- **protocol 协议(标准):** Internet 中所有的通信行为都受协议制约。对等的实体在通讯过程当中，应该遵守的规则集合，是一个标准和规范。协议定义了在两个或多 个通信实体之间交换的 **format, order of messages sent (报文格式和次序)**，以及 在报文传输和/或接收或 其他事件方面所采取的 **actions (动作)**
- 协议控制发送、接收消息 eg. TCP, IP, HTTP, FTP, PPP, Skype, 802.11

例：一个web的浏览器运行在这个PC机上，他们首先要建立起一个TCP的连接， 然后我按照 http 的协议规范，向对方发出请求。发出请求之后，就是把这个报文封装在 http 请求的报文格式当中，按照TCP的规范发给对方。对方建立起TCP的连接之后，就能够收到这个报文，然后根据协议解析这个报文，读取对方请求的信息/动作，捡取消息后把该消息封装成http相应的报文格式发送给对方。

<img src="/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-12%2015.39.04.png" alt="截屏2023-01-12 15.39.04" style="zoom:35%;" />



### 1.3 Network structure

<center>
  <img src="/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-12%2016.30.32.png" alt="截屏2023-01-12 16.30.32" style="zoom:80%;" />
  <br> 
  Internet = network edge + access nekwork + network core
</center>



#### Network edge

**network edge 网络边缘，不属于基础设施:** hosts (clients and servers) -> host(客户端, 手机, 电脑)可以跑应用(游戏，电子商务) -> sends/receives packets of data

主机发送功能：获取应用消息，**分成 smaller chunks (小的数据块)**，称为 **packets**，**长度为 L bits**。以 **transmission rate R** 将数据包传输到接入网络。**link transmission rate = link bandwidth = link capacity**

<img src="/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-12%2016.51.46.png" alt="截屏2023-01-12 16.51.46" style="zoom:35%;" />

![截屏2023-01-12 16.54.31](/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-12%2016.54.31.png)



#### Access networks & physical media

- **access networks (physical media) 接入网络和物理媒体, 属于基础设施:** wired, wireless communication links. 就是把边缘接入到网络核心, 可以将报文发给另外一个主机。
- 接入有一个非常重要的指标：**bandwidth (data rate) of access network: bps (bits per second), Kbps, Mbps, Gbps**
- **将端系统和边缘路由器连接(connect end systems to edge router)** 有几种接入方式：住宅接入网络（图片左下角）、单位接入网络 (学校、公司)、无线接入网络（图片左上角）。有独享和共享接入方式。例：那我们现在通过这个中国电信的这个光纤接入到电信的这个网络交换设备，是独享。在公司/学校里，如果使用的是有限接入公司的带宽，和几百个电脑共享这个带宽，凌晨访问可能可以有100Mps，但是平常下午5、6点就可能只有3-4Mps

<img src="/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-13%2014.59.38.png" alt="截屏2023-01-13 14.59.38" style="zoom:25%;" />

在 **Access networks & physical media** 中有几种 **将端系统和边缘路由器连接(connect end systems to edge router)** 的连接方式



##### 住宅接入网络 DSL & cable

宽带住宅接人有两种最流行的类型是：**数字用户线 (Digital Subscriber Line, DSL)** 和 **cable**。住户通常从提供本地电话接入的本地电话公司处获得 DSL 因特网接入 。 因此，当使用DSL时，用户的本地电话公司也是它的lSPc 



在此之前，我们先了解一下 modem(调制解调器) 和 router(路由器) 区别:

<img src="/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-13%2021.28.37.png" alt="截屏2023-01-13 21.28.37" style="zoom: 25%;" />

modem 能將互联网带入您的家庭/企业，建立并维护与 ISP 的专用 link，以至于我们才可以访问互联网。

之所以我们需要使用 modem 的原因是因为：计算机和互联网上使用的是两种不同类型的信号（计算机是数字信号且只读取数字信号，互联网上的信号是模拟信号且只读取模拟信号。A computer only reads digital signals. The internet only reads analog signals.）

当模拟信号从互联网上传入我们家时，modem 就会将输入的 analog signals 解调为 digital signals，以便计算机能够理解。反之，modem 也可以将来自计算机的输出的 digital signals 解调为 analog signals。

<img src="/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-13%2021.32.48.png" alt="截屏2023-01-13 21.32.48" style="zoom:43%;" />



所以从技术上来讲，其实并不需要 router 如果只想要一台设备访问 internet，但是如果有多台机器就需要使用 router 了。

![截屏2023-01-13 21.49.34](/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-13%2021.49.34.png)



modem 分为 DSL modem 和 cable modem：

<img src="/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-13%2021.42.05.png" alt="截屏2023-01-13 21.42.05" style="zoom:43%;" />



router 可以通过网线连接有限设备，通过 Wi-Fi 连接无线信号。下面这附图演示了，多个不同的网络是如何连接到互联网的。

![截屏2023-01-13 21.46.14](/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-13%2021.46.14.png)



一般情况下，router 内部都有一个 switch交换机来连接有限设备，假如 switch 有3条接口，那我就可以连接3个有限设备。但是如果我有更多的设备，需要有线连接，那么我就需要额外的 swith：

<img src="/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-13%2021.48.08.png" alt="截屏2023-01-13 21.48.08" style="zoom:40%;" />

为什么20M宽带，我最大下载速度只能到2.5M? 

宽带太小一般用的单位是20Mb，而我们平时一般是用MB作单位的。他们之间的换算关系是：1Byte=8bit。



###### Access network: Digital Subscriber Line (DSL)

- 是使用调制解调方式，直接用电话线和互联网连接，但是带宽不是很大。use **existing telephone line** to central office **DSLAM (DSL接入共享器)**
- DSL线路上的数据被传到互联网，DSL线路上的语音被传到电话网，DSL有专用的连接到中央办公室的通道
- < 2.5 Mbps upstream transmission rate (typically < 1 Mbps) 上行/上传速度
- < 24 Mbps downstream transmission rate (typically < 10 Mbps) 下行/下载速度
- 因为这些上行速率和下行 速率是不同的，所以这种接入被称为是不对称的。因为他的下载速度比上传速度快得多
- 数据在专享线路的不同频段传输。现有电话线: 0~4kHz为电话; 4~50kHz 为上行数据; 50kHz~IMHz 为下行数据。

家庭的 DSL modem 得到 数字数据 后将其转换为 高频音，以通过电话线传输给 本地中心局CO(central office); 来自许多家庭的模拟信号在 DSLAM 处被转换回数字形式 。

<img src="/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-13%2021.00.42.png" alt="截屏2023-01-13 21.00.42" style="zoom:45%;" />

虽然使用 DSL 比cable modem慢，但并不用像有线连接那样与邻居共享宽带。每个使用DS L的用户都有自己的专用连接，而不是共享线路，而且更加便宜，因为它使用的是几乎无处不在的普通电话线。

![截屏2023-01-13 22.23.41](/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-13%2022.23.41.png)



###### Access network: cable network

- DSL 利用电话公司现有的本地电话基础设施，而**电缆因特网接入 (cable Internet access )** 通常由向用户提供的**有线电视的同一提供商提供**，也就是说用户可以利用有线电视的 cable 来上网

<img src="/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-13%2022.28.16.png" alt="截屏2023-01-13 22.28.16" style="zoom: 30%;" />

- 但是有一个缺点就是用户需要和他附近的其他家庭共享宽带。住宅从提供有线电视的公司获得了电缆因特网接入。如图所示，光缆将电缆头端连接到地区枢纽，从这里使用传统的同轴电缆到达各家各户和公寓。每个地区枢纽通常支持 500 -5000 个家庭。因为在这个系统中应用了光纤和同轴电缆，所以它经常被称为**混合光纤同轴 (Hybrid Fiber Coax, HFC) 系统。**所以在高峰期网速就会比较慢。
- **Asymmetric (非对称):** 最高 **30 Mbps 的下行传输速率 (downstream transmission rate)** 和 **2 Mbps 上行传输速率 (upstream transmission rate)**。因为这些上行速率和下行 速率是不同的，所以这种接入被称为是不对称的 。 
- 线缆和光纤网络将个家庭用户接入到 ISP 路由器，各用户共享到线缆头端的接入网络。与DSL不同, DSL每个用户一个专用线路到CO(central office)。电缆因特网接入需要特殊的调制解调器，这种调制解调器称为电缆调制解调器 (cable modem) 。 

![截屏2023-01-13 15.14.03](/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-13%2015.14.03.png)

有线电视信号线缆双向改造，大家是共享的带宽
FDM: 在不同频段传输不同信道的数据，数字电视和上网数据(上下行)

<img src="/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-13%2015.14.37.png" alt="截屏2023-01-13 15.14.37" style="zoom:40%;" />

| **接入类型**                              | **互联网服务提供商** | **依托的固有基础设施**                 | **使用的技术**                                               |
| ----------------------------------------- | -------------------- | -------------------------------------- | ------------------------------------------------------------ |
| 数字用户线 (Digital Subscriber Line, DSL) | 本地电话公司         | 由双绞铜线组成的电话线网络             | 数字用户线复用器 (DSLAM)                                     |
| 电缆因特网接入 (cable Internet access)    | 有线电视公司         | 由光线和同轴电缆组成的混合光线同轴系统 | 电缆调制解调器端接系统 (Cable Modem Termination System, CMTS) |
| 光纤到户 (fiber to the home, FTTH)        | 本地中心局           | 建立一条直接入户的光纤路径             | 光线线路端接器 (Optical Line Terminator, OLT)                |



##### 企业接入网络 (Ethernet)

**Enterprise access networks (Ethernet) 企业接入网(以太网):** 经常被企业或者大学等机构采用，公司、大学校园和企业等单位的终端用户使用双绞铜线，通过局域网 (LAN) 的方式接入以太网 (Ethernet) 交换机，连接边缘路由器。10 Mbps, 100Mbps, 1Gbps, 10Gbps传输率。现在，端系统经常直接接到以太网络交换机上。

<img src="/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-13%2022.51.37.png" alt="截屏2023-01-13 22.51.37" style="zoom:40%;" />



##### 无线接入网络 Wireless

**Wireless access networks (无线接入网络) 有两种:** 

- **wireless LANs (无线局域网):** 各 wireless end systems 共享 wireless router (Wi-Fi), wireless LANs = WLAN = Wi-Fi
- **wide-area wireless access (广域无线接入):** 通过 **base station(基站)** 或者叫 **access point(接入点)**

![截屏2023-01-13 22.54.37](/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-13%2022.54.37.png)

##### **Physical media (物理媒体)** 

- **signal:** propagates between transmitter/receiver pairs
- **physical link:** lies between transmitter & receiver
- **guided media:** 信号沿着固体媒介被导引: copper, coax, fiber
- **unguided media:** 开放的空间传输电磁波或者光信号，在电磁或者光信号中承 载数字数据 e.g., radio
- **twisted pair (TP):** 两根绝缘铜导线拧合(two insulated copper wires). Category 5: 100 Mbps, 1 Gbps Ethernet. Category 6: 10Gbps

- **coaxial cable:** two concentric copper conductors, bidirectional. Broadband: multiple channels on cable, HFC
- **fiber optical cable:** glass fiber carrying light pulses. high-speed operation: high-speed point-to-point transmission (e.g., 10’s-100’s Gbps transmission rate). low error rate: repeaters spaced far apart, immune to electromagnetic noise



#### Network core

- 目的/作用：数据交换
- 实现的方式有两种：packet switching 分组交换 & circuit switching 电路交换

**network core 属于基础设施:** 就是**一堆互相连接的路由器(mesh of interconnected routers)**，网络核心能够把所有的东西发给我所需要的目标主机，网络核心连接着所有端系统，从而我可以跟所有的端系统通信。

<img src="/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-12%2016.56.27.png" alt="截屏2023-01-12 16.56.27" style="zoom:30%;" />

##### packet switching 分组交换

- **store-and-forward (存储-转发):** 网络带宽资源不再分分为一个个片，传输时使用全部带宽

  - 将要传送的 messages/data 分成一个个单位 packet(分组)
  - 将packet从一个路由器传到相邻路由器(hop)，一段段最终从源端传到目标端，期间可能通过许多不同的路由器，就会不断发生存储和转发。在转发之前，节点必须收到整个 packet，延迟比 circuit switching 要大，排队时间长。但是**换取了资源共享性**
  - each packet 采用链路的最大传输能力(带宽)
  - 在一个邮局通信系统中，邮局收到一份邮件之后，先存储下来，然后把相同目的地的邮件一起转发到下一个目的地，这个过程就是存储转发过程，分组交换也使用了存储转发过程。

  **<u>在一个速率为R bps 的 link，一个长度为L-bit packet 以 R bps 的速率传输到 link 的存储转发延时需要 L/R seconds</u>**

  Example: L = 7.5 Mbits，R = 1.5 Mbps

  one-hop transmission delay(每次存储的延迟) = 5 s。注意接收也需要存储的延迟，图中就应该是有10s。

  end-end delay = 2L/R (assuming zero propagation delay)

  ![截屏2023-01-12 17.28.55](/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-12%2017.28.55.png)



- **queueing delay, loss (排队延迟和丢失):** 如果 arrival rate (in bits) to link > transmission rate: packets 将在路由器上排队，等待在link上传输。如果 memory (buffer) 填满/用完了，packets 可能会 **被抛弃/丢失 dropped (lost)**。 可以说这是 <u>packet switching 分组交换</u> 为了获得共享性所必须要付的代价。

  ![截屏2023-01-12 17.51.38](/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-12%2017.51.38.png)



- **Two key network-core functions:**

  - **routing (路由)**: 决定分组采用的源到目标的路径

  - **forwarding (转发)**: 将分组从路由器的输入链路转移到输出链路

  ![截屏2023-01-12 17.58.14](/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-12%2017.58.14.png)



##### circuit switching 电路交换

端到端的资源被分配给从源端 到目标端的呼叫 “call”:

- 图中 <u>each link has 4 circuits: call gets 2nd circuit in top link and 1st circuit in right link</u>
- 是 **独享资源(dedicated resources): **no sharing，每个呼叫一旦建立起来就能够保证性能
- 如果呼叫没有数据发送，被分配的资源就会被浪费 (no sharing). 就像两个人打电话，但是却沉默不语，电信公司仍然要收钱
- 通常被 traditional telephone networks 采用

<img src="/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-12%2017.09.06.png" alt="截屏2023-01-12 17.09.06" style="zoom:25%;" />

In circuit switching，网络带宽资源会被分为一个个片(piece)，网络资源(如带宽)被分成片的两种方式：

- 频分(Frequency-Division Multiplexing): 交换接电和交换节点之间的链路带宽比较宽， 两个host在通讯之前在每一条链路上找到空闲的一片
- 时分(Time-Division Multiplexing): 划分时间片的方式。每个周期的第一片，分给第一个用户使用; 每个周期的第二片，分给第二个用户使用...

<img src="/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-12%2017.19.57.png" alt="截屏2023-01-12 17.19.57" style="zoom:35%;" />

![截屏2023-01-12 17.25.55](/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-12%2017.25.55.png)



##### Packet switching vs circuit switching

同样的网络资源，Packet switching 允许更多用户使用网络（共享性，按需分配），避免了 circuit switching 占线却并没有传输数据的浪费资源现象。适合于对突发式数据传输(great for bursty data)。但是过度使用会造成网络拥塞:分组延时和丢失，对可靠地数据传输需要协议来约束: 拥塞控制。

<img src="/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-12%2018.28.53.png" alt="截屏2023-01-12 18.28.53" style="zoom:50%;" />

![截屏2023-01-12 18.31.24](/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-12%2018.31.24.png)



### 1.4 Internet structure and ISP

#### Internet structure

- 互联网结构：网络中的网络 network of networks，网络把主机连接起来，而互连网（internet）是把多种不同的网络连接起来，因此互连网是网络的网络。而互联网（Internet）是全球范围的互连网。
- **ISPs (Internet Service Providers):** 互联网服务提供商，可以从互联网管理机构获得许多 IP 地址，同时拥有通信线路以及路由器等联网设备，个人或机构向 ISP 缴纳一定的费用就可以接入互联网。 目前的互联网是一种多层次 ISP 结构，ISP 根据覆盖面积的大小分为第一层 ISP、区域 ISP 和接入 ISP。互联网交换点 IXP 允许两个 ISP 直接相连而不用经过第三个 ISP。

- **End systems (端系统)** 通过接入**ISPs** 连接到互联网 (eg. 住宅，公司和大学的ISPs)

- 接入ISPs相应的必须是互联的，因此任何2个端系统可相互发送分组到对方

<img src="/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-12%2023.14.26.png" alt="截屏2023-01-12 23.14.26" style="zoom:43%;" />



问题: 给定数百万接入ISPs，如何将它们互联到一起。

如果将每个接入ISP直接连接到彼此不能扩展(scale)，需要O(N2)连接。

<img src="/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-12%2018.53.33.png" alt="截屏2023-01-12 18.53.33" style="zoom:30%;" />

所以我们可以将每个接入ISP都连接到全局ISP(全局范围内覆盖)：客户ISPs和提供者ISPs有经济合约，这样当然好，但是如果世界上不可能只有一个ISP网络，由于有利可图，肯定会有能做出ISP技术的人出来跟他一起竞争。

<img src="/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-12%2018.53.47.png" alt="截屏2023-01-12 18.53.47" style="zoom:30%;" />

但是，如果全局ISP是可行的业务，那会有竞争者有利可图，一定会有竞争：

<img src="/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-12%2018.54.31.png" alt="截屏2023-01-12 18.54.31" style="zoom:30%;" />

竞争: 但如果全局ISP是有利可为的业务，那会有竞争者

合作: 通过ISP之间的合作可以完成业务的扩展，肯定会有互联，对等互联的结算关系。图中ISP A、B、C大家都接入了IXP网络，其中 IXP 就叫 **Internet exchange point**

<img src="/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-12%2018.58.19.png" alt="截屏2023-01-12 18.58.19" style="zoom:30%;" />

**Internet Content Providers (内容提供商网络):** 可能会构建它们自己的网络，将它们的服务、内容更 加靠近端用户，向用户提供更好的服务。而且不用给用其他ISP网络，连接若干local ISP和各级(包括一层)ISP,更加靠近用户。搭建自己的网络就不要给其他ISP网络的运营商交钱，减少运营成本。e.g. Google, Microsoft, Akamai

<img src="/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-12%2019.00.38.png" alt="截屏2023-01-12 19.00.38" style="zoom:30%;" />



#### ISP的三个层次和连接

目前的互联网是一种多层次 ISP 结构，ISP 根据覆盖面积的大小分为第一层 ISP、区域 ISP 和接入 ISP。互联网交换点 IXP 允许两个 ISP 直接相连而不用经过第三个 ISP。

- **中心：第一层ISP（如UUNet, BBN/Genuity, Sprint, AT&T）**国家/国际覆盖，速率极高。直接与其他第一层ISP相连。与大量的第二层ISP和其他客户网络相连
- **第二层ISP**: 更小些的ISP **(regional ISP)**，与一个或多个第一层ISPs，也可能与其他第二层ISP
- **第三层ISP与其他本地ISP**，**local ISP, access net** (与端系统最近)

- POP: 高层ISP面向客户网络的接入点，涉及费用结算。如一个低层ISP接入多个高层ISP，多宿(multi home)
- 对等接入: 2个ISP对等互接，不涉及费用结算
- IXP:多个对等ISP互联互通之处，通常不涉及费用结算。对等接入
- ICP自己部署专用网络，同时和各级ISP连接

在网络的最中心，一些为数不多的充分连接的大范围网络(分布广、节点有限、 但是之间有着多重连接)

- "tier-1" commercial ISPs (e.g., Level 3, Sprint, AT&T, NTT), national & international coverage
- content provider network (e.g., Google): 将它们的数据中心接入ISP，方便周边用户的访问;通常私有网络之间用专网绕过第一层ISP和区域ISPs

![截屏2023-01-12 19.08.47](/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-12%2019.08.47.png)

![截屏2023-01-12 19.16.35](/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-12%2019.16.35.png)



### 1.5 Performance: loss, delay, throughput

网络核心采用的是 packet switching, 所以可能会产生 loss and 四个delay。

#### loss and delay

**Delay 产生的原因:** 在路由器当中，每条 link 都对应相应的队列，如果有一个packet需要传输，他就会先通过查路由表决定通过哪条队列，通过其 link 往外走。如果这条 link 上，当前没有 packet 在传输，就直接可以传。但是如果有其他的 packet 在传输，那就必须排在队列当中。 只有排到队头，才可以被传输。

**Loss 产生的原因:** 队列是有限的，如果来了一个 packet 加入这个队列，但是队列已经满了，这是 packet 就会被丢弃。丢失的 packet 可能会被前一个节点或源端系统重传，或根本不重传

<img src="/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-12%2023.30.21.png" alt="截屏2023-01-12 23.30.21" style="zoom:35%;" />



#### Four sources of packet delay

节点延时 nodal delay 可以分为4个部分：

| 名称                                | 描述                                 | 计算公式                                                     |
| ----------------------------------- | ------------------------------------ | ------------------------------------------------------------ |
| **nodal processing (节点处理延时)** | 数据在路由器中处理需求的时间         | NA                                                           |
| **queueing delay (排队延时)**       | 数据在路由器前等待前面数据处理的时间 | L: packet length (bits), R: link bandwidth (bps),<br />a: average packet arrival rate<br />traffic intensity (流量强度) = La/R<br />La/R = 0: 平均排队延时很小<br />La/R -> 1: 延时变得很大<br />La/R > 1: 平均排队延时将趋向无穷大<br />所以设计系统时流量强度不能大于1 |
| **transmission delay (传输延时)**   | 数据在信道上传播所花费的时间         | L/R <br />L: packet length (bits), R: link bandwidth (bps)   |
| **propagation delay (传播延时)**    | 数据从主机到信道上所用的时间         | d/s<br />d = link length, s = 在媒体上的传播速度             |

- **nodal processing (节点处理延时):** 检查 bit级差错，检查 packet(首部) 有没有出错和决定将分组导向何处的处理消耗的时间
- **queueing delay (排队延时):** 在输出链路上等待传输的时间，依赖于路由器的拥塞程度。
- **transmission delay (传输延时):** R=链路带宽(bps)，L=分组长度(bits)，将分组发送到链路上的时间 (传输延时) = L/R，存储转发延时
- **propagation delay (传播延时): **d = 物理链路的长度，s = 在媒体上的传播速度 (~3x10^8 m/sec)，传播延时 = d/s

<img src="/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-12%2020.43.13.png" alt="截屏2023-01-12 20.43.13" style="zoom:33%;" />

<center>
  <img src="/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-12%2020.46.17.png" alt="截屏2023-01-12 20.46.17" style="zoom:18%;" />
  <img src="/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-12%2020.46.28.png" alt="截屏2023-01-12 20.46.28" style="zoom:18%;" />

![Screenshot 2023-02-07 at 15.44.23](Typora_Picture/Screenshot%202023-02-07%20at%2015.44.23.png)

![Screenshot 2023-02-07 at 15.44.57](Typora_Picture/Screenshot%202023-02-07%20at%2015.44.57.png)



<img src="/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-12%2023.25.39.png" alt="截屏2023-01-12 23.25.39" style="zoom:30%;" />



#### throughput 吞吐量

- **单位时间内，从原主机向目标主机发出去有效的比特的数量**，在源端和目标端之间传输的速率 (bits/time unit), rate (bits/time unit) at which bits transferred between sender/receiver (end-to-end)
  - **instantaneous (瞬间吞吐量):** 在**一个时间点**的速率
  - **average (平均吞吐量):** 在一个**长时间内平均值**

**server (服务器)** 发送 bits 到管道, 他的有效吞吐量取决于细的管道 (取决于第 I 个管道)。吞吐量 = min{Rs,Rc}

![截屏2023-01-12 23.33.59](/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-12%2023.33.59.png)

<img src="Typora_Picture/Screenshot%202023-02-07%20at%2016.07.17.png" alt="Screenshot 2023-02-07 at 16.07.17" style="zoom:53%;" />

**bottleneck link (瓶颈链路):** 端到端路径上，限制端到端吞吐的 link (最细的link就是他的 bottleneck link 瓶颈链路)

端到端平均吞吐=min{R1，R2,...,Rn}

![截屏2023-01-12 23.42.16](/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-12%2023.42.16.png)



在互联网场景中，我们一般都是分组交换，按需使用，这条link是共用的，n 个设备，那么每个设备的带宽将是 1/n，每个设备所获得的带宽是平均的，取决于 n 个设备。假设有10个设备，那么每个设备的带宽将是 1/10

<img src="/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-12%2023.52.47.png" alt="截屏2023-01-12 23.52.47" style="zoom:40%;" />



### 1.6 Protocol layers, service models

#### protocol layers 协议层次

- 网络是一个复杂的系统! (Networks are complex, with many "pieces": hosts, routers, links of various media, applications, protocols, hardware, software)
- 问题是：如何设计组织和实现这个复杂的计算机网络功能呢？层次化



**layering (层次化/分层)：**层次化方式实现复杂网络功能，每一层实现一个服务(方法)each layer implements a service (function)

- 将网络复杂的功能分层功能明确的层次，每一层实现了其中一个或一组功能，功能中有其上层可以使用的功能: 服务
- 本层协议实体相互交互执行本层的协议动作，目的是实现本层功能，通过接口为上层提供更好的服务
- 在实现本层协议的时候，直接利用了下层所提供的服务
- 本层的服务: 借助下层服务实现的本层协议实体之间交互带来的新功能(上层可以利用的) + 更下层所提供的服务

就像是打仗的时候，司令官(application layer)不会直接给士兵下令，而是给团长下命令一层一层传达，直到最底层士兵层(Physical layer)就不会往下传了，他只能自己指挥自己。整个下面的层次向上提供服务，团长给师长提供的服务，当然包括连长给团长提供的服务以及自己的服务，就是每一层都包括了其底下的服务 + 自己增加到新服务。通过层连接口向上提供服务。

![截屏2023-01-13 00.14.25](/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-13%2000.14.25.png)



#### Service models

<img src="/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-13%2001.33.27.png" alt="截屏2023-01-13 01.33.27" style="zoom:50%;" />

##### Internet protocol stack

![截屏2023-01-13 01.30.33](/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-13%2001.30.33.png)

![截屏2023-01-13 23.23.40](/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-13%2023.23.40.png)

![截屏2023-01-13 01.28.38](/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-13%2001.28.38.png)



##### ISO/OSI reference model

- **presentation (表示层):** 允许应用 解释(interpret) 传输的数据, e.g., 加密，压缩，机器相关的表示转换
- **session (会话层):** 数据交换的同步，检查点，恢复

**Internet protocol stack (互联网协议栈)** 没有这两层! 这些服务，如果需要的话，必须被应用实现吗?

![截屏2023-01-13 01.26.26](/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-13%2001.26.26.png)

<img src="/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-13%2001.34.49.png" alt="截屏2023-01-13 01.34.49" style="zoom:70%;" />

<img src="/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-13%2001.35.09.png" alt="截屏2023-01-13 01.35.09" style="zoom:70%;" />







##### Encapsulation 封装和解封装

**Application (应用层):** 报文(message)

**Transport (传输层):** 报文段(segment): TCP段，UDP数据报

**Network (网络层):** 分组packet (如果无连接方式: datagram 数据报)

**Link (数据链路层):** 帧(frame)

**Physical (物理层):** 位(bit)

在原端做一个大的封装（从Application -> Physical），在目标端做一个大的解封装（从Physical -> Application）

![截屏2023-01-13 01.12.47](/Users/chenziyang/Desktop/Typora_Picture/%E6%88%AA%E5%B1%8F2023-01-13%2001.12.47.png)



## <u>02. Application layer 交换报文，实现网络应用</u>

一些网络应用的例子: E-mail, Web, 文本消息, 远程登录, P2P文件共享, 即时通信, 多用户网络游戏, 流媒体(YouTube, Hulu, Netflix), 社交网络, Internet 电话, 实时电视会议, 搜索

当我们想创造一个新的网络应用应该怎么做呢？

在端系统上编程通过网络基础设施提供的服务，应用进程彼此通信，注意：网络核心中没有应用层软件，网络核心没有应用层功能，网络应用只在端系统上存在 ，快速网络应用开发和部署。

<img src="/Users/chenziyang/Desktop/Typora_Picture/Screenshot%202023-01-16%20at%2018.11.18.png" alt="Screenshot 2023-01-16 at 18.11.18" style="zoom:30%;" />

### 2.1 principles of network applications

在本章中，我们学习有关 principles of network applications (应用层协议原理) 和实现方面的知识。我们从定义几个关键的应用层概念开始，其中包括应用程序所需要的网络服务、客户和服务器、进程和运输层接口。我们详细考察几种网络应用程序，包括Web、电子邮件、
DNS和对等文件分发。然后我们将涉及开发运行在TCP和UDP上的网络应用程序。

因此，当研发新应用程序时，你需要编写将在多台端系统上运行的软件，例如，该软件能够用C、Java或Python来编写。
重要的是，你不需要写在网络核心设备如路由器或链路层交换机上运行的软件. 换句话来讲，就是我们的软件是基于我们上城里有开发，你底层是怎么用什么协议去通信的我们根本不用管。如果是开发软件我们也只需要知道应用层的一些协议。



应用程序研发者很可能利用现代网络应用程序中所使用的两种主流体系结构之一 (possible structure of applications):

- Client-server
- peer-to-peer (P2P)



#### Client-server

- <u>在C/S体系结构中，有一个总是打开的主机称为服务器，它服务于来自许多其他称为客户的主机的请求。</u>
- 一个经典的例子是web应用程序，其中总是打开的Web服务器服务于来自浏览器(运行在客户主机上)的请求。当Web服务器按收到来自某客户对某对象的请求时，它向该客户发送所请求的对象作为响应。(在谷歌上面输入一个URL链接，谷歌就会返回一个页面作为响应)
- <u>C/S体系结构的服务器具有**固定的、周知的**地址，该地址称为**IP地址**</u> （我们的S端服务器的IP是固定的，谷歌的域名会被解析成一个IP）。具有C/S体系结构的应用程序包括Web、FTP、Telnet和电子邮件等.

![Screenshot 2023-02-07 at 21.22.55](Typora_Picture/Screenshot%202023-02-07%20at%2021.22.55.png)



#### peer-to-peer (P2P)

- 在一个P2P体系结构中，对位于数据中心的专用服务器几乎没有依赖。相反，应用程序在间断连接的主机对之间使用直接通信，这些主机对被称为**对等方(peer-peer)**。P2P体系结构的最引人入胜的特性之一是它们的**自扩展性(self scalability): new peers bring new service capacity, as well as new service demands. 新的同行带来了新的业务容量，也带来了新的业务需求。**
- P2P架构的应用也有客户端进程和服务器进程之分
- 但是他的数据安全性没有CS模式好。

![Screenshot 2023-02-07 at 21.24.21](Typora_Picture/Screenshot%202023-02-07%20at%2021.24.21.png)

#### Inter-process communication 进程通信

**process**: a program running in a host

within same host, two processes can communicate using **inter-process communication** (defined by OS)

不同主机，通过交换报文(Message)来通信。对每对**Inter-process communication (进程通信)**，我们通常将这两个进程之一标识为客户(client)，而另一个进程标识为服务器(server)：

- **client process (客户端进程):** 发起通信的进程
- **server process (服务器进程): **等待连接，然后提供服务的进程

多数应用程序是由通信进程对组成，每对中的两个进程互相发送**message**。从一不进程向另一个进程发送的报文**必须通过下层的网络**。进程通过一个称为 **套接字(socket)** 的软件接口向网络发送报文和从网络接收报文（process sends/receives messages to/from its socket 进程向 socket 发送报文或从 socket 接收报文）

在这个图，为我们这个程序试运行在我们的应用层。应用程式由应用开发者控制。应用层之下，都是由操作系统控制。我们想要发送数据和接收数据，只能通过socket api来进行。socket 就像一个门一样，我们想要传输信息直接把数据放到这个门里面，然后对方想要接收信息就从这个门里面接收信息

![Screenshot 2023-02-07 at 21.43.21](Typora_Picture/Screenshot%202023-02-07%20at%2021.43.21.png)



#### Addressing processes

进程为了接收 massage，必须有一个 **identifier(标识)**。那么怎么寻址一个进程呢？

<u>**process identifier** includes both **IP address** and **port number** associated with process on host</u>

- **找主机地址:** 在因特网中，主机由其 **32 位的 IP address** 且它能够唯一地标识该主机就够了。
- **找目的地端口号 (port number):** 除了知道报文送往自的地的**主机地址**外，发送进程还必须指定运行在按收主机上的**接收进程(接收socket)**。因为一般而言一台主机能够运行许多网络应用，这些信息是需要的。**目的地端口号 (port number)**用于这个目的。己经给流行的应用分配了特定的端口号 (eg, HTTP server: 80, mail server: 25)



#### What transport service does an app need?

应用需要传输层提供什么样的服务? 如何描述传输层的服务? 不同的应用需要不同的传输服务

![Screenshot 2023-02-08 at 13.21.31](Typora_Picture/Screenshot%202023-02-08%20at%2013.21.31.png)

- **data loss 数据丢失率**
  - 有些应用则要求100%的可靠数据传输(如文件)
  - 有些应用(如音频)能容忍一定比例以下的数据丢失

- **delay sensitive 延迟敏感度**
  - 有些应用程序(如互动游戏)需要低延迟才能使用
  - 其他一些应用程序(如电子邮件)并不关心

- **bandwidth 吞吐**
  - 一些应用(如多媒体)必须 需要最小限度的吞吐，从而使得应用能够有效运转
  - 一些应用能充分利用可供使 用的吞吐(弹性应用)





#### Internet transport layer services

Internet 传输层提供的服务

![Screenshot 2023-02-07 at 23.03.04](Typora_Picture/Screenshot%202023-02-07%20at%2023.03.04.png)

**UDP存在的必要性**

- 能够区分不同的进程，而IP服务不能，在IP提供的主机到主机端到端功能的基础上，区分了主机的应用进程
- 无需建立连接，省去了建立连接时间，适合事务性的应用
- 不做可靠性的工作，例如检错重发，适合那些对实时性要求比较高而对正确性要求不高的应用。因为为了实现可靠性(准确性、保序等)，必须付出时间代价(检错重发)
- 没有拥塞控制和流量控制，应用能够按照设定的速度发送数据。而在TCP上面的应用，应用发送数据的速度和主机向网络发送的实际速度是不一致的，因为有流量控制和拥塞控制



#### Internet apps: application / transport layer protocols

![Screenshot 2023-02-08 at 14.52.16](Typora_Picture/Screenshot%202023-02-08%20at%2014.52.16.png)



### 2.2 Web and HTTP

#### Web

- Web 是一种应用，http是支持Web应用的协议
- Web page consists of base HTML-file which embeds several referenced objects. object can be HTML file, JPEG image, Java applet, audio file,… Web 页面 (Web page) (也叫文档)是由对象组成的。 一个对象 (object) 只是一个文件，诸如一个HTML文件、一个JPEG图形、 一个Java小程序或一个视频片段这样的文件， 且它们可通过一个URL地址寻址。 多数Web页面含有一个HTML基本文件 (baseHTML file) 以及几个引用对象。 例如，如果一个Web页面包含HTML文本和5个JPEG图形，那么这个 Web 页面有 6 个对象: 一个 HTML 基本文件加 5 个图形 。
- **URL: Uniform Resource Locator 通用资源定位**

<img src="Typora_Picture/Screenshot%202023-02-08%20at%2015.48.21.png" alt="Screenshot 2023-02-08 at 15.48.21" style="zoom:43%;" />



#### HTTP

HTTP: hypertext transfer protocol (超文本传输协议) 文本与文本之间任意指向的关系

Web的应用层协议

**client/server model (客户/服务器模式):**

- **client:** 请求、接收和显示 Web对象的浏览器 **(request)**
- **server:** 对请求进行响应， 发送对象的Web服务器 **(response)**

![Screenshot 2023-02-09 at 01.11.33](Typora_Picture/Screenshot%202023-02-09%20at%2001.11.33.png)





#### Non-persistent HTTP & Persistent HTTP

在许多因特网应用程序中，客户和服务器在一个相当长的时间范围内通信，其中客户发出一系列请求并且服务器对每个请求进行响应。

依据应用程序以及该应用程序的使用方式，这一系列请求可以以规则的 <u>**间隔周期性** 地或者 **问断性地一个按一个发出**</u>。当这种客户-服务器的交互是经TCP进行的，应用程序的研制者就需要做一个重要决定，即每个请求/响应对是经一个单独的TCP连接发送，还是所有的请求及其响应经相同的TCP连接发送呢？

即每个请求/响应对是经一个单独的 TCP 连接发送，还是所有的请求及其响应经相同的 TCP 连接发送?

- 每个请求/响应对是经一个单独的 TCP 连接发送 就是 Non-persistent HTTP
- 所有的请求及其响应经相同的 TCP 连接发送 就是 Persistent HTTP

HTTP既能够使用非持续连接，也能够使用持续连接:

<img src="Typora_Picture/Screenshot%202023-02-09%20at%2014.41.11.png" alt="Screenshot 2023-02-09 at 14.41.11" style="zoom:50%;" />



##### Non-persistent HTTP

**往返时间RTT(round-trip time)**: 一个小的分组从客户端到服务器，在回到客户端的时间(传输时间忽略)

这引起浏览器在它和 Web 服务器之间发起一个 TCP 连接;这涉及一次“三次握手”过程，

即客户向服务器发送一个小 TCP 报文段，服务器用一个小 TCP 报文段做出确认和响应， 最后，客户向服务器返回确认 。 三次握手中前两个部分所耗费的时间占用了一个 RTT。 完 成了三次握手的前两个部分后，客户结合 三次握手的第三部分(确认)向该 TCP 连接发 送一个 HTTP 请求报文 。 一 旦该请求报文到达服务器，服务器就在该 TCP 连接上发送 HTML文件 。 该 HTTP 请求/响应用去了另 一个 RTT。 因此，粗略地讲，总的响应时间就是两个 RTT 加上服务器传输 HTML 文件的时间 。

![Screenshot 2023-02-09 at 15.09.33](Typora_Picture/Screenshot%202023-02-09%20at%2015.09.33.png)

![Screenshot 2023-02-09 at 15.10.14](Typora_Picture/Screenshot%202023-02-09%20at%2015.10.14.png)

缺点：

- 每个对象要2个 RTT
- 操作系统必须为每个TCP连接分配资源。（必须为每一个请求的对象建立和维护一个全新的连接。对于每个这样的连接，在客户和服务器中都要分配TCP的缓冲区和保持TCP变量，这给Web服务器带来了严重的负担，因为一台Web服务器可能同时服务于数以百计不同的客户的请求。）



##### Persistent HTTP

- 服务器在发送响应后保持连接打开。
- 同一客户端/服务器之间的后续HTTP消息通过开放连接发送。
- 客户端在遇到引用对象时立即发送请求。
- 对于所有引用的对象，只需一个RTT。





#### HTTP message format

HTTP 规范 [RFC 1945; RFC 2616; RFC 7540] 包含了对 HTTP 报文格式的定义。

HTTP 报文有两种:请求报文和响应报文。

**Method type**

put一般是修改，get查询，post增加/提交，delete删除

![Screenshot 2023-02-09 at 16.55.56](Typora_Picture/Screenshot%202023-02-09%20at%2016.55.56.png)

##### HTTP request message format

Get 请求报文一般没有实体行

<img src="Typora_Picture/Screenshot%202023-02-09%20at%2016.58.58.png" alt="Screenshot 2023-02-09 at 16.58.58" style="zoom:50%;" />

<img src="Typora_Picture/Screenshot%202023-02-09%20at%2016.52.12.png" alt="Screenshot 2023-02-09 at 16.52.12" style="zoom:50%;" />

**Uploading form input:**

- **Post：**使用 POST 方法时使用该实体体。当用户提交表单时，HTTP客户常常使用 POST 方法，例如当用户向搜素引擎提供搜索关键词时。使用 POST 报文时，用户仍可以向服务器请求一个web 页面，但web页面的特定内容依赖于用户在表单字段中输入的内容。如果方法字段的值为 POST 时，则实体体中包含的就是用 户在表单字段中的输人值。
- **Get：**使用 GET 方法时实体体（entily body）为空

![Screenshot 2023-02-09 at 17.15.15](Typora_Picture/Screenshot%202023-02-09%20at%2017.15.15.png)



##### HTTP response message format

![Screenshot 2023-02-09 at 18.00.36](Typora_Picture/Screenshot%202023-02-09%20at%2018.00.36.png)

<img src="Typora_Picture/Screenshot%202023-02-09%20at%2019.46.57.png" alt="Screenshot 2023-02-09 at 19.46.57" style="zoom:50%;" />

##### HTTP response status codes

位于服务器 -> 客户端的响应报文中的首行

一些状态码的例子:

![Screenshot 2023-02-09 at 20.35.35](Typora_Picture/Screenshot%202023-02-09%20at%2020.35.35.png)



#### User-server state: cookies

header line 首部行

![Screenshot 2023-02-09 at 21.06.33](Typora_Picture/Screenshot%202023-02-09%20at%2021.06.33.png)

![Screenshot 2023-02-09 at 21.28.20](Typora_Picture/Screenshot%202023-02-09%20at%2021.28.20.png)

![Screenshot 2023-02-09 at 21.28.46](Typora_Picture/Screenshot%202023-02-09%20at%2021.28.46.png)

#### Web caching (proxy server)

- **Web 缓存器 (Web cache)** 也叫代理服务器 (proxy server) , 它是能够代表初始 Web 服务器来满足 HTTP 请求的网络实体。
- Web 缓存器有自己的磁盘存储空间， 并在存储空间中保存最近请求过的对象的副本。
- 可以配置用户的浏览器，使得用户的所有 HTTP 请求首先指向 Web 缓存器。一旦某浏览器被配置，每个对某对象的浏览器请求首先被定向到该Web 缓存器 。
- 缓存既是客户端又是服务器，通常缓存是由ISP安装 (大学、公司、居民区ISP)

<img src="Typora_Picture/Screenshot%202023-02-09%20at%2021.33.08.png" alt="Screenshot 2023-02-09 at 21.33.08" style="zoom:50%;" />

为什么要使用Web缓存 ?

- 降低客户端的请求响应时 间
- 可以大大减少一个机构内 部网络与Internent接入 链路上的流量
- 互联网大量采用了缓存: 可以使较弱的ICP也能够 有效提供内容



![Screenshot 2023-02-09 at 22.54.23](Typora_Picture/Screenshot%202023-02-09%20at%2022.54.23.png)





### 2.3 Email

因特网电子邮件系统的总体情况，有3个主要组成部分：

- **user agents (用户代理):** 又名 “邮件阅读器”, 撰写、编辑和阅读邮件。如Outlook、Foxmail，输出和输入邮件保存在服务器上

- **mail servers (邮件服务器):** 邮箱中管理和维护发送给用户的邮件，输出报文队列保持待发送邮件报文

- **Simple Mail Transfer Protocol (简单邮件传输协议):** SMTR是因特网电子邮件中主要的应用层协议。

  client: sending mail server

  server: receiving mail server

agents = 通过用户代理软件来访问电子邮件这个应用，因此这个软件就是我们这个应用的代理。浏览器是Web应用的应用代理

<img src="Typora_Picture/Screenshot%202023-02-13%20at%2014.06.39.png" alt="Screenshot 2023-02-13 at 14.06.39" style="zoom:50%;" />

![Screenshot 2023-02-13 at 15.05.41](Typora_Picture/Screenshot%202023-02-13%20at%2015.05.41.png)



#### SMTP [RFC 2821]

<img src="Typora_Picture/Screenshot%202023-02-13%20at%2015.03.59.png" alt="Screenshot 2023-02-13 at 15.03.59" style="zoom:60%;" />

<img src="Typora_Picture/Screenshot%202023-02-13%20at%2015.20.48.png" alt="Screenshot 2023-02-13 at 15.20.48" style="zoom:60%;" />

<img src="Typora_Picture/Screenshot%202023-02-13%20at%2015.44.43.png" alt="Screenshot 2023-02-13 at 15.44.43" style="zoom:67%;" />

![Screenshot 2023-02-13 at 16.59.45](Typora_Picture/Screenshot%202023-02-13%20at%2016.59.45.png)

![Screenshot 2023-02-13 at 17.00.01](Typora_Picture/Screenshot%202023-02-13%20at%2017.00.01.png)

![Screenshot 2023-02-13 at 17.00.14](Typora_Picture/Screenshot%202023-02-13%20at%2017.00.14.png)

![Screenshot 2023-02-13 at 17.00.51](Typora_Picture/Screenshot%202023-02-13%20at%2017.00.51.png)



### 2.4 DNS

Domain Name System 运行在UDP上

域名/主机名 => IP地址

在IP协议中，我们与目标主机交互，需要记住对方的IP192.168.0.1，这就像我们要记住好多朋友的电话一样。电话也太难记了，所以我们需要有个电话本，记录小明 => 18316160606的对应关系。好比www.baidu.com对应10.0.21.4。

<img src="/Users/chenziyang/Desktop/Typora_Picture/Screenshot%202023-02-14%20at%2020.18.49.png" alt="Screenshot 2023-02-14 at 20.18.49" style="zoom:40%;" />

- **主机别名 (host aliasing): **有着复杂主机名的主机能拥有一个或者多个别名

  例如，一台名为 relayl. west- coast. enterprise. com 的主机，可能还有两个别名为 enter­ prise. com 和 www. enterprise.com

  在这种情况下， relay1. west- coast enterprise. com 也称为 **规范主机名 (canonical hoslname)** 。 主机别名(当存在时)比主机规范名更 加容易记忆 。 应用程序可以调用 DNS 来获得主机别名对应的规范主机名以及主机的 IP地址。

- **邮件服务器别名 (mail server aliasing): **显而易见，人们也非常希望电子邮件地址好记忆。

  例如，如果 Bob在雅虎邮件上有一个账户， Bob 的邮件地址就像 hob@ya­hoo. com这样简单。 然而，雅虎邮件服务器的主机名可能更为复杂，不像 ya­hoo. com 那样简单好记(例如，规范主机名可能像 relay1. west- coasL hotmail com 那样)。

  电子邮件应用程序可以调用 DNS，对提供的主机名别名进行解析，以获得该主机的规范主机名及其 IP 地址。

  事实上，MX 记录(参见后面)允许一个公司的邮件服务器和 Web 服务器使用相同(别名化的)的主机名，例如，一个公司的 Web 服务器和邮件服务器都能叫作 enterprise. com。

- **负载分配 (load distribution)** 。 DNS 也用千在冗余的服务器(如冗余的 Web 服务器 等)之间进行负载分配 。 繁忙的站点(如 cnn. com) 被冗余分布在多台服务器上 ， 每台服务器均运行在不同的端系统上，每个都有着不同的 IP 地址 。 由千这些冗余 的 Web 服务器， 一个 IP 地址集合因此与同一个规范主机名相联系 。 DNS 数据库中 存储着这些 IP 地址集合 。 当客户对映射到某地址集合的名字发出一个 DNS 请求 时，该服务器用 IP 地址的整个集合进行响应，但在每个回答中循环这些地址次 序 。 因为客户通常总是向 IP 地址排在最前面的服务器发送 HTTP 请求报文，所以 DNS 就在所有这些冗余的 Web 服务器之间循环分配了负载 。 DNS 的循环同样可以 用千邮件服务器，因此，多个邮件服务器可以具有相同的别名。一些内容分发公 司如 Akamai 也以更加复杂的方式使用 DNS [ Dilley 2002] , 以提供 Web 内容分发



<img src="/Users/chenziyang/Desktop/Typora_Picture/Screenshot%202023-02-14%20at%2020.28.43.png" alt="Screenshot 2023-02-14 at 20.28.43" style="zoom:40%;" />



#### DNS Name Space

![img](/Users/chenziyang/Desktop/Typora_Picture/1653728249232-a57e0bde-fd8e-4a93-aba5-ee6667ccf476.jpeg)



上图展示了 DNS 服务器的部分层次结构，从上到下依次为根域名服务器、顶级域名服务器和权威域名服务器。域名和IP地址的映射关系必须保存在域名服务器中，供所有其他应用查询。



#### DNS hierarchy

<img src="/Users/chenziyang/Desktop/Typora_Picture/Screenshot%202023-02-14%20at%2021.13.44.png" alt="Screenshot 2023-02-14 at 21.13.44" style="zoom:33%;" />

- **根域名服务器 (root name servers):** 根域名服务器是最高层次的域名服务器。每个根域名服务器都知道所有的顶级域名服务器的域名及其IP地址。因特网上共有13个不同IP地址的根域名服务器。当本地域名服务器向根域名服务器发出查询请求时，路由器就把查询请求报文转发到离这个DNS客户最近的一个根域名服务器。这就加快了DNS的查询过程，同时也更合理地利用了因特网的资源。

<img src="Typora_Picture/Screenshot%202023-02-14%20at%2020.53.30.png" alt="Screenshot 2023-02-14 at 20.53.30" style="zoom:30%;" />



- **顶级域名服务器 (top-level domain (TLD) servers)** 这些域名服务器负责管理在该顶级域名服务器注册的所有二级域名。当收到DNS查询请求时就给出相应的回答（可能是最后的结果，也可能是下一级权限域名服务器的IP地址)。

  - 负责com, org, net, edu, aero，博物馆和所有顶级国家域名，例如:uk, fr, ca, jp
  - <u>Network Solutions</u> maintains servers for <u>com</u> TLD
  - <u>Educause</u> for <u>edu</u> TLD

  

- **权威域名服务器 (authoritative DNS servers):** 这些域名服务器负责<u>管理某个区的域名</u>。每一个主机的域名都必须在某个权限域名服务器处注册登记。<u>因此权限域名服务器知道其管辖的域名与IP地址的映射关系</u>。另外，权限域名服务器还知道其下级域名服务器的地址。

<img src="Typora_Picture/Screenshot%202023-02-14%20at%2021.03.59.png" alt="Screenshot 2023-02-14 at 21.03.59" style="zoom:30%;" />





#### Local DNS server

本地域名服务器**不属于**上述的域名服务器的等级结构。当一个主机发出DNS请求报文时，这个报文就首先被送往该主机的本地域名服务器。**本地域名服务器起着代理的作用**，会将该报文转发到上述的域名服务器的等级结构中。本地域名服务器离用户较近，一般不超过几个路由器的距离，也有可能就在同一个局域网中。本地域名服务器的IP地址需要直接配置在需要域名解析的主机中。

- 并不严格属于层次结构
- 每个ISP (居民区的ISP、公司、大学)都有一个本地DNS服务器，也称为“默认名字服务器”
- 当一个主机发起一个DNS查询时，查询被送到其本地DNS服务器。起着代理的作用，将查询转发到层次结构中

<center>
  <img src="Typora_Picture/Screenshot%202023-02-15%20at%2012.30.05.png" alt="Screenshot 2023-02-15 at 12.30.05" style="zoom:43%;" />
  <br>
  如果目标名字在Local Name Server中




#### Domain name resolution

域名解析分为两种，递归和迭代。

##### recursive query

- 名字解析负担都放在当前联络的名字服务器上
- 问题：root DNS server 的负担太重，所以我们要学习/使用 iterated queries

<img src="Typora_Picture/Screenshot%202023-02-15%20at%2012.33.51.png" alt="Screenshot 2023-02-15 at 12.33.51" style="zoom:40%;" />

##### iterated query

- 迭代的方式，大大节省了根域名服务器的压力。
- 由于域名解析的报文并不长，DNS域名解析的过程采用的UDP的传输协议，大大的增加了传输间的效率。
- DNS解析服务器是分布式的，在主域名解析服务器向其他域名解析服务器直接同步数据时，采用的是TCP的传输协议。

<img src="Typora_Picture/Screenshot%202023-02-15%20at%2000.19.24.png" alt="Screenshot 2023-02-15 at 00.19.24" style="zoom:40%;" />

当你输入一个网址的时候：

1. 请求本地缓存，查询host域名配置
2. 本地缓存没有，查询本地DNS服务器。什么是本地DNS服务器呢？其实并不是配置在你家里的，而是你的宽带属于哪个服务商，就会使用哪个服务商的DNS。
3. 本地DNS服务器没有缓存，查询根域名服务器。
4. 根域名服务器会指向顶级域名服务器
5. 顶级域名服务器会指向权威域名服务器
6. 最终拿到权威域名服务器结果，并缓存在本地DNS服务器



#### DNS: caching, updating records

- 一旦(任何)名称服务器学会了映射，它就 **caches mapping (缓存映射)**，由于 主机和主机名 与 IP 地址间的映射并不是永久的，local DNS 服务器在 <u>**一段时间后 (TTL, 通常设置为两天)**</u>将丢弃缓存的信息。
- TLD服务器通常缓存在本地名称服务器中，因此根名称服务器不常被访问
- **cached entries(缓存的条目)** 可能会 **out-of-date 过期** (尽最大努力将名称转换为地址!)，如果name host更改了IP地址，可能直到缓存条目的所有TTLs过期才会被全网所知
- 共同实现 DNS 分布式数据库的所有 DNS 服务器存储了 资源记录 (Resource Record , RR), RR 提供了主机名到 IP 地址的映射，每个 DNS 回答报文包含了一条或多条资源记录

<img src="Typora_Picture/Screenshot%202023-02-15%20at%2012.59.54.png" alt="Screenshot 2023-02-15 at 12.59.54" style="zoom:40%;" />

<img src="Typora_Picture/Screenshot%202023-02-15%20at%2012.51.26.png" alt="Screenshot 2023-02-15 at 12.51.26" style="zoom:40%;" />





#### DNS protocol, messages

<img src="Typora_Picture/Screenshot%202023-02-15%20at%2012.41.32.png" alt="Screenshot 2023-02-15 at 12.41.32" style="zoom:40%;" />

<img src="Typora_Picture/Screenshot%202023-02-15%20at%2012.42.01.png" alt="Screenshot 2023-02-15 at 12.42.01" style="zoom:45%;" />



#### Inserting records into DNSe

上面的讨论只是关注如何从 DNS 数据库中取数据。你可能想知道这些数据最初是怎 么进入数据库中的

<img src="Typora_Picture/Screenshot%202023-02-15%20at%2014.42.54.png" alt="Screenshot 2023-02-15 at 14.42.54" style="zoom:50%;" />



### 2.7 socket programming with UDP and TCP

典型的网络应用是由一对程序(即客户程序和服务器程序)组成的，它们位于两个不同的端系统中。当运行这两个程序时，创建了一个客户进程和一个服务器进程，同时它们通过从套接字读出和写入数据在彼此之间进行通信。 开发者创建一个网络应用时，其主要任务就是编写 client 程序和 server 程序的代码。

目标: 学习如何构建能借助sockets进行通信的C/S应用程序（eg. 服务器与客户端的交互：服务器接收数据并将字符转换为大写，服务器将修改后的数据发送到客户端，客户端接收修改后的数据并在其屏幕上显示行）

- socket 其实就是操作系统提供给程序员操作「网络协议栈」的接口，是一套用于不同 host 间通信的API，你能通过socket 的接口，来控制协议栈工作，从而用它来实现网络通信，达到跨主机通信。
- 他工作在我们的TCP IP协议栈之上
- 要通过 socket 与不同的组织建立联系，我们只需要指定主机的IP号和端口号，IP地址用于唯一标识你的网络设备。那为什么还要额外指定一个端口好呢？如果没有端口，操作系统就没有办法区分数据到底应该发到哪一个应用之上。因此，端口主要用于区分主机上的不同应用。
- 通过 socket 我们可以建立一条用于不同组织不同应用之间的虚拟数据通道，并且他是应用对应用的，就像是一条数据线，连接在不同应用的插槽上。

socket建立之后，我们的消息收发都通过socket，变得非常方便。Socket是双方会话关系的本地标识。在研发阶段，开发者必须最先做的一个决定是: 应用程序是运行在 TCP上还是运行在 UDP上。

**socket 一般分为 TCP 网络编程和 UDP 网络编程。**

- 针对**TCP协议 (reliable, Data Stream, byte streamoriented)**，Socket是一个**<u>四元组 (本地ip，本地port，对方ip，对方port).</u>** 
  - TCP是 面向连接的，并且为两个端系统之间的数据流动提供 **可靠的字节流通道 (TCP provides reliable, in-order byte-stream transfer (“pipe”) between client and server)**
  - TCP 要求收发数据的双方扮演不同的角色：Server/Client

- 针对**UDP协议 (unreliable datagram)**，Socket是一个**<u>二元组 (本地ip，本地port).</u>** 

  - UDP 是无连接的，且发送数据前不握手，从一个端系统向另一个端系统发送独立的数据分组，不对交付提供任何保证。

  - sender 将目标的 IP 地址和端口# 显式附加到 each packet

  - receiver 从收到的数据包中提取发送方的IP地址和端口。传输的数据可能会丢失或无序接收

我们通过一个简单的 UDP 应用程序和一个简单的 TCP应用程序来介绍 UDP 和 TCP套接字编程。



#### TCP socket programming

##### TCP Server

服务器首先运行，等待连接建立：

```python
from socket import*
```

1. **ServerSocket:** **创建 **服务器套接字

```python
serverSocket = socket(AF_INET, SOCK_STREAM) ## 创建 TCP 服务器 welcoming socket
## 第一个参数指示底层网络使用的是 IPv4。第二个参数指示该 socket 是 SOCK_STREAM 类型，这表明它是一个 TCP socket
```

2. **bind:** 将套接字 **绑定 **到一个本地地址和端口上

3. **listen:** 将套接字设定为监听模式，准备接受客户端请求

```python
serverSocket.bind(('0.0.0.0', 12000)) ## 将我们创建的 socket 关联到我们主机的某一个 network interface(IP) 和 port 上
serverSocket.listen(1) ## 将socket设定为监听模式, 准备接受客户端请求/聆听某个客户敲门, 其中参数定义了请求连接的最大数(至少为1)
print ('The server is ready to receive')
```

4. **accept: 阻塞** 等待客户端请求到来。当请求到来后，接受连接请求，返回一个新的对应于此客户端连接的套接字socketClient

5. **IO流操作:** 用返回的套接字socketClient和客户端进行通信

6. **accept:** 返回，等待另一个客户端请求

```python
while True: ## loop forever
     connectionSocket, addr = serverSocket.accept() 
    ## 当客户敲该门时，程序为 serverSocket 调用 accept()方法
    ## 这在服务器中创建了一个称为 connectionSocket 的新socket，由这个特定的客户专用。
    ## 客户和服务器则完成了握手，在 客户的 clientSocket 和服务器的 serverSocket 之间创建了 一个 TCP 连接。
    
     sentence = connectionSocket.recv(1024).decode() ## read bytes from socket (but not address as in UDP)
     capitalizedSentence = sentence.upper()
     connectionSocket.send(capitalizedSentence.encode()) 
      ## 借助于创建的 TCP 连接，客户与服务器现在能够通过该连接相互发送字节。
      ## 使用 TCP, 从一侧发送的所有字节不仅确保到达另一侧，而且确保按序到达。
```

7. **close:** 关闭套接字

```python
     connectionSocket.close() ## close connection to this client (but not welcoming socket)
```



##### TCP Client

客户端主动和服务器建立连接：

```python
from socket import *
```

1. **Socket:** 创建客户端套接字

```python
clientSocket = socket(AF_INET, SOCK_STREAM) 
## 该行创建了client socket，称为 clientSocket
## 第一个参数仍指示底层网络使用的是 IPv4. 第二个参数指示该套接字是 SOCK_STREAM 类型. 这表明它是一个 TCP 套接字
```

值得注意的是当我们创建该客户套接字时仍未指定其端口号; 相反，我们让操作系统为我们做此事（没有bind）

2. **connect:** 向服务器发出连接请求

```python
clientSocket.connect(("127.0.0.1", 12000)) 
## create TCP socket for server, remote port 12000
## 这行代码执行完后, 执行三次握手, 并在客户和服务器之间创建起一条 TCP 连接
```

3. **IO流操作:** 和服务器进行通信

```python
sentence = input('Input lowercase sentence:') ## 从用户获得了一个句子, 字符串 sentence 连续收集字符 直到用户键入回车以终止
clientSocket.send(sentence.encode()) ## 发送 sentence 到 TCP, 无需附加 server name, port 
modifiedSentence = clientSocket.recv(1024) ## 当字符到达服务器时，它们被放置在字符串 modifiedSentence 中
print (‘From Server:’, modifiedSentence.decode())
```

4. **close:** 关闭套接字

```py
clientSocket.close() ## 关闭套接字，因此关闭了客户和服务器之间的 TCP 连接. 它引起客户中的TCP向服务器中的TCP发送一条TCP报文
```



#### C/S socket interaction: TCP

<img src="Typora_Picture/Screenshot%202023-02-16%20at%2019.35.10.png" alt="Screenshot 2023-02-16 at 19.35.10" style="zoom:53%;" />



#### UDP socket programming

- 在客户端和服务器之间没有连接，没有握手

- 发送端在每一个报文中明确地指定目标的IP地址和端口 号
- 服务器必须从收到的分组中提取出发送端的IP地址和端 口号
- 传送的数据可能乱序， 也可能丢失（不可靠的字节组的传送服务）



##### UDP Server

只有一个socket：

| Socket | IP      | Port |
| ------ | ------- | ---- |
| 8888   | 1.1.1.1 | 80   |

```python
from socket import *
```

1. **serverSocket:** 创建套接字

```python
from socket import *
serverPort = 12000
serverSocket = socket(AF_INET, SOCK_DGRAM) ## create UDP socket, SOCK_DGRAM = UDP
```

2. **bind:** 将套接字绑定到一个本地地址和端口上

```python
serverSocket.bind(('', serverPort))
print ('The server is ready to receive')
```

3. **recvfrom:** 阻塞等待接收消息

4. 收到的消息被封装在 modifiedMessage 里，里面有对方的ip和端口

5. **sendto:** 可以根据对方的DatagramPacket再像对方发送消息

```python
while True:
    message, clientAddress = serverSocket.recvfrom(2048) ## 从 UDP socket 读取消息，获取 client IP 和 port
    modifiedMessage = message.decode().upper() ## send upper case string back to this client
    serverSocket.sendto(modifiedMessage.encode(), clientAddress)
```



##### UDP Client

```py
from socket import *
```

1. **clientSocket:** 创建客户端套接字

```py
serverName = ‘hostname’
serverPort = 12000
clientSocket = socket(AF_INET, SOCK_DGRAM) ## 创建了客户的套接字，称为 clienLSocket
## 第一个参数指示了地址簇, AF_INET 指示了底层网络使用了 IPv4
## 第二个参数指示了该套接字是 SOCK_DGRAM 类型的，这意味着它是一个 UDP 套接字
```

2. **message:** 创建小写用户输入字符串。
3. **sendto(): **为报文附上目的地址 (serverName , serverPort) 并且向进程的套接字 **clientSocket** 发送结果分组

```py
message = input('Input lowercase sentence:') ## get user keyboard input 
clientSocket.sendto(message.encode(),(serverName, serverPort)) ## Attach server name, port to message; send into socket
```

4. **modifiedMessage:** 将server修改完的字符串从 socket 放入 modifiedMessage

```py
modifiedMessage, serverAddress = clientSocket.recvfrom(2048) ## read reply characters from socket into string
print (modifiedMessage.decode()) ## 打印出 modifiedMessage 大写字符串
```

5. **close:** 关闭套接字

```py
clientSocket.close()
```

我们可以发现，tcp和udp各自用一套端口，哪怕都是8000，但是互不冲突。



#### C/S socket interaction: UDP

<img src="Typora_Picture/Screenshot%202023-02-16%20at%2019.34.36.png" alt="Screenshot 2023-02-16 at 19.34.36" style="zoom:43%;" />



## <u>03. Transport Layer 进程间的逻辑通信</u>

运输层协议为运行在不同 主机上的**应用进程之间**提供了 **逻辑通信 (logic communicalion) 功能**

从应用程序的角度看，通过逻辑通信，运行不同进程的主机好像使用socket直接相连一样;

实际上，这些主机也许位于地球的两侧，通过很多路由器及多种不同类型的链路相连。应用进程使用运输层提供的逻辑通信功能彼此发送报文，而无须考虑承载这些 message 的物理基础设施的细节

<img src="Typora_Picture/Screenshot%202023-02-16%20at%2022.14.32.png" alt="Screenshot 2023-02-16 at 22.14.32" style="zoom:50%;" />



### 3.1 transport-layer services and protocols

- 为运行在不同主机上的应用进程提供 **logical end-to-end connection (逻辑通信)**，逻辑通信的意思是“好像是这样通信，但事实上并非真的这样通信”。
- Transport layer protocols run in **end systems** (传输协议运行在端系统)

  - 发送方: <u>breaks application **messages** into **segments**, passes to network layer</u> (将应用层的报文分成报文段，传递给网络层)

  - 接收方: <u>**reassembles segments** into **messages**, passes to application layer</u> (将报文段重组成报文，然后传递给应用层)

![Screenshot 2023-02-16 at 23.07.56](Typora_Picture/Screenshot%202023-02-16%20at%2023.07.56.png)

- 网络应用程序可以使用多种的运输层协议 (Internet传输层协议有两种，即 TCP 和 UDP). 每种协议都能为调用的应用程序提供一组不同的运输层服务。

- **TCP: reliable, data stream, in-order delivery**

  - 多路复用、解复用
  - congestion control (拥塞控制)
  - flow control (流量控制)
  - connection setup (建立连接)

- **UDP: unreliable, datagram, unordered delivery**

  - 多路复用、解复用

  - extension of “best-effort” IP (从network layer的主机到主机变成了进程到进程，除此之外，就没有添加更多的其它额外服务了)

都不提供的服务: delay guarantees(延时保证), bandwidth guarantees(带宽保证)



### 3.2 multiplexing and demultiplexing

在一台主机中经常有多个应用进程同时分别和另一台主机中的多个应用进程通信，一个进程(作为网络应用的一部分)有一个或多个 socket。这表明运输层有一个很重要的功能——复用 (multiplexing)和分用(demultiplexing)。

- **复用 (multiplexing): **从多个 socket 接收来自多个进程的message，根据 socket 对应的IP地址和端口号等信息对报文段用头部加以封装 (该头部信息用于以后的解复用)，然后将报文段传递到网络层
- **分用/解复用 (demultiplexing): **根据报文段的头部信息中的IP地址和端口号将接收到的报文段发给正确的socket (和对应的应用进程)。

对接收到的报文进行差错检测。网络层的IP数据报首部中的检验和字段，只对首部差错进行检验。 根据应用程序的不同需求，运输层需要有两种不同的运输协议，即面向连接的TCP和无连接的UDP。

![Screenshot 2023-02-16 at 22.52.03](Typora_Picture/Screenshot%202023-02-16%20at%2022.52.03.png)

运输层向高层用户屏蔽了下面网络核心的细节（如网络拓扑、所采用的路由选择协议等），它使应用进程看见的就是好像在两个运输层实体之间有一条端到端的逻辑通信信道。



#### Connectionless demux

无连接(UDP)多路解复用

![Screenshot 2023-02-17 at 14.13.19](Typora_Picture/Screenshot%202023-02-17%20at%2014.13.19.png)

![Screenshot 2023-02-17 at 14.15.59](Typora_Picture/Screenshot%202023-02-17%20at%2014.15.59.png)



#### Connection-oriented demux

面向连接(TCP)的多路复用

![Screenshot 2023-02-17 at 14.03.19](Typora_Picture/Screenshot%202023-02-17%20at%2014.03.19.png)





### 3.3 connectionless transport: UDP

UDP只在IP的数据报服务之上增加了很少一点的功能：

- 复用和分用的功能
- 差错检测的功能，发现错误的就扔掉

虽然UDP用户数据报只能提供不可靠的交付，但UDP在某些方面有其特殊的优点。



UDP 的主要特点 

- **connectionless:** 发送数据之前不需要建立连接， 因此减少了开销和发送数据之前的时延。UDP发送端和接收端之间没有握手，每个UDP报文段都被 独立地处理

- **best-effort:** 尽最大努力交付，即不保证可靠交付，因此主机不需要维持复杂的连接状态表。

- **面向报文:** UDP对应用层交下来的报文， 既不合并，也不拆分，而是保留这些报文的边界。 UDP 一次交付一个完整的报文。
- **没有拥塞控制:** 因此网络出现的拥塞不会使源主机的发送速率降低。这对某些实时应用是很重要的。 很适合对时延要求较高的多媒体通信的要求。
- **没有流量控制:** 应用->传输的速率= 主机->网络的速率

- <u>**small header size:** 只有8个字节，比TCP的20个字节的首部要短。</u>
- 支持一对一、一对多、多对一和多对多的交互通信。

发送方UDP对应用程序交下来的报文，在添加首部后就向下交付IP层。UDP对应用层交下来的报文，既不合并，也不拆分，而是保留这些报文的边界。应用层交给UDP多长的报文，UDP就照样发送， 即一次发送一个报文。

接收方UDP对IP层交上来的UDP用户数据报，在去除首部后就原封不动地交付上层的应用进程，一次交付一个完整的报文。应用程序必须选择合适大小的报文。

若报文太长，UDP把它交给IP层后，IP层在传送时可能要进行分片，这会降低IP层的效率。若报文太短，UDP 把它交给IP 层后，会使IP数据报的首部的相对长度太大，这也降低了IP层的效率。

![Screenshot 2023-02-17 at 19.35.00](Typora_Picture/Screenshot%202023-02-17%20at%2019.35.00.png)



#### UDP checksum

**UDP checksum作用：确定当 UDP 报文段从源到达目的地移动时. 其中的比特是否发生了改变（只是检测错误，检测出来就丢弃这个报文，但是不能恢复这个报文）**

![Screenshot 2023-02-17 at 17.26.50](Typora_Picture/Screenshot%202023-02-17%20at%2017.26.50.png)

**Internet checksum: example 01**

注意:当数字相加时，在最高位的进位要回卷，再加到结果上（**回卷 wraparound**：前面溢出来的数，拉到最后再往上加）

目标端:校验范围+校验和=1111111111111111 通过校验，否则没有通过校验

注:求和时，必须将进位回卷到结果上

![Screenshot 2023-02-17 at 17.29.46](Typora_Picture/Screenshot%202023-02-17%20at%2017.29.46.png)



**Internet checksum: example 02**

假定我们有下面 3 个 16 比特的字:

<img src="Typora_Picture/Screenshot%202023-02-17%20at%2019.47.17.png" alt="Screenshot 2023-02-17 at 19.47.17" style="zoom:53%;" />

- 注意到最后一次加法有溢出，它要被回卷。
- 该和 0100101011000010 的反码运算结果是 1011010100111101 (反码运算就是将所有的 0 换成 1 所有的 1 转换成 0), 这就变为了检验和。 
- 在接收方，全部的4个16比特字(包括检验和) 加在一起，即 1011010100111101 (checksum) + 另外3个16比特字。
- 如果该分组中没有引入差错 ，则显然在接收方处该和将是1111111111111111。 如果这些比特有一个是 0, 那么我们就知道该分组中已经出现了差错 。



### 3.4 principles of reliable data transfer

可靠数据传输(rdt)的原理

数据的可靠传输是计算机网络中的通用概念，也是UDP和TCP的基石。计算机五层模型中，上层需要借助下层提供的功能来完成数据的传输，那么如果下层不可靠，我们该如何保证数据的可靠传输？

![Screenshot 2023-02-17 at 23.46.11](Typora_Picture/Screenshot%202023-02-17%20at%2023.46.11.png)

**(b) service implementation**

![Screenshot 2023-02-17 at 23.46.25](Typora_Picture/Screenshot%202023-02-17%20at%2023.46.25.png)

- 通过调用 rdt_send()函数，上层可以调用数据传输协议的发送方。它将要发送的数据可靠交付给位于接收方的较高层。
- 在接收端，当分组从信道的接收端到达时，将调用 rdt_rcv()。
- 当 rdt 协议想要向较高层交付数据时，将通过调用 deliver_data()来完成
- 除了交换含有待传送 的数据的分组之外，rdt 的发送端和接收端还需往返交换控制分组。rdt的发送端和接收端都要通过调用 udt_send()发送分组给对方

接下来会一步步假设，一步步的暴露问题，来看看可靠性传输RDT是如何演进的？只考虑 单向数据传输 (unidirectional data transfer)。但控制信息是双向流动的 (But control info will flow on both directions) 因为有反馈机制。

有限状态机 (Finite-State Machine. FSM) 来描述发送方和接收方



#### RDT 1.0 All reliable

**scenario: 下层的信道是完全可靠的 (没有比特差错，没有分组丢失)**

发送方和接收方的FSM：发送方将数据发送到下层信道，接收方从下层信道接收数据

所以rdt1.0做的工作就是<u>封装和解封装</u>

<img src="Typora_Picture/Screenshot%202023-02-17%20at%2023.59.18.png" alt="Screenshot 2023-02-17 at 23.59.18" style="zoom:50%;" />



#### RDT 2.0 Bit errors

**scenario: 下层信道可能出现差错 (underlying channel may flip bits in packet 分组中的比特可能翻转, 0变为1, 1变为0)**

应对手段：

- **checksum:** 用校验和的方式进行<u>差错检测</u> (error detection)

- **feedback:** send control msgs (ACK,NAK) from receiver to sender

  - **acknowledgements (ACKs):** 接收方显式的告诉发送方分组已经被接收 (no error scenario)

  - **negative acknowledgements (NAKs):** 接收方显式地告诉发送方分组出现了差错 (error scenario, 发送方接收到NAK后，会重传分组)

**过程描述：**发送方发送packet到下层信道，接收方接收，通过校验和发现数据有差错，返回NAK,发送方再次发送原packet；无差错返回ACK，发送方发送新的pactet。所以Rdt2.0新机制就是采用了差错控制编码进行差错检测

<u>**stop and wait (停等协议):** 发送方发送一个分组，然后等待接收方的应答。只有应答之后才会发送下一个分组。</u>

![Screenshot 2023-02-18 at 16.55.15](Typora_Picture/Screenshot%202023-02-18%20at%2016.55.15.png)

**存在问题 (fatal flaw):** ACK/NAK分组也可能出错/受损

所以引出了 Rdt 2.1



#### RDT 2.1 ACK/NAK corrupted

**scenario: 2.0 中接收方返回的 ACK/NAK 有可能出错，如果重传数据，还有可能重复。**

应对手段：

- **加上序号 (adds sequence number):** 给每个packet加上序号，哪怕客户端接收到重复数据，也能判断到重复。（比如说， 我们想要传的第一组分组接受方返回了很模糊的信号，我们的发送方管他三七二十一就再次发送这个分组，并且标序号为0证明他是上一个的重复。接收方可以发现这次重复的分组，如果他之前的分组有错的话就直接替换，如果没有错的话就丢弃）
- 停止等待：发送方只发送一个分组，然后等待接收方的应答的方式称为停止等待协议

**Sender:**

- 在分组中加入序列号，两个序列号(0，1) 就足够了，一次只发送一个未经确认 的分组
- 必须检测ACK/NAK是否出错(需要EDC )
- 状态数变成了两倍，必须记住当前分组的序列号为0还是1

![Screenshot 2023-02-18 at 17.00.18](Typora_Picture/Screenshot%202023-02-18%20at%2017.00.18.png)

**Receiver:**

- 必须检测接收到的分组是否是重复的，状态会指示希望接收到的分组的序号为0还是1
- 但是 receiver 并不知道 sender 是否正确收到了其ACK/NAK

![Screenshot 2023-02-18 at 17.02.25](Typora_Picture/Screenshot%202023-02-18%20at%2017.02.25.png)

- receiver 不知道它最后发送的 ACK/NAK 是否被正确地收到
- sender 不对收到的 ACK/NAK 给确认，没有所谓的确认的确认;
- 比如，receiver 发送 ACK，如果后面 receiver 收到的是: 老分组p0，则 ACK 错误。下一个分组P1，ACK 正确

![Screenshot 2023-02-18 at 17.07.06](Typora_Picture/Screenshot%202023-02-18%20at%2017.07.06.png)



#### RDT 2.2: NAK-free protocol

**scenario: 发送方需要识别ACK和NACK两套状态管理，太复杂了**

应对手段：

●取消NACK：取消了NACK的方式，那么接收方怎么告诉发送方数据错了呢？可以通过返回ACK+上一个packet的序号的方式返回。

●重复ACK：当接收方收到重复的ACK时，说明下一个packet发送失败了。接收方会重发当前ACK序号后的报文

![Screenshot 2023-02-18 at 17.20.56](Typora_Picture/Screenshot%202023-02-18%20at%2017.20.56.png)

![Screenshot 2023-02-18 at 17.21.35](Typora_Picture/Screenshot%202023-02-18%20at%2017.21.35.png)

存在问题：返回的ACK也有可能丢失，发送方就会一直等待确认。

所以引出了 Rdt3.0



#### RDT 3.0 Errors & loss

**scenario: 发送方会一直等待ACK，但是ACK有可能丢失，除了比特受损外 (Error)，底层信道还会丢包 (Loss)**

应对手段：

- **倒计数定时器 (countrlown timer):** 对应时间内没收到ACK就直接触发超时重传机制 (认为可能传输过程中 loss 了). 发送端超时重传:如果到时没有收到ACK->重传 (链路层的timeout时间确定的, 传输层timeout时间是适应式的)

存在问题：RDT3.0以及之前，一直采用停止等待协议，也就是一个包没收到响应就不会发送下一个，信道利用率太低。由此引入了流水线协议。

**sender:**

![Screenshot 2023-02-18 at 21.37.00](Typora_Picture/Screenshot%202023-02-18%20at%2021.37.00.png)

![Screenshot 2023-02-18 at 21.24.37](Typora_Picture/Screenshot%202023-02-18%20at%2021.24.37.png)

- 过早超时(延迟的ACK)也能够正常工作; 但是效率较低，一半的分组和确认是重复的;
- 设置一个合理的超时时间也是比较重要的;

![Screenshot 2023-02-18 at 21.25.12](Typora_Picture/Screenshot%202023-02-18%20at%2021.25.12.png)





#### RDT 3.0 stop-and-wait operation 

rdt3.0可以工作，但链路容量比较大的情况下，性能很差。链路容量比较大，一次发一个PDU 的不能够充分利用链路的传输能力

example:

- 在这两个端系统之间的光速 **往返传播时延RTT大约为30毫秒**。
- 假设 ACK 分组很小(以便我们可以忽略其发送时间)，接收方一旦收到一个数据分组的最后 1 比特后立即发送 ACK
- 假定彼此通过一条**发送速率R为 1 Gbps (每秒10^9比特)**的信道相连 。 
- 包括首部字段和数据的**分组长 L 为 1000 字节 (8000 比特)**，发送一个分组进入 1 Gbps 链路实际所需时间是:

![Screenshot 2023-02-19 at 00.51.06](Typora_Picture/Screenshot%202023-02-19%20at%2000.51.06.png)

![Screenshot 2023-02-19 at 00.50.44](Typora_Picture/Screenshot%202023-02-19%20at%2000.50.44.png)

![Screenshot 2023-02-19 at 00.52.16](Typora_Picture/Screenshot%202023-02-19%20at%2000.52.16.png)



#### RDT 3.0 Pipelined protocols 

**流水线协议 (Pipelined protocols):** 为了提高信道的利用率，我们需要能够批量发送分组。当发送方窗口>1,我们称之为流水线协议。

- **range of sequence numbers must be increased ([0,1] => [0, N-1])**. 增加序号的范围，用多个bit表示分组的序号
- 所需序号范围和对缓冲的要求取决于数据传输协议如何处理丢失、损坏及延时过大的分组。解决流水线的差错恢复有两种基本方法是 **回退N步(Go-Back- N, GBN)** 和 **选择重传(Selective Repeat, SR)**
- **buffering at sender and/or receiver.** 在发送方/接收方要有缓冲区
  - sender buffer: 缓冲那些已发送但没有确认的分组，可能需要重传
  - receiver buffer: 缓存那些巳正确接收的分组，上层用户取用数据的速率 ≠ 接收到的数据速率。接收到的数据可能乱序，排序交付(可靠)

![Screenshot 2023-02-19 at 02.08.23](Typora_Picture/Screenshot%202023-02-19%20at%2002.08.23.png)

![Screenshot 2023-02-19 at 02.09.52](Typora_Picture/Screenshot%202023-02-19%20at%2002.09.52.png)



##### GBN (Go-Back-N)

先明白一个概念 **WS (window size)** 代表可发送，或者可接收的窗口的长度。

- 在 stop-and-wait operation 中，发送方只能发送一个分组，等待确认后，再发送下一个，所以：发送方窗口=1，接收方窗口=1。
- 但是在 Pipelined protocols 中的 GBN (Go-Back-N)，那些已被发送但还未被确认的分组的许可序号范围可以被看成是一个在序号范围内长度为 N 的窗口 。随着协议的运行，该窗口在序号空间向前滑动。因此，N 常被称为窗口长度 (window size) 。接收方窗口=1，发送方窗口=N。
- GBN 协议也常被称为 **滑动窗口协议 (sliding-window protocol)** 



###### sending window

![Screenshot 2023-02-19 at 02.21.28](Typora_Picture/Screenshot%202023-02-19%20at%2002.21.28.png)

假设一开始没有发送任何一个分组, **window size = 5**

![Screenshot 2023-02-19 at 03.12.43](Typora_Picture/Screenshot%202023-02-19%20at%2003.12.43.png)

**如果发送 packet 0 1 2 3 4, nextseqnum(前沿) 往后移5位:**

![Screenshot 2023-02-19 at 03.13.01](Typora_Picture/Screenshot%202023-02-19%20at%2003.13.01.png)

**收到 packet 0 的确认(ACK), send_base(后延) 往后移1位:**

![Screenshot 2023-02-19 at 03.13.39](Typora_Picture/Screenshot%202023-02-19%20at%2003.13.39.png)

**如果收到 packet 1 2 3 4 的确认(ACK), send_base(后延) 往后移4位:**

![Screenshot 2023-02-19 at 03.18.41](Typora_Picture/Screenshot%202023-02-19%20at%2003.18.41.png)



###### receiving window

接收窗口 (receiving window) = 接收缓冲区

![Screenshot 2023-02-19 at 12.32.49](Typora_Picture/Screenshot%202023-02-19%20at%2012.32.49.png)



- **sender sets timer for oldest in-flight pkt:** 发送方只为最早的未经确认的分组维护一个定时器，如果产生超时，将重新发送该分组后的所有分组，也就是顾名思义的回退N步。
- **discard (don’t buffer) out-of-order pkt 丢弃乱序:** 接收方窗口只有1，如果接收到比较大的序号分组，都会选择丢弃。

- **在接收端，乱序的不缓存**。因此哪个n分组丢失了GB到那个分组n，即使n以后的分组传送都是正确的

![Screenshot 2023-02-19 at 02.27.48](Typora_Picture/Screenshot%202023-02-19%20at%2002.27.48.png)

<img src="Typora_Picture/Screenshot%202023-02-19%20at%2012.41.20.png" alt="Screenshot 2023-02-19 at 12.41.20" style="zoom:45%;" />



##### SR (Selective Repeat)

接收方窗口=N，发送方窗口=N。

- **sender maintains timer for each unacked packet:** 发送方为**每个分组**都设置了重传定时器，发送方只重发那些没有收到 ACK 的packets. 接收方单独确认所有正确接收的 packets. 

- **out-of-order to buffer:** 接收方可以乱序接收分组，当最头部分组整体接收完毕，滑动窗口可以整体后移。收到乱序分组可以缓存packets，以便最终 in-order delivery to upper layer (按顺序交付给上层)。也就是说，packet 有序：交给上层。无序：先缓存，等有序了再交给上层

![Screenshot 2023-02-19 at 12.29.55](Typora_Picture/Screenshot%202023-02-19%20at%2012.29.55.png)

![Screenshot 2023-02-20 at 16.02.34](Typora_Picture/Screenshot%202023-02-20%20at%2016.02.34.png)

![Screenshot 2023-02-20 at 15.41.22](Typora_Picture/Screenshot%202023-02-20%20at%2015.41.22.png)



##### Pipelined Summary

![Screenshot 2023-02-20 at 15.16.31](Typora_Picture/Screenshot%202023-02-20%20at%2015.16.31.png)

![Screenshot 2023-02-17 at 23.37.54](Typora_Picture/Screenshot%202023-02-17%20at%2023.37.54.png)



### 3.5 connection-oriented transport: TCP

既然我们已经学习了可靠数据传输的基本原理，我们就可以转而学习 TCP 了。TCP 是因特网运输层的面向连接的可靠的运输协议。我们在本节中将看到，为了提供可靠数据传输，TCP依赖于前一节所讨论的许多基本原理、其中包括差错检测、重传、累积确认、定时器以及用于序号和确认号的首部字段。TCP 定义在 RFC 793、 RFC 1122、 RFC 1323、 RFC 2018 以及 RFC 2581 中。

![Screenshot 2023-02-20 at 19.58.31](Typora_Picture/Screenshot%202023-02-20%20at%2019.58.31.png)



#### TCP segment structure

与 UDP 一 样，TCP 首部包括源端口号和目的端口号 ，它被用于多路复用/分解来自或送到上层应用的数据。另外，同UDP一样，TCP 首部也包括**检验和字段 (checksum field)**。 TCP 报文段首部还包含下列字段 :

- **32 bits 的序号字段 (sequence number field):** TCP连接中传送的数据流中的每一个字节都编上一个序号。序号字段的值则指的是本报文段所发送的数据的第一个字节的序号。
- **32 比特的确认号字段 (acknowl­ edgment number field): **是期望收到对方的下一个报文段的数据的第一个字节的序号。
- **16 bits 的接收窗口字段 (receive window field ):** 该字段用于流量控制。作为接收方让发送方设置发送窗口的依据，单位为字节。窗口值经常在动态变化着，此字段明确指出现在允许对方发送的数据量。注意：不是滑动窗口的大小，滑动窗口的大小是固定的，他是用来记录接受缓冲区的大小，如果大小为0，就不会发送数据了。以此达到流量控制。
- **4 bits 的首部长度字段 (header length field):** 该字段指示了以 32 比特的字为单位的 TCP 首部长度。由于 TCP 选项字段的原因， TCP 首部的长度是可变的。(通常 选项字段为空 ，所以 TCP 首部的典 型长度是 20 字节)
- **可选与变长的选项字段 (options field): **该字段用于发送方与接收方 **协商最大报文段长度 (MSS)** 时，或在高速网络环境下用作窗口调节因子时使用 。 首部字段中还定义了一个时间戳选项。可参见 RFC 854 和 RFC 1323 了解其他细节。
  - **MSS (Maximum Segment Size) 是TCP 报文段中的数据字段的最大长度。 数据字段加上TCP 首部才等于整个的TCP 报文段。 所以，MSS是“TCP 报文段长度减去TCP 首部长度。**
- **6 bits的标志字段 (flag field):**  
  - **紧急URG:** 当URG=1时，表明紧急指针字段有效。它告诉系统此报文段中有紧急数据，应尽快传送(相当于高优先级的数据)。
  - **确认ACK:** 只有当ACK =1时确认号字段才有效。当ACK =0 时，确认号无效。
  - **推送PSH (PuSH):** 接收TCP收到 PSH =1的报文段，就尽快地交付接收应用进程，而不再等到整个缓存都填满了后再向上交付。
  - **复位 RST (ReSeT):** 当 RST=1时，表明TCP连接中出现严重差错（如由于主机崩溃或其他原因 ），必须释放连接，然后再重新建立运输连接。
  - **同步SYN:** 同步SYN=1表示这是一个连接请求或连接接受报文。 与ACK配合实现。
  - **终止FIN (FINish):** 用来释放一个连接。FIN=1表明此报文段的发送端的数据已发送完毕，并要求释放运输连接。
- 所以，响应ACK = 请求SEQ + 请求字节数

![Screenshot 2023-02-20 at 20.02.58](Typora_Picture/Screenshot%202023-02-20%20at%2020.02.58.png)



##### TCP sequence number, ACK

- **TCP sequence number: **segment 的第一个字节在 data stream 的编号，代表当前报文的发送序号。
- **ACK:** 期望从另一方收到的下一个字节的序号，累积确认。代表接收方需要的数据将从对方哪个序号开始。

![Screenshot 2023-02-20 at 20.05.14](Typora_Picture/Screenshot%202023-02-20%20at%2020.05.14.png)

##### TCP序号和确认号之间的关系

之前讲的都是单向传递，在这里 Telnet 是双向数据传递，互相发送数据和确认，两个互为接受方和发送方。

作为接收方a对上一次b发送的数据的确认。Seq是自己传给对方的字节流的数据开始点 (序号)，Ack是希望对方传给自己的字节流开始点 (确认号)。 客户端发出的每一个字符到了服务器，服务器要回转回来，然后客户端要给出相应的确认。

假设客户和服务器的起始序号分别是 42 和 79。 前面讲过，一个报文段的序号就是该 报文段数据字段首字节的序号 。 因此，客户发送的第一个报文段的序号为 42, 服务器发送的第一个报文段的序号为 79。 前面讲过，确认号就是主机正在等待的数据 的下一个字节序 号 。 在 TCP 连接建立后但没有发送任何数据之前，该客户等待字节 79, 而该服务器等待字节 42。

- Host A: 

  - 在它的数据字段里包含一字节的字符 'A' 的 ASCII 码。

  - 第一个报文段的序号字段里是 42。

  - 另外，由于 A 还没有接收到来自 B 的任何数据，因此该第一个报文段中的确认号字段中是 79。即，当前的报文段数据是从第42个字节开始，希望从B那里获取从第79个字节开始的报文段

- Host B: 

  - 首先它是为所收到数据提供一个确认，通过在确认号字段中填入 43, 告诉 A 它已经成功地收到 字节 42 及以前的所有字节，现在正等待着字节 43 的出现。

  - 该报文段的第二个目的是回显字符'B'。因此，在第二个报文段的数据字段里填入的是字符 'B' 的 ASCII 码。

  - 第二个报文段的序号为 79, 它是该 TCP 连接上从服务器到客户的数据流的起始序号，这也正是 B 要发送的第一个字节的数据。即，收到42。返回ACK43 (接收到了42号及以前的报文，希望从A那里获取从第43个字节开始的报文段), 并且发送第79个报文

- Host A: 该报文段的数据字段为空。收到79之后，返回ACK80，说我接受到了字节流中序号为 79 及以前的字节，希望你发送下一个从80开始的，并且发送第43个报文

<img src="Typora_Picture/Screenshot%202023-02-18%20at%2021.43.01.png" alt="Screenshot 2023-02-18 at 21.43.01" style="zoom: 50%;" />



##### TCP round trip time, timeout

- **Problem:** TCP 和 rdt 协议一样采用超时/重传机制来处理报文段的丢失问题。但是问题就是定时器的超时时间设置。
- **设置 timeout 的间隔必须 > RTT**

![Screenshot 2023-02-20 at 22.17.18](Typora_Picture/Screenshot%202023-02-20%20at%2022.17.18.png)



###### EstimatedRTT

- **SampleRTT:** 比如发了50个报文，我抽取的5个报文作为SampleRTT进行统计。
- **EstimatedRTT:** SampleRTT的均值，一旦获得一个新 SampleR'IT 时，TCP 就会根据下列公式来更新EstimatedRTT

![Screenshot 2023-02-20 at 23.06.26](Typora_Picture/Screenshot%202023-02-20%20at%2023.06.26.png)

![Screenshot 2023-02-20 at 23.07.26](Typora_Picture/Screenshot%202023-02-20%20at%2023.07.26.png)

EstimatedRTT 是 一个 SampleRIT 值的加权平均值。这个加权平均 对最近的样本赋予的权值要大于对旧样本赋予的权值。这是很自然的，因为越近的样本越能更好地反映网络的当前拥塞情况

从统计学观点讲，这种平均被称为 **指数加权移动平均 (Exponential Weighted Moving Average, EWMA)** 。 在 EWMA中的"指数"一词看起来是指一个给定的 SampleRTT 的权值在更新的过程中呈指数型快速衰减

下图显示了当 a= 1/8 时，在 gaia cs. umass. edu (在美国马萨诸塞州的 Amherst) 与 fantasia eurecom. fr (在法国南部)之间的 一 条 TCP 连接上的 SampleRTT 值与 Estimate­dRTT的值。显然SampleRTT 的变化在 EstimaLedRTT 的计算中趋于平缓了 。

![Screenshot 2023-02-20 at 23.13.39](Typora_Picture/Screenshot%202023-02-20%20at%2023.13.39.png)



###### DevRTT

使用DevRTT的原因是我们想要一个更好的 safety margin

- 除了估算RTT外，测量RTT的变化也是有价值的。
- [RFC6298] 定义了 **RTT偏差DevRTT**, 用于估算 SampleRTT一般会偏离 EstimatedRTT 的程度:
- 就是先计算一个往返时间的估计值，在此基础上加上一个偏差范围的四倍，相当于计算了短时间内能覆盖99%以上情况的超时时间

![Screenshot 2023-02-20 at 23.19.42](Typora_Picture/Screenshot%202023-02-20%20at%2023.19.42.png)



#### TCP reliable data transfer

TCP是一种流水线的传输方式，那么TCP属于GBN 还是属于SR呢，其实TCP是GBN和SR的混合体。

![Screenshot 2023-02-20 at 23.44.15](Typora_Picture/Screenshot%202023-02-20%20at%2023.44.15.png)

![Screenshot 2023-02-21 at 00.00.47](Typora_Picture/Screenshot%202023-02-21%20at%2000.00.47.png)

- 顺序接收：因为有了分组编号，接收方收到乱序的分组后，不会选择丢弃，而是缓存起来，排好序。返回的ACK仍然是第一个未收到的分组序号。
- 超时重传：tcp发送方只为最早的分组设置一个定时器，当分组未收到ACK触发超时重传，并获得ACK应答后，才开始为下一个未确认分组开始计时。
- 选择确认：发送方未接收到分组的ACK时，只会重新发送单个分组，而不会发送所有分组。



##### TCP: retransmission scenarios

<img src="Typora_Picture/Screenshot%202023-03-08%20at%2013.26.16.png" alt="Screenshot 2023-03-08 at 13.26.16" style="zoom:40%;" />

<img src="Typora_Picture/Screenshot%202023-03-08%20at%2013.26.27.png" alt="Screenshot 2023-03-08 at 13.26.27" style="zoom:40%;" />



##### TCP fast retransmit

快速重传 (TCP fast retransmit)：基于接收方ACK确认机制，ACK序号为按顺序第一个未收到的分组。**发送方接收到三次相同的ACK序号后，会触发快速重传机制**，重传ACK序号标识的分组。

<img src="Typora_Picture/Screenshot%202023-03-17%20at%2013.18.15.png" alt="Screenshot 2023-03-17 at 13.18.15" style="zoom:40%;" />





#### TCP flow control

- 一般来说，我们总是希望数据传输得更快一些
- 但如果**发送方把数据发送得过快，接收方就可能来不及接收，这就会造成数据的丢失**
- 所谓**流量控制(flow control）就是让发送方的发送速率不要太快，要让接收方来得及接收**
- 利用**滑动窗口机制 (rwnd) **可以很方便地在TCP连接上实现对发送方的流量控制。
  - TCP接收方利用自己的接收窗口的大小来限制发送方发送窗口的大小。
  - TCP发送方收到接收方的 rwnd = 0 通知后，应启动持续计时器。持续计时器超时后，向接收方发送 rwnd 探测报文。

- TCP发送方的发送窗口 = min {自身拥塞窗口，TCP接收方的接收窗口}

<img src="Typora_Picture/Screenshot%202023-03-17%20at%2013.45.18.png" alt="Screenshot 2023-03-17 at 13.45.18" style="zoom:30%;" />

**Example:**

initial 发送窗口 = 400, -> initial rwnd = 400

<img src="Typora_Picture/Screenshot%202023-03-17%20at%2013.29.26.png" alt="Screenshot 2023-03-17 at 13.29.26" style="zoom:50%;" />

![Screenshot 2023-03-17 at 13.30.39](Typora_Picture/Screenshot%202023-03-17%20at%2013.30.39.png)

TCP发送方收到接收方的 rwnd = 0 通知后，应启动持续计时器。持续计时器超时后，向接收方发送 rwnd 探测报文。

![Screenshot 2023-03-17 at 13.31.30](Typora_Picture/Screenshot%202023-03-17%20at%2013.31.30.png)





### 3.6 TCP congestion control

有时，发送方和接收方性能后很好，结果是中途的网络带宽不行，网络中堵塞了。这时候如果还是依然大量的发送消息，反而会造成更大面积的网络拥塞。

- manifestations (表现为):

  - lost packets (buffer overflow at routers) 丢包 (路由器缓冲区溢出)

  - long delays (queueing in router buffers) 长时间延迟 (在路由器缓冲区排队)

#### TCP Tahoe

- slow-start
- congestion avoidance

![Screenshot 2023-03-17 at 13.34.43](Typora_Picture/Screenshot%202023-03-17%20at%2013.34.43.png)



#### TCP Reno

- fast retransmit
- fast recovery

有时，个别报文段会在网络中丢失，但实际上网络并未发生拥塞。这将导致发送方超时重传，并误认为网络发生了拥塞，发送方把拥塞窗口cwnd又设置为最小值1，并错误地启动慢开始算法，因而降低了传输效率。

- 采用快重传算法可以让发送方尽早知道发生了个别报文段的丢失。

- 所谓快重传，就是使发送方尽快进行重传，而不是等超时重传计时器超时再重传。
  - 要求接收方不要等待自己发送数据时才进行捎带确认，而是要立即发送确认；
  - 即使收到了失序的报文段也要立即发出对已收到的报文段的重复确认。
  - 发送方一旦收到3个连续的重复确认，就将相应的报文段立即重传，而不是等该报文段的超时重传计时器超时再重传。

之前的例子中，当拥塞窗口值 cwnd = 24 时发生了超时重传，而此时网络并没有发生拥塞，但是发送方却误认为网络发生了拥塞，于是发送方把拥塞窗口 cwnd 减少到 1，并错误的启动慢开始算法，降低了传输效率。

![Screenshot 2023-03-17 at 13.38.47](Typora_Picture/Screenshot%202023-03-17%20at%2013.38.47.png)



![Screenshot 2023-03-17 at 13.42.38](Typora_Picture/Screenshot%202023-03-17%20at%2013.42.38.png)



## <u>04. Network (Data Plane) 端到端</u>

Network layer 将 段(segment) 从一台发送主机移动到一台接收主机，是**主机之间的逻辑通信**，能够被分解为两个相互作用的部分，即 **data plane (数据平面)** 和 **control plane (控制平面)**

Two key network-layer functions:

- forwarding: 将分组从路由器的输入接口转发到合适的输出接口，通过单个路口的过程。就是说从不同的端口收来的分组，然后通过合适的端口打出去。是局部功能（转发是在数据平面中实现的唯一功能）
- routing: 使用路由算法来决定分组从发送主机到目标接收主机的路径，从出发地到目的地的行程规划过程。是全局功能。（路由选择在网络层的控制平面中实现）

![Screenshot 2023-03-18 at 00.27.49](Typora_Picture/Screenshot%202023-03-18%20at%2000.27.49.png)

<img src="Typora_Picture/Screenshot%202023-03-17%20at%2023.54.53.png" alt="Screenshot 2023-03-17 at 23.54.53" style="zoom:40%;" />



### 4.1 Overview of network layer

<img src="Typora_Picture/Screenshot%202023-03-18%20at%2000.38.12.png" alt="Screenshot 2023-03-18 at 00.38.12" style="zoom:50%;" />

#### data plane

- 本地，每个路由器功能
- 确定到达路由器输入端口的 datagram 如何 **forward** 到路由器输出端口
- 转发功能:
  - 传统方式：基于目标地址 + 转发表
  - SDN方式：基于多个字段 + 流表

<img src="Typora_Picture/image-20230318002806489.png" alt="image-20230318002806489" style="zoom:60%;" />



#### control plane

- network-wide logic (网络范围内的逻辑)

- 确定 datagram 如何沿着从源主机到目标主机的 end-to-end 路径在路由器之间路由

- two control-plane approaches:

  - **traditional routing algorithms(Per-router):** implemented in routers (在路由器中实现)

    在每一个路由器中的单独路由器算法元件，在控制平面进行交互

    <img src="Typora_Picture/Screenshot%202023-03-18%20at%2000.31.28.png" alt="Screenshot 2023-03-18 at 00.31.28" style="zoom:40%;" />

  - **software-defined networking (SDN):** implemented in (remote) servers (在远程的服务器中实现)

    一个不同的 (通常是远程的) controller interacts with local control agents (CAs) 

    <img src="Typora_Picture/Screenshot%202023-03-18%20at%2000.34.44.png" alt="Screenshot 2023-03-18 at 00.34.44" style="zoom:45%;" />



### 4.2 What’s inside a router 

Router architecture overview (路由器体系架构):

![Screenshot 2023-03-18 at 16.02.35](Typora_Picture/Screenshot%202023-03-18%20at%2016.02.35.png)



#### Input port functions:

- link layer 把frame当中的数据部分提取出来数据部分 (可能是一个IP的分组) 
- 交给 network layer 实体中的队列 (**queuing**: if datagrams arrive faster than forwarding rate into switch fabric (queueing delay and loss due to input buffer overflow))
- 排到对头后按照路由处理器交下来的路由表，找到合适的端口，把它放出去 (**根据 header field values**，使用输入端口内存中的转发表查找输出端口(“匹配+动作”))，**完成输入端口处理**
  - **destination-based forwarding (传统转发方式):** 根据 datagram 头部的目标IP地址，来查路由表转发
  - **generalized forwarding (SDN):** 查这个分组的多个层面的头部信息，匹配相应流表的字段，然后找到匹配的流表来action
- 通过fabric做一个局部的交换，从输入端口转到输出端口。

![Screenshot 2023-03-18 at 17.04.21](Typora_Picture/Screenshot%202023-03-18%20at%2017.04.21.png)

#### Input port queuing

所以分组有可能会因为其他分组正在输出同一个端口等待而导致堵塞，如果一直堵着有可能会造成丢失

所以说 network layer 输入端口缓存的目的就是为了匹配瞬间的输入速率和输出速率的不一致性，需要一个queue来匹配不一致性

<img src="Typora_Picture/Screenshot%202023-03-18%20at%2017.49.58.png" alt="Screenshot 2023-03-18 at 17.49.58" style="zoom:40%;" />



#### Switching fabrics

- 然后我们来看一下**fabric**怎么样 **将 packet 从 input buffer 传输到合适的 output buffer**
- **switching rate:** 分组可以按照 switching rate 从输入传输到输出
  - 运行速度经常是输入/输出链路速率的**若干倍**，如果有N 个输入端口，交换机构的  switching rate 必须是输入线路速度的N倍，才不会成为瓶颈
- 有三种常见的fabric的工作模式:

![Screenshot 2023-03-18 at 17.58.08](Typora_Picture/Screenshot%202023-03-18%20at%2017.58.08.png)

##### Switching via memory

- 第一代路由器就是在CPU直接控制下的交换，采用传统的计算机
- 分组被拷贝到系统内存，CPU从分组的头部提取出目标地址，查找转发表，找到对应的输出端口，拷贝到输出端口
- Problems:
  - 转发速率被内存的带宽限制 (**datagram 通过BUS两遍**)，所以 系统总线(bus) 本身就会成为fabric交换速度的瓶颈，带宽每分钟交换或者是转发分组的速率很低
  - 一次只能转发一个分组

![Screenshot 2023-03-18 at 18.07.48](Typora_Picture/Screenshot%202023-03-18%20at%2018.07.48.png)



##### Switching via a bus

- datagram 只要通过一次 share bus (共享总线，不是系统总线)，从输入端口转发到输出端口
- Problem:
  - bus contention (总线竞争): 交换速度受限于总线带宽
  - 1次处理一个分组
  - 对于接入或企业级路由器速度足够 (但不适合区域或骨干网络)

![Screenshot 2023-03-18 at 18.16.52](Typora_Picture/Screenshot%202023-03-18%20at%2018.16.52.png)



##### Switching via interconnection network

- 通过互联网络 (Banyan, crossbar等) 的交换，将多个处理器连接成多处理器，同时并发转发多个分组，克服总线带宽限制
- 当分组从左上角端口到达，转给下面端口; 控制器短接相应的两个总线
- advanced design: 将数据报分片为**固定长度的信元**，通过交换网络交换

![Screenshot 2023-03-18 at 18.21.11](Typora_Picture/Screenshot%202023-03-18%20at%2018.21.11.png)



#### destination-based forwarding (传统转发方式):

![Screenshot 2023-03-18 at 17.28.41](Typora_Picture/Screenshot%202023-03-18%20at%2017.28.41.png)

##### Longest prefix matching 最长前缀匹配

![Screenshot 2023-03-18 at 17.36.00](Typora_Picture/Screenshot%202023-03-18%20at%2017.36.00.png)



#### Output ports & queueing

![Screenshot 2023-03-18 at 18.54.51](Typora_Picture/Screenshot%202023-03-18%20at%2018.54.51.png)

![Screenshot 2023-03-18 at 19.03.13](Typora_Picture/Screenshot%202023-03-18%20at%2019.03.13.png)



### 4.3 IP: Internet Protocol

#### IPv4 addressing

**IP = 网络号＋主机号**，IP 地址具有以下结构： 

- **subnet part (网络号，子网部分):** devices in same subnet have common **high order bits**
- **host part (主机号，主机部分):** remaining **low order bits** 

首先要知道的是 IP地址 不能标识主机 或者 路由器本身，而是一个 **interface (接口)**，主机/路由器上的链路层接口

![Screenshot 2023-03-18 at 19.13.50](/Users/chenziyang/Desktop/Typora_Picture/Screenshot%202023-03-18%20at%2019.13.50.png)

#### Subnets

- 不需要经过 intervening router (中间的路由器)，就可以物理上相互到达的 device interfaces (设备接口)
- 通过在主机号字段中拿一部分作为子网号，把两级 IP 地址划分为三级 IP 地址。
- IP 地址 = {< 网络号 >, < 子网号 >, < 主机号 >}

<img src="/Users/chenziyang/Desktop/Typora_Picture/Screenshot%202023-03-18%20at%2022.11.04.png" alt="Screenshot 2023-03-18 at 22.11.04" style="zoom:40%;" />

/24 代表前面24位，高位的24位是网络号，意味着后面8位数是主机号

![Screenshot 2023-03-18 at 22.13.07](/Users/chenziyang/Desktop/Typora_Picture/Screenshot%202023-03-18%20at%2022.13.07.png)



#### IP Datagram format

![Screenshot 2023-03-19 at 00.14.18](/Users/chenziyang/Desktop/Typora_Picture/Screenshot%202023-03-19%20at%2000.14.18.png)



#### IP 分片和重组(Fragmentation & Reassembly)

- **网络链路有MTU (最大传输单元)** –链路层帧所携带的最大数据长度

  <center>
    <img src="/Users/chenziyang/Desktop/Typora_Picture/Screenshot%202023-03-19%20at%2000.34.11.png" alt="Screenshot 2023-03-19 at 00.34.11" style="zoom:50%;" />
    <img src="/Users/chenziyang/Desktop/Typora_Picture/Screenshot%202023-03-19%20at%2000.36.47.png" alt="Screenshot 2023-03-19 at 00.36.47" style="zoom:50%;" />

- 不能直接分片

  - 分片后加上头部，相同的ID
  - offset (偏移量) 当作序号，第一个分组的 offset = 0，第二个分组的 offset = 1480bits = 185Bytes，第二个分组的 offset = 2960bit = 370Bytes

  <img src="/Users/chenziyang/Desktop/Typora_Picture/Screenshot%202023-03-19%20at%2000.40.37.png" alt="Screenshot 2023-03-19 at 00.40.37" style="zoom:50%;" />

  ![Screenshot 2023-03-19 at 00.46.10](/Users/chenziyang/Desktop/Typora_Picture/Screenshot%202023-03-19%20at%2000.46.10.png)

![Screenshot 2023-03-19 at 00.31.29](/Users/chenziyang/Desktop/Typora_Picture/Screenshot%202023-03-19%20at%2000.31.29.png)



#### Host如何获得一个IP地址?

两种方法:

- **config file:** 系统管理员将地址配置在一个文件中

  - Wintel: control-panel -> network -> configuration -> tcp/ip -> properties

  - UNIX: /etc/rc.config

- **DHCP:** Dynamic Host Configuration Protocol: 从服务器中动态获得一个IP地址 (plug-and-play)



#### DHCP: Dynamic Host Configuration Protocol (UDP)

- 以便使用DHCP分配即插即用IP地址，网络将需要有一个DHCP服务器来执行该功能
- 当有一个客户端出现，他是一个想要IP地址的主机，将从DHCP服务器请求并接收IP地址，使用DHCP协议。
- 当主机离开网络时，他会放弃他的IP地址，然后可以被另一个主机重用或回收，或者可能由该主机在以后的时间点续订。

- **作用: 允许主机在加入网络的时候，动态地从服务器那里获得IP地址**
  - 可以更新对主机在用IP地址的租用期-租期快到了
  - 重新启动时，允许重新使用以前用过的IP地址
  - 支持移动用户加入到该网络(短期在网)



通常DHCP服务器将配置在路由器中，并为该路由器所连接的所有子网提供服务

![Screenshot 2023-03-19 at 17.03.16](/Users/chenziyang/Desktop/Typora_Picture/Screenshot%202023-03-19%20at%2017.03.16.png)



##### 4 important DHCP message overview:

- <u>host broadcasts (主机广播): **DHCP discover message**</u> [optional] （广播：DHCP server在那里嘛）
- <u>DHCP server responds (DHCP服务器提供报文相应): **DHCP offer message**</u> [optional] （我是DHCP server，这是你可以用的IP）
- <u>host requests IP address (主机请求IP地址): **DHCP request message **</u> （好的，我接受这个IP地址）
- <u>DHCP server sends address (DHCP服务器发送地址): **DHCP ack message**</u> （好的，你现在拥有这个IP地址）

<img src="Typora_Picture/Screenshot%202023-03-19%20at%2017.26.04.png" alt="Screenshot 2023-03-19 at 17.26.04" style="zoom:40%;" />

##### DHCP: 不仅仅可以返回IP addresses

- DHCP can return allocated **IP address** on subnet (可以返回IP地址)
- **address of first-hop router** for client (第一跳路由器的IP地址)
- **name and IP address of DNS sever** (DNS服务器的域名和IP地址)
- **network mask** (子网掩码，为了划分网络号和主机号的)

<img src="Typora_Picture/Screenshot%202023-03-19%20at%2021.09.46.png" alt="Screenshot 2023-03-19 at 21.09.46" style="zoom:30%;" />



#### 一个ISP如何获得一个地址块?

**ICANN: Internet Corporation for Assigned Names and Numbers**

- 分配 addresses
- 管理 DNS
- 分配 domain names，解决冲突



## <u>05. Network (Control Plane)</u>

我们将关注单个路由器在每个路由器函数的数据平面中到更广泛的网络视图，研究路由问题，比如说如何确定从原地址到目的地，我们还将研究网络管理和网络配置的问题。

![Screenshot 2023-03-19 at 21.24.40](Typora_Picture/Screenshot%202023-03-19%20at%2021.24.40.png)



### 5.1 Intro: control plane

2 种构建 network control plane 的方法:

- per-router control (traditional)
- logically centralized control (software defined networking)



### 5.2 routing protocols

- **routing:** 路由就是计算从一个网络到其他网络如何走的问题，按照某种指标 (传输延迟,所经过的站点数目等) 找到一条从源节点到目标节点的较好路径

- 任何路由算法的目标都是确定一条好的路径或一条好的路由:


![Screenshot 2023-03-19 at 21.37.28](Typora_Picture/Screenshot%202023-03-19%20at%2021.37.28.png)

![Screenshot 2023-03-19 at 22.09.35](Typora_Picture/Screenshot%202023-03-19%20at%2022.09.35.png)



#### Routing algorithm classification

Routing algorithm 分为 Static or Dynamic，也可以分为 Global or Decentralized.

尽管它们有相同的共同目标，即计算最短路径，最小成本路径，但他们实际上计算最短路径的方式不一样:

- **Static**: routes change **slowly** over time
- **Dynamic**: routes change more **quickly**，周期性更新，根据链路代价的变化而变化
- **Global/centralized**: all routers 拥有完整的拓扑(topology) 和边(link)的代价的信息，算法必须知道网络中每个链路的成本 (**"link state"** algorithms)
- **Decentralized**: 路由器只知道与它有物理连接关系的邻居路由器，路由器以迭代、分布式的方式计算出最低开销路径 。 没有节点拥有关于所有网络链路开销的完整信息 (**"distance vector"** algorithms)

![Screenshot 2023-03-20 at 11.14.21](Typora_Picture/Screenshot%202023-03-20%20at%2011.14.21.png)



#### 5.2.1 Link state (Dijkstra)

**缺点:** Dijkstra算法起初选了一个最优的path，于是都用这个path传，最后会导致这个path的堵塞，Dijkstra算法就会继续选择另一个最优的path......一直这样反反复复，切换path的行为就叫做路径的振荡

Dijkstra’s link-state routing algorithm

- 链路状态算法中，每个结点 (经广播) 与所有其他结点交谈，但它仅告诉它们与它直接相连链路的费用。

- **centralized**: network **topology**, **所有节点都知道每个链路的成本**，通过“link state broadcast” 实现，**所有节点具有相同信息**
- **computes least cost paths** from one node (“source”) to all other nodes
  - gives **forwarding table** for that node
- **iterative**: after *k* iterations, know least cost path to *k* destinations

2类节点:

- **临时节点(tentative node):** 还**没有**找到从源节点到此节点的最优路径的节点
- **永久节点(permanent node) N’:**已经**找到了**从源节点到此节点的最优路径的节点

<img src="Typora_Picture/Screenshot%202023-03-20%20at%2011.58.33.png" alt="Screenshot 2023-03-20 at 11.58.33" style="zoom:40%;" />

![Screenshot 2023-03-20 at 22.52.56](Typora_Picture/Screenshot%202023-03-20%20at%2022.52.56.png)

**algorithm complexity**: n nodes, each iteration needs to check all nodes, w, not in N’, n(n+1)/2 comparisons: O(n2)

![Screenshot 2023-03-20 at 14.19.50](Typora_Picture/Screenshot%202023-03-20%20at%2014.19.50.png)

##### *Examples 01*

![Screenshot 2023-03-20 at 23.38.55](Typora_Picture/Screenshot%202023-03-20%20at%2023.38.55.png)

##### *Examples 02*

![Screenshot 2023-03-22 at 12.24.15](Typora_Picture/Screenshot%202023-03-22%20at%2012.24.15.png)

##### *Examples 03*

![Screenshot 2023-03-20 at 23.31.13](Typora_Picture/Screenshot%202023-03-20%20at%2023.31.13.png)



##### *Examples 04*

Consider the network below. Please use Dijkstra’s shortest-path algorithm to compute the shortest path from node *h* to all network nodes.

<center>
  <img src="Typora_Picture/image-20230330232945016.png" alt="image-20230330232945016" style="zoom:80%;" />
  <img src="Typora_Picture/Screenshot%202023-03-30%20at%2023.47.52.png" alt="Screenshot 2023-03-30 at 23.47.52" style="zoom:40%;" />
  <img src="Typora_Picture/Screenshot%202023-03-31%20at%2001.10.53.png" alt="Screenshot 2023-03-31 at 01.10.53" style="zoom:50%;" />

| Step | N'       | D(f),p(f) | D(g),p(g) | D(e),p(e) | D(c),p(c) | D(d),p(d) | D(b),p(b) | D(a),p(a) |
| ---- | -------- | --------- | --------- | --------- | --------- | --------- | --------- | --------- |
| 0    | h        | **2,h**   | 5,h       | infinite  | infinite  | infinite  | infinite  | infinite  |
| 1    | hf       |           | **5,h**   | infinite  | infinite  | infinite  | 10,f      | infinite  |
| 2    | hfg      |           |           | 13,g      | infinite  | **9,g**   | 10,f      | infinite  |
| 3    | hfgd     |           |           | 13,g      | 15,d      |           | **10,f**  | infinite  |
| 4    | hfgdb    |           |           | 13,g      | 15,d      |           |           | **12,b**  |
| 5    | hfgdba   |           |           | **13,g**  | 14,a      |           |           |           |
| 6    | hfgdbae  |           |           |           | **14,a**  |           |           |           |
| 7    | hfgdbaec |           |           |           |           |           |           |           |





#### 5.2.2 Distance vector (Bellman-Ford equation)

- 距离向量算法中，**每个结点**仅与它的**直接相连的邻居交谈**，但它为其邻居提供了从它自己到网络中 (它所知道的) 所有其他结点的最低费用估计。

![Screenshot 2023-03-21 at 13.46.58](Typora_Picture/Screenshot%202023-03-21%20at%2013.46.58.png)

![Screenshot 2023-03-21 at 13.58.21](Typora_Picture/Screenshot%202023-03-21%20at%2013.58.21.png)

![Screenshot 2023-03-21 at 14.17.34](Typora_Picture/Screenshot%202023-03-21%20at%2014.17.34.png)

![Screenshot 2023-03-21 at 22.21.34](Typora_Picture/Screenshot%202023-03-21%20at%2022.21.34.png)

![Screenshot 2023-03-22 at 00.43.36](Typora_Picture/Screenshot%202023-03-22%20at%2000.43.36.png)



##### Distance vector: link cost changes

在 Distance vector 中，当节点检测到本地链路开销变化，更新路由信息，重新计算 distance vector，如果DV发生变化，通知邻居

**"good news travels fas"**

- t0: y检测链路开销变化，更新DV，通知邻居。
- t1: z接收y的更新，更新它的表，计算新的最小代价到x，将它的DV发送给它的邻居。
- T2: y接收z的更新，更新它的距离表。Y的最小代价不变，所以Y不会向z发送消息。



**"bad news travels slow" – count-to-infinity problem:**

- many iterations before algorithm stabilizes

![Screenshot 2023-03-22 at 00.55.10](Typora_Picture/Screenshot%202023-03-22%20at%2000.55.10.png)



#### 5.2.3 Link State & Distance Vector 算法的比较

- **Link State:** 需要全局信息。因此，当在每台路由器中实现时，每个节点(经广播)与所有其他节点通信，但仅告诉它们与它直接相连链路的开销。我们通过快速比较它们各自的属性来总结所学的链路状态与距离向量算法。（会有振荡: oscillations）

- **Distance Vector:** 每个节点仅与它的直接相连的邻居交谈，但它为其邻居提供了从它自已到网络中(它所知道的)所有其他节点的最低开销估计。
- 记住 N 是节点(路由器)的集合，而 E 是边(链 路)的集合 。

![Screenshot 2023-03-22 at 00.46.05](Typora_Picture/Screenshot%202023-03-22%20at%2000.46.05.png)



### 5.3 intra-AS routing

Making routing scalable:

- **scale:** 拥有数十亿个目的地，不能将所有目的地存储在路由表中!
- **administrative autonomy:** 因特网=网络中的网络，每个网络管理员可能都想控制自己网络中的路由。因特网是 ISP 的网络，其中每个 ISP 都有它自己的路由器网络。ISP 通常希望按自己的意愿运行路由器。一个组织应当能够按自己的愿望运行和管理其网络，还要能将其网络与其他外部网络连接起来 。

这两个问题都可以通过将路由器组织进 **自治系统 (Autonomous System , AS)** 来解决。

- 其中每个 **Autonomous System** 由一组通常处在相同管理控制下的路由器组成。
- 通常在一个ISP中的路由器以及互联它们的链路构成一个 **Autonomous System**
- 然而，某些 ISP 将它们的网络划分为多个 **Autonomous System**。特别是某些一级 ISP 在其整个网络中使用一个庞大的 **Autonomous System**, 而其他 ISP 则将它们的 ISP 拆分为数十个互联的  **Autonomous System**
- 一个自治系统由其全局唯一的 **自治系统 (Autonomous System , AS)**号 (ASN) 所标识 [RFC1930]。就像IP 地址那样，AS 号由 ICANN 区域注册机构所分配 [ICANN 2016] 。

#### Internet approach to scalable routing

将 routers 聚合到称为 **"autonomous systems" (AS)** 的区域 (又名 "domains")

![Screenshot 2023-03-22 at 14.18.01](Typora_Picture/Screenshot%202023-03-22%20at%2014.18.01.png)



<img src="Typora_Picture/Screenshot%202023-03-22%20at%2016.02.04.png" alt="Screenshot 2023-03-22 at 16.02.04" style="zoom: 50%;" />

<center>
  <img src="Typora_Picture/Screenshot%202023-03-22%20at%2016.02.19.png" alt="Screenshot 2023-03-22 at 16.02.19" style="zoom:49%;" />
  <img src="Typora_Picture/Screenshot%202023-03-22%20at%2016.02.32.png" alt="Screenshot 2023-03-22 at 16.02.32" style="zoom:49%;" />
</center>

![Screenshot 2023-03-22 at 16.07.24](Typora_Picture/Screenshot%202023-03-22%20at%2016.07.24.png)



### 5.4 Three intra domain routing protocols

#### RIP

RIP: Routing Information Protocol [RFC 1723] (Distance vector 算法)

- 在 1982年发布的BSD-UNIX 中实现
- distance metric: # hops (max = 15 hops)，每条 link cost = 1
- DV每隔30秒和邻居交换一次DV in response message (advertisement 通告) 
- 每个 advertisement 包括: 最多25个 destination subnets (in IP addressing sense)

![Screenshot 2023-03-22 at 18.20.29](Typora_Picture/Screenshot%202023-03-22%20at%2018.20.29.png)



#### OSPF (LS)

OSPF: Open Shortest Path First [RFC 2328]

- **"open": publicly available** 指路由选择协议规范是公众可用的(与之相反的是 Cisco 的 EIGRP 协议)
- 使用 **link-state routing**
  - 每个路由器将 OSPF link-state 通告 (advertisements) (直接通过IP而不是使用TCP/UDP)发送到整个AS中的所有其他路由器
  - 多链路 costs metrics 可能: bandwidth, delay
  - 每个路由器都有完整的 topology (拓扑结构)，采用Dijkstra算法计算转发表
- IS-IS路由协议: 几乎和OSPF一样

- 安全:所有 OSPF messages authenticated (消息验证，防止恶意入侵)
- 支持在单个 AS 中的层次结构:

![Screenshot 2023-03-22 at 18.43.54](Typora_Picture/Screenshot%202023-03-22%20at%2018.43.54.png)



#### IGRP

IGRP: Interior Gateway Routing Protocol

- DV based
- formerly Cisco-proprietary for decades (became open in 2013 [RFC 7868])





### 5.4 routing among the ISPs: BGP (DV)

![Screenshot 2023-04-15 at 18.54.52](Typora_Picture/Screenshot%202023-04-15%20at%2018.54.52.png)

![Screenshot 2023-04-15 at 18.56.44](Typora_Picture/Screenshot%202023-04-15%20at%2018.56.44.png)







## <u>06. Link Layer and LANs 点到点传输层功能</u>

- hosts and routers = nodes
- 沿着通信路径,连接个相邻节点的 communication path = links (wired, wireless, LANs)
- 第二层协议数据单元帧 frame, encapsulates datagram

- 数据报(分组)在不同的链路上以不同的链路协议传送:

  - 第一跳链路: Ethernet 以太网 (先坐飞机)
  - 中间链路: 帧中继链路 (然后高铁)

  - 最后一跳: 802.11 (最后轿车)

- 不同的链路协议提供不同的服务（比如在链路层上提供(或没有)可靠数据传送）

![Screenshot 2023-04-06 at 23.57.19](Typora_Picture/Screenshot%202023-04-06%20at%2023.57.19.png)



### 6.1 services

- **framing, link access:** 

  - 将数据报封装在帧中，**加上 header (帧头)、trailer (帧尾部)**

  - 如果采用的是共享性介质，信道接入获得信道访问权

  - 在帧头部使用“MAC”(物理)地址来标示源和目的 (不同于IP地址)

    <img src="Typora_Picture/Screenshot%202023-04-07%20at%2000.01.09.png" alt="Screenshot 2023-04-07 at 00.01.09" style="zoom:50%;" />

- **reliable delivery between adjacent nodes:**
  - 在低出错率的链路上(光纤和双绞线电缆)很少使用
  - 在无线链路经常使用:出错率高

- **flow control:** 使得相邻的发送和接收方节点的速度匹配

- **error detection:** 差错由信号衰减和噪声引起，接收方检测出的错误: 通知发送端进行重传或丢弃帧

- **error correction:** 接收端检查和纠正bit错误，不通过重传来纠正错误

- **half-duplex and full-duplex: **

  - 半双工 (half-duplex): 链路可以双向传输，但一次只能收或只能发

  - 全双工 (full-duplex): 但一次可以同时收或发



#### Network interface card 网卡

- 链路层功能在 **适配器 adaptor (network interface card NIC)** 上实现或者在一个 **芯片组 (chip)** 上
- 接到主机的系统总线上，硬件、软件和固件的综合体

![Screenshot 2023-04-05 at 14.08.46](Typora_Picture/Screenshot%202023-04-05%20at%2014.08.46.png)

![Screenshot 2023-04-05 at 14.04.23](Typora_Picture/Screenshot%202023-04-05%20at%2014.04.23.png)



### 6.2 error detection, correction

#### 6.2.1 Error detection 错误检测

- EDC: 差错检测和纠正位(冗余位) error detection and correction bits (e.g., redundancy)
- D: 数据由差错检测保护，可以包含头部字段 data protected by error checking, may include header fields 

错误检测不是100%可靠的！协议会漏检一些错误，但是很少，更长的EDC字段可以得到更好的检测和纠正效果。

<img src="Typora_Picture/Screenshot%202023-04-05%20at%2014.11.18.png" alt="Screenshot 2023-04-05 at 14.11.18" style="zoom:40%;" />



#### 6.2.2 Parity checking 奇偶校验

**Even Parity (偶校验):** 发送方只需包含一个附加的比特，选择它的值，使得这d+1比特 (初始信息加上一个校验比特) 中1的总数是**偶数**

![Screenshot 2023-04-05 at 14.16.54](Typora_Picture/Screenshot%202023-04-05%20at%2014.16.54.png)

#### 6.2.3 Internet checksum 因特网检验和

与后面要讨论的常用于链路层的 CRC 相比，它们提供相对弱的差错保护

<img src="Typora_Picture/Screenshot%202023-04-05%20at%2018.07.26.png" alt="Screenshot 2023-04-05 at 18.07.26" style="zoom:50%;" />

#### 6.2.4 Cyclic Redundancy Check (CRC) 循环冗余校验

- 强大的差错检测码
- 将**数据比特 D**, 看成是**二进制的数据**
- **生成多项式 G**: 双方协商 r+1位模式(r次方)，生成和检查所使用的位模式

![Screenshot 2023-04-05 at 18.26.44](Typora_Picture/Screenshot%202023-04-05%20at%2018.26.44.png)

所有 CRC 计算采用 **模2算术来做 = 异或 XOR (相同为0，不同为1)**

乘以 2^k 就是以一种比特模式左移 k 个位置，假设 D=101110, d=6 (位数), G=1001 和 r=3 (向左移3位) 的情况下的计算过程。 在这种情况下传输的 9 个比特是 101110011 。 你应该自行检查 一下这些计算，并核对 一 下 D * 2^k = nG XOR R 的确成立。

![Screenshot 2023-04-05 at 19.40.05](Typora_Picture/Screenshot%202023-04-05%20at%2019.40.05.png)



### 6.3 multiple access protocols

- **分布式算法 -> 决定把这个 共享式的channel 分配给哪个 node 来使用**，即: 决定节点什么时候可以发送?
- 关于共享控制的通信必须用借助信道本身传输
  - 没有带外的信道，各节点使用其协调信道使用
  - 用于传输控制信息

- 节点通过这些协议来规范它们在共享的广播信道上的传输行为
- 两种类型的链路: 点对点, 广播 broadcast (共享线路或媒体)
- **2个或更多站点同时传送: 冲突(collision)**，多个节点在同一个时刻发送，则会收到2个或多个信号叠加

- 所以当多个节点处于活跃状态时，为了确保广播信道执行有用的工作，以某种方式协调活跃节点的传输是必要的。这种协调工作由多路访问协议负责。



**理想的 multiple access protocol:**

给定: **multiple access channel (MAC)** of rate ***R* bps**，必要条件:

- 当仅有一个节点发送数据时，该节点具有 **R bps 的吞吐量** 
- 当有 **M 个节点**发送数据时，每个可以以**R/M 的平均速率**发送
- 协议是**分散的**; 这就是说不会因某主节点故障而使整个系统崩溃
- 协议是**简单的**，使实现不昂贵



#### 6.3.1 MAC protocols

three broad classes:

- **channel partitioning 信道划分**
  - 把 channel 划分成更小的 "pieces" (time slots, frequency, code)
  - 分配 pieces 给每个节点专用

- **random access 随机访问，想用的时候就用**
  - channel 不划分，允许 collisions
  - 冲突后恢复

- **taking turns 依次轮流**
  - 节点依次轮流，但是有很多数据传输的节点可以获得较长的信道使用权

![Screenshot 2023-04-07 at 00.05.56](Typora_Picture/Screenshot%202023-04-07%20at%2000.05.56.png)

#### 6.3.2 channel partitioning

##### Channel partitioning MAC protocols: TDMA

将时间划 分为 时间帧 (time frame), 并进 一 步划分每个时间帧为 N 个时隙 (slot)

![Screenshot 2023-04-07 at 00.07.59](Typora_Picture/Screenshot%202023-04-07%20at%2000.07.59.png)

- 轮流使用信道，信道的时间分为周期
- 每个 站点(station) 使用每周期中**固定的时隙** (length = packet transmission time)传输帧
- 如果站点无帧传输，时隙空闲 -> 浪费

下面 6-station LAN，1、3、4 have packets to send，slot 2、5、6空闲

![Screenshot 2023-04-06 at 15.51.39](Typora_Picture/Screenshot%202023-04-06%20at%2015.51.39.png)



##### Channel partitioning MAC protocols: FDMA

- 信道的有效频率范围被分成一个个小的频段
- 每个站点被分配一个固定的频段
- 分配给站点的频段如果没有被使用，则空闲

下面 6-station LA，1、3、4 have packets to send，frequency bands (频段) 2、5、 6 idle (空闲)

![Screenshot 2023-04-06 at 23.39.28](Typora_Picture/Screenshot%202023-04-06%20at%2023.39.28.png)



#### 6.3.3 Random access protocols

- 当节点有帧要发送时
  - 以信道带宽的**全部 R bps**发送
  - 没有节点间的预先协调

- 两个或更多 node 同时传输 ➜ 可能有 collision，涉及碰撞的每个节点将反复地重发它的 帧 (packet)，直到该帧无碰撞地通过为止 

随机存取协议 (random access MAC protocol) 规定:

- 如何检测冲突
- 如何从冲突中恢复(如:通过稍后的重传)

examples of random access MAC protocols:

- unslotted ALOHA, slotted ALOHA
- CSMA, CSMA/CD, CSMA/CA



##### Slotted ALOHA

我们以最简单的随机接入协议之一：时隙 ALOHA (Slotted ALOHA) 协议，开始我们对 随机接入协议 (Random access protocols) 的学习

![Screenshot 2023-04-07 at 00.10.59](Typora_Picture/Screenshot%202023-04-07%20at%2000.10.59.png)

![Screenshot 2023-04-07 at 00.12.12](Typora_Picture/Screenshot%202023-04-07%20at%2000.12.12.png)

![Screenshot 2023-04-07 at 00.13.08](Typora_Picture/Screenshot%202023-04-07%20at%2000.13.08.png)

![Screenshot 2023-04-07 at 00.24.20](Typora_Picture/Screenshot%202023-04-07%20at%2000.24.20.png)



##### Pure (unslotted) ALOHA 效率比时隙ALOHA更差！

- 简单、无须节点间在时间上同步，每个node各发各的不管别人

- 当有帧需要传输: 马上传输

- 冲突的概率增加:
  - 帧在t0发送，和其它在[t0 -1, t0 +1]区间内开始发送的帧冲突
  - 和当前帧冲突的区间(其他帧在此区间开始传输)增大了一倍

<img src="Typora_Picture/Screenshot%202023-04-22%20at%2014.17.26.png" alt="Screenshot 2023-04-22 at 14.17.26" style="zoom:50%;" />



#### 6.3.4 CSMA (carrier sense multiple access) 礼貌的对话人

CSMA (载波侦听多路访问): **listen before transmit**, 在传输前先侦听信道, 不打断别人正在进行的说话:

- 如果侦听到信道 idle 空闲，传送整个帧
- 如果侦听到信道 busy 忙，推迟传送

但是冲突仍然可能发生: 由 propagation delay 造成: 两个节点可能侦听不到正在进行的传输

冲突: 整个冲突帧的传输时间都被浪费了，是无效的传输(红 黄区域)
传播延迟(距离)决定了冲突的概率



CSMA/CD (collision detection)



### 6.4 LANs

 • addressing, ARP and

RARP
 • Ethernet • switches



### 6.5 a day in the life of a web request













