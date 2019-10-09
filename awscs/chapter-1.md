# AWS 简介
## 什么是云计算
云计算是通过互联网按需交付IT资源和应用程序，并按需付费。无论是运行向数百万移动用户共享照片的应用程序，还是提供支持业务关键运营的服务，云提供了对灵活和低成本IT资源的快速访问。使用云计算，您不需要在硬件上进行大量的前期投资，也不需要花费大量时间管理硬件。相反，您可以提供正确类型和合适大小的计算资源，以支持您最新的聪明想法或运营您的IT部门。使用云计算，您几乎可以立即访问所需的任意数量的资源，而且只需支付您使用的资源的费用。
云计算的优点
Cloud	computing	introduces	a	revolutionary	shift	in	how	technology	is	obtained,	used,	and managed,	and	in	how	organizations	budget	and	pay	for	technology	services.	With	the	ability to	reconfigure	the	computing	environment	quickly	to	adapt	to	changing	business requirements,	organizations	can	optimize	spending.	Capacity	can	be	automatically	scaled	up or	down	to	meet	fluctuating	usage	patterns.	Services	can	be	temporarily	taken	offline	or	shut down	permanently	as	business	demands	dictate.	In	addition,	with	pay-per-use	billing,	AWS Cloud	services	become	an	operational	expense	instead	of	a	capital	expense. While	each	organization	experiences	a	unique	journey	to	the	cloud	with	numerous	benefits, six	advantages	become	apparent	time	and	time	again,	as	illustrated	in	Figure	1.1.

云计算带来了技术获取、使用和管理方式的革命性转变，以及组织如何为技术服务进行预算和支付。云计算能够快速重新配置计算环境，以适应不断变化的业务需求，组织可以优化支出。容量可以自动增加或减少，以满足波动的使用模式。服务可以暂时脱机或根据业务需求永久关闭。此外，使用按次计费，aws云服务成为一种运营费用，而不是资本费用。虽然每个组织都经历了一次独特的云端之旅，带来了许多好处，但六个好处却一次又一次地显现出来，如图-1.1所示。

Global in minutes
Variable VS.capital expense
Economies of Scale
Increace speed and ingility
Focus on business differentiators
Stop guessing capacity


## AWS 基本原理

aws的核心旨在安全的云服务平台上通过互联网提供it资源的按需交付，提供计算能力、存储、数据库、内容交付和其他功能，以帮助企业扩展和增长。
At	its	core,	AWS	provides	on-demand	delivery	of	IT	resources	via	the	Internet	on	a	secure cloud	services	platform,	offering	compute	power,	storage,	databases,	content	delivery,	and other	functionality	to	help	businesses	scale	and	grow.	Using	AWS	resources	instead	of	your own	is	like	purchasing	electricity	from	a	power	company	instead	of	running	your	own generator,	and	it	provides	the	key	advantages	of	cloud	computing:	Capacity	exactly	matches your	need,	you	pay	only	for	what	you	use,	economies	of	scale	result	in	lower	costs,	and	the service	is	provided	by	a	vendor	experienced	in	running	large-scale	networks. AWS	global	infrastructure	and	AWS	approach	to	security	and	compliance	are	key foundational	concepts	to	understand	as	you	prepare	for	the	exam. Global	Infrastructure AWS	serves	over	one	million	active	customers	in	more	than	190	countries,	and	it	continues	to expand	its	global	infrastructure	steadily	to	help	organizations	achieve	lower	latency	and higher	throughput	for	their	business	needs. AWS	provides	a	highly	available	technology	infrastructure	platform	with	multiple	locations worldwide.	These	locations	are	composed	of	regions	and	Availability	Zones.	Each	region	is	a separate	geographic	area.	Each	region	has	multiple,	isolated	locations	known	as	Availability Zones.	AWS	enables	the	placement	of	resources	and	data	in	multiple	locations.	Resources aren’t	replicated	across	regions	unless	organizations	choose	to	do	so. Each	region	is	completely	independent	and	is	designed	to	be	completely	isolated	from	the other	regions.	This	achieves	the	greatest	possible	fault	tolerance	and	stability.	Each Availability	Zone	is	also	isolated,	but	the	Availability	Zones	in	a	region	are	connected	through low-latency	links.	Availability	Zones	are	physically	separated	within	a	typical	metropolitan region	and	are	located	in	lower-risk	flood	plains	(specific	flood	zone	categorization	varies	by region).	In	addition	to	using	a	discrete	uninterruptable	power	supply	(UPS)	and	on-site backup	generators,	they	are	each	fed	via	different	grids	from	independent	utilities	(when available)	to	reduce	single	points	of	failure	further.	Availability	Zones	are	all	redundantly connected	to	multiple	tier-1	transit	providers.	By	placing	resources	in	separate	Availability Zones,	you	can	protect	your	website	or	application	from	a	service	disruption	impacting	a single	location.
	You	can	achieve	high	availability	by	deploying	your	application	across	multiple Availability	Zones.	Redundant	instances	for	each	tier	(for	example,	web,	application,	and database)	of	an	application	should	be	placed	in	distinct	Availability	Zones,	thereby creating	a	multisite	solution.	At	a	minimum,	the	goal	is	to	have	an	independent	copy	of each	application	stack	in	two	or	more	Availability	Zones.
