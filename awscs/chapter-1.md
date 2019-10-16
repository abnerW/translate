# AWS 简介

## 什么是云计算

* 云计算是通过互联网按需交付IT资源和应用程序，并按需付费。无论是运行向数百万移动用户共享照片的应用程序，还是提供支持业务关键运营的服务，云提供了对灵活和低成本IT资源的快速访问。使用云计算，您不需要在硬件上进行大量的前期投资，也不需要花费大量时间管理硬件。相反，您可以提供正确类型和合适大小的计算资源，以支持您最新的聪明想法或运营您的IT部门。使用云计算，您几乎可以立即访问所需的任意数量的资源，而且只需支付您使用的资源的费用。

### 云计算的优点

 * 云计算带来了技术获取、使用和管理方式的革命性转变，以及组织如何为技术服务进行预算和支付。
 * 云计算能够快速重新配置计算环境，以适应不断变化的业务需求，组织可以优化支出。
 * 容量可以自动增加或减少，以满足波动的使用模式。
 * 服务可以暂时脱机或根据业务需求永久关闭。
 * 此外，使用按次计费，AWS云服务成为一种运营费用，而不是资本费用。
 * 虽然每个组织都经历了一次独特的云端之旅，带来了许多好处，但六个好处却一次又一次地显现出来，如图-1.1所示。

#### 可变经济支出 Variable VS.capital expense

* 让我们先从资本支出换成可变运营支出的能力开始。你不必再数据中心和服务器上投入大量资金，而只需在消耗计算资源时支付，只需支付所消耗的资源。

#### 规模经济 Economies of Scale

* 云计算的另一个优势是，组织可以从大规模的规模经济中获益。通过使用云计算，你可以实现比你自己更低的可变成本。因为数十万客户的使用是在云中聚合的，所以像AWS这样的提供商可以实现更高的规模经济，这就意味着更低的价格。

#### 提升速度 Increace speed and ingility

* 在云计算环境中，只需单击一下即可获得新的IT资源，这允许组织将向开发人员提供这些资源所需的时间从几周减少到几分钟，这将显著提高组织的速度和敏捷性，因为实验和开发所需的成本和时间大大降低。

#### 专注于业务差异性 Focus on business differentiators

* 云计算使组织能够专注于他们的业务优先事项，而不是沉重的服务器负担、堆叠和供电。通过接受这种模式转变，组织可以停止在运行和维护数据中心上花钱。这使得组织能够专注于使其业务与众不同的项目，比如分析千兆字节的数据，传送视频内容，构建伟大的移动应用，甚至探索火星。

#### 停止容量评估 Stop guessing capacity

* 当您在部署应用程序之前做出容量决定时，您通常要么坐在昂贵的空闲资源上，要么处理有限的容量。组织可以停止猜测满足其业务需求所必需的基础设施的容量需求。它们可以根据需要访问尽可能多的或尽可能少的内容，并根据需要进行扩展或缩小，只需提前几分钟通知。

#### 全球分钟级 Global in minutes

* 云计算的另一个优势是能够在几分钟内全球化。组织只需点击几下，就可以轻松地将其应用程序部署到世界各地的多个位置。这允许组织在全球范围内提供冗余，并提供更低的以最低的成本为客户提供延迟和更好的体验。过去只有最大的企业才能负担得起全球化，但云计算使这一能力民主化，使任何组织都成为可能。虽然关于云计算的这些优势的具体问题不太可能出现在考试中，但是了解这些优势有助于合理化适当的答案。

### 云计算部署模型

* 本次考试关注的两种主要云计算部署模型是基于云的"一体化"部署和混合部署，了解每种策略如何应用于架构选项和决策非常重要。

* 一个基于云的应用程序完全部署在云中，应用程序的所有组件都在云中运行。云中的应用程序要么是在云中创建的，要么是从现有的基础设施中迁移来利用云计算的好处的。基于云的应用程序可以构建在低级基础设施上或者可以使用更高级别的服务，从核心基础设施的管理、架构和扩展需求中提供抽象。

