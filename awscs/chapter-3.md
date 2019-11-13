# 第三章 Amazon Elastic Computer Cloud(Amazon EC2) 和 Amazon Elastic Block Store(Amazon EBS)
**《AWS认证解决方案架构师-联合考试》中的本章节目标包括不限于如下内容：**

## 第一点 设计高可用、低成本、容错、可扩展的系统

### 找出和识别云架构考虑因素，例如：基础组件和有效性设计

**包括如下内容：**
```
  * 怎么设计云服务
  * 计划和设计
  * 监控和日志
```

## 第二点 实现/部署

### 使用Amazon Ec2、amazon Simple Storage Service（amazon S3）、AWS Elastic Beanstalk、AWS Cloudformation、AWS Opsworks、amazon Virtual Private Cloud（amazon Vpc）和AWS Identity And Access Management（iam）确定适当的技术和方法来编码和实现云解决方案。

**包含如下内容**
```
  * 配置一个Amazon Machine Image（AMI）
  * 配置服务以满足云上得合规性需求
  * 在AWS全球基础设施上发布实例

```

## 第三点 数据安全

### 认识到关键的灾难恢复技术及其实现
**包含如下内容**
```
  * 灾难恢复
  * Amazon EB
```

## 简介
在本章中，你将会学习Amazon Elastic Compute Cloud（Amazon EC2）和Amazon Elastic Block Store（Amazon EBS）如何提供基本的计算元素和块等级的存储，用以运行你在AWS上的workloads。对于考试来说，主要聚焦你需要理解的关键话题，包括如下内容：

* 实例类型和amazon机器映像（amis）如何定义在云上启动的实例的功能
* 如何安全地访问云上运行的实例
* 如何使用称为安全组的虚拟防火墙保护实例
* 如何让您的实例为无人参与启动配置自己
* 如何在云上监视和管理实例
* 如何改变现有实例的能力，支付选项可用于可负担性和灵活性的最佳组合
* 租赁选项和放置组如何提供选项以优化合规性和性能
* 实例存储与Amazon EBS卷有何不同以及它们何时有效
* 通过Amazon EBS提供哪些类型的卷
* 如何在amazon ebs上保护您的数据

## Amazon Elastic Compute Cloud(Amazon EC2)
Amazon EC2是AWS一个主要的web服务，在云上提供弹性调整计算的能力。

### 计算基础
* 计算是指完成工作量所需的计算能力。如果你的工作量很小，比如一个网站很少有访客，那么你的计算需求就很小。一个很大的工作量，比如针对一个常见的癌症目标筛选一千万种化合物，可能需要大量计算。您需要的计算量可能会随着时间的推移而急剧变化

* Amazon EC2允许您通过启动名为Instances的虚拟服务器来获取计算。当您启动一个实例时，您可以随心所欲地使用该计算，就像使用本地服务器一样。因为您要为实例的计算能力付费，当实例运行时，您将按小时收费。当您停止实例时，将不再收费。

* 在AWS上启动实例有两个关键概念：（1）专用于实例的虚拟硬件数量和（2）加载在实例上的软件，这两个维度的新实例分别由实例类型和AMI控制。

#### 实例类型
* 实例类型定义了支持Amazon EC2实例的虚拟硬件。有几十种可用的实例类型，在以下维度中有所不同：
```
 * 虚拟CPUs（vCPUs）
 * 内存
 * 存储（大小和类型）
 * 网络性能
```

* 实例类型根据这些值之间的比率分组为多个系列。例如，M4系列提供了计算、内存和网络资源的平衡，对于许多应用程序来说，这是一个很好的选择。在每个系列中，都有几个在大小上呈线性放大的选择。图3.1显示了M4系列中的四个实例大小。请注意，vCPU与内存的比率随大小呈线性放大而保持不变。每个大小的每小时价格也呈线性放大。例如，一个m4.xlarge实例的成本是m4.large实例的两倍。
|---|---|---|
|类型|vCPUs|内存|
m4.large|2|8|
m4.xlarge|4|16|
m4.2xlarge|8|32|
m4.4xlarge|16|64|

图3.1 m4家族的实例内存和vCPUs 

备注：
```
 原文档为图，此处转换为表格。但仍叫做：图3.1
```

* 不同的实例类型族会调整比率以适应不同类型的工作负载，但它们都会在族中显示这种线性放大行为。表3.1列出了一些可用的族

**表3.1：实例类型族示例**
* 家族
|---|---|
|c4|计算型-针对需要大量处理的工作负载|
|r3|内存型-内存密集型工作负载|
|i2|存储型-需要大量快速SSD存储的工作负载|
|g2|基于GPU实例-用于图形和通用GPU计算工作负载|

* 为了响应客户需求并利用新的处理器技术，AWS偶尔会引入新的实例系列。请查看AWS网站上的当前列表。选择实例类型时要考虑的另一个变量是网络性能。对于大多数实例类型，AWS发布了网络性能的相对度量：低、中或高。某些实例类型指定10 gbps的网络性能。随着实例类型的增长，族内的网络性能将提高。

* 对于需要更高网络性能的工作负载，许多实例类型支持增强的网络。增强的网络通过启用称为单根I/O虚拟化（SR-IOV）的功能减少了虚拟化对网络性能的影响。这会导致每秒包数（PPS）更多，延迟更低，在编写本文时，有一些实例类型支持C3、C4、D2、I2、M4中的增强型网络，和r3系列（请参阅AWS文档以获取当前列表）。在实例上启用增强的网络包括确保安装了正确的驱动程序并修改实例属性。增强的网络仅适用于在amazon虚拟私有云（amazon vpc）中启动的实例，这在第4章中讨论过，“亚马逊虚拟私有云（Amazon VPC）。”

#### Amazon Machine Images（AMIs）
Amazon Machine Image（AMI）定义了实例启动是要在实例上运行的的初始化软件。AMI定义了实例启动时软件状态的各个方面，包括：
```
 * 操作系统以及其配置
 * 任何不定的初始化状态
 * 应用或者系统软件
```

* 所有的AMIs都是基于X86 OSs，无论是Linux还是Windows。
* AMIs有四个源：
```
  * 通过AWS发布
    AWS发布的AMIs有许多不同版本的操作系统，包括linux和windows；
    其中包括linux的多个发行版（包括ubuntu、red hat和Amazon自己的发行版）以及windows 2008和windows 2012。
    基于其中一个AMIs启动实例将导致默认的os设置，类似于从标准OS ISO映像安装OS。
  * AWS集市
    AWS marketplace是一个在线商店，它帮助客户查找、购买并立即开始使用运行在Amazon EC2上的软件和服务。许多AWS合作伙伴已经在AWS marketplace上提供了他们的软件。这提供了两个好处：客户不需要安装软件，许可协议也适用于云计算，从AWS marketplace ami启动的实例会产生实例类型的标准小时成本加上额外软件的每小时额外费用（一些开源AWS marketplace包没有额外的软件费用）。
  * 由现有实例生成
    AMI可以从现有的Amazon EC2实例创建。
    这是AMIs的一个非常常见的来源。
    客户从发布的AMI启动一个实例，然后该实例被配置为满足所有客户的更新、管理、安全的企业标准，等等。
    然后从配置的实例生成一个AMI，并用于生成该OS的所有实例，这样，所有新实例都遵循公司标准，单个项目更难启动不一致的实例
  * 上传虚拟服务器
    使用AWS vm导入/导出服务，客户可以从各种虚拟化格式创建映像，
    包括raw、vhd、vmdk和ova。
    支持的操作系统（Linux和Windows）的当前列表可以在AWS文档中找到。
    客户有责任遵守其操作系统供应商的许可条款。
```