Security	and	Compliance Whether	on-premises	or	on	AWS,	information	security	is	of	paramount	importance	to
organizations	running	critical	workloads.	Security	is	a	core	functional	requirement	that protects	mission-critical	information	from	accidental	or	deliberate	theft,	leakage,	integrity compromise,	and	deletion.	Helping	to	protect	the	confidentiality,	integrity,	and	availability	of systems	and	data	is	of	the	utmost	importance	to	AWS,	as	is	maintaining	your	trust	and confidence. This	section	is	intended	to	provide	a	very	brief	introduction	to	AWS	approach	to	security	and compliance.	Chapter	12,	“Security	on	AWS,”	and	Chapter	13,	“AWS	Risk	and	Compliance,”	will address	these	topics	in	greater	detail,	including	the	importance	of	each	on	the	exam. Security Cloud	security	at	AWS	is	the	number	one	priority.	All	AWS	customers	benefit	from	data center	and	network	architectures	built	to	satisfy	the	requirements	of	the	most	securitysensitive	organizations.	AWS	and	its	partners	offer	hundreds	of	tools	and	features	to	help organizations	meet	their	security	objectives	for	visibility,	auditability,	controllability,	and agility.	This	means	that	organizations	can	have	the	security	they	need,	but	without	the	capital outlay	and	with	much	lower	operational	overhead	than	in	an	on-premises	environment. Organizations	leveraging	AWS	inherit	all	the	best	practices	of	AWS	policies,	architecture,	and operational	processes	built	to	satisfy	the	requirements	of	the	most	security-sensitive customers.	The	AWS	infrastructure	has	been	designed	to	provide	the	highest	availability while	putting	strong	safeguards	in	place	regarding	customer	privacy	and	segregation.	When deploying	systems	on	the	AWS	Cloud	computing	platform,	AWS	helps	by	sharing	the	security responsibilities	with	the	organization.	AWS	manages	the	underlying	infrastructure,	and	the organization	can	secure	anything	it	deploys	on	AWS.	This	affords	each	organization	the flexibility	and	agility	they	need	in	security	controls. This	infrastructure	is	built	and	managed	not	only	according	to	security	best	practices	and standards,	but	also	with	the	unique	needs	of	the	cloud	in	mind.	AWS	uses	redundant	and layered	controls,	continuous	validation	and	testing,	and	a	substantial	amount	of	automation to	ensure	that	the	underlying	infrastructure	is	monitored	and	protected	24/7.	AWS	ensures that	these	controls	are	consistently	applied	in	every	new	data	center	or	service. Compliance When	customers	move	their	production	workloads	to	the	AWS	Cloud,	both	parties	become responsible	for	managing	the	IT	environment.	Customers	are	responsible	for	setting	up	their environment	in	a	secure	and	controlled	manner.	Customers	also	need	to	maintain	adequate governance	over	their	entire	IT	control	environment.	By	tying	together	governance-focused, audit-friendly	service	features	with	applicable	compliance	or	audit	standards,	AWS	enables customers	to	build	on	traditional	compliance	programs.	This	helps	organizations	establish and	operate	in	an	AWS	security	control	environment.
	Organizations	retain	complete	control	and	ownership	over	the	region	in	which their	data	is	physically	located,	allowing	them	to	meet	regional	compliance	and	data residency	requirements.