* 混合部署是许多企业采用的一种常见方法，它将基于云的资源和现有资源之间的基础设施和应用程序连接起来，通常在现有的数据中心中。最常见的混合部署方法是在云和现有的内部部署基础设施之间扩展和增长组织的基础设施，同时将云资源连接到内部系统。选择在对基础设施的现有投资和迁移到云计算之间，不需要二元决策。利用专用连接、身份联合和集成工具，组织可以跨内部部署和云服务运行混合应用程序。

## AWS 基本原理

* AWS的核心是在安全的云服务平台上通过互联网提供IT资源的按需交付，提供计算能力、存储、数据库、内容交付，以及其他帮助企业扩大规模和增长的功能。使用AWS资源而不是自己的资源就像从电力公司购买电力而不是运行自己的发电机，它提供了云计算的关键优势：容量完全符合您的需求，您只需支付所用的资源，规模经济导致成本降低，服务由有经验的运营大型网络的供应商提供。**AWS全球基础设施和AWS安全与合规方法是准备考试时需要理解的关键基础概念**。

### 全球基础设施

* AWS为190多个国家的100多万活跃客户提供服务，并继续稳步扩展其全球基础设施，以帮助企业实现较低的延迟和较高的吞吐量，满足其业务需求。AWS提供了一个高可用的技术基础设施平台，在全球有多个位置。这些位置由Regions和可用域组成。每个Region是一个单独的地理区域。每个Region有多个称为可用域的独立位置。AWS允许在多个位置放置资源和数据。除非组织选择跨Region复制资源。每个Region都是完全独立的，并且被设计成与其他Region完全隔离。这样可以实现最大的容错性和稳定性。每个可用域也被隔离，但是，一个地区的可用域通过低延迟链路连接。可用域在典型的大都市地区内物理上是分开的，并且位于低风险的洪泛平原（特定的洪泛区分类因地区而异）。此外，还使用离散的不间断电源（UPS）和现场备用发电机通过独立公用设施（如可用）的不同电网供电，以进一步减少单点故障。可用域均冗余连接到多个一级公交供应商。通过将资源放置在单独的可用区域，您可以保护您的网站或应用程序免受服务中断对单个位置的影响。

```
 提示：
    您可以通过跨多个可用性区域部署应用程序来实现高可用性。应用程序的每一层（例如，Web、应用程序和数据库）的冗余实例应放置在不同的可用性区域中，从而创建多站点解决方案。至少，目标是在两个或多个可用性区域中拥有每个应用程序堆栈的独立副本
```

### 安全和合规

* 无论是在本地还是在AWS上，信息安全对于运行关键工作负载的组织。安全性是一项核心功能要求，可保护关键任务信息免受意外或蓄意的盗窃、泄漏、完整性受损和删除。帮助保护系统和数据的机密性、完整性和可用性对AWS至关重要，保持你的信任和信心。本节旨在简要介绍AWS的安全和合规方法。第12章"AWS安全"和第13章"AWS风险和合规"将更详细地讨论这些主题，包括每个主题在考试中的重要性。

#### 安全

* AWS的云安全是首要任务。所有AWS客户都受益于为满足最安全敏感组织的要求而构建的数据中心和网络架构。AWS及其合作伙伴提供了数百种工具和功能，帮助组织实现其安全目标，实现可见性、可审计性，可控性和敏捷性。这意味着组织可以拥有所需的安全性，但不需要资金支出，而且与内部环境相比，操作开销要低得多。利用AWS的组织继承了AWS策略、体系结构和以及为满足最安全敏感客户的要求而构建的操作流程。AWS基础设施旨在提供最高的可用性，同时在客户隐私和隔离方面实施强有力的保护措施。在AWS云计算平台上部署系统时，AWS通过与组织共享安全职责来提供帮助。AWS管理底层基础设施，组织可以保护其在AWS上部署的任何内容。这为每个组织提供了安全控制所需的灵活性和灵活性。该基础设施不仅按照安全最佳实践和标准进行构建和管理，而且考虑到云的独特需求。AWS使用冗余和分层控制、连续验证和测试，以及大量的自动化，以确保底层基础设施24/7受到监控和保护。AWS确保这些控制在每个新的数据中心或服务中得到一致的应用。