### 安全地使用实例
* 一旦启动，实例就可以通过Internet进行管理。AWS有许多服务和特性来确保这种管理可以简单而安全地完成

#### 寻址实例
有几种方法可以在创建实例时通过Web寻址 
* 公共域名系统（DNS）名称
 当你启动一个实例时，AWS创建可用于访问实例的dns名称。此dns名称是自动生成的，客户无法指定。可以在AWS管理控制台的"描述"选项卡中或通过命令行界面（cli）或应用程序编程界面（api）找到此名称。此dns名称仅在实例正在运行，无法转移到其他实例

* 公共IP
 已启动的实例也可能分配了公用IP地址。此IP地址是从AWS保留的地址分配的，无法指定。此IP地址在Internet上是唯一的，仅在实例运行时持续存在，并且无法传输到其他实例。

* 弹性IP
 弹性IP地址是Internet上唯一的地址，您可以独立保留并与Amazon EC2实例关联。与公共IP类似，有一些关键的区别。这个IP地址会一直存在，直到客户释放它，并且不会绑定到单个实例的生存期或状态。因为在实例出现故障时，可以将它转移到替换实例，它是一个公共地址，可以在外部共享，而无需将客户端耦合到特定实例。

* 备注
```
 私有ip地址和弹性网络接口（enis）是amazon vpc上下文中可用的附加实例寻址方法，这些将在第4章中讨论。 
```

#### 初始化访问

* Amazon EC2使用公钥密码加密和解密登录信息。公钥密码使用公钥加密一段数据，并使用关联的私钥解密数据。这两个密钥一起称为密钥对。可以通过AWS管理控制台、CLI或API创建密钥对，或者客户可以上传自己的密钥对。AWS存储公钥，而私钥由客户保存。私钥对于第一次获得对实例的安全访问至关重要。

* 备注
```
 安全地存储您的私钥。当Amazon EC2启动Linux实例时，公钥存储在实例上的/.ssh/authorized\u keys文件中，并创建一个初始用户。初始用户可能因操作系统而异。例如，Amazon Linux发行版的初始用户是ec2-user，对实例的初始访问是通过使用ec2-user和通过ssh登录的私钥获得的，此时可以配置其他用户并注册到LDAP等目录中。
```

* 在启动windows实例时，Amazon EC2 会为本地管理员帐户生成一个随机密码，并使用公钥对密码进行加密。对实例的初始访问是通过使用私钥解密密码获得的，在控制台中或通过API。解密后的密码可用于通过RDP使用本地管理员帐户登录到实例。此时，您可以创建其他本地用户和/或连接到活动目录域

* 备注
```
 最佳实践：修改初始的本地管理员密码。
```

#### 虚拟防火墙保护
* AWS允许您通过称为安全组的虚拟防火墙控制进出实例的流量。安全组允许您基于端口、协议、，和源/目标。安全组具有不同的功能，这取决于它们是与Amazon VPC还是Amazon EC2 classic相关联。表3.2比较了这些不同的功能（Amazon VPC在第4章中讨论） 

|---|---|
|安全组类型|能力|
|EC2-Classic安全组|控制实例外出流量|
|VPC安全组|控制进入和出去的流量|
表 3.2 不通的安全组
* 当实例启动时，安全组和实例向关联，每个实例必须至少有一个安全组，但也可以有多个。

* 安全组为默认拒绝，即不允许安全组规则未明确允许的任何通信。规则由表3.3中的三个属性定义。当一个实例与多个安全组关联时，规则是聚合的，并且允许每个组允许的所有流量。例如，如果安全组A允许72.58.0.0/16的RDP流量，而安全组B允许0.0.0.0/0的HTTP和HTTPS流量，并且您的实例与这两个组关联，然后rdp和http/s流量都将被允许进入您的实例。

|---|---|
|属性|含义|
|端口|受此规则影响的端口号。例如，用于http通信的端口80|
|协议|受此规则影响的通信量的通信标准|
|源/目的|标识通信的另一端，传入流量规则的源，或传出通信规则的目标。源/目标可以通过两种方式定义：CIDR阻止定义特定IP地址范围的X.X.X.X/X样式定义。安全组包括与给定安全组关联的任何实例。这有助于防止耦合安全组规则有特定的IP地址|
* 安全组是有状态的防火墙；也就是说，会记住传出消息，以便允许通过安全组进行响应，而不需要显式的入站规则。

* 安全组是在实例级别应用的，而不是传统的在外围保护的内部部署防火墙。这样做的效果是，攻击者不必为了访问安全组中的所有实例而破坏单个外围，而是必须为每个实例重复地破坏安全组。

### 实例的生命周期
* Amazon ec2有几个特性和服务，可以在其整个生命周期中方便地管理Amazon EC2实例。

#### 启动
当启动一个新的Amazon EC2实例的时候，还有一些附加服务非常有用。

##### 引导（Bootstrapping）
* 云的一个巨大好处是能够以本地硬件不可能的方式编写虚拟硬件管理脚本。为了实现这一点，必须有一些方法来配置实例，并在启动实例时以编程方式安装应用程序。在启动时提供要在实例上运行的代码的过程称为引导。

* 启动实例时的参数之一是名为userdata的字符串值。此字符串将传递给操作系统，以便在实例首次启动时作为启动过程的一部分执行在linux实例上，这可以是shell脚本，在windows实例上，这可以是批处理样式脚本或powershell脚本。脚本可以执行以下任务：
```
 * 将修补程序和更新应用于操作系统
 * 注册目录服务
 * 安装应用软件
 * 从要在实例上运行的存储中复制较长的脚本或程序
 * 安装Chef或Puppet并为实例分配角色，以便配置管理软件可以配置实例
```

* 备注
```
 UserDAta 和实例一起存储的，且不加密，因此在UserData中不要包含任何机密是非常重要的（例如：密码和秘钥）。

```
##### VM导入/导出

* 除了将虚拟实例导入为AMIs之外，VM导入/导出使您可以轻松地将虚拟机（VM）从亚马逊的EC2实例从现有的环境导入，并将它们导出回您的Office环境。您只能导出以前导入的Amazon EC2实例。无法导出从AMIS在AWS中启动的实例。    

##### 实例元数据

* 实例元数据是关于实例的数据，您可以使用这些数据来配置或管理正在运行的实例。这是唯一的，因为它是一种机制，可以从操作系统中获取实例的AWS属性，而无需调用AWS API对http://169.254.169.254/latest/meta-data/的http调用将返回实例元数据树的顶部节点。实例元数据包含多种属性，包括：
```
 * 关联的安全组
 * 实例ID
 * 实例类型
 * 用于启动实例的AMI
```
* 这只是开始触及元数据中可用信息的表面有关完整列表，请参阅AWS文档

