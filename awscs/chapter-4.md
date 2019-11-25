# 第四章 Amazon Virtual Private Cloud(Amazon VPC)
**《AWS认证解决方案架构师-联合考试》中的本章节目标包括不限于如下内容：**

## 第一点 设计高可用、低成本、容错、可扩展的系统
### 找出和识别云架构考虑因素，例如：基础组件和有效性设计

**包括如下内容：**
```
  * 怎么设计云服务
  * 计划和设计
  * 熟悉如下内容：
    AWS架构最佳事件
    架构权衡决策（例如：高可用 vs 成本，Amazon 关系数据库服务[RDS] VS 在Amazon EC2上安装你自己的数据库）
  * 混合IT架构（例如，直接连接，存储网关，VPC，目录服务）
```
## 第二点 实现/部署

### 使用Amazon Ec2、Amazon Simple Storage Service（Amazon S3）、AWS Elastic Beanstalk、AWS Cloudformation、AWS Opsworks、Amazon Virtual Private Cloud（Amazon VPC）和AWS Identity And Access Management（IAM）确定适当的技术和方法来编码和实现云解决方案。

**包含如下内容**
```
  * 在混合IT架构中操作和扩展服务管理
  * 配置服务以支持云中的合规性要求
```
## 第三点 数据安全

### 认识并实施安全实践以实现最佳的云部署和维护
**可能包含如下内容**
```
 * AWS安全属性（客户工作负载下至物理层）
 * Amazon Virtual Private Cloud (VPC) 
 * 入口和出口过滤，以及哪些AWS服务和功能适合
 * "核心"Amazon EC2和S3安全特性集
 * 整合通用常规安全产品（防火墙和VPN）
 * 复杂的访问控制（构建复杂的安全组、ACL等） 
```

## 简介
* Amazon虚拟私有云（Amazon VPC）是AWS云中自定义的虚拟网络。您可以提供自己的AWS逻辑隔离部分，类似于设计和实现将在本地数据中心中运行的独立网络。本章探讨Amazon VPC的核心组件，在练习中，您将学习如何在云中构建自己的Amazon VPC。通过考试需要对Amazon VPC的拓扑结构和故障排除有很强的了解，我们强烈建议您完成本章中的练习

## Amazon Virtual Private Cloud(Amazon VPC)
* Amazon VPC是Amazon弹性计算云（Amazon EC2）的网络层，它允许您在AWS中构建自己的虚拟网络。您可以控制Amazon VPC的各个方面，包括选择自己的IP地址范围；创建自己的子网；配置自己的路由表、网络网关和安全设置。在一个区域内，您可以创建多个Amazon VPC，并且每个Amazon VPC在逻辑上是隔离的，即使它共享其IP地址空间。

* 创建Amazon VPC时，必须通过选择无类域间路由（CIDR）块（如10.0.0.0/16）来指定IPv4地址范围。Amazon VPC创创建之后，Amazon VPC的地址范围不能改变。一个Amazon VPC最大地址范围可达/16(65536个可用地址)，最小地址范围/28(16个可用地址)，并且和他们将要连接的其它任何网络重叠。

* Amazon VPC服务是在Amazon EC2服务之后发布的；因此，AWS中有两个不同的网络平台：EC2 Classic和EC2-VPC。Amazon EC2最初是与其他AWS客户共享的单一平面网络EC2 Classic一起发布的。因此，在Amazon VPC服务到达之前创建的AWS帐户可以将实例启动到EC2 Classic network和EC2-VPC中。支持EC2-VPC的AWS帐户将在每个区域中创建一个默认VPC，在每个可用性区域中创建一个默认子网，VPC分配的CIDR块将是172.31.0.0/16。

* 图4.1 说明一个地址空间：10.0.0.0/16包含两个不同子网（10.0.0.0/24和10.0.1.0/24）的Amazon VPC。两个子网分别在不通的可用区域，并且指定了本地路由的路由表。

* 一个Amazon VPC包含如下的组件：
```
 * 子网
 * 路由表
 * 动态主机协议（DHCP）选项集
 * 安全组
 * 网络控制列表(ACLs)
```

* 一个 Amazon VPC 包含如下可选组件：
```
 * Internet 网关(IGWs)
 * 弹性IP地址(EIP）
 * 弹性网络接口（ENIs)
 * Endpoints
 * Peering
 * 网络地址转换实例和NAT网关
 * VPG,CGWs,VPNs
```