#### 合规

* 当客户将其生产工作负载转移到AWS云时，双方负责管理IT环境。客户负责以安全和受控的方式建立其环境。客户还需要对其整个IT控制环境保持适当的治理。通过将治理集中在一起，有利于审计的服务功能，通过适用的合规或审计标准，AWS使客户能够建立在传统的合规计划之上。这有助于组织在AWS安全控制环境中建立和运行。

```
提示：
    组织对其数据所在的区域保持完全的控制权和所有权，使它们能够满足区域法规遵从性和数据驻留要求。
```

AWS提供给组织的IT基础设施是按照安全最佳实践和各种IT安全标准设计和管理的。以下是AWS遵守的许多认证和标准的部分列表：

```
  * 服务组织控制（soc）1/国际保证标准参与（ISAE）3402、SOC 2和SOC 3
  * 《联邦信息安全管理法》（FISMA），国防部信息保证认证和认可程序（DICAP），以及联邦风险和授权管理计划（FEDRAMP）   * 支付卡行业数据安全标准（PCI DSS）
  * 一级国际标准化组织（ISO）9001、ISO 27001，而iso 27018 
```

AWS提供了有关其IT控制环境的广泛信息，以帮助组织以报告、认证、认证和其他第三方认证的形式实现监管承诺。 


## AWS 云计算平台 

  AWS提供了许多云服务，您可以将它们结合起来以满足业务或组织需求（请参见图1.2）。了解所有的平台服务将使您成为一名全面的解决方案架构师，了解本书中概述的服务和基本概念将有助于您为《AWS认证解决方案架构师-联合考试》做好准备。


本节按类别介绍主要的AWS云服务。随后的章节提供了与考试相关的服务的更深入的视图。

### 平台访问

  要访问AWS云服务，可以使用AWS管理控制台、AWS命令行界面（cli）或AWS软件开发工具包（sdk）。

* AWS管理控制台是一个用于管理AWS云服务的web应用程序。控制台为执行许多任务提供直观的用户界面。每个服务都有自己的控制台，可以从AWS管理控制台访问。控制台还提供有关帐户和帐单的信息。

* AWS命令行界面（cli）是用于管理AWS云服务的统一工具，只需下载和配置一个工具，就可以从命令行控制多个服务，并通过脚本实现自动化。

* AWS软件开发工具包（sdk）提供了一个应用程序编程接口（api），它与基本构成AWS平台的web服务进行交互。sdk为许多不同的编程语言和平台提供支持，允许您使用首选语言。

对于Web服务端点，使用SDK可以通过提供对许多服务的编程访问来减少编码的复杂性。 

### 计算和网络服务

  AWS提供各种计算和网络服务，为企业开发和运行其工作负载提供核心功能。这些计算和网络服务可与存储、数据库和应用程序服务一起使用，为计算、查询处理提供完整的解决方案，以及广泛应用的存储。本节提供核心计算和网络服务的高级描述

### Amazon Elastic Compute Cloud（Amazon EC2)

  Amazon Elastic Compute Cloud（Amazon EC2）是一个在云中提供可调整大小的计算能力的Web服务，它允许组织获取和配置Amazon数据中心的虚拟服务器，并利用这些资源来构建和托管软件系统。组织可以从各种操作系统和资源配置（内存、CPU、存储等）中选择最适合每个工作负载的应用程序配置文件。Amazon EC2提供了一个真正的虚拟计算环境，允许组织使用各种操作系统启动计算资源，使用自定义应用程序加载它们，并在保持完全控制的同时管理网络访问权限

