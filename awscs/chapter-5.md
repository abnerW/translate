# 第五章 Elastic Load Balancing, Amazon CloudWatch, 以及Auto Scaling
**《AWS认证解决方案架构师-联合考试》中的本章节目标包括不限于如下内容：**

## 第一点 设计高可用、低成本、容错、可扩展的系统
### 找出和识别云架构考虑因素，例如：基础组件和有效性设计
* 弹性和可扩展性

## 第二点 实现/部署

### 使用Amazon Ec2、Amazon Simple Storage Service（Amazon S3）、AWS Elastic Beanstalk、AWS Cloudformation、AWS Opsworks、Amazon Virtual Private Cloud（Amazon VPC）和AWS Identity And Access Management（IAM）确定适当的技术和方法来编码和实现云解决方案。

**包含如下内容**
```
  * 在AWS全球基础设施上发布实例
```
## 第三点 数据安全

### 认识并实施安全实践以实现最佳的云部署和维护
**可能包含如下内容**
```
 * CloudWatch Logs
```

### 第四点 Troubleshooting
**可能包含如下内容**
```
 一般故障排除信息和问题 
```
## 简介

* 在本章，将会学习如何在AWS上，独立或者组合一起使用ELB，Amazon CloudWatch和Auto Scaling帮助你高效、经济有效地部署高可用和优化的工作负载。

* ELB是一个高可用的服务，用于讲流量分发到Amazon EC2实例上，包括提供灵活性和控制到Amazon EC2实例的访问进入请求的选项。

* Amazon CloudWatch 是一个监控AWS 云资源和运行在AWS上的应用的服务。它收集并跟踪指标，收集并监控日志文件，设置告警。Amazon CloudWatch有一个免费的基本监控等级，和需要额外付费的更加详细的监控等级。

* Auto Scaling 是一个允许按照你设置的条件，通过扩缩Amazon EC2数量维持你的用用的高可用的服务。

* 这章分别讲述如上三个服务，但也强调如何协同工作，使你在AWS上构建更加健壮和高可用的体系结构。

## ELB

* 能够访问云中大量服务器（如AWS上的Amazon EC2实例）的一个优点是能够为最终用户提供更一致的体验。确保一致性的一种方法是跨多个服务器平衡请求负载。负载平衡器是一种机制，它自动跨多个Amazon EC2实例分配流量。您可以在Amazon EC2实例上管理自己的虚拟负载平衡器，也可以利用称为弹性负载平衡的AWS云服务，该服务为您提供托管负载平衡器。

* 弹性负载平衡服务允许您在一个或多个可用性区域中跨一组Amazon EC2实例分发流量，从而使您能够在应用程序中实现高可用性。弹性负载平衡支持到Amazon EC2实例的超文本传输协议（HTTP）、超文本传输协议安全（HTTPS）、传输控制协议（TCP）和安全套接字层（SSL）通信的路由和负载平衡。弹性负载平衡为域名系统（DNS）配置提供了一个稳定的、单一规范名称记录（CNAME）入口点，并支持面向Internet和面向内部应用程序的负载平衡器。弹性负载平衡支持Amazon EC2实例的运行状况检查，以确保流量不会路由到不正常或失败的实例。另外，弹性负载平衡可以根据收集到的指标自动扩展。

* 使用弹性负载平衡有几个优点。由于弹性负载平衡是一种托管服务，因此它可以自动伸缩以满足应用程序流量增加的需求，并且在一个区域内作为服务是高度可用的。弹性负载平衡通过在多个可用性区域中跨正常实例分布流量，帮助您实现应用程序的高可用性。此外，弹性负载平衡与自动伸缩服务无缝集成，以自动伸缩负载平衡器后面的Amazon EC2实例。最后，弹性负载平衡是安全的，它与Amazon虚拟私有云（Amazon VPC）一起在应用层之间内部路由流量，允许您只公开面向Internet的公共IP地址。弹性负载平衡还支持集成的证书管理和SSL终止。

* 备注
ELB服务本身也是高可用的，可以用于构建高可用体系结构。

### Load Balancers类型

* ELB为处理不同种类的连接提供了许多种的负载均衡器，包括：Internet-facing， internal以及支持加密连接的负载均衡器。

#### Internet-Facing 负载均衡器

* 顾名思义，Internet-Facing的负载平衡器是一种负载平衡器，它通过Internet接收来自客户端的请求，并将它们分发给在负载平衡器中注册的Amazon EC2实例。 

* 当您配置负载均衡器时，它将接收一个公共DNS名称，客户端可以使用该名称向您的应用程序发送请求。DNS服务器将DNS名称解析为负载均衡器的公用IP地址，客户端应用程序可以看到该地址 

* 备注：
  AWS推荐的最佳实践始终是通过其DNS名称而不是通过负载均衡器的IP地址引用负载均衡器，以便提供一个单一、稳定的入口点。

* 由于弹性负载平衡可伸缩以满足流量需求，因此不建议将应用程序绑定到可能不再是负载均衡器资源池一部分的IP地址。

* 在Amazon 的VPC中，ELB仅仅支持IPV4.在EC2-Classic中ELB支持IPV4和IPv6。

#### Internal 负载均衡器

* 在多层应用程序中，在应用程序的各层之间进行负载平衡通常很有用。例如，Internet-Facing的负载平衡器可能接收并平衡到表示层或web层的外部流量，然后Amazon EC2实例将其请求发送到位于应用层前面的负载平衡器。您可以使用内部负载平衡器将流量路由到具有专用子网的VPCs中的Amazon EC2实例。

#### Https 负载均衡器