The	IT	infrastructure	that	AWS	provides	to	organizations	is	designed	and	managed	in alignment	with	security	best	practices	and	a	variety	of	IT	security	standards.	The	following	is a	partial	list	of	the	many	certifications	and	standards	with	which	AWS	complies: Service	Organization	Controls	(SOC)	1/International	Standard	on	Assurance Engagements	(ISAE)	3402,	SOC	2,	and	SOC	3 Federal	Information	Security	Management	Act	(FISMA),	Department	of	Defense Information	Assurance	Certification	and	Accreditation	Process	(DIACAP),	and	Federal Risk	and	Authorization	Management	Program	(FedRAMP) Payment	Card	Industry	Data	Security	Standard	(PCI	DSS)	Level	1 International	Organization	for	Standardization	(ISO)	9001,	ISO	27001,	and	ISO	27018 AWS	provides	a	wide	range	of	information	regarding	its	IT	control	environment	to	help organizations	achieve	regulatory	commitments	in	the	form	of	reports,	certifications, accreditations,	and	other	third-party	attestations.


## AWS	云计算平台 

  aws提供了许多云服务，您可以将它们结合起来以满足业务或组织需求（请参见图1.2）。了解所有的平台服务将使您成为一名全面的解决方案架构师，了解本书中概述的服务和基本概念将有助于您为《AWS认证解决方案架构师-联合考试》做好准备。


本节按类别介绍主要的aws云服务。随后的章节提供了与考试相关的服务的更深入的视图。

### 平台访问

  要访问aws云服务，可以使用aws管理控制台、aws命令行界面（cli）或aws软件开发工具包（sdk）。

* aws管理控制台是一个用于管理aws云服务的web应用程序。控制台为执行许多任务提供直观的用户界面。每个服务都有自己的控制台，可以从aws管理控制台访问。控制台还提供有关帐户和帐单的信息。

* aws命令行界面（cli）是用于管理aws云服务的统一工具，只需下载和配置一个工具，就可以从命令行控制多个服务，并通过脚本实现自动化。

* aws软件开发工具包（sdk）提供了一个应用程序编程接口（api），它与基本构成aws平台的web服务进行交互。sdk为许多不同的编程语言和平台提供支持，允许您使用首选语言。

对于Web服务端点，使用SDK可以通过提供对许多服务的编程访问来减少编码的复杂性。 

### 计算和网络服务

  aws提供各种计算和网络服务，为企业开发和运行其工作负载提供核心功能。这些计算和网络服务可与存储、数据库和应用程序服务一起使用，为计算、查询处理提供完整的解决方案，以及广泛应用的存储。本节提供核心计算和网络服务的高级描述

### Amazon Elastic Compute Cloud（Amazon EC2)

  Amazon Elastic Compute Cloud（Amazon EC2）是一个在云中提供可调整大小的计算能力的Web服务，它允许组织获取和配置Amazon数据中心的虚拟服务器，并利用这些资源来构建和托管软件系统。组织可以从各种操作系统和资源配置（内存、CPU、存储等）中选择最适合每个工作负载的应用程序配置文件。Amazon EC2提供了一个真正的虚拟计算环境，允许组织使用各种操作系统启动计算资源，使用自定义应用程序加载它们，并在保持完全控制的同时管理网络访问权限

### aws lambda

  是一个面向后端web开发人员的零管理计算平台，它在aws云上为您运行代码，并为您提供细粒度的定价结构。aws lambda在一个区域的多个可用性区域中运行自己的aws计算组amazon ec2实例，它提供了aws基础设施的高可用性、安全性、性能和可扩展性 

### 自动伸缩

* Auto Scaling允许组织根据为特定工作负载定义的条件自动向上或向下扩展Amazon EC2容量（见图1.3）。它不仅可以帮助维护应用程序可用性并确保所需数量的Amazon EC2实例正在运行，但它也允许资源进行扩展以满足动态工作负载的需求，组织可以优化成本，而不是为峰值负载提供资源，只使用实际需要的容量。

* 自动伸缩非常适合于具有稳定需求模式的应用程序，也适合于在使用中体验每小时、每天或每周变化的应用程序 

### 弹性负载均衡

* 弹性负载平衡在云中跨多个Amazon EC2实例自动分配传入的应用程序流量。它使组织能够在其应用程序中实现更高级别的容错，无缝地提供分配应用程序流量所需的负载平衡容量。

### AWS Elastic Beanstalk 

* AWS Elastic Beanstalk是在AWS上启动和运行Web应用程序的最快和最简单的方式。开发人员只需上传他们的应用程序代码，该服务就会自动处理所有细节，如资源配置、负载平衡、自动伸缩，它为各种平台提供支持，包括php、java、python、ruby、node.js、.net和go。使用aws弹性beanstalk，组织可以完全控制为应用程序提供动力的aws资源，并可以随时访问底层资源。

### Amazon虚拟私有云（Amazon VPC）