### AWS lambda

  是一个面向后端web开发人员的零管理计算平台，它在AWS云上为您运行代码，并为您提供细粒度的定价结构。AWS lambda在一个区域的多个可用性区域中运行自己的AWS计算组Amazon ec2实例，它提供了AWS基础设施的高可用性、安全性、性能和可扩展性 

### 自动伸缩（Auto Scaling）

* Auto Scaling允许组织根据为特定工作负载定义的条件自动向上或向下扩展Amazon EC2容量（见图1.3）。它不仅可以帮助维护应用程序可用性并确保所需数量的Amazon EC2实例正在运行，但它也允许资源进行扩展以满足动态工作负载的需求，组织可以优化成本，而不是为峰值负载提供资源，只使用实际需要的容量。

* 自动伸缩非常适合于具有稳定需求模式的应用程序，也适合于在使用中体验每小时、每天或每周变化的应用程序 

### 弹性负载均衡

* 弹性负载平衡在云中跨多个Amazon EC2实例自动分配传入的应用程序流量。它使组织能够在其应用程序中实现更高级别的容错，无缝地提供分配应用程序流量所需的负载平衡容量。

### AWS Elastic Beanstalk 

* AWS Elastic Beanstalk是在AWS上启动和运行Web应用程序的最快和最简单的方式。开发人员只需上传他们的应用程序代码，该服务就会自动处理所有细节，如资源配置、负载平衡、自动伸缩，它为各种平台提供支持，包括php、java、python、ruby、node.js、.net和go。使用AWS弹性beanstalk，组织可以完全控制为应用程序提供动力的AWS资源，并可以随时访问底层资源。

### Amazon虚拟私有云（Amazon VPC）

* Amazon虚拟私有云（Amazon vpc）允许组织提供AWS云的逻辑隔离部分，在那里他们可以在自己定义的虚拟网络中启动AWS资源。组织可以完全控制虚拟环境，包括选择ip地址范围、创建子网，以及路由表的配置和网络网关。此外，组织可以使用硬件或软件虚拟专用网（VPN）连接或专用电路使用AWS直接连接将其公司数据中心网络扩展到AWS

### AWS Direct Connect

* AWS direct connect允许组织建立从其数据中心到AWS的专用网络连接。使用AWS direct connect，组织可以在AWS和其数据中心、办公室或托管环境之间建立专用连接，这在许多情况下可以降低网络成本，增加带宽吞吐量，提供比基于Internet的VPN连接更一致的网络体验。

### Amazon Route 53 

* 亚马逊Route53是一个高度可用和可扩展的域名系统（DNS）网络服务。它的目的是通过将人类可读的名称（如www.example.com）转换为计算机用来相互连接的数字IP地址（如192.0.2.1），为开发人员和企业提供一种极其可靠和经济高效的方式来将最终用户路由到Internet应用程序。允许您直接从AWS购买和管理域。

### 存储和内容分发

AWS提供各种满足需要的存储服务，诸如：Amazon简单存储服务，Amzzon CloudFront，Amazon弹性块服务。本章节只是存储和内容分发服务的概述。

#### Amazon S3

* Amazon Simple Storage Service（Amazon S3）为开发人员和IT团队提供了高度持久和可扩展的对象存储，可以处理几乎无限量的数据和大量并发用户。组织可以存储任何类型的对象，如HTML页面、源代码文件、图像文件和加密数据，并使用基于http的协议访问它们。Amazon s3为各种各样的用例提供经济高效的对象存储，包括备份和恢复、近线归档、大数据分析、灾难恢复、云应用程序和内容分发。

#### Amazon Glacier

* Amazon Glacier是一种安全、耐用、成本极低的存储服务，用于数据存档和长期备份。组织可以以非常低的每月每GB成本可靠地存储大量或少量数据。为了使客户的成本保持在较低水平，Amazon Glacier针对不常访问的数据进行了优化，在这种情况下，检索时间适合几个小时。AmazonS3与Amazon Glacier紧密集成，允许组织为其工作负载选择正确的存储层。 

#### Amazon Elastic Block Storage（Amazon EBS）