* 您可以创建一个负载平衡器，它使用SSL/传输层安全（TLS）协议进行加密连接（也称为SSL卸载）。此功能启用负载平衡器与启动HTTPS会话的客户端之间的通信加密，以及负载平衡器与后端实例之间的连接。弹性负载平衡提供了具有预定义SSL协商配置的安全策略，可用于协商客户端和负载平衡器之间的连接。为了使用SSL，您必须在负载平衡器上安装一个SSL证书，该证书用于终止连接，然后在向后端Amazon EC2实例发送请求之前解密来自客户端的请求。您可以选择在后端实例上启用身份验证。

* 弹性负载平衡不支持负载平衡器上的服务器名称指示（SNI）。这意味着，如果您希望使用一个SSL证书在弹性负载平衡背后的Amazon EC2实例群中托管多个网站，则需要为证书中的每个网站添加一个使用者替代名称（SAN），以避免网站用户在访问网站时看到警告消息。

### 监听器

* 每个负载平衡器必须配置一个或多个侦听器。侦听器是检查连接请求的进程，例如，配置为负载平衡器的A记录名称的CNAME。每个监听器都配置了一个协议和一个端口（客户端到负载平衡器）用于前端连接，一个协议和一个端口用于后端（负载平衡器到Amazon EC2实例）连接。弹性负载平衡支持以下协议：
```
 * HTTP
 * HTTPS
 * TCP
 * SSL
```

* 弹性负载平衡支持在两个不同的开放系统互连（OSI）层上运行的协议。在OSI模型中，第4层是传输层，它描述了客户机和后端实例之间通过负载均衡器的TCP连接。第4层是可为负载平衡器配置的最低级别。第7层是应用程序层，描述从客户端到负载平衡器以及从负载平衡器到后端实例的HTTP和HTTPS连接的使用。SSL协议主要用于在不安全的网络（如Internet）上加密机密数据。SSL协议在客户端和后端服务器之间建立安全连接，并确保在客户端和服务器之间传递的所有数据都是私有的。

### 配置 ELB
* 弹性负载平衡允许您配置负载平衡器的许多方面，包括空闲连接超时、跨区域负载平衡、连接排出、代理协议、粘性会话和运行状况检查。可以使用AWS管理控制台或命令行界面（CLI）修改配置设置。下面介绍一些选项。

#### Idle 连接超时
* 对于客户机通过负载平衡器发出的每个请求，负载平衡器维护两个连接。一个连接到客户端，另一个连接到后端实例。对于每个连接，负载平衡器管理一个空闲超时，当在指定的时间段内没有数据通过连接发送时触发该超时。空闲超时时间过后，如果没有发送或接收数据，负载平衡器将关闭连接。

* 默认情况下，弹性负载平衡将两个连接的空闲超时设置为60秒。如果HTTP请求没有在空闲超时时间内完成，则负载平衡器将关闭连接，即使数据仍在传输中。您可以更改连接的空闲超时设置，以确保长时间的操作（如文件上载）有时间完成。

* 如果您使用HTTP和HTTPS侦听器，我们建议您为Amazon EC2实例启用keep alive选项。您可以在web服务器设置或Amazon EC2实例的内核设置中启用keep alive。启用Keep alive时，允许负载平衡器重用到后端实例的连接，从而降低CPU利用率。

* 备注
```
 要确保负载平衡器负责关闭到后端实例的连接，请确保为keep-alive时间设置的值大于负载平衡器上的空闲超时设置。
```

#### 跨域负载均衡
* 为了确保请求流量在负载平衡器的所有后端实例之间均匀路由，无论它们位于哪个可用区域，都应在负载平衡器上启用跨区域负载平衡。跨区域负载平衡减少了在每个可用性区域中维护同等数量的后端实例的需要，并提高了应用程序处理一个或多个后端实例丢失的能力。但是，仍然建议您在每个可用性区域中保持大约相等数量的实例，以获得更高的容错性。

* 对于客户端缓存DNS查找的环境，传入的请求可能有利于某个可用性区域。使用跨区域负载平衡，请求负载中的这种不平衡分布在区域中所有可用的后端实例中，减少了配置错误的客户端的影响。



#### 连接排除
* 应该启用连接排除，以确保负载均衡器停止向撤销或不健康的实例发送请求，同时保持现有连接打开。这使负载平衡器能够完成对这些实例的飞行请求。

* 启用连接排除时，可以指定负载均衡器的最大时间，以便在将实例报告为注销之前保持连接的有效性。最大超时值可以设置在1秒到3600秒之间（默认是300秒）。当达到最大时限时，负载均衡器强制关闭与撤销注册实例的连接。

#### 代理协议
* 当您对前端和后端连接使用TCP或SSL时，负载平衡器会将请求转发到后端实例，而不修改请求头。如果启用代理协议，则会向请求头添加一个可读的头，其中包含源IP地址、目标IP地址和端口号等连接信息。然后将头作为请求的一部分发送到后端实例。

* 在使用代理协议之前，请验证负载平衡器是否位于启用了代理协议的代理服务器后面。如果代理服务器和负载平衡器上都启用了代理协议，则负载平衡器将向请求添加另一个头，该请求已具有来自代理服务器的头。根据后端实例的配置方式，此重复可能会导致错误。

#### 粘性会话
* 默认情况下，负载平衡器以最小的负载将每个请求独立路由到注册的实例。但是，您可以使用粘性会话功能（也称为会话关联），该功能使负载平衡器能够将用户的会话绑定到特定实例。这可以确保会话期间来自用户的所有请求都发送到同一实例。管理粘性会话的关键是确定负载平衡器应将用户的请求持续路由到同一实例的时间。如果应用程序有自己的会话cookie，则可以配置弹性负载平衡，以便会话cookie遵循应用程序的会话cookie指定的持续时间。如果应用程序没有自己的会话cookie，可以通过指定自己的粘性持续时间来配置弹性负载平衡以创建会话cookie。弹性负载平衡创建一个名为AWSELB的cookie，用于将会话映射到实例。