#### 管理实例
* 当帐户中的实例数开始攀升时，很难跟踪它们。标签不仅可以帮助您管理Amazon EC2实例，还可以帮助您管理许多AWS云服务。标记是可以与实例或其他服务关联的键/值对。标记可用于标识实例的属性，如项目、环境（开发、测试等）、可计费部门等。每个实例最多可以应用10个标记。表3.4显示了一些标签建议。

|---|---|
|键|值|
|项目|TimeEntry|
|环境|Production|
|计费代码|4004|

表 3.4 样例标记

#### 监控实例
* AWS提供了一个名为amazon cloudwatch的服务，它为Amazon EC2实例以及其他AWS基础设施提供监控和警报。Amazon CloudWatch在第5章"Elastic Load Balancing, Amazon CloudWatch, 和 Auto Scaling"中进行了详细讨论。 

#### 修改实例
实例有几个方面可以在启动后修改:

* 实例类型

更改实例的实例类型的能力大大提高了在云中运行工作负载的灵活性。不必在工作负载启动前几个月提交特定的硬件配置，可以使用实例类型的最佳估计值来启动工作负载。如果需要证明计算高于或低于预期，则可以将实例更改为更适合工作负载的不同大小可以使用AWS管理控制台、cli或api调整实例的大小。若要调整实例的大小，请将状态设置为“已停止”。在您选择的工具中选择“更改实例类型”功能（实例类型在控制台中作为实例设置列出，在cli中作为实例属性列出），然后选择所需的实例类型。重新启动实例，进程就完成了。

* 安全组

如果实例在amazon vpc中运行（在第4章中讨论），则可以在实例运行时更改与实例关联的安全组。对于amazon vpc以外的实例（称为ec2 classic），启动后不能更改安全组的关联。
#### 终端保护

* 当不再需要Amazon EC2实例时，可以将状态设置为terminated，实例将被关闭并从AWS基础设施中移除。为了防止通过AWS管理控制台、CLI或API终止，可以为实例启用终止保护启用后，终止实例的调用将失败，直到禁用终止保护。这有助于防止由于人为错误而意外终止。

* 请注意，这只是防止来自AWS管理控制台、cli或api的终止调用。它不阻止操作系统关闭命令触发的终止、自动缩放组的终止（在第5章中讨论）或现货价格变化导致的现货实例的终止（在下一节中讨论）。

### 选项
在Amazon EC2中有几个额外的选项可用于改进成本优化、安全性和性能，这对于考试来说非常重要。

#### 价格选项
* Amazon EC2实例处于运行状态时，每小时向您收费，但每小时收费的金额可能会根据三种定价选项而有所不同：按需实例、保留实例和现货实例。

* 按需实例
在AWS网站上发布的每种实例类型的每小时价格表示按需实例的价格。这是最灵活的定价选项，因为它不需要预先承诺，并且客户可以控制何时启动该实例以及何时终止该实例。这是三种定价方案中每计算小时成本效益最低的，但是它的灵活性允许客户通过为不可预测的工作负载提供可变的计算级别来节省。

* 保留实例
保留实例定价选项允许客户为可预测的工作负载进行容量保留。通过对这些工作负载使用保留实例，客户可以比按需时薪节省高达75%。当购买预订时，客户为该预订实例指定实例类型和可用性区域，并在预订期间为该实例获得较低的有效小时价格。另一个好处是，AWS数据中心的容量是为该客户保留的。决定预订成本的因素有两个：定期承诺和付款选择

承诺期限是保留的期限，可以是一年或三年。承诺时间越长，折扣就越大。
保留实例有三种不同的付款方式：
```
 All Upfront---所有的订房费用都是预付的，在租期内没有每月的费用。
 Partial Upfront---部分预付款提前支付部分预订费，剩余部分在本协议有效期内按月分期支付。
 No Upfront---在本协议有效期内，无需提前按月分期支付全部预订费。
```
折扣金额越大，顾客预付的钱越多

例如，让我们看看提前三年预订对m4.2xlarge实例的有效小时成本的影响。在两种定价选项下连续运行一个实例三年（或26280小时）的成本如表3.5所示。

|---|---|---|
|价格选项|有效的小时成本|三年总成本|
|按需实例|0.479/hour|$0.479/hour*26280hours=$12588.12 |
|三年全部预付费|$4694/26280hours=$0.1786/hour|$4694|
|节省||63%|

表 3.5 保留实例价格样例
* 备注
```
 本例使用撰写本文时发布的价格。AWS迄今已多次降价，因此请查看AWS网站上的当前定价信息。
```

当您的计算需求发生变化时，您可以修改保留的实例，并继续从容量保留中受益。修改不会更改保留实例的剩余期限；它们的结束日期保持不变。不收费，您也不会收到任何新的账单或发票。修改与购买是分开的，不会影响您使用、购买或出售保留实例的方式您可以通过以下一种或多种方式修改整个预订或仅修改一个子集。

```
 同一区域内的交换机可用性区域。              
 在EC2-VPC和EC2 Classic之间切换。              
 更改同一实例系列中的实例类型（仅限Linux实例）。
```

* 现货实例

对于不具有时间关键性并且能够容忍中断的工作负载，spot实例提供了最大的折扣。对于spot实例，客户指定他们愿意为某个实例类型支付的价格。当客户的出价高于当前现货价格时，客户将收到请求的实例。这些实例将像所有其他Amazon EC2实例一样运行，客户将只支付实例运行小时的现货价格。实例将运行到：
```
客户终止它们。
现货价格高于客户的出价。
没有足够的未使用容量来满足现场实例的需求。
```

如果Amazon ec2需要终止spot实例，实例将收到一个终止通知，在amazonec2终止实例之前提供两分钟的警告。由于存在中断的可能性，spot实例只能用于能够容忍中断的工作负载。这可能包括分析、财务建模、大数据、媒体编码、科学计算和测试

**不同定价模式的架构**对于考试来说，重要的是要知道如何利用不同的定价模式来创建一个具有成本效益的架构。这样的架构可能在相同的工作负载中包含不同的定价模式。例如，一个平均每天访问5000次的网站，但在周期性高峰期间，每天访问量会增加到20000次，可能会购买两个保留实例来处理平均流量，但在高峰期间，需要依赖OnDemand实例来满足计算需求。图3.2显示了这样一种架构。

图 3.2 A workload using a mix of On-Demand and Reserved Instances  

#### 租赁选项
AmazonEC2实例有几个租赁选项，可以帮助客户实现安全性和法规遵从性目标。

##### 共享租赁

共享租赁是所有Amazon EC2实例的默认租赁模型，无论实例类型、定价模型等如何。共享租赁意味着一台主机可以容纳来自不同客户的实例。由于AWS不使用过度配置，并将实例与同一主机上的其他实例完全隔离，这是一种安全的租赁模式。

##### 专用实例
专用实例运行在专用于单个客户的硬件上。当客户运行更多专用实例时，更多底层硬件可能专用于其帐户。帐户中的其他实例（未指定为专用的实例）将在共享租用上运行，并在硬件级别与帐户中的专用实例隔离

##### 专用主机
Amazon EC2专用主机是一个物理服务器，具有完全专用于单个客户使用的Amazon EC2实例容量。通过允许您使用现有的服务器绑定的软件许可证来解决许可要求，并降低成本。客户完全控制特定的主机在启动时运行实例。这与专用实例不同，因为专用实例可以在任何专用于帐户的硬件上启动。