* amazon虚拟私有云（amazon vpc）允许组织提供aws云的逻辑隔离部分，在那里他们可以在自己定义的虚拟网络中启动aws资源。组织可以完全控制虚拟环境，包括选择ip地址范围、创建子网，以及路由表的配置和网络网关。此外，组织可以使用硬件或软件虚拟专用网（VPN）连接或专用电路使用AWS直接连接将其公司数据中心网络扩展到AWS

### AWS Direct Connect

* aws direct connect允许组织建立从其数据中心到aws的专用网络连接。使用aws direct connect，组织可以在aws和其数据中心、办公室或托管环境之间建立专用连接，这在许多情况下可以降低网络成本，增加带宽吞吐量，提供比基于Internet的VPN连接更一致的网络体验

### Amazon	Route	53 

* 亚马逊Route53是一个高度可用和可扩展的域名系统（DNS）网络服务。它的目的是通过将人类可读的名称（如www.example.com）转换为计算机用来相互连接的数字IP地址（如192.0.2.1），为开发人员和企业提供一种极其可靠和经济高效的方式来将最终用户路由到Internet应用程序。允许您直接从aws购买和管理域。

### 存储和内容分发

AWS提供各种满足需要的存储服务，诸如：Amazon简单存储服务，Amzzon CloudFront，Amazon弹性块服务。本章节只是存储和内容分发服务的概述。

#### Amazon S3

* Amazon Simple Storage Service（Amazon S3）为开发人员和IT团队提供了高度持久和可扩展的对象存储，可以处理几乎无限量的数据和大量并发用户。组织可以存储任何类型的对象，如HTML页面、源代码文件、图像文件和加密数据，并使用基于http的协议访问它们。amazon s3为各种各样的用例提供经济高效的对象存储，包括备份和恢复、近线归档、大数据分析、灾难恢复、云应用程序和内容分发。

#### Amazon Glacier

* Amazon Glacier是一种安全、耐用、成本极低的存储服务，用于数据存档和长期备份。组织可以以非常低的每月每GB成本可靠地存储大量或少量数据。为了使客户的成本保持在较低水平，AmazonGlacier针对不常访问的数据进行了优化，在这种情况下，检索时间适合几个小时。AmazonS3与AmazonGlacier紧密集成，允许组织为其工作负载选择正确的存储层 

#### Amazon Elastic Block Storage（Amazon EBS）

* Amazon弹性块存储（Amazon EBS）为Amazon EC2实例提供持久的块级存储卷。每个Amazon EBS卷在其可用区内自动复制，以保护组织不受组件故障的影响，提供高可用性和耐用性。通过提供一致和低延迟的性能，Amazon EBS提供了运行各种工作负载所需的磁盘存储。

#### AWS Storage Gateway

* AWS存储网关是一项将内部软件设备与基于云的存储连接起来的服务，可在组织的内部IT环境和AWS存储基础设施之间提供无缝和安全的集成。该服务支持与现有应用程序一起工作的行业标准存储协议。它提供低功耗的通过在本地维护频繁访问的数据的缓存，同时在AmazonS3或AmazonGlacie中安全地存储加密的所有数据，从而保持稳定的性能。

#### AWS CloudFront

* amazon cloudfront是一个内容交付web服务，它与其他aws云服务集成，使开发人员和企业能够以低延迟、高数据传输速度和无最低使用承诺的方式向全球用户分发内容。Amazon CloudFront可以使用边缘位置的全球网络来交付您的整个网站，包括动态、静态、流式和交互式内容。对内容的请求会自动路由到最近的边缘位置，因此内容会以最佳性能交付给全球各地的最终用户

### 数据库服务

* aws提供了完全托管的关系数据库服务和nosql数据库服务，以及作为服务的内存缓存和PB级的数据仓库解决方案。本小节概述了数据库服务包含哪些产品：

#### Amazon RDS

* amazon关系数据库服务（amazon rds）提供了一个完全托管的关系数据库，支持许多流行的开源和商用数据库引擎。这是一个经济高效的服务，允许组织启动安全、高可用、容错的数据库。在几分钟内就可以生产数据库了。由于amazon rds管理耗时的管理任务，包括备份、软件修补、监视、扩展和复制，因此组织资源可以集中于产生收入的应用程序和业务，而不是普通的操作任务。

#### Amazon	DynamoDB

* Amazon DYNAMODB是一种快速灵活的NoSQL数据库服务，适用于任何规模的需要一致的、毫秒级延迟的所有应用程序。它是一个完全托管的数据库，支持文档和键/值数据模型。它灵活的数据模型和可靠的性能使它非常适合移动、Web、游戏、广告技术，物联网和许多其他应用。