#### 健康检查
* 弹性负载平衡支持运行状况检查，以测试弹性负载平衡负载平衡器后面的Amazon EC2实例的状态。在运行状况检查时运行状况良好的实例的状态为“正在运行”。在运行状况检查时，任何不正常的实例的状态都是“服务中断”。负载平衡器对所有已注册的实例执行运行状况检查，以确定该实例处于正常状态还是不正常状态。健康检查是ping、连接尝试或定期检查的页。您可以设置运行状况检查之间的时间间隔，以及在运行状况检查页包含计算方面时等待响应的时间量。最后，在实例被标记为不正常之前，可以设置连续运行状况检查失败次数的阈值。

#### 备注
* 弹性负载平衡负载平衡器后的更新

长时间运行的应用程序最终将需要维护，并使用较新版本的应用程序进行更新。当使用在弹性负载平衡负载平衡器后面运行的Amazon EC2实例时，可以手动注销这些与负载平衡器关联的长时间运行的Amazon EC2实例，然后注册新启动的Amazon EC2实例，这些实例是从安装的新更新开始的。

## Amazon CloudWatch
* Amazon CloudWatch是一项服务，您可以使用它来实时监控AWS资源和应用程序。使用Amazon CloudWatch，您可以收集和跟踪度量，创建发送通知的警报，并根据定义的规则更改要监视的资源。

* 例如，您可以选择监视CPU利用率来决定何时在应用层中添加或删除Amazon EC2实例。或者，如果AWS看不到的特定于应用程序的度量是评估扩展需求的最佳指标，那么可以执行PUT请求，将该度量推送到Amazon CloudWatch中。然后可以使用此自定义度量来管理容量。

* 您可以指定一段时间内度量的参数，并在达到阈值时配置警报和自动操作。Amazon CloudWatch支持多种类型的操作，例如向Amazon简单通知服务（Amazon SNS）主题发送通知或执行自动缩放策略。

* Amazon CloudWatch为支持的AWS产品提供基本或详细的监控。基本监控每五分钟向Amazon CloudWatch发送一次数据点，以获得有限数量的预选指标，而不收取任何费用。详细的监控每分钟都会向Amazon CloudWatch发送数据点，并允许数据聚合以收取额外费用。如果要使用详细监视，则必须启用“基本”作为默认设置。

* Amazon CloudWatch支持大多数AWS云服务的监视和特定度量，包括：自动缩放、Amazon CloudFront、Amazon CloudSearch、Amazon DynamoDB、Amazon EC2、Amazon EC2容器服务（Amazon ECS）、Amazon ElastiCache、Amazon Elastic Block Store（Amazon EBS）、弹性负载平衡、Amazon Elastic MapReduce（Amazon EMR），Amazon Elasticsearch服务、Amazon Kinisis Streams、Amazon Kinisis Firehose、AWS Lambda、Amazon机器学习、AWS OpsWorks、Amazon Redshift、Amazon关系数据库服务（Amazon RDS）、Amazon Route 53、Amazon SNS、Amazon简单队列服务（Amazon SQS）、Amazon S3、AWS简单工作流服务（Amazon SWF）、AWS存储网关、AWS WAF，以及Amazon WorkSpaces。

### 备注
* 读取警报
```
  您可能有一个利用Amazon DynamoDB的应用程序，您想知道何时读取请求达到某个阈值，并通过电子邮件提醒自己。
  您可以通过在Amazon DynamoDB表中使用ProvisionedReadCapacityUnits来实现这一点，您需要为其设置一个警报。
  您只需在多个连续时段内设置一个阈值，然后将电子邮件指定为通知类型。
  现在，当阈值持续超过时段数时，指定的电子邮件将提醒您读取活动。
```

* 可以通过执行GET请求来检索Amazon CloudWatch度量。使用详细监视时，还可以在指定的时间长度内聚合度量。Amazon CloudWatch不跨区域聚合数据，但可以在区域内聚合多个可用性区域。

* AWS提供了包含在每个服务中的一组丰富的度量，但是您也可以定义自定义度量来监视AWS不具有可见性的资源和事件，例如，Amazon EC2实例内存消耗和磁盘度量，这些度量对 Amazon EC2 实例的操作系统可见，但对AWS不可见，或者对运行在AWS不知道的实例上的应用程序特定阈值不可见。Amazon CloudWatch支持一个应用程序编程接口（API），该接口允许程序和脚本将度量作为名称-值对放入Amazon CloudWatch中，然后可以使用该名称-值对以与默认Amazon CloudWatch度量相同的方式创建事件和触发警报。

* Amazon CloudWatch Logs可用于监视、存储和访问来自Amazon EC2实例、AWSCloudTrail和其他源的日志文件。然后可以检索日志数据并实时监视事件。例如，可以跟踪应用程序日志中的错误数，并在错误率超过阈值时发送通知。Amazon CloudWatch日志还可以用于在Amazon S3或Amazon Glacier中存储日志。日志可以无限期保留，也可以根据不再需要时删除旧日志的老化策略保留。

* CloudWatch Logs代理提供了一种为运行Amazon Linux或Ubuntu的Amazon EC2实例向CloudWatch日志发送日志数据的自动化方法。您可以在现有的Amazon EC2实例上使用Amazon日志代理安装程序来安装和配置日志记录代理程序。安装完成后，代理将确认它已启动，并在禁用之前保持运行。Amazon CloudWatch在使用该服务时有一些限制，您应该记住这些限制。每个AWS帐户限制为每个AWS帐户5000个警报，默认情况下（在编写本文时），度量数据保留两周。如果您想保持数据更长的时间，您将需要将日志移动到一个持久存储区，如Amazon S3或amazonlacier。您应该熟悉Amazon CloudWatch开发者指南中Amazon CloudWatch的限制。