* Amazon弹性块存储（Amazon EBS）为Amazon EC2实例提供持久的块级存储卷。每个Amazon EBS卷在其可用区内自动复制，以保护组织不受组件故障的影响，提供高可用性和耐用性。通过提供一致和低延迟的性能，Amazon EBS提供了运行各种工作负载所需的磁盘存储。

#### AWS Storage Gateway

* AWS存储网关是一项将内部软件设备与基于云的存储连接起来的服务，可在组织的内部IT环境和AWS存储基础设施之间提供无缝和安全的集成。该服务支持与现有应用程序一起工作的行业标准存储协议。它提供低功耗的通过在本地维护频繁访问的数据的缓存，同时在Amazon S3或Amazon Glacie中安全地存储加密的所有数据，从而保持稳定的性能。

#### AWS CloudFront

* Amazon cloudfront是一个内容交付web服务，它与其他AWS云服务集成，使开发人员和企业能够以低延迟、高数据传输速度和无最低使用承诺的方式向全球用户分发内容。Amazon CloudFront可以使用边缘位置的全球网络来交付您的整个网站，包括动态、静态、流式和交互式内容。对内容的请求会自动路由到最近的边缘位置，因此内容会以最佳性能交付给全球各地的最终用户

### 数据库服务

* AWS提供了完全托管的关系数据库服务和nosql数据库服务，以及作为服务的内存缓存和PB级的数据仓库解决方案。本小节概述了数据库服务包含哪些产品：

#### Amazon RDS

* Amazon关系数据库服务（Amazon rds）提供了一个完全托管的关系数据库，支持许多流行的开源和商用数据库引擎。这是一个经济高效的服务，允许组织启动安全、高可用、容错的数据库。在几分钟内就可以生产数据库了。由于Amazon rds管理耗时的管理任务，包括备份、软件修补、监视、扩展和复制，因此组织资源可以集中于产生收入的应用程序和业务，而不是普通的操作任务。

#### Amazon DynamoDB

* Amazon DYNAMODB是一种快速灵活的NoSQL数据库服务，适用于任何规模的需要一致的、毫秒级延迟的所有应用程序。它是一个完全托管的数据库，支持文档和键/值数据模型。它灵活的数据模型和可靠的性能使它非常适合移动、Web、游戏、广告技术，物联网和许多其他应用。

#### Amazon Redshift

* Amazon Redshift是一个快速、完全管理、PB级的数据仓库服务，它使分析结构化数据变得简单且经济高效。Amazon Redshift提供了一个标准的SQL接口，允许组织使用现有的商业智能工具。通过利用提高I/O效率和跨多个节点并行查询的柱状存储技术，Amazon Redshift能够提供快速的查询性能。Amazon Redshift体系结构允许组织自动执行与提供、配置和监视云数据仓库相关的大多数常见管理任务。

#### Amazon ElastiCache 

* Amazon Elasticache是一个Web服务，它简化了云中内存缓存的部署、操作和扩展。该服务允许组织从快速、托管的内存缓存中检索信息，而不是完全依赖速度较慢的基于磁盘的数据库，从而提高了Web应用程序的性能。在撰写本文时，Amazon Elasticache支持memcached和redis缓存引擎。

### 管理工具

* AWS提供各种工具，帮助企业管理自己的AWS资源。本章节概述了AWS提供给企业的管理工具。

#### Amazon CloudWatch

* Amazon cloudwatch是一项针对AWS云资源和AWS上运行的应用程序的监视服务，它允许组织收集和跟踪度量、收集和监视日志文件以及设置警报。通过利用Amazon cloudwatch，组织可以在系统范围内了解资源利用率、应用程序性能，以及运营健康。通过使用这些洞察力，组织可以根据需要做出反应，以保持应用程序的平稳运行。 

#### AWS CloudFormation

* AWS cloudformation为开发人员和系统管理员提供了创建和管理相关AWS资源集合的有效方法，以有序和可预测的方式提供和更新它们。AWS cloudformation定义了一种基于json的模板语言，可用于描述工作负载所需的所有AWS资源。模板可以提交给AWS cloudformation，服务将负责以适当的顺序配置和配置这些资源（参见图1.4）。