## Subnets
* 子网是Amazon VPC的IP地址范围的一部分，可以在其中启动Amazon EC2实例、Amazon关系数据库服务（Amazon RDS）数据库和其他AWS资源，CIDR块定义子网（例如，10.0.1.0/24和192.168.0.0/24）。您可以创建的最小子网是/28（16个IP地址）。AWS保留每个子网的前四个IP地址和最后一个IP地址，用于内部网络。例如，定义为/28的子网有16个可用IP地址；减去AWS所需的5个IP，得到11个IP地址，供您在子网中使用。

* 创建Amazon VPC后，可以在每个可用区域中添加一个或多个子网。子网位于一个可用区域内，不能跨越区域。这是检查中可能出现的一个重要点，请记住，一个子网等于一个可用区域。但是，您可以在一个可用区域中有多个子网。

* 子网可以分为公共的，私有的，或仅限VPN。公用子网是关联路由表（稍后讨论）将子网的流量定向到Amazon VPC的IGW（稍后讨论）的子网。private子网是关联路由表不将子网的流量定向到Amazon VPC的IGW的子网。仅限VPN的子网是其中关联的路由表将子网的流量定向到Amazon VPC的VPG（稍后讨论），并且没有到IGW的路由。无论子网的类型如何，子网的内部IP地址范围始终是私有的（即，在Internet上不可路由）。

* 默认的Amazon vpc在区域内的每个可用区域中都包含一个公共子网，网络掩码为/20。

## 路由表（Route Tables）
* 路由表是Amazon VPC中的一个逻辑结构，它包含一组应用于子网的规则（称为路由），用于确定网络流量的定向位置Amazon VPC中的子网可以相互通信。您可以修改路由表并添加自己的自定义路由。您还可以使用路由表指定哪些子网是公用的（通过将Internet流量定向到IGW）哪些子网是专用的（通过没有将流量定向到IGW的路由）。

* 每一个路由表包含一个本地路由。通过这个本地路由可以和Amazon VPC进行通信，并且这个路由不能删除也不能修改。可以添加额外的路由来引导流量通过IGW（稍后讨论）、VPG（稍后讨论）或NAT实例（稍后讨论）退出Amazon VPC。在本章末尾的练习中，您可以实践这是如何实现的。

* 关于路由表你应该记住如下几点：
```
 * 你的VPC有一个隐性路由
 * 你的VPC会自动附带一个主路由表，你可以修改它
 * 您可以为VPC创建其他自定义路由表
 * 每个子网都必须与控制子网路由的路由表相关联。如果未将子网与特定路由表显式关联，则子网使用主路由表
 * 您可以用已创建的自定义表替换主路由表，以便每个新子网自动与其关联
 * 表中的每条路由指定一个目的地CIDR和一个目标；例如，目的地为172.16.0.0/12的流量是VPG的目标。AWS使用与流量匹配的最特定路由来确定如何路由流量 
```

## 网关（Internet Gateways）
* Internet网关（IGW）是一个水平扩展、冗余且高度可用的Amazon VPC组件，允许Amazon VPC中的实例与Internet之间进行通信。IGW在Amazon VPC路由表中为Internet可路由流量提供目标，并对已分配公共IP地址的实例执行网络地址转换。

* Amazon VPC中的Amazon EC2实例只知道它们的私有IP地址。当流量从实例发送到Internet时，IGW将应答地址转换为实例的公共IP地址（或EIP地址，稍后介绍），并维护实例私有IP地址和公共IP地址的一对一映射。当实例接收到来自Internet的流量时，IGW将目标地址（公共IP地址）转换为实例的私有IP地址，并将流量转发给Amazon VPC。

* 必须执行以下操作才能创建具有Internet访问权限的公用子网
```
 * 附件一个IGW到你的Amazon VPC
 * 创建一个子网路由表规则，用于发送所有的非本地流量（0.0.0.0/0）到IGW
 * 配置你的网络ACLs和安全组规则，以允许相关流量流入和流出你的实例
```

* 你必须执行如下操作，以便于Amazon EC2实例能够发送流量到Internet和接收来自Internet的流量。
```
 * 分配一个public IP地址或者EIP地址
```