## Auto Scaling
* 将应用程序部署到云中的一个明显优势是能够启动服务器，然后根据不同的工作负载发布服务器。按需配置服务器，然后在不再需要时释放它们，可以为非稳定状态的工作负载节省大量成本。例如，特定体育赛事的网站、月末数据输入系统、支持闪电销售的零售购物网站、发布新歌期间的音乐艺术家网站、宣布成功收入的公司网站或计算每日活动的夜间处理运行。

* Auto Scaling是一项服务，它允许您通过根据定义的标准向外扩展和向内扩展来自动扩展Amazon EC2的容量。通过自动伸缩，您可以确保在需求高峰或需求高峰期间运行Amazon EC2实例的数量增加，以保持应用程序性能，
* 拥抱尖峰
```
 许多web应用程序都会基于超出您控制范围的事件而意外增加负载。
 例如，你的公司可能会在一个受欢迎的博客或电视节目中被提及，从而导致比预期更多的人访问你的网站。
 提前设置自动缩放功能将允许您接受并承受这种快速增长的请求数量。
 自动缩放将放大您的站点以满足不断增长的需求，然后在事件平息时缩小。
```

### Auto Scaling 计划
* 自动缩放有几个方案或计划，您可以使用这些方案或计划来控制自动缩放的执行方式。

#### 维持当前的实例等级
* 您可以将自动缩放组配置为始终保持最小或指定数量的运行实例。要保持当前实例级别，自动缩放对自动缩放组中正在运行的实例执行定期运行状况检查。当自动缩放发现一个不正常的实例时，它会终止该实例并启动一个新实例。

* 备注
```
 在任何时候都需要一致数量的Amazon EC2实例的稳态工作负载可以使用自动伸缩来监视和保持特定数量的Amazon EC2实例的运行。
```
#### 手动缩放
* 手动缩放是缩放资源的最基本方式。您只需指定自动缩放组的最大、最小或期望容量的更改即可。自动缩放管理创建或终止实例的过程，以保持更新的容量。
* 备注
```
 手动扩展对于增加不经常发生的事件的资源非常有用，
 例如发布一个新的游戏版本，该版本可供下载并需要用户注册。
 对于超大规模的事件，甚至弹性负载平衡负载平衡器也可以通过与您的本地解决方案架构师或AWS支持人员协作来预热。
```

#### 计划缩放
* 有时，您确切地知道何时需要增加或减少组中的实例数，这仅仅是因为这种需要是按可预测的时间表出现的。例如，月底、季度末或年末处理等定期事件，以及其他可预测的重复事件。计划缩放意味着缩放操作将作为时间和日期的函数自动执行。

* 备注
```
 定期事件，如月底、季度或年度处理，或计划的和定期的自动加载和性能测试，可以在计划的事件发生时进行预期，并且可以适当地增加自动缩放。
```

#### 动态缩放
* 动态缩放允许您定义在缩放策略中控制自动缩放过程的参数。例如，您可以创建一个策略，当Amazon CloudWatch测量的网络带宽达到某个阈值时，向web层添加更多Amazon EC2实例。

### 自动缩放组件
* 自动缩放有几个组件需要配置才能正常工作：启动配置、自动缩放组和可选缩放策略

#### 启用配置
* 启动配置是自动伸缩用于创建新实例的模板，它由配置名称、Amazon Machine Image（AMI）、Amazon EC2实例类型、安全组和实例密钥对组成。每个自动缩放组一次只能有一个启动配置。

* 下面的CLI命令将创建具有以下属性的启动配置：
```
 Name: myLC
 AMI: ami-0535d66c
 Inatance type: m3.medium
 Security groups: sg-f57cde9d
 Instance key pair: myKeyPair
 > aws autoscaling create-launch-configuration -–launch-configuration-name myLC --image-id ami-0535d66c --instance-type m3.medium --security-groups sg-f57cde9d --key-name myKeyPair
```
* 在EC2 Classic中启动的实例的安全组可以用安全组名来引用，如“SSH”或“Web”，也可以用安全组名来引用，如sg-f57cde9d。如果在Amazon VPC中启动实例，建议使用，必须使用安全组标识来引用要与自动缩放启动配置中的实例关联的安全组。

* 启动配置的默认限制是每个区域100个。如果超过此限制，则创建启动配置的调用将失败。您可以通过在命令行运行describe-account-limits来查看和更新此限制，如下所示。
```
 > aws autoscaling describe-account-limits
```
* 自动伸缩可能会导致您达到其他服务的限制，例如您当前可以在一个区域内启动的默认Amazon EC2实例数，即20个。在使用AWS构建更复杂的架构时，务必记住您正在使用的所有AWS云服务的服务限制。

* 备注
```
 当使用CLI运行命令失败时，请首先检查语法。
 如果签出，请验证正在尝试的命令的限制，并检查是否未超出限制。
 一些限制可以提高，通常默认为一个合理的值，以限制竞争条件、循环中运行的错误脚本或其他可能导致意外的AWS资源高使用率和计费的类似自动化。
 可以在AWS服务限制下的AWS通用参考指南中查看AWS服务限制。
 您可以通过在AWS支持中心在线创建一个支持案例，然后在“关于”下选择“服务限制增加”来提高限制。
 然后在网上表格中填写相应的服务和增值限制。
```

####自动缩放组
* 自动缩放组是由自动缩放服务管理的Amazon EC2实例的集合。每个自动缩放组包含配置选项，这些选项控制自动缩放时应启动新实例并终止现有实例。自动缩放组必须包含可以在组中的名称和最小和最大数量的实例。您可以选择指定所需容量，即组必须始终具有的实例数。如果未指定所需容量，则默认所需容量是指定的最小实例数。