### 放置组
放置组是单个可用性区域内实例的逻辑分组。放置组使应用程序能够参与低延迟、10 Gbps的网络建议将放置组用于受益于低网络延迟和/或高网络吞吐量的应用程序。请记住，这表示实例之间的网络连接。若要将此网络性能完全用于放置组，请选择支持增强网络和10 Gbps网络性能的实例类型。

### 实例存储

* 实例存储（有时称为临时存储）为实例提供临时块级存储。此存储位于物理连接到主机的磁盘上。实例存储非常适合于经常更改的信息（如缓冲区、缓存、临时数据和其他临时内容）的临时存储，或用于跨实例组（如Web服务器的负载平衡池）复制的数据。Amazon ec2实例可用的实例存储的大小和类型取决于实例类型。在编写本文时，各种实例类型可用的存储空间从无实例存储到242tb实例存储不等实例类型还确定实例存储卷的硬件类型虽然有些提供硬盘驱动器（hdd）实例存储，但其他实例类型使用固态驱动器（ssd）来提供非常高的随机i/o性能。              

* 实例存储包含在Amazon ec2实例的成本中，因此对于适当的工作负载来说，它们是非常经济有效的解决方案。实例存储的关键方面是它们是临时的，当发生如下情况时，实例存储中的数据会丢失：
```
 * 底层的磁盘驱动失效
 * 实例停止（如果实例重启，数据会持久化）
 * 实例终结
```
* 因此，不要依赖实例存储来获取有价值的长期数据。相反，可以通过raid建立一定程度的冗余，或者使用支持冗余和容错的文件系统，比如hadoop的hdfs。将数据备份到更持久的数据存储解决方案，如Amazon简单存储服务（Amazon S3）或Amazon EBS，通常足以满足恢复点目标。

## Amazon Elastic Block Store（Amazon EBS）

* 虽然实例存储是实现适当工作负载的经济方法，但其有限的持久性使它们不适合许多其他工作负载对于需要更持久的块存储的工作负载，amazon提供amazon ebs


### Elastic Block Store Basic
* Amazon EBS提供持久块级存储卷，用于Amazon EC2实例。每个Amazon EBS卷在其可用性区域内自动复制，以保护您免受组件故障的影响，提供高可用性和耐用性。Amazon EBS卷有多种类型，性能特点和价格不同。可以将多个amazon ebs卷附加到单个Amazon ec2实例，但一次只能将一个卷附加到单个实例。

###Amazon EBS 卷类型
* Amazon EBS卷有几种不同的类型。类型在基础硬件、性能和成本等方面有所不同。了解不同类型的属性很重要，这样您就可以指定满足工作负载在考试中的性能要求的最经济高效的类型。

#### 磁卷
* 磁卷具有所有amazon ebs卷类型中最低的性能特征。因此，它们的每千兆字节成本最低。对于适当的工作负载，它们是一个优秀的、经济高效的解决方案。

* 一个具有磁性的Amazon EBS卷的大小可以从1 GB到1 TB不等，平均为100 IOPS，但能够突发到数百IOPS。它们最适合于：
```
 很少访问数据的工作负载             
 顺序读取              
 需要低成本存储的情况
```
* 不管您在卷上实际存储了多少数据，都会根据所提供的数据空间量对磁卷进行计费。

#### 通用固态硬盘
* 通用ssd卷提供经济高效的存储，非常适合各种工作负载。它们以适合各种工作负载的中等价位提供强大的性能。
* 一个通用的ssd卷的大小可以从1gb到16tb不等，并提供每千兆字节3 iops的基线性能，最高可达10000 iops。例如，如果您提供1 TB的卷，您可以期望3000 IOPS的基线性能。5 TB容量不能提供15000 IOPS基线，因为它将在10000 IOPS时达到上限1 TB以下的通用固态硬盘卷还具有长时间突发高达3000 IOPS的能力例如，如果您有一个500 GB的卷，您可以期望1500 IOPS的基线无论何时不使用这些IOPS，它们都会累积为I/O信用。当您的卷流量很大时，它将以高达3000 IOPS的速率使用I/O信用，直到它们耗尽。此时，性能恢复到1500 IOPS。在1 TB时，卷的基线性能已经达到3000 IOPS，因此不适用突发行为。
              
* 通用SSD卷是根据所提供的数据空间量计费的，而不管您实际在卷上存储了多少数据它们适用于各种各样的工作负载，其中最高的磁盘性能并不重要，例如：
```
 * 系统启动盘
 * 中小型数据库
 * 开发测试环境
```

#### 配置的IOPS固态硬盘
* 配置的IOPS SSD卷旨在满足I/O密集型工作负载的需要，特别是对存储性能和随机访问I/O吞吐量一致性敏感的数据库工作负载。虽然它们是每GB最昂贵的Amazon EBS卷类型，但它们以可预测的方式提供了任何Amazon EBS卷类型中最高的性能。
* 配置的IOPS固态硬盘卷的大小可以从4 GB到16 TB不等。当您提供一个配置的IOPS SSD卷时，您不仅指定大小，而且还指定期望的IOPS数量，直到最大的30倍数量的GB的体积，或20000 IOPS。您可以在RAID 0配置中将多个卷条带化在一起，以获得更大的大小和更高的性能在给定的一年中，Amazon EBS在99.9%的时间内提供了10%的IOPS性能
* 定价基于卷的大小和保留的IOPS数量，每千兆字节的成本略高于一般用途的SSD卷，并根据卷的大小而不是用于存储数据的卷的数量来应用根据提供的IOPS数量（无论是否已使用）额外收取每月费用。

* 配置的IOPS SSD卷提供可预测的高性能，非常适合于如下场景：
```
 * 需要持续IOPS性能的关键业务应用程序
 * 大型数据库工作负载
```

|---|---|---|---|
|特性|通用SSD|配置的IOPS SSD| 磁盘|
|使用场景|系统启动盘，虚拟桌面，小中型数据库，开发和测试环境|关键业务应用程序需要持续的IOPS性能e或超过10000 IOPS或每个卷160MB的吞吐量，大型数据库|很少访问数据的冷工作负载，存储成本最低很重要的场景|
|卷大小|1	GiB–16TiB|4GiB-16TiB|1GiB-1TiB|
|最大吞吐量|160MB|320MB|40-90MB|
|IOPS性能|3 IOPS/GiB（高达10000 IOPS）的基线性能，对于1000 GiB以下的卷，能够突发到3000 IOPS |始终在配置级别执行，最高可达20000 IOPS最大值|平均100 IOPS，能够突发到数百IOPS|
表格3.6 EBS卷类型对比

* 备注
```
 * 在撰写本文时，AWS发布了两种新的HDD卷类型：吞吐量优化HDD和冷HDD随着时间的推移，预计这些新类型将取代当前的磁卷类型，满足任何需要HDD性能的工作负载的需要。              
 * 吞吐量优化的HDD卷是为频繁访问、大数据、数据仓库和日志处理等吞吐量密集型工作负载而设计的低成本HDD卷体积可高达16 TB，最大IOPS为500，最大吞吐量为500 Mb/s。这些体积比一般用途SSD卷便宜得多。              
 * 冷硬盘卷是为访问频率较低的工作负载而设计的，例如每天需要较少扫描的较冷数据卷最多可以达到16 TB，最大吞吐量为250，最大吞吐量为250兆字节/秒。
```