* 您可以将路由范围设置为路由表（0.0.0.0/0）未明确知道的所有目的地，也可以将路由范围设置为较窄的IP地址范围，例如：AWS之外公司公共终结点的公共IP地址或Amazon VPC之外的其他Amazon EC2实例的EIP地址。

* 图4.2展示了一个地址空间为10.0.0.0/16的Amazon VPC，一个子网地址范围为10.0.0.0/24，一个路由表，一个附加的IGW，以及一个带有私有IP地址和EIP地址的Amazon EC2实例，路由表包含两条路由：允许跨VPC通信的本地路由和将所有非本地流量发送到IGW（IGW id）的路由，注意Amazon EC2实例有一个公共IP地址（EIP=198.51.100.2）；可以从Internet访问此实例，流量可能会产生并返回到此实例。

## 动态主机配置协议（DHCP）
* 动态主机配置协议DHCP为在TCP/IP网络上的主机传递配置信息提供了标准。DCCP消息的选项字段包含了配置参数，参数中包含：域名，域名服务，以及netbios-node-type。

* AWS会自动为你创建的Amazon VPC创建和关联一个DCCP选项集，并且设置两个选项：域名服务（默认是：AmazonProvidedDNS）和域名（默认是你的region的域名）。AmazonProvidedDNS是Amazon的一个域名系统服务，此选项适用于需要在亚马孙VPC上通信的实例。

* Amazon VPC的DHCP option sets元素允许您将Amazon EC2主机名分配定向到自己的资源。要将自己的域名分配给实例，请创建自定义DHCP选项集并将其分配给Amazon VPC。可以在DHCP选项集中配置以下值：
```
 * domain-name-servers 最多四个域名服务器的IP地址，用逗号分隔。默认值为AmazonProvidedDNS。
 * domain-name 在此处指定所需的域名
 * ntp-servers 最多四个网络时间协议服务器的IP地址，用逗号分隔。
 * netbios-name-servers 最多四个NetBIOS名字服务器的IP地址，用逗号分隔。
 * netbios-node-type 将此值设置为：2。
```
* 只能为每个Amazon VPC分配一个DHCP选项集。

## 弹性IP地址（Elastic IP Addresses(EIPs)）
AWS 在每个Region维持一个公共IP地址池，并使它们可供您与Amazon VPCs中的资源关联。弹性IP地址（EIP）是池中的静态公用IP地址，您可以将其分配给您的帐户（从池中提取）并释放（返回池）。EIP允许您维护一组保持固定的IP地址，而底层基础设施可能会随着时间而改变。以下是考试中有关EIP的重要要点:
```
 * 必须先分配一个EIP供VPC使用，然后再将其分配给一个实例。
 * EIP是特定于一个区域的（也就是说，不能将一个区域中的EIP分配给另一个区域中Amazon VPC内的实例）。
 * 网络接口和EIP是一一对应的关系
 * 可以将EIP从一个实例移到另外一个实例，可以是同一个Amazon VPC，也可以是同一个Region的不同Amazon VPC。
 * 在您明确释放EIP之前，EIP仍与您的AWS帐户关联。
 * 为您的帐户分配的EIP会收取费用，即使它们与资源没有关联。
```

## 弹性网络接口（Elastic Network Interfaces(ENIs)）
* 弹性网络接口（ENI）是一个虚拟网络接口，可以附加到Amazon VPC中的实例。ENIs仅在Amazon VPC中可用，并且它们在创建时与子网相关联。它们可以有一个公共IP地址和多个私有IP地址。如果有多个专用IP地址，其中一个是主IP地址。通过ENI为实例分配第二个网络接口允许它是双宿的（在不同的子网中有网络存在）。独立于特定实例创建的ENI将持续存在，而不管它附加到的任何实例的生存期如何；如果基础实例失败，则可以通过将ENI附加到替换实例来保留IP地址。              

* ENIs允许您创建一个管理网络，在Amazon VPC中使用网络和安全设备，在不同的子网上创建具有工作负载/角色的双主实例，或者创建一个低成本、高可用性的解决方案