* 下面的CLI命令将创建一个自动缩放组，该组引用以前的启动配置并包含以下规范：
```
 Name: myASG
 Launch configuration: myLC
 Availability Zones: us-east-1a and us-east-1c
 Minimum size: 1
 Desired capacity: 3
 Maximum capacity: 10
 Load balancers: myELB
 > aws autoscaling create-auto-scaling-group --auto–scaling-group-name myASG --launch-configuration-name myLC --availability-zones us-east-1a, us-east-1c --minsize 1 --max-size 10 --desired-capacity 3 --load-balancer-names myELB
```

* 图5.1 描述在创建名为myELB的负载平衡器并设置启动配置myLC和自动缩放组myASG之后部署的AWS资源

* 自动缩放组可以使用随需应变或现场实例作为它管理的Amazon EC2实例。按需是默认的，但可以通过引用与自动缩放组相关的启动配置（现货价格“0.15”）中的最大出价价格来使用SPOT实例。您可以通过使用新的出价创建新的发布配置，然后将其与您的自动缩放组关联来更改出价。如果实例的价格低于或等于您的出价，它们将在您的自动缩放组中启动。自动缩放组中的SPOT实例遵循与自动缩放组外的SpPosits相同的准则，并且需要灵活的应用程序，并且可以容忍Amazon EC2实例，这些通知在短时间内终止，例如，当现货价格高于启动配置中设置的出价价格时。启动配置可以引用按需实例或点实例，但不能同时引用两者。

* 备注
```
 * 完全正确
 自动缩放支持使用经济高效的Spot实例。
 当您托管希望提供额外计算能力但价格受限的站点时，这非常有用。
 一个例子是“freemium”站点模型，在这个模型中，您可以免费向用户提供一些基本功能，并为付费使用的高级用户提供附加功能。
 现货实例可用于提供基本功能时，通过引用与自动缩放组相关的启动配置（-spot-price"0.15"）中的最大出价价格。
```

#### 缩放策略
* 您可以将Amazon CloudWatch警报和缩放策略与自动缩放组相关联，以动态调整自动缩放。当超过阈值时，Amazon CloudWatch会发送警报以触发对当前在负载平衡器后接收流量的Amazon EC2实例数量的更改（放大或缩小）。在Amazon CloudWatch警报向Auto Scaling组发送消息后，Auto Scaling将执行相关的策略来缩放组。策略是一组指令，告诉自动缩放是缩小、启动关联启动配置中引用的新Amazon EC2实例，还是缩小和终止实例。

* 配置缩放策略有几种方法：您可以通过特定数量的实例来增加或减少，例如添加两个实例；您可以针对特定数量的实例，例如最多五个Amazon EC2实例；或者可以基于百分比进行调整。您还可以根据一组根据报警阈值触发器的大小而变化的缩放调整来逐步缩放和增加或减少组的当前容量。

* 可以将多个缩放策略与自动缩放组关联。例如，可以使用CPU利用率触发器CPULoad和CloudWatch度量CPU utilization创建策略，以指定在两分钟内CPU利用率大于75%时向外扩展。如果20分钟内CPU利用率低于40%，则可以将另一个策略附加到同一个自动缩放组以进行缩放。以下CLI命令将创建刚才描述的缩放策略。
```
 > aws autoscaling put-scaling-policy --auto-scaling-group-name myASG --policy-name CPULoadScaleOut --scaling-adjustment 1 --adjustment-type ChangeInCapacity --cooldown 30 
 > aws autoscaling put-scaling-policy --auto-scaling-group-name myASG --policy-name CPULoadScaleIn --scaling-adjustment -1 --adjustment-type ChangeInCapacity --cooldown 600
```
* 下面的CLI命令将Amazon CloudWatch警报与缩放策略相关联，以便进行缩小和放大，如图5.2所示。在本例中，Amazon CloudWatch警报按Amazon Resource Name（ARN）引用缩放策略。

* 图5.2 带策略的自动缩放组

```
 > aws cloudwatch put-metric-alarm --alarm name capacityAdd --metric-name CPUUtilization --namespace AWS/EC2 --statistic Average –-period 300 --threshold 75 --comparison-operator GreaterThanOrEqualToThreshold --dimensions "Name=AutoScalingGroupName, Value=myASG" --evaluation-periods 1 --alarm-actions arn:aws:autoscaling:us-east-1:123456789012:scalingPolicy:12345678-90ab-cdef- 1234567890ab:autoScalingGroupName/myASG:policyName/CPULoadScaleOut --unit Percent 
 > aws cloudwatch put-metric-alarm --alarm name capacityReduce --metric-name CPUUtilization --namespace AWS/EC2 --statistic Average --period 1200 --threshold 40 --comparison-operator GreaterThanOrEqualToThreshold --dimensions "Name=AutoScalingGroupName, Value=myASG" --evaluation-periods 1 --alarm-actions arn:aws:autoscaling:us-east-1:123456789011:scalingPolicy:11345678-90ab-cdef- 1234567890ab:autoScalingGroupName/myASG:policyName/CPULoadScaleIn --unit Percent
```

* 如果前一段中定义的缩放策略与名为myASG的自动缩放组相关联，并且CPU利用率超过75%超过5分钟，如图5.3所示，将启动一个新的Amazon EC2实例并将其附加到名为myELB的负载平衡器。

* 图5.3 Amazon CloudWatch 警告触发缩容

* 一个推荐的最佳实践是快速扩展和缓慢扩展，这样您可以对突发或峰值做出响应，但避免意外地过快终止Amazon EC2实例，只有在突发持续时才需要启动更多Amazon EC2实例。自动缩放还支持一个冷却期，这是一个可配置的设置，用于确定何时暂停自动缩放组的短期缩放活动。