#### Amazon EBS优化实例
* 当使用除磁卷和Amazon EBS I/O之外的任何卷类型时，使用Amazon EBS优化实例以确保Amazon EC2实例准备好利用Amazon EBS卷的I/O是很重要的。Amazon EBS优化实例使用优化的配置堆栈，并为Amazon EBS I/O提供额外的专用容量。此优化通过最小化Amazon EBS I/O与实例的其他流量之间的争用，为Amazon EBS卷提供最佳性能当您为一个实例选择Amazon EBS optimized时，您需要为该实例支付额外的每小时费用检查AWS文档以确认哪些实例类型可用作Amazon EBS优化实例。

### 数据保护

在Amazon EBS卷的整个生命周期中，有几个实践和服务在您参加考试时应该知道。

#### 备份/恢复（快照）

无论卷类型如何，您都可以通过拍摄时间点快照来备份Amazon EBS卷上的数据。快照是增量备份，这意味着仅保存设备上自最近快照以来已更改的块。

##### 拍摄快照
可以通过许多方法拍摄快照：
```
 * 通过AWS管理控制台
 * 通过CLI
 * 通过API
 * 通过设置常规快照的计划
```

* 快照的数据使用Amazon S3技术存储。拍摄快照的操作是免费的。您只需支付快照数据的存储成本。              
* 当您请求快照时，将立即创建时间点快照，并且可以继续使用卷，但快照可能会保持挂起状态，直到所有修改的块都传输到Amazon S3。              
* 重要的是要知道，虽然快照是使用Amazon S3技术存储的，但它们存储在AWS控制的存储中，而不是您帐户的Amazon s3存储桶中。这意味着您不能像其他Amazon S3对象那样操作它们。相反，您必须使用Amazon EBS快照功能来管理它们。快照被约束到创建它们的区域，这意味着您只能使用它们在同一区域中创建新卷。如果需要在其他区域中还原快照，可以将快照复制到其他区域。

##### 通过快照创建卷

* 要使用快照，可以从快照创建一个新的Amazon EBS卷。执行此操作时，会立即创建卷，但会延迟加载数据。这意味着可以在创建卷时访问该卷，如果请求的数据尚未还原，则将在第一次请求时还原该卷。因此，最好通过访问卷中的所有块来初始化从快照创建的卷。              

* 快照还可以用于增加Amazon EBS卷的大小。要增加Amazon EBS卷的大小，请拍摄该卷的快照，然后从快照中创建所需大小的新卷。将原始卷替换为新卷。

##### 恢复卷
* 由于Amazon EBS卷在实例的生命周期之后仍然存在，因此如果实例失败，可以恢复数据。如果Amazon EBS支持的实例失败，并且启动驱动器上有数据，那么将卷与实例分离相对简单。除非卷的DeleteOnTermination标志设置为false，否则应在实例终止之前分离该卷。然后可以将卷作为数据卷附加到另一个实例，并读取和恢复数据。

##### 加密选项
* 许多工作负载都要求静态加密数据，这是因为法规遵从性或内部公司标准。Amazon EBS为所有卷类型提供本机加密。

* 当你启动一个加密的Amazon EBS卷时，Amazon使用AWS密钥管理服务（KMS）来处理密钥管理。除非您选择在该服务中单独创建的主密钥，否则将创建新的主密钥。您的数据和相关密钥使用行业标准AES-256算法加密。加密发生在承载Amazon EC2实例的服务器上，因此，数据实际上是在主机和存储媒体之间以及媒体上传输时加密的（有关支持Amazon EBS加密的实例类型列表，请参阅AWS文档）。加密是透明的，因此所有数据访问都与未加密的卷相同，而且，加密卷上的IOPS性能与未加密卷上的相同，对延迟的影响最小。从加密卷上获取的快照会自动加密，从加密快照创建的卷也会自动加密。

## 总结

* Compute是完成工作负载所需的计算能力。Amazon EC2是向客户提供计算的主要服务。
* 实例类型定义了支持该实例的虚拟硬件。可用的实例类型在vcpu、内存、存储和网络性能方面各不相同，几乎可以满足任何工作负载。
* AMI定义实例的初始软件状态，包括操作系统和应用程序。AIS有四个来源：AWS发布的通用OSS，合作伙伴在AWS市场发布了AMIS，软件包预先安装，客户从现有的亚马逊EC2实例生成AMI，并从虚拟服务器上传AMIS 。
* 实例可以通过公共DNS名称、公共IP地址或弹性IP地址来寻址。要访问新启动的Linux实例，请使用密钥对的私有部分通过SSH连接到该实例。要访问新创建的Windows实例，请使用密钥对的私有部分来解密随机初始化的本地管理员密码。
* 进出实例的网络流量可以由一个称为安全组的虚拟防火墙控制。安全组允许基于方向、端口、协议和源/目标地址阻止通信的规则。
* 引导允许您运行一个脚本，用操作系统配置和应用程序初始化您的实例。此功能允许实例在启动时自行配置。实例启动后，您可以更改其实例类型，或者对于Amazon VPC实例，更改与之关联的安全组。
* 实例的三种定价选项是按需、保留实例和现货。OnDemand的每小时成本最高，无需预先承诺，并让您完全控制实例的生命周期。保留实例需要承诺，并在保留的整个生命周期内降低总体成本。Spot实例是AWS根据客户的出价提供的空闲计算能力。每小时成本的节省可能非常大，但是当出价超过客户当前出价时，实例可以关闭。 
* 实例存储是包含在实例每小时成本中的块存储。可用存储的数量和类型因实例类型而异。实例存储在相关实例停止时终止，因此它们只应用于临时数据或提供冗余的体系结构（如Hadoop的HDFS）。
* Amazon EBS提供多种类型的持久块存储。磁力每千兆字节的成本最低，性能适中。通用SSD是一种经济高效的存储，可提供高达10000 IOPS的速度。配置的IOPS SSD具有最高的每千兆字节成本，非常适合于对存储性能敏感的I/O密集型工作负载。快照是存储在Amazon S3中的Amazon EBS卷的增量备份。Amazon EBS卷可以加密。

## 考试基础
### 了解启动Amazon EC2实例的基础知识
* 要启动实例，必须指定AMI（在启动时定义实例上的软件）和实例类型（定义支持实例的虚拟硬件（内存、vCPUs等）

### 了解哪些架构适合Amazon EC2的定价选项
* Spot实例最适合于能够容纳中断的工作负载。保留实例最适合于一致的、长期的计算需求。按需实例提供灵活的计算以响应缩放需求。

### 了解如何组合多种定价选项
* 从而实现成本优化和可扩展性。按需实例可用于扩展在保留实例上运行的web应用程序，以响应临时流量高峰。对于具有多个从队列中读取的保留实例的工作负载，可以使用Spot实例以经济高效的方式减轻繁重的通信量。这只是无数工作负载可能使用不同定价选项的例子中的两个。

### 了解增强网络的好处
* 增强的网络使您能够获得更高的PPS性能、更低的网络抖动和更低的延迟。

### 了解虚拟机导入/导出的功能
* VM导入/导出允许您将现有的VM导入AWS作为Amazon EC2实例或AMIS。通过VM导入/导出导入的Amazon EC2实例也可以导出回虚拟环境。