#### Amazon	Redshift

* Amazon Redshift是一个快速、完全管理、PB级的数据仓库服务，它使分析结构化数据变得简单且经济高效。Amazon Redshift提供了一个标准的SQL接口，允许组织使用现有的商业智能工具。通过利用提高I/O效率和跨多个节点并行查询的柱状存储技术，Amazon Redshift能够提供快速的查询性能。Amazon Redshift体系结构允许组织自动执行与提供、配置和监视云数据仓库相关的大多数常见管理任务。

#### Amazon	ElastiCache 

* Amazon Elasticache是一个Web服务，它简化了云中内存缓存的部署、操作和扩展。该服务允许组织从快速、托管的内存缓存中检索信息，而不是完全依赖速度较慢的基于磁盘的数据库，从而提高了Web应用程序的性能。在撰写本文时，Amazon Elasticache支持memcached和redis缓存引擎。

### 管理工具

* AWS提供各种工具，帮助企业管理自己的AWS资源。本章节概述了AWS提供给企业的管理工具。

#### Amazon CloudWatch

* amazon cloudwatch是一项针对aws云资源和aws上运行的应用程序的监视服务，它允许组织收集和跟踪度量、收集和监视日志文件以及设置警报。通过利用amazon cloudwatch，组织可以在系统范围内了解资源利用率、应用程序性能，以及运营健康。通过使用这些洞察力，组织可以根据需要做出反应，以保持应用程序的平稳运行。 

#### AWS CloudFormation

* aws cloudformation为开发人员和系统管理员提供了创建和管理相关aws资源集合的有效方法，以有序和可预测的方式提供和更新它们。aws cloudformation定义了一种基于json的模板语言，可用于描述工作负载所需的所有aws资源。模板可以提交给aws cloudformation，服务将负责以适当的顺序配置和配置这些资源（参见图1.4）。

#### AWS CloudTrail

* aws cloudtrail是一个web服务，它记录aws api对某个帐户的调用，并提供日志文件供审计和审查。记录的信息包括api调用方的身份、api调用的时间、api调用方的源ip地址、请求参数和服务返回的响应元素。

#### AWS Config

* aws config是一个完全托管的服务，它向组织提供aws资源清单、配置历史记录和配置更改通知，以启用安全性和治理。使用aws config组织可以发现现有的aws资源，导出包含所有配置详细信息的aws资源清单，并确定资源在任何时间点的配置方式。这些功能支持合规审核、安全性分析、资源更改跟踪和故障排除 


### 安全和身份

* aws提供安全和身份服务，帮助组织在云上保护他们的数据和系统。下一节将从一个较高等级讨论这些服务。

#### AWS Identity and Access Management （IAM)

* aws身份和访问管理（IAM）使组织能够安全地控制其用户对aws云服务和资源的访问。使用IAM，组织可以创建和管理aws用户和组，并使用权限允许和拒绝其对aws资源的访问。

#### AWS Key Management Service(KMS)

* aws密钥管理服务（kms）是一种托管服务，它使组织能够轻松创建和控制用于加密其数据的加密密钥，并使用硬件安全模块（hsms）保护密钥的安全性。aws kms与其他几个aws云服务集成，以帮助保护与这些服务一起存储的数据。

#### AWS Directory Service

* AWS目录服务允许组织在AWS云上设置和运行Microsoft Active Directory，或将其AWS资源连接到现有的内部部署Microsoft Active Directory。组织可以使用它来管理用户和组、提供对应用程序和服务的单点登录、创建和应用组策略，域加入amazon ec2实例，简化基于云的linux和microsoft windows工作负载的部署和管理。


#### AWS Certificate Manager

* aws证书管理器是一种服务，允许组织轻松地配置、管理和部署安全套接字层/传输层安全（ssl/tls）证书，以便与aws云服务一起使用。它消除了购买、上载和续订ssl/tls证书的耗时的手动过程。使用aws证书管理器，组织可以快速请求证书，将其部署到aws资源（如弹性负载平衡或amazon cloudfront发行版）上，并让aws证书管理器处理证书续订。

#### AWS Web Application Firewall (WAF)

* AWS Web应用程序防火墙（WAF）有助于保护Web应用程序免受可能影响应用程序可用性、危害安全性或消耗过多资源的常见攻击和利用。AWS WAF通过定义可自定义的Web安全规则，使组织能够控制允许或阻止哪些通信流到其Web应用程序