#### AWS CloudTrail

* AWS cloudtrail是一个web服务，它记录AWS api对某个帐户的调用，并提供日志文件供审计和审查。记录的信息包括api调用方的身份、api调用的时间、api调用方的源ip地址、请求参数和服务返回的响应元素。

#### AWS Config

* AWS config是一个完全托管的服务，它向组织提供AWS资源清单、配置历史记录和配置更改通知，以启用安全性和治理。使用AWS config组织可以发现现有的AWS资源，导出包含所有配置详细信息的AWS资源清单，并确定资源在任何时间点的配置方式。这些功能支持合规审核、安全性分析、资源更改跟踪和故障排除 


### 安全和身份

* AWS提供安全和身份服务，帮助组织在云上保护他们的数据和系统。下一节将从一个较高等级讨论这些服务。

#### AWS Identity and Access Management （IAM)

* AWS身份和访问管理（IAM）使组织能够安全地控制其用户对AWS云服务和资源的访问。使用IAM，组织可以创建和管理AWS用户和组，并使用权限允许和拒绝其对AWS资源的访问。

#### AWS Key Management Service(KMS)

* AWS密钥管理服务（KMS）是一种托管服务，它使组织能够轻松创建和控制用于加密其数据的加密密钥，并使用硬件安全模块（hsms）保护密钥的安全性。AWS KMS与其他几个AWS云服务集成，以帮助保护与这些服务一起存储的数据。

#### AWS Directory Service

* AWS目录服务允许组织在AWS云上设置和运行Microsoft Active Directory，或将其AWS资源连接到现有的内部部署Microsoft Active Directory。组织可以使用它来管理用户和组、提供对应用程序和服务的单点登录、创建和应用组策略，域加入Amazon ec2实例，简化基于云的linux和microsoft windows工作负载的部署和管理。


#### AWS Certificate Manager

* AWS证书管理器是一种服务，允许组织轻松地配置、管理和部署安全套接字层/传输层安全（ssl/tls）证书，以便与AWS云服务一起使用。它消除了购买、上载和续订ssl/tls证书的耗时的手动过程。使用AWS证书管理器，组织可以快速请求证书，将其部署到AWS资源（如弹性负载平衡或Amazon cloudfront发行版）上，并让AWS证书管理器处理证书续订。

#### AWS Web Application Firewall (WAF)

* AWS Web应用程序防火墙（WAF）有助于保护Web应用程序免受可能影响应用程序可用性、危害安全性或消耗过多资源的常见攻击和利用。AWS WAF通过定义可自定义的Web安全规则，使组织能够控制允许或阻止哪些通信流到其Web应用程序

### Application Services 

AWS provides a variety of managed services to use with applications. The following section explores the application services at a high level. 
* AWS提供多种和应用一起使用的托管服务。下面章节以一个高等级概述应用服务。

#### Amazon API Gateway

* Amazon api gateway是一个完全托管的服务，它使开发人员可以轻松地创建、发布、维护、监视和保护任何规模的api。组织可以创建一个api，作为应用程序访问数据、业务逻辑或后端服务功能的“前门”（例如：运行在Amazon ec2上的工作负载，在AWS lambda或任何web应用程序上运行的代码）。Amazon api gateway处理接受和处理多达数十万个并发api调用所涉及的所有任务，包括流量管理、授权和访问控制、监视和api版本管理


#### Amazon Elastic Transcoder

* Amazon Elastic转码器是一种在云中进行媒体转码的技术。它被设计成一种高度可扩展且经济高效的方式，供开发者和企业将媒体文件从源格式转换（或转码）为可在智能手机、平板电脑和个人电脑等设备上播放的版本。

#### Amzaon Simple Notification Service （Amazon SNS）