### 了解通过internet访问实例的方法
* 您可以通过公共IP地址、弹性IP地址或公共DNS名称通过web访问Amazon EC2实例。访问Amazon VPC内的实例还有其他方法，包括私有IP地址和ENIs。

### 了解实例存储的生存期
* 实例存储区中的数据在实例停止或终止时丢失。实例存储数据在操作系统重新启动后仍然有效。

### 了解Amazon EC2定价选项的特性
* 按需实例不需要预先承诺，可以随时启动，并按小时计费。保留的实例需要一个预先的承诺，并且根据它们是否全部预先支付、部分预先支付或不预先支付而在成本上有所不同。当您的出价超过当前的现货价格时，将启动现货实例。现货实例将运行，直到现货价格超过您的出价，在这种情况下，该实例将得到两分钟的警告和终止。

### 知道什么决定了网络性能
* 每个实例类型都针对低、中、高或10 Gbps的网络性能进行评级，较大的实例类型通常具有较高的评级。另外，一些实例类型提供了增强的网络，从而进一步提高了网络性能。

### 了解什么是实例元数据以及如何获取它
* 元数据是关于Amazon EC2实例的信息，例如实例ID、实例类型和安全组，这些信息可以从实例中获得。它可以通过对特定IP地址的HTTP调用获得。              

### 了解安全组如何保护实例
* 安全组是控制进出Amazon EC2实例流量的虚拟防火墙。默认情况下，它们是拒绝的，您可以通过添加指定通信方向、端口、协议和目标地址的规则（通过无类域间路由[CIDR]块）来允许通信。它们应用于实例级别，这意味着同一安全组中实例之间的通信必须遵守该安全组的规则。它们是有状态的，这意味着传出规则将允许响应，而无需关联传入规则。

### 知道如何解释安全组的影响
* 当一个实例是多个安全组的成员时，其效果是所有组中所有规则的联合。
### 了解不同的Amazon EBS卷类型、它们的特性和它们相应的工作负载
* 磁卷提供100 IOPS的平均性能，最多可配置1 TB。它们适合冷的和不常访问的数据。通用SSD卷提供3个IOPS/GB，最高可达10000 IOPS，较小的卷能够突发3000 IOPS。它们最多可配置16 TB，适用于开发/测试环境、小型数据库等。配置的IOPS固态硬盘最多可为16 TB的卷提供20000个一致的IOPS。对于执行许多事务的大型数据库等工作负载，它们是最佳选择。

### 知道如何加密Amazon EBS卷
* 任何卷类型都可以在启动时加密。加密基于AWS KMS，对附加实例上的应用程序透明。

### 了解快照的概念和过程。
* 快照提供Amazon EBS卷的时间点备份，并存储在Amazon S3中。后续快照是增量快照，它们只存储增量。当您请求快照时，将立即创建时间点快照，并且可以继续使用卷，但快照可能会保持挂起状态，直到所有修改的块都传输到Amazon S3。快照可以在区域之间复制。


### 了解Amazon EBS优化实例如何影响Amazon EBS性能
* 除了控制Amazon EBS卷内外性能的IOPS之外，还可以使用Amazon EBS优化实例来确保Amazon EBS I/O的额外专用容量。

## 练习
有关完成这些练习的帮助，请参阅以下用户指南：
* Amazon EC2(Linux): http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html
* Amazon EC2(Windows): http://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/concepts.html
* Amazon EBS: http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AmazonEBS.html

### 练习 3.1

#### 启动并连接到Linux实例
在本练习中，您将启动一个新的Linux实例，使用SSH登录，并安装任何安全更新。
 * 1. 在Amazon EC2控制台中启动一个实例。
 * 2. 选择Amazon Linux AMI。
 * 3. 选择t2.medium实例类型。
 * 4. 在默认VPC或EC2 Classic中启动实例。
 * 5. 为实例分配一个公共IP地址。
 * 6. 向 Key:Name，Value:Exercise 3.1的实例添加标记。
 * 7. 创建一个名为Cert Book的新安全组。
 * 8. 在Cert Book中添加一个规则，允许从工作站的IP地址（www.WhatsMyIP.org是确定IP地址的好方法）进行SSH访问。
 * 9. 启动实例。
 * 10. 当提示输入密钥对时，请选择您已经拥有的密钥对或创建新的密钥对，然后下载私有部分。Amazon生成keyname.pem文件，您需要keyname.ppk文件通过SSH连接到实例。Puttygen.exe是一个从.pem文件创建.ppk文件的实用程序。
 * 11. 使用公共IP地址、用户名ec2 user和keyname.ppk文件SSH到实例中。
 * 12. 在命令行提示符下，运行sudo yum update-security -y。
 * 13. 关闭SSH窗口并终止实例。

### 练习 3.2
#### 使用引导启动Windows实例
在本练习中，您将启动一个Windows实例并指定一个非常简单的引导脚本。然后您将确认引导脚本已在实例上执行。
* 1. 在Amazon EC2控制台中启动一个实例。
* 2. 选择Microsoft Windows Server 2012基本AMI。
* 3. 选择t2.medium实例类型。
* 4. 在默认VPC或EC2 Classic中启动实例。
* 5. 为实例分配一个公共IP地址。
* 6. 在“高级详细信息”部分中，输入以下文本作为用户数据：<script>md c:\temp</script>              
* 7. 向Key:Name，Value:Exercise 3.2的实例添加标记。
* 8. 使用练习3.1中的证书簿安全组。
* 9. 启动实例。
* 10. 使用练习3.1中的密钥对。
* 11. 在连接实例UI上，解密管理员密码，然后下载RDP文件以尝试连接到实例。您的尝试应失败，因为证书簿安全组不允许RDP访问。
* 12. 打开证书簿安全组并添加允许从您的IP地址访问RDP的规则。
* 13. 再次尝试通过RDP访问实例。
* 14. 连接RDP会话后，打开Windows资源管理器并确认已创建c:\ temp文件夹。
* 15. 结束RDP会话并终止实例。

### 练习 3.3
#### 确认实例停止时实例存储丢失
在本练习中，你将观察到在实例停止后Amazon EC2上的数据将会丢失。
* 1. 在Amazon管理控制台启动一台实例；
* 2. 选择Microsoft Windows Server 2012基本AMI
* 3. 选择m3.medium 实例类型
* 4. 在默认VPC或EC2 Classic中启动实例。
* 5. 给实例分配一个public IP地址
* 6. 给实例增加一个tag，Key：Name，Value：Exercise 3.3
* 7. 使用练习3.2中更新的证书簿安全组。
* 8. 启动实例；
* 9. 使用练习-3.1中的密钥对
* 10. 通过RDP解密管理员密码登录到实例。
* 11. 连接RDP会话后，打开Windows资源管理器。
* 12. 创建一个新的文件夹：z:\temp
* 13. 注销RDP会话；
* 14.  在控制台中，将实例的状态设置为Stopped
* 15. 一旦实例停止成功，在启动实例；
* 16. 使用RDP重新登录到实例。
* 17. 打开Windows资源管理器并确认z:\ temp文件夹已消失；
* 18. 结束RDP会话并终止实例。