## 端点（Endpoints）
* Amazon VPC端点允许您在Amazon VPC和另一个AWS服务之间创建私有连接，而无需通过Internet或NAT实例、VPN连接或AWS直接连接进行访问。可以为单个服务创建多个终结点，还可以使用不同的路由表从不同的子网对同一服务强制实施不同的访问策略。

* Amazon VPC端点目前支持与Amazon Simple Storage Service（Amazon S3）的通信，未来还将增加其他服务。要创建Amazon VPC端点，必须执行以下操作：
```
 * 指定Amazon VPC
 * 指定服务。一个服务是通过带有如下前缀列表的形式定义：com.amazonaws.<region>.<service>。
 * 指定策略。您可以允许完全访问或创建自定义策略。此策略可以随时更改。
 * 指定路由表。路由将被添加到每个指定的路由表中，该表将服务声明为目标，端点声明为目标 
```

* 表-4.1 是一个路由表的示例。该路由表具有将所有Internet业务（0.0.0.0/0）引导到IGW的现有路由。从另一个AWS服务（例如，Amazon S3或Amazon DynamoDB）的子网中的任何业务将被发送到IGW，以便达到该服务。 

表-4.1 带有IGW路由规则的路由表
|---|---|
|Destination|Target|
|10.0.0.0/16|Local|
|0.0.0.0/0|igw-1a2b3c4d|

* 表4.2是一个示例路由表，它具有将所有Internet流量引导到IGW和所有Amazon S3流量到Amazon VPC端点的现有路由。 

表-4.2 带有IGW路由规则和VPC端点规则的路由表
|---|---|
|Destination|Target|
|10.0.0.0/16|Local|
|0.0.0.0/0|igw-1a2b3c4d|
|p1-1a2b3c4d|vpce-11bb22cc|

* 表4.2中描述的路由表将把从同一区域中的Amazon S3的子网的任何通信量定向到端点。所有其他互联网流量都流向您的IGW，包括流向其他服务和其他地区的Amazon S3的流量。

## Peering
* 一个Amazon VPC对等连接是两个Amazon VPC之间的网络连接，它使任何一个Amazon VPC中的实例能够彼此通信，就好像它们在同一个网络中一样。您可以在自己的Amazon VPC之间创建一个Amazon VPC对等连接，也可以在单个区域内的另一个AWS帐户中创建一个Amazon VPC对等连接。对等连接既不是网关也不是Amazon VPN连接，并且不会引入通信的单点故障。              
* 对等连接是通过请求/接受协议创建的。请求的Amazon VPC的所有者向对等的Amazon VPC的所有者发送请求到peer。如果对等的Amazon VPC在同一个账户内，则由其VPC ID标识；如果对等的VPC在不同的账户内，则由账户ID和VPC ID标识；对等的Amazon VPC的所有者在对等请求到期前有一周时间接受或拒绝与请求的Amazon VPC对等的请求。              一个

* Amazon VPC可能有多个对等连接，对等是Amazon VPC之间的一对一关系，这意味着两个Amazon VPC之间不能有两个对等协议。另外，对等连接不支持传递路由。图4.3描述了传递路由。

* 图-4.3 VPC对等连接不支持传递路由（待增加图）

* 在图4.3中，VPC A有两个对等连接，分别是VPC B和VPC。因此，VPC A可以直接与VPC B和C通信。由于对等连接不支持传输路由，所以VPC A不能作为VPC B和C之间通信的传输点。为了使VPC B和C相互通信，对等连接必须在它们之间显式创建连接。以下是关于窥视考试的要点：              
```
 * 不能在具有匹配或重叠CIDR块的Amazon vpc之间创建对等连接
 * 不能在不同区域的Amazon VPC之间创建对等连接
 * Amazon VPC对等连接不支持传递路由
 * 同一时间同一个Amazon VPC之间不能有多个对等连接
```

## 安全组
* 安全组是一个虚拟有状态防火墙，它控制到AWS资源和Amazon EC2实例的入站和出站网络流量。所有Amazon EC2实例都必须启动到一个安全组中。如果启动时未指定安全组，则实例将被启动到Amazon VPC的默认安全组中。默认安全组允许安全组内所有资源之间的通信，允许所有出站通信，并拒绝所有其他通信。您可以更改默认安全组的规则，但不能删除默认安全组。表4.3描述了默认安全组的设置。

* 表-4.3 安全组规则（待增加）