* Amazon简单通知服务（Amazon SNS）是一种协调和管理向接收者投递或发送消息的web服务。在Amazon sns中，有两种类型的客户端-发布者和订阅者，也称为生产者和消费者。发布服务器通过生成消息并将消息发送到主题（逻辑访问点和通信通道）与订阅服务器异步通信。订阅服务器在订阅该主题时通过受支持的协议之一使用或接收消息或通知 

#### Amazon Simple Email Service（Amazon SES）

* Amazon简单电子邮件服务（Amazon SES）是一种经济高效的电子邮件服务，组织可以使用它向客户发送事务性电子邮件、营销消息或任何其他类型的内容。Amazon SES还可以用于接收消息并将其传递到Amazon S3存储桶，通过AWS Lambda函数调用自定义代码，或者向Amazon SNS发布通知。

#### Amazon Simple Workflow Service(Amazon SWF)

* Amazon Simple Workflow Service（Amazon SWF）帮助开发人员构建、运行和扩展具有并行或顺序步骤的后台作业。Amazon SWF可以看作是云上的完全受管状态跟踪器和任务协调器。在常见的体系结构模式中，如果应用程序的步骤需要500毫秒以上才能完成，跟踪处理状态并在任务失败时提供恢复或重试的能力至关重要。

#### Amazon Simple Queue Service(Amazon SQS)

* Amazon Simple Queue Service（Amazon SQS）是一种快速、可靠、可扩展、完全托管的消息队列服务。Amazon SQS使分离云应用程序的组件变得简单且经济高效。使用Amazon SQS，组织可以在任何吞吐量级别传输任何数量的数据，不丢失消息或要求其他服务始终可用。

## 概述

* "云计算"一词是指通过互联网按需交付IT资源，按需付费。组织不必购买、拥有和维护数据中心和服务器，而是可以根据需要获取计算能力、存储、数据库和其他服务等技术。使用云计算，AWS在一个安全的环境中管理和维护技术基础设施，企业通过互联网访问这些资源来开发和运行他们的应用程序。容量可以立即增长或缩减，企业只支付他们使用的东西。

* 云计算带来了技术获取、使用和管理方式的革命性转变，以及组织如何为技术服务进行预算和支付。虽然每个组织都经历了一次独特的云端之旅，带来了众多好处，六个优势一次又一次地显现出来。了解这些优势可以帮助架构师形成能够为组织带来持续利益的解决方案。

* AWS提供了一个高可用性的技术基础设施平台，在全球有多个位置。这些位置由区域和可用性区域组成。这使组织能够在全球多个位置放置资源和数据。有助于保护机密性、完整性，系统和数据的可用性对于AWS来说是至关重要的，同时也维护了世界各地组织的信任和信心。

* AWS提供了一套广泛的全球计算、存储、数据库、分析、应用程序和部署服务，帮助组织更快地移动、降低IT成本和扩展应用程序。对这些服务的广泛了解使解决方案架构师能够在AWS平台上设计有效的分布式应用程序和系统


## 考试基础

### 了解全球基础设施

* AWS提供了一个高可用的技术基础设施平台，在全球有多个位置。这些位置由Regions和可用域组成。每个Region都位于一个单独的地理区域，并且有多个独立称为可用性区域的位置，

### 理解Region

* AWS区域是由一组数据中心组成的物理地理位置。AWS区域允许在全球多个位置放置资源和数据。每个区域完全独立，设计为与其他区域完全隔离。这将实现最大可能的容错性和稳定性。除非组织选择跨区域复制资源。

### 理解可用域

* 可用域是一个区域内的一个或多个数据中心，旨在与其他可用性区域中的故障隔离。可用性区域为同一Region内的其他可用域域提供廉价、低延迟的网络连接。通过将资源放在不同的可用域中，组织可以保护其网站或应用程序免受影响单个位置的服务中断的影响。

### 理解混合部署模型

* 混合部署模型是一种体系结构模式，为基础设施和应用程序提供基于云的资源和不在云中的现有资源之间的连接。