### 练习 3.4
#### 启动一个Spot实例
在这个练习中，你将会创建一个Spot实例
* 1. 在Amazon EC2 控制台，进入Spot 请求页；
* 2. 查看m3.medium价格历史，特别时最近的价格；
* 3. 记下最近的价格和可用区域；
* 4. 在Amazon EC2 控制台启动一个实例；
* 5. 选择Amazon Linux AMI;
* 6. xuanze t2.medium 实例类型；
* 7. 在配置实例页面，请求一个Spot实例；
* 8. 在默认VPC或EC2 Classic中启动实例（注意，默认VPC将定义实例的可用区域）；
* 9. 给实例分配一个public IP地址；
* 10. 请求一个Spot实例，并输入一个出价高于记录的现货价格几美分（的价格）；
* 11. 结束启动实例；
* 12. 回到Spot请求页，查看你的请求，如果你的出价足够高，你应该看到实例状态改变为：Active，并出现一个实例ID；
* 13. 在Amazon EC2 控制台的实例页面找到实例，注意：Spot生命周期在描述中的生命周期字段表示。
* 14. 一旦实例处于running，结束它。

### 练习 3.5 
#### 存取Metadata
在这个练习中，你将会从OS存取实例的Metadata。
* 1. 在Amazon EC2控制台里启动一个实例；
* 2. 选贼Amazon Linux AMI；
* 3. 选择t2.medium 实例类型；
* 4. 在默认VPC或EC2 Classic中启动实例;
* 5. 为实例分配一个public IP地址；
* 6. 给实例增加一个tag，Key：Name，Value：Exercise 3.5
* 7. 使用Cert Book 安全组
* 8. 启动实例；
* 9. 使用练习-3.1中（10）的key对；
* 10. 通过Public IP地址，以用户名：ec2-user，和keyname.ppk文件，使用SSH连接实例；
* 11. 在Linux 提示命令行，输入如下信息获取可用的metadata列表：curl	http://169.254.169.254/latest/meta-data/ 
* 12. 看一个值，将名字增加到上URL的尾部，例如找到安全组类型增加到尾部：curl	http://169.254.169.254/latest/meta-data/security-groups；
* 13. 尝试其他的值，以/结尾的名字包含更长的子值列表；
* 14. 关闭SSH窗口并结束实例；

### 练习 3.6
#### 创建一个Amazon EBS卷，展示实例结束后仍然存在
在这个练习中，您将看到Amazon EBS卷如何在实例生命周期之外持续存在。
* 1. 在Amazon EC2 控制台启动一个实例；
* 2. 选择Amazon Linux AMI；
* 3. 选择t2.medium实例类型；
* 4. 通过默认VPC或者EC2-Classic启动实例；
* 5. 为实例分配一个public IP地址；
* 6. 增加第二个50G的卷，注意：在结束实例后删除Root卷；
* 7. 给实例增加一个tag，Key：Name，Value：Exercise 3.6；
* 8. 使用Cert Book安全组（前面练习中创建的）；
* 9. 启动实例；
* 10. 在EBS控制台上找到两个两个卷，将他们都命名为：Exercise 3.6；
* 11. 结束实例；
注意：启动驱动已经删除，但是第二个Amazon EBS卷仍然存在，现在可以说可用，不要删除这个可用的卷。

### 练习 3.7
#### 拍摄快照和恢复
这个练习指导你拍摄快照，并通过三种方法恢复。
* 1. 在Amazon EBS控制台找到你在练习3.6中创建的卷；
* 2. 拍摄快照，并命名卷的名字为：Exercise 3.7；
* 3. 在快照控制台，等待快照完成（当卷是空的时候，拍摄快照应该是非常快）；
* 4. 在AWS 快照管理控制台的快照页面，选择最新的快照，选择创建卷；
* 5. 使用默认配置创建卷；
* 6. 在找到快照，并再创建一个卷；设置这个新卷的大小为：100G（使用快照并将快照还原为新的、更大的卷，是用以说明如何解决增大现有卷的大小的问题的），重新找到快照的位置并选择复制，复制快照到另外一个Region，并将描述写为：Exercise 3.7；
* 7. 进入6中快照要复制到的那个Region，等待快照变成可用；
* 8. 在新的Region中使用快照创建卷，这就是如何在Regions之间共享Amazon EBS卷的方法，那就是：拍摄快照，并复制快照；
* 9. 删除上面的4个卷；

### 练习 3.8
#### 启动一个加密卷
在这个实例中，你将启动一个带有加密的Amazon EBS卷的Amazon EC2实例，并存一些数据在这个卷上，用以确认加密对实例时透明的。
* 1. 在Amazon EC2控制台启动一个实例；
* 2. 选择Microsoft Window Server 2012 AMI；
* 3. 选择m3.medium实例类型；
* 4. 通过默认VPC或者EC2-Classic启动实例；
* 5. 给实例分配一个Public IP地址；
* 6. 在存储页面上，为实例增加一个大小为50GB的加密Amazon EBS卷；
* 7. 为实例增加一个标记，键：Name，值：Exercise 3.8；
* 8. 使用练习3.2中更新的Cert BOOK安全组；
* 9. 启动实例；
* 10. 选择练习3.1中的Key对；
* 11. 解密administrator密码并使用RDP登陆到实例；
* 12. 一旦RDP会话连接，打开Notepad；
* 13. 向Notdpad中输入一些随机信息，保存为：d:\testfile.txt，然后关闭Notepad；
* 14. 在Windows Explorer中找到：d:\testfile.txt，用Notepad打开，确认Notepad中的数据不是加密的；
* 15. 注销；
* 16. 结束实例；

### 练习 3.9
#### 分离引导驱动器并重新连接到另一个实例
在这个练习中，你将练习从一个停止的驱动上移除Amazon EBS卷并连接到两外一个实例，恢复数据。
* 1. 在Amazon EC2控制台启动一个实例；
* 2. 选择Microsoft Windows Server 2012 Base AMI；
* 3. 选择t2.medium 实例类型；
* 4. 通过默认的VPC或者EC2-Classic启动实例；
* 5. 给实例分配一个Public IP地址；
* 6. 为实例增加一个标记，键：Name，值：Exercise 3.9 Source；
* 7. 使用前面练习中的Cert BOOK安全组；
* 8. 使用练习3.1中的key对启动实例；
* 9. 在Amazon EC2控制台启动第二个实例；
* 10. 选择Microsof Windows Server 2012 Base AMI；
* 11. 选择t2.medium 实例类型；
* 12. 通过默认的VPC或者EC2-Classic启动实例；
* 13. 给实例分配一个public IP地址；
* 14. 为实例增加一个标记，键：Name，值：Exercise 3.9 Destination；
* 15. 使用前面练习中的Cert BOOK安全组；
* 16. 使用练习3.1中的key对启动实例；
* 17. 一旦两个实例都处于running状态，停止第一个实例，记住实例的实例ID；
* 18. 在Amazon EC2控制台进入Amazon EBS页面并通过实例ID找到附加的原始实例的卷，将卷和实例分开；
* 19. 当卷变成可用状态时，将卷与第二个实例（Destination）相连接；
* 20. 使用administrator账户通过RDP登录到Destination实例；
* 21. 打开命令行窗口（cmd.exe）
* 22. 在命令行提示窗口，输入如下命令：
```
  C:\Users\Administrator >diskpart 
  DISKPART>select disk 1 
  DISKPART>online disk 
  DISKPART>exit C:\Users\Administrator>dir e:
```
从停止的原始驱动移除的卷现在作为目标实例的E:驱动是可读了，因此卷的数据也能获取到；
* 23. 结束所有的实例，并在这个过程中，确认删除所有的卷。