* 对于每个安全组，可以添加控制实例的入站流量的规则和控制出站流量的单独规则集。例如，表4.4描述了web服务器的安全组。

*表-4.4 Web 服务的安全组规则（待增加）
* 以下是关于窥视考试的要点：
```
 * 您最多可以为每个Amazon VPC创建500个安全组。
 * 每个安全组最多可以添加50个入站和50个出站规则。如果需要对一个实例应用100多个规则，则最多可以将五个安全组与每个网络接口关联。
 * 可以指定允许规则，但不能指定拒绝规则。这是安全组和acl之间的一个重要区别。
 * 您可以为入站和出站流量指定单独的规则。
 * 默认情况下，在将入站规则添加到安全组之前，不允许入站流量。
 * 默认情况下，新安全组具有允许所有出站流量的出站规则。您可以删除该规则并添加仅允许特定出站流量的出站规则。
 * 安全组是有状态的。这意味着无论出站规则如何，对允许的入站流量的响应都允许流出，反之亦然。这是安全组和网络ACL之间的一个重要区别。
 * 与同一安全组关联的实例不能相互通信，除非您添加了允许它的规则（默认安全组除外）。
 * 您可以在启动后更改与实例关联的安全组，这些更改将立即生效。
```

## 网络访问控制列表（ACLs）
* 网络访问控制列表（ACL）是另一个安全层，在子网级别充当无状态防火墙。网络ACL是AWS按顺序计算的规则的编号列表，从编号最低的规则开始，以确定与网络ACL关联的任何子网中是否允许通信。Amazon vpc是用一个可修改的默认网络ACL创建的，该ACL与允许所有入站和出站流量的每个子网相关联。当您创建自定义网络ACL时，其初始配置将拒绝所有入站和出站通信，直到您创建允许其他方式的规则。您可以使用与安全组相似的规则设置网络ACL，以便向Amazon VPC添加安全层，也可以选择使用默认的网络ACL，该ACL不过滤通过子网边界的流量。总的来说，每个子网都必须与网络ACL相关联。

* 表-4.5 展示了安全组和网络ACL之间的不同。应对考试，你应该记住安全组和网络ACL之间如下的不同点。
* 表-4.5 安全组和网络ACLs对比
|---|---|
|安全组|网络ACL|
|实例登记操作（防护的第一层|在子网登记（防护的第二层|
|进支持允许的规则|支持允许规则和拒绝规则|
|状态稳定：允许自动返回流量，不管任何规则|状态不稳定：返回流量必须清晰定义被允许|
|在决定是否允许流量之前，AWS会评估所有规则|AWS在决定是否允许流量时按数字顺序处理规则|
|选择性地应用于单个实例|自动应用于关联子网中的所有实例；这是防御的备份层，因此您不必依赖于指定安全组的人|


## 网络地址转换（NAT）实例以及NAT网关
* 默认情况下，在Amazon VPC中启动到私有子网的任何实例都无法通过IGW与Internet通信。如果私有子网中的实例需要从Amazon VPC直接访问Internet才能应用安全更新、下载修补程序或更新应用程序软件，则会出现此问题。AWS提供了NAT实例和NAT网关，允许部署在私有子网中的实例访问Internet。对于常见的用例，我们建议您使用NAT网关而不是NAT实例。NAT网关提供了更好的可用性和更高的带宽，并且比NAT实例需要更少的管理工作。

### NAT实例
* 网络地址转换（NAT）实例是Amazon-Linux Amazon机器映像（AMI），其设计用于接受来自私有子网内实例的流量，将源IP地址转换为NAT实例的公共IP地址，并将流量转发到IGW。此外，NAT实例维护转发流量的状态，以便将响应流量从Internet返回到私有子网中的适当实例。这些实例的名称中有字符串amzn-ami-p-vpc-nat，可以在Amazon EC2控制台中进行搜索

* 若要允许专用子网中的实例通过NAT实例通过IGW访问Internet资源，必须执行以下操作：
```
 * 使用出站规则为NAT创建安全组，该出站规则按端口、协议和IP地址指定所需的Internet资源。
 * 将Amazon Liinux Nat AMI 作为公共子网中的实例启动，并将其与NAT安全组关联。
 * 禁用NAT的源/目标检查属性。
 * 配置与专用子网关联的路由表，以将绑定到Internet的流量定向到NAT实例（例如，i-1a2b3c4d）。
 * 分配EIP并将其与NAT实例关联。
```
* 此配置允许私有子网中的实例发送出站Internet通信，但它阻止实例接收由Internet上的某人发起的入站通信。