* 如果您启动一个Amazon EC2实例，您将收到一整小时运行时间的账单。消耗的部分实例小时数按完整小时计费。这意味着，如果您有一个允许的扩展策略，可以在一小时内启动、终止和重新启动多个实例，那么即使您在不到一小时内终止其中的一些实例，也将为您启动的每个实例计费一个完整的小时。为提高成本效益，建议的最佳做法是在需要时快速扩展，但扩展速度要慢一些，以避免重新启动新的和单独的Amazon EC2实例，以应对在几分钟内上下波动但通常在一小时内仍需要更多资源的工作负载需求激增。

* 备注
```
  迅速扩容，慢慢缩容。
```

* 重要的是要考虑使用自动缩放功能启动Amazon EC2实例的引导。在每个新启动的Amazon EC2实例正常运行并能够接受流量之前，配置它需要时间。启动更快且可更快加载的实例可以更快地加入容量池。此外，更加无状态而不是有状态的实例将更优雅地进入和退出自动缩放组。

* 备注
```
 * 按比例打补丁(Rolliing out a patch at scale)
 在Amazon EC2实例的大型部署中，可以使用自动伸缩来简化向实例发布补丁的过程。如果需要，可以修改与Auto Scaling组相关联的启动配置，以引用新的AMI甚至新的Amazon EC2实例。然后，您可以一次或以小组的形式注销或终止一个实例，新的Amazon EC2实例将引用新的补丁AMI。
```

## 总结
* 本章介绍了三种服务：

* 弹性负载平衡，用于在一个或多个可用性区域中跨一组Amazon EC2实例分发流量，以实现应用程序更高级别的容错。

* Amazon CloudWatch，它监视资源和应用程序。Amazon CloudWatch用于收集和跟踪度量，创建发送通知的警报，并根据您定义的规则更改要监视的资源。

* 自动缩放，它允许您使用您定义的条件自动缩放Amazon EC2的容量。这三个服务可以非常有效地结合使用，在AWS上创建具有弹性体系结构的高可用应用程序

## 考试基础
* 了解弹性负载平衡服务提供了什么。弹性负载平衡是一种高度可用的服务，它分布在Amazon EC2实例上的流量，并包括提供灵活性和控制传入请求到Amazon EC2实例的选项。

* 了解弹性负载平衡服务提供的负载平衡器的类型以及何时使用每种类型的负载平衡器。顾名思义，面向Internet的负载平衡器是一种负载平衡器，它通过Internet接收来自客户端的请求，并将它们分发给在负载平衡器中注册的Amazon EC2实例。内部负载平衡器用于将流量路由到具有专用子网的VPCs中的Amazon EC2实例。当您要加密负载平衡器与启动HTTPS会话的客户端之间的数据以及负载平衡器与后端实例之间的连接时，将使用HTTPS负载平衡器。

* 了解弹性负载平衡服务提供的侦听器类型，以及使用每个侦听器的用例和要求。侦听器是检查连接请求的进程。它配置有用于前端（客户端到负载平衡器）连接的协议和端口，以及用于后端（负载平衡器到后端实例）连接的协议和端口。

* 了解弹性负载平衡的配置选项。弹性负载平衡允许您配置负载平衡器的许多方面，包括空闲连接超时、跨区域负载平衡、连接排出、代理协议、粘性会话和运行状况检查。

* 了解什么是弹性负载平衡健康检查以及为什么它很重要。弹性负载平衡支持运行状况检查，以测试弹性负载平衡负载平衡器后面的Amazon EC2实例的状态。

* 了解Amazon CloudWatch服务提供了什么以及使用它的用例。Amazon CloudWatch是一项服务，您可以使用它来实时监控AWS资源和应用程序。使用Amazon CloudWatch，您可以收集和跟踪度量，创建发送通知的警报，并根据定义的规则更改要监视的资源。例如，您可以选择监视CPU利用率来决定何时在应用层中添加或删除Amazon EC2实例。或者，如果AWS看不到的特定于应用程序的度量是评估扩展需求的最佳指标，那么可以执行PUT请求，将该度量推送到Amazon CloudWatch中。然后可以使用此自定义度量来管理容量。

* 了解这两种类型的基本和详细监视之间的区别-适用于Amazon CloudWatch。Amazon CloudWatch为支持的AWS产品提供基本或详细的监控。基本监控每五分钟向Amazon CloudWatch发送一次数据点，以获得有限数量的预选指标，而不收取任何费用。详细的监控每分钟都会向Amazon CloudWatch发送数据点，并允许进行额外收费的数据聚合。如果要使用详细监视，则必须启用“基本”作为默认设置。

* 了解自动缩放以及为什么它是AWS云的一个重要优势。将应用程序部署到云中的一个明显优势是能够启动服务器，然后根据不同的工作负载发布服务器。按需配置服务器，然后在不再需要时释放它们，可以为非稳定状态的工作负载节省大量成本。

* 知道何时以及为什么使用自动缩放。Auto Scaling是一项服务，它允许您通过根据定义的标准向外扩展和向内扩展来自动扩展Amazon EC2的容量。通过自动伸缩，您可以确保在需求高峰或需求高峰期间运行Amazon EC2实例的数量增加，以保持应用程序性能，并在需求停滞或低谷期间自动减少，以将成本降至最低。

* 了解支持的自动缩放计划。自动缩放有几个方案或计划，您可以使用这些方案或计划来控制自动缩放的执行方式。自动缩放计划被命名为“保持当前即时级别”、“手动缩放”、“计划缩放”和“动态缩放”。

* 了解如何构建自动缩放启动配置和自动缩放组，以及它们的用途。启动配置是自动伸缩用于创建新实例的模板，由配置名称、AMI、Amazon EC2实例类型、安全组和实例密钥对组成。

* 了解什么是扩展策略以及使用它的用例。自动缩放与CloudWatch警报一起使用缩放策略来确定自动缩放组应在何时向外缩放或向内缩放。每个CloudWatch警报监视一个度量，并在该度量超过您在策略中指定的阈值时将消息发送到自动缩放。