## 复习题
### 1. Your web application needs four instances to support steady traffic nearly all of the time. On the last day of each month, the traffic triples. What is a cost-effective way to handle this traffic pattern?
* A. Run 12 Reserved Instances all of the time.
* B. Run four On-Demand Instances constantly, then add eight more On-Demand Instances on the last day of each month.
* C. Run four Reserved Instances constantly, then add eight On-Demand Instances on the last day of each month. 
* D. Run four On-Demand Instances constantly, then add eight Reserved Instances on the last day of each month.

### 2. Your order-processing application processes orders extracted from a queue with two Reserved Instances processing 10 orders/minute. If an order fails during processing, then it is returned to the queue without penalty. Due to a weekend sale, the queues have several hundred orders backed up. While the backup is not catastrophic, you would like to drain it so that customers get their confirmation emails faster. What is a cost-effective way to drain the queue for orders? 
* A. Create more queues. 
* B. Deploy additional Spot Instances to assist in processing the orders. 
* C. Deploy additional Reserved Instances to assist in processing the orders. 
* D. Deploy additional On-Demand Instances to assist in processing the orders. 

### 3. Which of the following must be specified when launching a new Amazon Elastic Compute Cloud (Amazon EC2) Windows instance? (Choose 2 answers) 
* A. The Amazon EC2 instance ID 
* B. Password for the administrator account 
* C. Amazon EC2 instance type 
* D. Amazon Machine Image (AMI) 

### 4. You have purchased an m3.xlarge Linux Reserved instance in us-east-1a. In which ways can you modify this reservation? (Choose 2 answers) 
* A. Change it into two m3.large instances. 
* B. Change it to a Windows instance. 
* C. Move it to us-east-1b. 
* D. Change it to an m4.xlarge. 

### 5. Your instance is associated with two security groups. The first allows Remote Desktop Protocol (RDP) access over port 3389 from Classless Inter-Domain Routing (CIDR) block 72.14.0.0/16. The second allows HTTP access over port 80 from CIDR block 0.0.0.0/0. What traffic can reach your instance?
* A. RDP and HTTP access from CIDR block 0.0.0.0/0 
* B. No traffic is allowed. 
* C. RDP and HTTP traffic from 72.14.0.0/16 
* D. RDP traffic over port 3389 from 72.14.0.0/16 and HTTP traffic over port 80 from 0.0.00/0 

### 6. Which of the following are features of enhanced networking? (Choose 3 answers) 
* A. More Packets Per Second (PPS) 
* B. Lower latency 
* C. Multiple network interfaces 
* D. Border Gateway Protocol (BGP) routing 
* E. Less jitter 

### 7. You are creating a High-Performance Computing (HPC) cluster and need very low latency and high bandwidth between instances. What combination of the following will allow this? (Choose 3 answers) 
* A. Use an instance type with 10 Gbps network performance. 
* B. Put the instances in a placement group. 
* C. Use Dedicated Instances. 
* D. Enable enhanced networking on the instances. 
* E. Use Reserved Instances. 

### 8. Which Amazon Elastic Compute Cloud (Amazon EC2) feature ensures that your instances will not share a physical host with instances from any other AWS customer? 
* A. Amazon Virtual Private Cloud (VPC) 
* B. Placement groups 
* C. Dedicated Instances 
* D. Reserved Instances 

### 9. Which of the following are true of instance stores? (Choose 2 answers) 
* A. Automatic backups 
* B. Data is lost when the instance stops. 
* C. Very high IOPS 
* D. Charge is based on the total amount of storage provisioned. 

### 10. Which of the following are features of Amazon Elastic Block Store (Amazon EBS)? (Choose 2 answers) 
* A. Data stored on Amazon EBS is automatically replicated within an Availability Zone.
* B. Amazon EBS data is automatically backed up to tape. 
* C. Amazon EBS volumes can be encrypted transparently to workloads on the attached instance. 
* D. Data on an Amazon EBS volume is lost when the attached instance is stopped. 

### 11. You need to take a snapshot of an Amazon Elastic Block Store (Amazon EBS) volume. How long will the volume be unavailable? 
* A. It depends on the provisioned size of the volume. 
* B. The volume will be available immediately. 
* C. It depends on the amount of data stored on the volume. 
* D. It depends on whether the attached instance is an Amazon EBS-optimized instance. 

### 12. You are restoring an Amazon Elastic Block Store (Amazon EBS) volume from a snapshot. How long will it be before the data is available? 
* A. It depends on the provisioned size of the volume. 
* B. The data will be available immediately. 
* C. It depends on the amount of data stored on the volume. 
* D. It depends on whether the attached instance is an Amazon EBS-optimized instance. 

### 13. You have a workload that requires 15,000 consistent IOPS for data that must be durable. What combination of the following steps do you need? (Choose 2 answers) 
* A. Use an Amazon Elastic Block Store (Amazon EBS)-optimized instance. 
* B. Use an instance store. 
* C. Use a Provisioned IOPS SSD volume. 
* D. Use a magnetic volume. 

### 14. Which of the following can be accomplished through bootstrapping? 
* A. Install the most current security updates. 
* B. Install the current version of the application. 
* C. Configure Operating System (OS) services. 
* D. All of the above. 

### 15. How can you connect to a new Linux instance using SSH? 
* A. Decrypt the root password. 
* B. Using a certificate 
* C. Using the private half of the instance’s key pair 
* D. Using Multi-Factor Authentication (MFA) 

### 16. VM Import/Export can import existing virtual machines as: (Choose 2 answers) 
* A. Amazon Elastic Block Store (Amazon EBS) volumes
* B. Amazon Elastic Compute Cloud (Amazon EC2) instances 
* C. Amazon Machine Images (AMIs) 
* D. Security groups 

### 17. Which of the following can be used to address an Amazon Elastic Compute Cloud (Amazon EC2) instance over the web? (Choose 2 answers) 
* A. Windows machine name 
* B. Public DNS name 
* C. Amazon EC2 instance ID 
* D. Elastic IP address 

### 18. Using the correctly decrypted Administrator password and RDP, you cannot log in to a Windows instance you just launched. Which of the following is a possible reason? 
* A. There is no security group rule that allows RDP access over port 3389 from your IP address. 
* B. The instance is a Reserved Instance. 
* C. The instance is not using enhanced networking. 
* D. The instance is not an Amazon EBS-optimized instance. 

### 19. You have a workload that requires 1 TB of durable block storage at 1,500 IOPS during normal use. Every night there is an Extract, Transform, Load (ETL) task that requires 3,000 IOPS for 15 minutes. What is the most appropriate volume type for this workload? 
* A. Use a Provisioned IOPS SSD volume at 3,000 IOPS. 
* B. Use an instance store. 
* C. Use a general-purpose SSD volume. 
* D. Use a magnetic volume. 

### 20. How are you billed for elastic IP addresses? 
* A. Hourly when they are associated with an instance 
* B. Hourly when they are not associated with an instance 
* C. Based on the data that flows through them 
* D. Based on the instance type to which they are attached