### NAT网关
* NAT网关是Amazon管理的资源，它的设计与NAT实例一样，但它更易于管理，并且在可用性区域内高度可用。若要允许专用子网中的实例通过NAT网关通过IGW访问Internet资源，必须执行以下操作：
```
 * 将与专用子网关联的路由表配置为直接绑定到Internet到NAT网关的流量（例如，NAT-1a2b3c4d）。
 * 分配EIP并将其与NAT网关关联。
```

* 与NAT实例一样，此托管服务允许出站Internet通信，并阻止实例接收由Internet上的某人发起的入站通信

* 备注
``` 
 要创建独立于可用区的体系结构，请在每个可用区中创建一个NAT网关，并配置路由以确保资源在同一可用区中使用NAT网关
```
在练习中将会证明NAT网关如何工作。

## 虚拟私有网关（VPGs），客户网关（CGWs），以及虚拟私有网络（VPNs）
* 您可以使用硬件或软件VPN连接将现有的数据中心连接到Amazon VPC，这将使Amazon VPC成为数据中心的扩展。Amazon VPC提供了两种将企业网络连接到VPC的方法：VPG和CGW。              
* 虚拟专用网关（VPG）是两个网络之间VPN连接的AWS端的虚拟专用网（VPN）集中器。客户网关（CGW）表示VPN连接客户端的物理设备或软件应用程序。在创建了Amazon VPC的这两个元素之后，最后一步是创建VPN隧道。VPN隧道是在从VPN连接的客户端生成流量之后建立的。图4.4显示了公司网络和Amazon VPC之间的单个VPN连接。

* 图4.4 与客户网络建立VPN连接的VPC（待增加）

* 必须指定创建VPN连接时计划使用的路由类型。如果CGW支持边界网关协议（BGP），则为动态路由配置VPN连接。否则，请为静态路由配置连接。如果要使用静态路由，则必须输入应与VPG通信的网络路由。路由将传播到Amazon VPC，以允许您的资源通过VGW和VPN隧道将网络流量路由回公司网络Amazon VPC还支持多个cgw，每个cgw都有一个VPN连接到一个VPG（多对一设计）。为了支持这种拓扑结构，CGW IP地址在区域内必须是唯一的。

* Amazon VPC将提供网络管理员配置CGW所需的信息，并与VPG建立VPN连接。VPN连接由两个Internet协议安全（IPSec）隧道组成，以提高Amazon VPC的可用性。以下是考试中需要了解的有关VPG、CGW和VPN的要点：
```
 * VPG是VPN隧道的AWS端。
 * CGW是VPN隧道客户端的硬件或软件应用程序。
 * 您必须启动从CGW到VPG的VPN隧道。
 * vpg支持BGP动态路由和静态路由。
 * VPN连接由两个隧道组成，以提高VPC的可用性。
```

## 总结




## 考试基础




## 练习




## 复习题

### 1. What is the minimum size subnet that you can have in an Amazon VPC? 
 * A. /24 
 * B. /26 
 * C. /28
 * D. /30 

### 2. You are a solutions architect working for a large travel company that is migrating its existing server estate to AWS. You have recommended that they use a custom Amazon VPC, and they have agreed to proceed. They will need a public subnet for their web servers and a private subnet in which to place their databases. They also require that the web servers and database servers be highly available and that there be a minimum of two web servers and two database servers each. How many subnets should you have to maintain high availability? 
 * A. 2 
 * B. 3 
 * C. 4 
 * D. 1 

### 3. Which of the following is an optional security control that can be applied at the subnet layer of a VPC? 
 * A. Network ACL 
 * B. Security Group 
 * C. Firewall 
 * D. Web application firewall 

### 4. What is the maximum size IP address range that you can have in an Amazon VPC? 
 * A. /16 
 * B. /24 
 * C. /28 
 * D. /30 

### 5. You create a new subnet and then add a route to your route table that routes traffic out from that subnet to the Internet using an IGW. What type of subnet have you created? 
 * A. An internal subnet 
 * B. A private subnet 
 * C. An external subnet 
 * D. A public subnet