* 了解如何将弹性负载平衡、Amazon CloudWatch和自动伸缩结合使用以提供动态伸缩。弹性负载平衡、Amazon CloudWatch和Auto Scaling可以一起使用，在AWS上创建具有弹性体系结构的高可用性应用程序。

## 练习
* 为辅助完成如下的练习，参考：
 ELB开发指南：http://docs.aws.amazon.com/ElasticLoadBalancing/latest/DeveloperGuide/elastic-loadbalancing.html
 Amazon CloudWatch开发指南：http://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/WhatIsCloudWatch.html
 Auto Scaling 用户指导：http://docs.aws.amazon.com/autoscaling/latest/userguide/WhatIsAutoScaling.html

### 练习 5.1
#### 创建一个ELB负载均衡器C
* 在这个练习中，你竟会使用 AWS Management Console创建一个ELB负载均衡器
```
1. 用带有一个Web服务器的AMI启动一个Amazon EC2实例，或者安装并配置一个web服务器；
2. 创建一个静态页面用于展示和健康检查返回HTTP 200；配置AmazonEC2实例80端口接收流量；

3. 向ELB负载均衡器注册Amazon EC2实例，并配置为使用运行状况检查页来评估实例的运行状况。
```

### 练习5.2
#### 使用一个Amazon CloudWatch Metric
1. 启动一个Amazon EC2 实例.
2. 用一个存在的Amazon CloudWatch metric 监控一个值.

### 练习5.3
#### 创建一个客户自定义 Amazon CloudWatch Metric
1. 创建一个客户自定义的内存使用Amazon CloudWatch metric.
2. 使用 CLI， PUT 值到metric.

### 5.4
#### 创建一个启动配置和Auto Scaling Group
1. 使用AWS Management Console用存在的AMI创建一个启动配置；
2. 使用此启动配置创建一个自动缩放组，组大小为四个，跨越两个可用区域。不要使用缩放策略。保持组的初始大小。
3. 手动终止一个Amazon EC2实例，观察Auto Scaling启动一个新的Amazonec2实例。.

### 5.5
#### 创建一个缩放策略
1. 使用AWS管理控制台为CPU利用率创建Amazon云监视度量和警报。
2. 使用练习5.4中的“自动缩放”组，编辑“自动缩放”组以包含使用CPU使用率警报的策略。
3. 在监控的Amazon EC2实例上提高CPU利用率，以观察自动伸缩。

### 5.6
#### 创建一个用于缩放的web应用
1. 创建一个小型web应用程序，该应用程序由一个弹性负载平衡负载平衡器、一个跨两个可用区域的自动缩放组（使用Amazon CloudWatch度量）和一个附加到自动缩放组使用的缩放策略的警报组成。
2. 通过移除实例并上下驱动度量以强制自动缩放，验证自动缩放是否正常工作。

## 复习题
### 1. Which of the following are required elements of an Auto Scaling group? (Choose 2
answers)
 * A. Minimum size
 * B. Health checks
 * C. Desired capacity
 * D. Launch configuration

### 2. You have created an Elastic Load Balancing load balancer listening on port 80, and you registered it with a single Amazon Elastic Compute Cloud (Amazon EC2) instance also listening on port 80. A client makes a request to the load balancer with the correct protocol and port for the load balancer. In this scenario, how many connections does the balancer maintain?
 * A. 1
 * B. 2
 * C. 3
 * D. 4

### 3. How long does Amazon CloudWatch keep metric data?
 * A. 1 day
 * B. 2 days
 * C. 1 week
 * D. 2 weeks

### 4. Which of the following are the minimum required elements to create an Auto Scaling launch configuration?
 * A. Launch configuration name, Amazon Machine Image (AMI), and instance type
 * B. Launch configuration name, AMI, instance type, and key pair
 * C. Launch configuration name, AMI, instance type, key pair, and security group
 * D. Launch configuration name, AMI, instance type, key pair, security group, and block device mapping

### 5. You are responsible for the application logging solution for your company’s existing applications running on multiple Amazon EC2 instances. Which of the following is the best approach for aggregating the application logs within AWS?
 * A. Amazon CloudWatch custom metrics
 * B. Amazon CloudWatch Logs Agent
 * C. An Elastic Load Balancing listener
 * D. An internal Elastic Load Balancing load balancer

### 6. Which of the following must be configured on an Elastic Load Balancing load balancer to accept incoming traffic?
 * A. A port
 * B. A network interface
 * C. A listener
 * D. An instance

### 7. You create an Auto Scaling group in a new region that is configured with a minimum size value of 10, a maximum size value of 100, and a desired capacity value of 50. However, you notice that 30 of the Amazon Elastic Compute Cloud (Amazon EC2) instances within the Auto Scaling group fail to launch. Which of the following is the cause of this behavior?
 * A. You cannot define an Auto Scaling group larger than 20.
 * B. The Auto Scaling group maximum value cannot be more than 20.
 * C. You did not attach an Elastic Load Balancing load balancer to the Auto Scaling
group.
 * D. You have not raised your default Amazon EC2 capacity (20) for the new region.

### 8. You want to host multiple Hypertext Transfer Protocol Secure (HTTPS) websites on a fleet of Amazon EC2 instances behind an Elastic Load Balancing load balancer with a single X.509 certificate. How must you configure the Secure Sockets Layer (SSL) certificate so that clients connecting to the load balancer are not presented with a warning when they connect?
 * A. Create one SSL certificate with a Subject Alternative Name (SAN) value for each
website name.
 * B. Create one SSL certificate with the Server Name Indication (SNI) value checked.
 * C. Create multiple SSL certificates with a SAN value for each website name.
 * D. Create SSL certificates for each Availability Zone with a SAN value for each website
name.