## Review Questions
1. Which of the following describes a physical location around the world where AWS clusters data centers?

 A. Endpoint 
 B. Collection 
 C. Fleet
 **D. Region**

2. Each AWS region is composed of two or more locations that offer organizations the ability to operate production systems that are more highly available, fault tolerant, and scalable than would be possible using a single data center. What are these locations called? 
 
 **A. Availability Zones**
 B. Replication areas
 C. Geographic districts
 D. Compute centers

3. What is the deployment term for an environment that extends an existing on-premises infrastructure into the cloud to connect cloud resources to internal systems?

 A. All-in deployment
 **B. Hybrid deployment**
 C. On-premises deployment
 D. Scatter deployment

4. Which AWS Cloud service allows organizations to gain system-wide visibility into resource utilization, application performance, and operational health?

 A. AWS Identity and Access Management (IAM)
 B. Amazon Simple Notification Service (Amazon SNS)
 **C. Amazon CloudWatch**
 D. AWS CloudFormation

5. Which of the following AWS Cloud services is a fully managed NoSQL database service?

 A. Amazon Simple Queue Service (Amazon SQS)
 **B. Amazon DynamoDB**
 C. Amazon ElastiCache
 D. Amazon Relational Database Service (Amazon RDS)

 6. Your company experiences fluctuations in traffic patterns to their e-commerce website based on flash sales. What service can help your company dynamically match the required compute capacity to the spike in traffic during flash sales?

 **A. Auto Scaling**
 B. Amazon Glacier
 C. Amazon Simple Notification Service (Amazon SNS)
 D. Amazon Virtual Private Cloud (Amazon VPC)

7. Your company provides an online photo sharing service. The development team is looking for ways to deliver image files with the lowest latency to end users so the website content is delivered with the best possible performance. What service can help speed up distribution of these image files to end users around the world?

 A. Amazon Elastic Compute Cloud (Amazon EC2)
 B. Amazon Route 53
 C. AWS Storage Gateway
 **D. Amazon CloudFront**

8. Your company runs an Amazon Elastic Compute Cloud (Amazon EC2) instance periodically to perform a batch processing job on a large and growing filesystem. At the end of the batch job, you shut down the Amazon EC2 instance to save money but need to persist the filesystem on the Amazon EC2 instance from the previous batch runs. What AWS Cloud service can you leverage to meet these requirements?

 A. Amazon Elastic Block Store (Amazon EBS)
 B. Amazon DynamoDB
 **C. Amazon Glacier**
 D. AWS CloudFormation 

9. What AWS Cloud service provides a logically isolated section of the AWS Cloud where organizations can launch AWS resources in a virtual network that they define?

 A. Amazon Simple Workflow Service (Amazon SWF)
 B. Amazon Route 53
 **C. Amazon Virtual Private Cloud (Amazon VPC)**
 D. AWS CloudFormation 

10. Your company provides a mobile voting application for a popular TV show, and 5 to 25 million viewers all vote in a 15-second timespan. What mechanism can you use to decouple the voting application from your back-end services that tally the votes?
 A. AWS CloudTrail
 **B. Amazon Simple Queue Service (Amazon SQS)**
 C. Amazon Redshift
 D. Amazon Simple Notification Service (Amazon SNS)


## word

* functional requirement 功能要求；功能条件说明书
* protects 保护; 防护; 实行贸易保护; protect的第三人称单数
* mission-critical关键的，至关重要的
* accidental 意外的; 偶然的; 偶然; 次要方面
* deliberate 故意的; 蓄意的; 存心的; 不慌不忙的; 小心翼翼的; 从容不迫的; 仔细考虑; 深思熟虑; 反复思考
* theft 偷; 偷窃; 盗窃罪
* leakage 泄漏量; 漏损量; 泄漏; 渗漏
* integrity 诚实正直; 完整; 完好
* compromise 妥协; 折中; 互让; 和解; 妥协方案; 达成妥协; 妥协，折中，让步; 违背; 达不到; 使陷入危险，使受到怀疑
* deletion   删除