### 6. What happens when you create a new Amazon VPC? 
 * A. A main route table is created by default. 
 * B. Three subnets are created by default—one for each Availability Zone. 
 * C. Three subnets are created by default in one Availability Zone. 
 * D. An IGW is created by default. 

### 7. You create a new VPC in US-East-1 and provision three subnets inside this Amazon VPC. Which of the following statements is true? 
 * A. By default, these subnets will not be able to communicate with each other; you will need to create routes. 
 * B. All subnets are public by default. 
 * C. All subnets will be able to communicate with each other by default. 
 * D. Each subnet will have identical CIDR blocks. 

### 8. How many IGWs can you attach to an Amazon VPC at any one time? 
 * A. 1 
 * B. 2 
 * C. 3 
 * D. 4 

### 9. What aspect of an Amazon VPC is stateful? 
 * A. Network ACLs 
 * B. Security groups 
 * C. Amazon DynamoDB 
 * D. Amazon S3 

### 10. You have created a custom Amazon VPC with both private and public subnets. You have created a NAT instance and deployed this instance to a public subnet. You have attached an EIP address and added your NAT to the route table. Unfortunately, instances in your private subnet still cannot access the Internet. What may be the cause of this? 
 * A. Your NAT is in a public subnet, but it needs to be in a private subnet. 
 * B. Your NAT should be behind an Elastic Load Balancer. 
 * C. You should disable source/destination checks on the NAT. 
 * D. Your NAT has been deployed on a Windows instance, but your other instances are Linux. You should redeploy the NAT onto a Linux instance. 
 
### 11. Which of the following will occur when an Amazon Elastic Block Store (Amazon EBS)backed Amazon EC2 instance in an Amazon VPC with an associated EIP is stopped and started? (Choose 2 answers)
 * A. The EIP will be dissociated from the instance.
 * B. All data on instance-store devices will be lost. 
 * C. All data on Amazon EBS devices will be lost. 
 * D. The ENI is detached. 
 * E. The underlying host for the instance is changed. 

### 12. How many VPC Peering connections are required for four VPCs located within the same AWS region to be able to send traffic to each of the others? 
 * A. 3 
 * B. 4 
 * C. 5 
 * D. 6 

### 13. Which of the following AWS resources would you use in order for an EC2-VPC instance to resolve DNS names outside of AWS? 
 * A. A VPC peering connection 
 * B. A DHCP option set 
 * C. A routing rule 
 * D. An IGW 

### 14. Which of the following is the Amazon side of an Amazon VPN connection? 
 * A. An EIP 
 * B. A CGW 
 * C. An IGW 
 * D. A VPG 

### 15. What is the default limit for the number of Amazon VPCs that a customer may have in a region? 
 * A. 5 
 * B. 6 
 * C. 7 
 * D. There is no default maximum number of VPCs within a region. 

### 16. You are responsible for your company’s AWS resources, and you notice a significant amount of traffic from an IP address in a foreign country in which your company does not have customers. Further investigation of the traffic indicates the source of the traffic is scanning for open ports on your EC2-VPC instances. Which one of the following resources can deny the traffic from reaching the instances? 
 * A. Security group 
 * B. Network ACL 
 * C. NAT instance
 * D. An Amazon VPC endpoint
 
###17. Which of the following is the security protocol supported by Amazon VPC? 
 * A. SSH 
 * B. Advanced Encryption Standard (AES) 
 * C. Point-to-Point Tunneling Protocol (PPTP) 
 * D. IPsec 

### 18. Which of the following Amazon VPC resources would you use in order for EC2-VPC instances to send traffic directly to Amazon S3? 
 * A. Amazon S3 gateway 
 * B. IGW 
 * C. CGW 
 * D. VPC endpoint 

### 19. What properties of an Amazon VPC must be specified at the time of creation? (Choose 2 answers) 
 * A. The CIDR block representing the IP address range 
 * B. One or more subnets for the Amazon VPC 
 * C. The region for the Amazon VPC 
 * D. Amazon VPC Peering relationships 

### 20. Which Amazon VPC feature allows you to create a dual-homed instance? 
 * A. EIP address 
 * B. ENI 
 * C. Security groups 
 * D. CGW