### 9. Your web application front end consists of multiple Amazon Compute Cloud (Amazon EC2) instances behind an Elastic Load Balancing load balancer. You have configured the load balancer to perform health checks on these Amazon EC2 instances. If an instance fails to pass health checks, which statement will be true?
 * A. The instance is replaced automatically by the load balancer.
 * B. The instance is terminated automatically by the load balancer.
 * C. The load balancer stops sending traffic to the instance that failed its health check.
 * D. The instance is quarantined by the load balancer for root cause analysis.

### 10. In the basic monitoring package for Amazon Elastic Compute Cloud (Amazon EC2), what Amazon CloudWatch metrics are available?
 * A. Web server visible metrics such as number of failed transaction requests
 * B. Operating system visible metrics such as memory utilization
 * C. Database visible metrics such as number of connections
 * D. Hypervisor visible metrics such as CPU utilization

### 11. A cell phone company is running dynamic-content television commercials for a contest. They want their website to handle traffic spikes that come after a commercial airs. The website is interactive, offering personalized content to each visitor based on location, purchase history, and the current commercial airing. Which architecture will configure Auto Scaling to scale out to respond to spikes of demand, while minimizing costs during quiet periods?
 * A. Set the minimum size of the Auto Scaling group so that it can handle high traffic volumes without needing to scale out.
 * B. Create an Auto Scaling group large enough to handle peak traffic loads, and then stop some instances. Configure Auto Scaling to scale out when traffic increases using the stopped instances, so new capacity will come online quickly.
 * C. Configure Auto Scaling to scale out as traffic increases. Configure the launch configuration to start new instances from a preconfigured Amazon Machine Image (AMI).
 * D. Use Amazon CloudFront and Amazon Simple Storage Service (Amazon S3) to cache changing content, with the Auto Scaling group set as the origin. Configure Auto Scaling to have sufficient instances necessary to initially populate CloudFront and Amazon ElastiCache, and then scale in after the cache is fully populated.

### 12. For an application running in the ap-northeast-1 region with three Availability Zones (apnortheast-1a, ap-northeast-1b, and ap-northeast-1c), which instance deployment provides
high availability for the application that normally requires nine running Amazon Elastic
Compute Cloud (Amazon EC2) instances but can run on a minimum of 65 percent
capacity while Auto Scaling launches replacement instances in the remaining Availability
Zones?
 * A. Deploy the application on four servers in ap-northeast-1a and five servers in apnortheast-1b, and keep five stopped instances in ap-northeast-1a as reserve.
 * B. Deploy the application on three servers in ap-northeast-1a, three servers in apnortheast-1b, and three servers in ap-northeast-1c.
 * C. Deploy the application on six servers in ap-northeast-1b and three servers in apnortheast-1c.
 * D. Deploy the application on nine servers in ap-northeast-1b, and keep nine stopped
instances in ap-northeast-1a as reserve.

### 13. Which of the following are characteristics of the Auto Scaling service on AWS? (Choose 3 answers)
 * A. Sends traffic to healthy instances
 * B. Responds to changing conditions by adding or terminating Amazon Elastic ComputeCloud (Amazon EC2) instances
 * C. Collects and tracks metrics and sets alarms
 * D. Delivers push notifications
 * E. Launches instances from a specified Amazon Machine Image (AMI)
 * F. Enforces a minimum number of running Amazon EC2 instances

### 14. Why is the launch configuration referenced by the Auto Scaling group instead of being part of the Auto Scaling group?
 * A. It allows you to change the Amazon Elastic Compute Cloud (Amazon EC2) instance type and Amazon Machine Image (AMI) without disrupting the Auto Scaling group.
 * B. It facilitates rolling out a patch to an existing set of instances managed by an Auto Scaling group.
 * C. It allows you to change security groups associated with the instances launched without having to make changes to the Auto Scaling group.
 * D. All of the above
 * E. None of the above

### 15. An Auto Scaling group may use: (Choose 2 answers)
 * A. On-Demand Instances
 * B. Stopped instances
 * C. Spot Instances
 * D. On-premises instances
 * E. Already running instances if they use the same Amazon Machine Image (AMI) as the Auto Scaling group’s launch configuration and are not already part of another Auto Scaling group

### 16. Amazon CloudWatch supports which types of monitoring plans? (Choose 2 answers)
 * A. Basic monitoring, which is free
 * B. Basic monitoring, which has an additional cost
 * C. Ad hoc monitoring, which is free
 * D. Ad hoc monitoring, which has an additional cost
 * E. Detailed monitoring, which is free
 * F. Detailed monitoring, which has an additional cost

### 17. Elastic Load Balancing health checks may be: (Choose 3 answers)
 * A. A ping
 * B. A key pair verification
 * C. A connection attempt
 * D. A page requestE. An Amazon Elastic Compute Cloud (Amazon EC2) instance status check

### 18. When an Amazon Elastic Compute Cloud (Amazon EC2) instance registered with an Elastic Load Balancing load balancer using connection draining is deregistered or unhealthy, which of the following will happen? (Choose 2 answers)
 * A. Immediately close all existing connections to that instance.
 * B. Keep the connections open to that instance, and attempt to complete in-flight requests.
 * C. Redirect the requests to a user-defined error page like “Oops this is embarrassing” or “Under Construction.”
 * D. Forcibly close all connections to that instance after a timeout period.
 * E. Leave the connections open as long as the load balancer is running.

### 19. Elastic Load Balancing supports which of the following types of load balancers? (Choose 3 answers)
 * A. Cross-region
 * B. Internet-facing
 * C. Interim
 * D. Itinerant
 * E. Internal
 * F. Hypertext Transfer Protocol Secure (HTTPS) using Secure Sockets Layer (SSL)

### 20. Auto Scaling supports which of the following plans for Auto Scaling groups? (Choose 3 answers)
 * A. Predictive
 * B. Manual
 * C. Preemptive
 * D. Scheduled
 * E. Dynamic
 * F. End-user request driven
 * G            