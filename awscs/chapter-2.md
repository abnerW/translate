# 第二章 Amazon 简单文件存储（Amazon S3) 和Amazon Glacier存储

**《AWS认证解决方案架构师-联合考试》中的本章节包括不限于如下内容：**

## 第一点 设计高可用，经济高效，零容错，可扩展的系统

### 找出和识别云架构考虑因素，例如：基础组件和有效性设计

**包括如下内容：**
```
  * 怎么设计云服务
  * 计划和设计
  * 监控和日志
  * 需要熟悉如下内容：
    * AWS架构最佳实践
    * 根据客户规范进行开发，包括定价/成本（例如，按需，保留，现货；恢复时间目标[RTO]和恢复点目标[RPO]灾难恢复设计）
  * 架构权衡决策（例如，高可用性与成本） 
  * 混合IT架构
  * 弹性和可扩展性
```

## 第二点 实现与部署

### 确定使用Amazon简单存储服务（Amazon S3）编写和实现云解决方案的适当技术和方法
**包括如下内容：**
```
  * 配置服务以支持云中的法规遵从性要求
  * 在AWS全球基础设施上发布实例
  * 配置AWS标识和访问管理（IAM）策略和最佳实践
```

## 第三点 数据安全

### 认识并实施安全实践以实现最佳的云部署和维护
**包括如下内容：**
```
  * AWS 安全体系结构：
    * "核心" Amazon S3安全功能集
    * 加密解决方案（如密钥服务）
    * 复杂的访问控制（构建复杂的安全组、访问控制列表[ACL]等） 
```

## 简介

* 本章旨在让您基本了解AWS上提供的核心对象存储服务：Amazon简单存储服务（Amazon S3）和Amazon Glacier。Amazon S3为开发人员和IT团队提供安全、持久和高度可扩展的云存储。Amazon S3是一种易于使用的对象存储，具有简单的Web服务界面，您可以使用该界面从Web上的任何位置存储和检索任何数量的数据。Amazon S3还允许您只为实际使用的存储付费，它消除了与传统存储相关的容量规划和容量限制。

* Amazon S3是AWS引入的第一个服务之一，它是基本的Web服务之一，几乎所有在AWS中运行的应用程序都直接或间接使用Amazon S3。Amazon S3可以单独使用或与其他AWS服务结合使用，它提供了与许多其他AWS云服务高度集成的服务。例如，Amazon S3作为Amazon Kinesis和Amazon Elastic MapReduce（Amazon EMR）的持久目标存储，用作Amazon Elastic Block Store（Amazon EBS）和Amazon Relational Database Service（Amazon RDS）快照的存储，它被用作Amazon RealStand和Amazon DynDoDB的数据分级或加载存储机制，在许多其他功能中。因为Amazon S3是如此灵活、高度集成和通常使用的，所以要详细理解该服务是很重要的。

* Amazon S3存储的常见常见包括：
```
  * 备份或者归档本地或者云上的数据
  * 内容、媒体和软件存储和分发
  * 大数据分析
  * 静态网站托管
  * 云本地移动和互联网应用程序托管
  * 灾难恢复
```

* 为了支持这些用例和更多的用例，Amazon S3提供了一系列为各种通用用例设计的**存储类**：通用、不经常访问和存档。为了帮助管理数据的整个生命周期，Amazon S3提供了可配置的生命周期策略。通过使用生命周期策略，您可以让数据自动迁移到最合适的存储类，而无需修改应用程序代码。

* Amazon Glacier是与Amazon S3相关的另一种云存储服务，但它以极低的成本为数据存档和长期备份进行了优化。Amazon Glacier适用于冷数据，这是很少被访问的数据，检索时间为3到5小时是可以接受的。Amazon Glacier可以同时用作Amazon S3的存储类（请参阅Amazon S3高级功能部分中的存储类和对象生命周期管理主题），作为一个独立的档案存储服务（见亚马逊冰川部分）。 

## 对象存储与传统的块和文件存储对比

* 在传统的IT环境中，主要有两种存储方式：块存储和文件存储。块存储在较低的原始存储设备级别运行，并将数据作为一组编号进行管理，固定大小的块。文件存储在操作系统级别的更高级别上运行，并将数据作为文件和文件夹的命名层次结构进行管理。块和文件存储通常通过网络以存储区域网络（SAN）的形式进行访问，用于块存储，使用的协议包括iscsi或光纤通道，或作为网络连接存储（NAS）文件服务器或文件存储"文件管理器"，使用诸如：通用Internet文件系统（CIFS）或网络文件系统（NFS）等协议。无论是直接连接还是网络连接、块或文件，此类存储都与使用存储的服务器和操作系统密切相关。

* Amazon S3对象存储是完全不同的，Amazon S3是云对象存储。Amazon S3存储不与服务器紧密关联，而是独立于服务器并通过Internet访问。数据不是使用SCSI、CIFS或NFS协议作为块或文件进行管理，而是使用基于标准HTTP谓词的应用程序接口（API）作为对象进行管理。

* 每个Amazon S3对象都包含数据和元数据。对象位于名为bucket的容器中，每个对象由唯一的用户指定密钥（filename）标识。bucket是一个简单的平面文件夹，没有文件系统层次结构。也就是说，可以有多个bucket，但是在一个bucket中不能有子bucket，每个bucket可以容纳无限数量的对象。

* 很容易将 Amazon S3对象（或对象的数据部分）看作一个文件，将密钥看作文件名。但是，要记住Amazon S3不是一个传统的文件系统，并且在很大程度上是不同的。在Amazon S3中，您可以获取一个对象或放置一个对象，同时对整个对象进行操作，而不是像对文件那样增量地更新对象的一部分。

* 不同于文件系统，Amazon S3是一种高度持久和高度可扩展的对象存储，它是为读取而优化的，并且是用一个故意最小化的特性集构建的。它为文件存储提供了一个简单而健壮的抽象，使您摆脱了在传统存储中通常必须处理的许多底层细节。例如，使用Amazon S3您不必担心设备或文件系统的存储限制和容量规划—单个存储桶可以存储无限数量的文件。您也不必担心数据的持久性或跨可用性区域的复制Amazon S3对象是自动的在一个Region内的多个设施中的多个设备上进行复制。与可伸缩性相同，如果您的请求率稳步增长，Amazon S3会自动分区bucket，以支持非常高的请求率和许多客户端的同时访问。

* 备注
```
  如果除了Amazon S3存储之外，还需要传统的块或文件存储，AWS 提供了选项。Amazon EBS服务为Amazon Elastic Compute Cloud（amazon EC2）实例提供块级存储。Amazon Elastic File System（Aws EFS）使用NFS v4协议提供网络连接共享文件存储（NAS存储）。 
```

## Amazon 简单存储服务（Amazon S3）基础

* 现在您已经了解了传统块和文件存储与云对象存储之间的一些关键区别，我们可以更详细地探讨amazon s3的基础知识。

## 桶（Bucket）

* bucket是存储在Amazon S3中的对象（文件）的容器（web文件夹）。每个Amazon S3对象都包含在bucket中。bucket构成Amazon S3的顶级命名空间，bucket名称是全局的。这意味着你的bucket名称必须在所有AWS帐户中是唯一的，就像域名系统（DNS）域名一样，不只是在您自己的帐户中。存储桶名称最多可以包含63个小写字母、数字、连字符和periods。您可以创建和使用多个存储桶；默认情况下，每个帐户最多可以有100个。

* 备注
```
 最好使用包含您的域名并符合DNS名称规则的存储桶名称。这样可以确保您的存储桶名称是您自己的，可以在所有区域使用，并且可以承载静态网站。
```

### AWS Regions

* 尽管Amazon S3 bucket的名称空间是全局的，但是每个Amazon S3 bucket都是在您选择的特定区域中创建的，这允许您控制数据的存储位置。
* 您可以创建和使用位于特定终端用户或客户集附近的存储桶，以最小化延迟
* 或者位于特定区域以满足数据位置和主权问题
* 或者位于远离主要设施的位置，以满足灾难恢复和法规遵从性需求

* 您可以控制数据的位置；Amazon S3存储桶中的数据存储在该区域中，除非您显式地将其复制到位于不同区域的另一个存储桶中。

### Objects

* 对象是存储在Amazon S3存储桶中的实体或文件。一个对象可以以任何格式存储几乎任何类型的数据。对象的大小可以从0字节到5tb，单个存储桶可以存储无限数量的对象。这意味着Amazon S3可以存储几乎无限数量的数据。

* 每个对象都由数据（文件本身）和元数据（关于文件的数据）组成。Amazon S3对象的数据部分对Amazon S3来说是不透明的。这意味着对象的数据被简单地看作是Amazon S3不知道或不关心您存储的数据类型的字节流，对于文本数据和二进制数据，该服务的作用并不不同。

* 与Amazon S3对象相关联的元数据是一组描述该对象的名称/值对。有两种类型的元数据：系统元数据和用户元数据。系统元数据由Amazon S3自己创建和使用，它包括最近修改的日期、对象大小、md5摘要，和http的Content-Type。用户元数据是可选的，只能在创建对象时指定。可以使用自定义元数据为数据添加对您有意义的属性。

### Keys

* 存储在s3存储桶中的每个对象都由一个称为密钥的唯一标识符标识。您可以将密钥视为文件名。一个密钥最多可以包含1024字节的unicode utf-8字符，包括嵌入的斜杠、反斜杠、点和破折号。

* 键在单个bucket中必须是唯一的，但是不同的bucket可以包含具有相同键的对象。 

### Object URL

Amazon S3是internet的存储，每个amazons3对象都可以通过使用web服务端点、bucket名称和对象密钥形成的唯一url来寻址。例如，url:http://mybucket.s3.amazonaws.com/jack.doc mybucket是S3 Bucket名称，jack.doc是密钥或文件名。如果创建了另一个对象，例如：http://mybucket.s3.amazonaws.com/fee/fi/fo/fum/jack.doc，那么bucket名称仍然是mybucket，但现在键或文件名是字符串fee/fi/fo/fum/jack.doc，键可以包含斜杠或反斜杠等分隔符，帮助您命名和逻辑组织Amazon S3对象，但对于Amazon S3来说，它只是一个扁平名称空间中的长键名，没有实际的文件和文件夹层次结构，更多信息请参见后面"Amazon S3高级特性"部分的主题"前缀和分隔符"。
	
* 备注
```
 为了方便起见，Amazon S3控制台和前缀和分隔符特性允许您在Amazon S3存储桶中导航，就像有一个文件夹层次结构一样。但是，请记住，bucket是没有结构的键的单一平面命名空间。
```

### Amazon S3 操作

Amazon S3 API故意很简单，只有几个常见的操作，包括：
* 创建/删除bucket
* 写对象
* 读对象
* 删除对象
* bucket中的keys列表

### REST 接口

* Amazon S3的本机接口是一个REST（表示状态传输）API。使用REST接口，您可以使用标准http或https请求来创建和删除bucket、KEYS列表以及读写对象。REST将标准http"verbs"（http方法）映射到常见的crud（create，read，update，delete）操作。create是http put（有时post）；read是http get；delete是http delete；update是http post（有时put）。

备注：
```
  始终对Amazon S3 api请求使用https，以确保您的请求和数据是安全的 
```
* 在大多数情况下，用户不直接使用REST接口，而是使用可用的高级接口来与Amazon S3进行交互。这些包括AWS软件开发工具包（SDKS）（包装库），用于IOS、Android、JavaScript、Java、.NET、Node.js、PHP、Python、Ruby、Go和C++，AWS命令行接口（CLI），以及AWS管理控制台

备注：
```
  Amazon S3最初除了REST API之外还支持SOAP（简单对象访问协议）API，但是您应该使用REST API, 遗留的https端点仍然可用，但不支持新功能.
```

### 持久性和高可用

* 数据持久性和可用性是相关的，但概念略有不同。持久性解决了一个问题："我的数据将来还会存在吗？", 可用性解决了这个问题，"我现在可以访问我的数据吗？",AmazonS3旨在为您的数据提供非常高的耐用性和可用性。

* AmazonS3标准存储是为99.999999999%的持久性和99.99%的对象可用性而设计的，例如，如果使用AmazonS3存储10000个对象，则平均每10000000年会损失一个对象。Amazon S3通过在一个区域内的多个设施中的多个设备上自动冗余地存储数据，从而实现了高耐久性。它旨在在不丢失用户数据的情况下，维持两个设施中数据的并发丢失。Amazon S3提供了一个专为关键任务和主要数据存储而设计的高耐久性存储基础设施。

* 如果您需要存储不需要如此高级别持久性的非关键或易于复制的派生数据（如图像缩略图），则可以选择以较低的成本使用减少冗余存储（RRS）。RRS提供99.99%的持久性，存储成本低于传统的Amazon S3存储

* 备注
```
  尽管Amazon S3存储在基础设施级别提供了非常高的持久性，但通过使用其他功能（如版本控制、跨区域复制和MFA删除）来防止用户级意外删除或覆盖数据仍然是一种最佳实践。

```

### 数据一致性
* Amazon S3是一个最终保持一致的系统。因为您的数据会自动复制到一个区域内的多个服务器和位置，所以数据中的更改可能需要一些时间才能传播到所有位置。因此，在某些情况下，您在更新后立即读取的信息可能会返回过时的数据。

* 对于新对象的PUTS，在这种情况下，这不是一个问题，Amazon S3提供了读写一致性。但是，对于现有对象（对象覆盖到现有密钥）和对象删除，Amazon S3提供了最终的一致性。

* 如果将新数据放入现有的密钥中，则后续的GET可能返回旧的数据。同样，如果删除一个对象，该对象的后续获取可能仍然读取被删除的对象。在所有情况下，对单个密钥的更新都是原子的，以便最终一致读取，将获得新数据或旧数据，但从来没有不一致的数据混合。

### 访问控制

* 默认情况下，Amazon S3是安全的；当您在Amazon S3中创建bucket或object时，只有您拥有访问权限。为了允许您对其他对象进行受控访问，Amazon S3提供了粗粒度访问控制（Amazon S3访问控制列表[ACL]）和细粒度访问控制（Amazon S3 bucket策略，AWS身份和访问管理[IAM]策略，以及查询字符串身份验证）。

* Amazon S3 ACL允许您授予某些粗粒度的权限：在对象或桶级上读、写或完全控制。ACL是在IAM存在之前创建的遗留访问控制机制。ACL现在被用于有限的用例集，例如，启用bucket日志记录或使承载静态网站的bucket具有world-readable。

Amazon S3 Bucket策略是Amazon S3推荐的访问控制机制，并提供更细粒度的控制。Amazon S3 Bucket策略与IAM策略非常相似，后者在第6章"AWS标识和访问管理（IAM）"中进行了讨论，但在以下方面有细微的不同：
```
  * 它们与bucket资源而不是IAM主体相关联。
  * 它们在策略中包含对IAM主体的显式引用。此主体可以与不同的AWS帐户关联，因此Amazon S3 Bucket策略允许您分配对Amazon S3资源的跨帐户访问。
```

* 使用Amazon S3 bucket策略，您可以指定谁可以访问bucket，从何处（通过无类域间路由[cidr]块或ip地址）访问bucket，以及在一天中的什么时间访问bucket。

* 最后，IAM策略可以直接与授予Amazon S3 bucket访问权限的IAM主体关联，就像它可以授予对任何AWS服务和资源的访问权限一样。显然，您只能将IAM策略分配给您控制的AWS帐户中的主体。

### 静态网站托管

* Amazon S3存储的一个非常常见的用例是静态网站托管。许多网站，特别是微型网站，不需要完整的Web服务器的服务。静态网站意味着网站的所有页面都只包含静态内容，不需要服务器端处理，如php、asp.net，或者jsp（注意，这并不意味着网站不能是交互式的和动态的；这可以通过客户端脚本来实现，比如嵌入在静态html网页中的javascript。）静态网站有很多优点：它们非常快，非常可伸缩，如果您在Amazon S3上托管一个静态网站，那么您还可以利用Amazon S3的安全性、持久性、可用性和可伸缩性。

* 因为每个Amazon S3对象都有一个URL，所以将bucket转换为网站相对简单，要托管静态网站，只需配置一个bucket进行网站托管，然后将静态网站的内容上传到bucket即可。

* 为静态网站托管配置Amazon S3存储桶:
```
 1.创建一个与所需网站主机名同名的bucket。
 2.上传静态文件到bucket；
 3.所有文件授权为public（可读）；
 4.为Bucket启用静态网站托管。这包括指定索引文档和错误文档；
 5.该网站现在可以在s3网站URL:<bucket-name>.s3-website-<aws-region>.amazonaws.com上找到；
 6.使用DNS CNAME或解析为Amazon S3网站URL的Amazon Route 53别名在您自己的域中为网站创建友好的DNS名称；
 7.现在在您的网站域名上将会找到该网站。

```

## Amazon S3 高级特性

* 除了基础知识外，还有一些Amazon S3的高级特性，您还应该熟悉这些特性。

### 前缀和分隔符

* AmazonS3在Bucket中使用平面结构，但在列出键名时支持使用前缀和分隔符参数。此功能允许您分层组织、浏览和检索Bucket中的对象。通常，您可以使用斜线（/）或反斜线（\）作为分隔符，然后使用带嵌入分隔符的键名称来模拟bucket的平面对象键命名空间中的文件和文件夹层次结构。

* 例如，您可能希望按服务器名称（如server42）存储一系列服务器日志，但按年份和月份组织，如下所示
```
 logs/2016/January/server42.log
 logs/2016/February/server42.log
 logs/2016/March/server42.log
```

* REST API、包装器SDK、Aws Cli和Amazon管理控制台都支持使用分隔符和前缀。这个特性使您可以逻辑地组织新的数据，并容易地维护现有文件上传或备份的现有文件的层次结构文件夹和文件结构。与iam或amazon s3 bucket策略一起使用，前缀和分隔符还允许您在单个bucket中创建等同于部门“子目录”或用户“主目录”，根据需要限制或共享对这些“子目录”（由前缀定义）的访问。

* 备注
```
 使用分隔符和对象前缀分层组织Amazon S3存储桶中的对象，但请始终记住Amazon S3并不是真正的文件系统。
```

### 存储类
* Amazon S3提供了一系列适合各种使用场景的存储类。

* Amazon S3 Standard 提供了高耐久性、高可用性、低延迟和高性能的通用对象存储。因为它提供低的第一字节延迟和高吞吐量，所以标准非常适合对频繁访问的数据进行短期或长期存储。对于大多数通用用例，amazon s3标准是开始的地方。

* Amazon S3 Standard– Infrequent  Access（Standard IA）提供了与Amazon S3标准相同的持久性、低延迟和高吞吐量，但专为寿命长、访问频率较低的数据而设计。标准IA的每GB月存储成本低于标准IA，但价格模型还包括最小对象大小（128KB）、最小持续时间（30天）和每GB检索成本，因此它最适合存储超过30天的不经常访问的数据。

* Amazon S3 Reduced Redundancy Storage（RRS）以较低的成本提供比标准或标准IA稍低的耐久性（4个9）。它最适合于可以轻松复制的派生数据，例如图像缩略图。

* 最后，Amazon Glacier存储类为不需要实时访问的数据（如存档和长期备份）提供安全、持久和极低成本的云存储。为了保持低成本，Amazon Glacier针对不常访问的数据进行了优化，其中检索时间为几个小时是合适的。要检索Amazon Glacier对象，可以使用Amazon S3 Api之一发出restore命令；3到5小时后，Amazon Glacier对象将复制到Amazon S3 RRS。请注意，恢复只是在Amazon S3 RRS中创建一个副本；在显式删除之前，原始数据对象将保留在amazonlacier中。还要注意，Amazon Glacier允许您每月免费检索存储在Amazon Glacier中的最多**5%**的Amazon S3数据；超出每日恢复限额的恢复将产生恢复费用。有关详细信息，请参阅AWS网站上的Amazon Glacier定价页面。

* 除了在Amazon S3中充当存储层之外，Amazon Glacier也是一个独立的存储服务，具有单独的API和一些独特的特性。然而，当您使用Amazon Glacier作为Amazon S3的存储类时，您总是通过Amazon S3 API与数据交互。有关更多详细信息，请参阅Amazon Glacier部分。

* 备注
```
 设置一个数据检索策略，以限制恢复到自由层或最大小时限制，以避免或尽量减少Amazon Glacier恢复费用。
```

### 对象生命周期管理

* Amazon S3对象生命周期管理大致相当于传统IT存储基础架构中的自动化存储分层。在许多情况下，数据有一个自然的生命周期，从“热”（经常访问）数据开始，随着时间的推移移动到“热”（不常访问）数据，在最终删除之前以“冷”（长期备份或存档）数据的形式结束其生命。

* 例如，许多业务文档在创建时被频繁访问，然后随着时间的推移变得不那么频繁。然而，在许多情况下，法规遵从性规则要求将业务文档存档并保持多年的可访问性。类似地，研究表明，文件、操作系统，而且数据库备份最常在创建后的头几天内访问，通常是在意外错误发生后进行恢复。一两周后，这些备份仍然是一项关键资产，但访问它们进行恢复的可能性要小得多。在许多情况下，合规性规则要求为几年。

* 使用Amazon S3生命周期配置规则，您可以通过自动将数据从一个存储类转换到另一个存储类，甚至在一段时间后自动删除数据，从而显著降低存储成本：
```
 备份数据最初存储在Amazon S3 Standard中。
 30天后，过渡到Amazon Standard-IA。
 90天后，过渡到Amazon Glacier。
 三年后，删除。
```

* 生命周期配置附加到bucket，可以应用于bucket中的所有对象，也可以仅应用于前缀指定的对象 

### Encryption（加密） 
* 强烈建议对Amazon S3中存储的所有敏感数据进行加密，无论是在飞行中还是在静止状态。为了加密飞行中的Amazon S3数据，您可以使用Amazon S3安全套接字层（SSL）API端点，这确保所有发送到Amazon S3和从Amazon S3发送的数据在传输过程中使用https协议加密。要在静止状态下加密Amazon S3数据，您可以使用服务器端加密（SSE）的几种变体。Amazon S3在将数据写入其数据中心的磁盘时在对象级别加密数据，并在您访问时为您解密。Amazon S3和AWS密钥管理服务（Amazon KMS）执行的所有SSE都使用256位高级加密标准（aes），您也可以使用客户端加密对静止的Amazon S3数据进行加密，在将数据发送到Amazon S3之前对客户端数据进行加密。. 

#### SSE-S3	(AWS-Managed Keys) 

* 这是一个完全集成的"复选框式"加密解决方案，AWS 负责Amazon S3的密钥管理和密钥保护，每个对象都用一个唯一的密钥加密。然后，实际的对象密钥本身由单独的主密钥进一步加密。至少每月发布一个新的主密钥，AWS 旋转密钥。加密的数据、加密密钥和主密钥都单独存储在安全主机上，进一步加强了保护。

#### SSE-KMS (AWS KMS Keys)

* 这是一个完全集成的解决方案，Amazon可以为Amazon S3处理密钥管理和保护，但您可以管理密钥。与SSE-S3相比，SSE-KMS提供了多个额外的好处。使用SSE-KMS，可以单独使用主密钥，它提供了对存储在Amazon S3和附加控制层中的对象的未经授权访问的保护。因此，您可以看到谁使用您的密钥访问了哪个对象，以及他们何时试图访问此对象。AWS KMS还允许您查看从无权解密数据的用户访问数据的任何失败尝试。

#### SSE-C (Customer-Provided Keys) 

* 当您想维护自己的加密密钥，但不想管理或实现自己的客户端加密库时，可以使用此选项。使用SSE-C，AWS将对您的对象进行加密/解密，而您可以在Amazon S3中完全控制用于加密/解密对象的密钥。

#### Client-Side Encryption

* 客户端加密是指在将应用程序发送到Amazon S3之前对其客户端上的数据进行加密。使用数据加密密钥有以下两个选项：
```
  * 使用AWS KMS管理的客户主密钥
  * 使用客户端主密钥
```

* 使用客户端加密时，保留对加密过程的端到端控制，包括对加密密钥的管理。

* 备注
```
  为了最大限度地简化和易于使用，使用服务器端加密与AWS托管密钥（SSE-S3或SSE-KMS）。
```
### 版本控制

* Amazon S3版本控制通过将每个对象的多个版本保存在bucket中（由唯一的版本ID标识），有助于防止意外或恶意删除数据。版本控制允许您保留、检索，并还原存储在Amazon S3存储桶中的每个对象的每个版本。如果用户意外更改或恶意删除了S3存储桶中的对象，除了bucket和object key之外，还可以通过引用版本id将对象还原到其原始状态。版本控制在bucket级别打开。一旦启用，版本控制就不能从bucket中删除，只能挂起。

### MFA Delete

* MFA Delete 在bucket版本控制的基础上添加另一层数据保护。MFA Delete需要额外的身份验证才能永久删除对象版本或更改bucket的版本控制状态。除了常规的安全凭据之外，MFA Delete还需要身份验证码（临时的，一次性密码）由硬件或Multi-Factor Authentication（MFA）设备生成。请注意，MFA删除只能由根帐户启用。

### Pre-Signed URLs

* 默认情况下，所有Amazon S3对象都是私有的，这意味着只有所有者有权访问。但是，对象所有者可以选择通过创建预签名的URL与其他人共享对象，使用他们自己的安全凭据授予下载对象的时间限制权限。为对象创建预签名的URL时，必须提供安全凭据并指定存储桶名称、对象密钥，http方法（get to download the object）和过期日期和时间。预签名的url仅在指定的持续时间内有效。这对于防止存储在Amazon S3中的媒体文件等web内容的"内容刮擦"特别有用。
 
### Multipart

* 为了更好地支持大型对象的上传或复制，Amazon S3提供了多部分上传API，这允许您将大型对象作为一组部件进行上传，这通常会提供更好的网络利用率（通过并行传输）、暂停和恢复的能力，以及在大小最初未知的情况下上传对象的能力。多部分上载是一个三步过程：启动、上载部件和完成（或中止）。部件可以按照任意顺序独立上传，如果需要，可以重新传输。上传完所有部分后，Amazon S3将这些部分组装起来以创建一个对象。

* 一般来说，对于大于100MB的对象，应该使用multipart upload；对于大于5GB的对象，必须使用multipart upload；当使用低级API时，必须将要上载的文件分成多个部分并跟踪这些部分；当使用AWS CLI（AWS S3 CP，aws s3 mv和aws s3 sync），对大型对象自动执行多部分上载。 

* 备注
``` 
  您可以在存储桶上设置对象生命周期策略，以便在指定的天数后中止不完整的多部分上载。这将最小化与未完成的多部分上载相关的存储成本。
```

### Range	GETs 
It	is	possible	to	download	(GET)	only	a	portion	of	an	object	in	both	Amazon	S3	and	Amazon Glacier	by	using	something	called	a	Range	GET.	Using	the	Range	HTTP	header	in	the	GET request	or	equivalent	parameters	in	one	of	the	SDK	wrapper	libraries,	you	specify	a	range	of bytes	of	the	object.	This	can	be	useful	in	dealing	with	large	objects	when	you	have	poor connectivity	or	to	download	only	a	known	portion	of	a	large	Amazon	Glacier	backup. Cross-Region	Replication Cross-region	replication	is	a	feature	of	Amazon	S3	that	allows	you	to	asynchronously replicate	all	new	objects	in	the	source	bucket	in	one	AWS	region	to	a	target	bucket	in	another region.	Any	metadata	and	ACLs	associated	with	the	object	are	also	part	of	the	replication. After	you	set	up	cross-region	replication	on	your	source	bucket,	any	changes	to	the	data, metadata,	or	ACLs	on	an	object	trigger	a	new	replication	to	the	destination	bucket.	To	enable cross-region	replication,	versioning	must	be	turned	on	for	both	source	and	destination buckets,	and	you	must	use	an	IAM	policy	to	give	Amazon	S3	permission	to	replicate	objects on	your	behalf. Cross-region	replication	is	commonly	used	to	reduce	the	latency	required	to	access	objects	in Amazon	S3	by	placing	objects	closer	to	a	set	of	users	or	to	meet	requirements	to	store	backup data	at	a	certain	distance	from	the	original	source	data.
	If	turned	on	in	an	existing	bucket,	cross-region	replication	will	only	replicate	new objects.	Existing	objects	will	not	be	replicated	and	must	be	copied	to	the	new	bucket	via	a separate	command.
Logging In	order	to	track	requests	to	your	Amazon	S3	bucket,	you	can	enable	Amazon	S3	server	access logs.	Logging	is	off	by	default,	but	it	can	easily	be	enabled.	When	you	enable	logging	for	a
bucket	(the	source	bucket),	you	must	choose	where	the	logs	will	be	stored	(the	target bucket).	You	can	store	access	logs	in	the	same	bucket	or	in	a	different	bucket.	Either	way,	it	is optional	(but	a	best	practice)	to	specify	a	prefix,	such	as	logs/	or	yourbucketname/logs/,	so that	you	can	more	easily	identify	your	logs. Once	enabled,	logs	are	delivered	on	a	best-effort	basis	with	a	slight	delay.	Logs	include information	such	as: Requestor	account	and	IP	address Bucket	name Request	time Action	(GET,	PUT,	LIST,	and	so	forth) Response	status	or	error	code Event	Notifications Amazon	S3	event	notifications	can	be	sent	in	response	to	actions	taken	on	objects	uploaded or	stored	in	Amazon	S3.	Event	notifications	enable	you	to	run	workflows,	send	alerts,	or perform	other	actions	in	response	to	changes	in	your	objects	stored	in	Amazon	S3.	You	can use	Amazon	S3	event	notifications	to	set	up	triggers	to	perform	actions,	such	as	transcoding media	files	when	they	are	uploaded,	processing	data	files	when	they	become	available,	and synchronizing	Amazon	S3	objects	with	other	data	stores. Amazon	S3	event	notifications	are	set	up	at	the	bucket	level,	and	you	can	configure	them through	the	Amazon	S3	console,	through	the	REST	API,	or	by	using	an	AWS	SDK.	Amazon	S3 can	publish	notifications	when	new	objects	are	created	(by	a	PUT,	POST,	COPY,	or	multipart upload	completion),	when	objects	are	removed	(by	a	DELETE),	or	when	Amazon	S3	detects that	an	RRS	object	was	lost.	You	can	also	set	up	event	notifications	based	on	object	name prefixes	and	suffixes.	Notification	messages	can	be	sent	through	either	Amazon	Simple Notification	Service	(Amazon	SNS)	or	Amazon	Simple	Queue	Service	(Amazon	SQS)	or delivered	directly	to	AWS	Lambda	to	invoke	AWS	Lambda	functions. Best	Practices,	Patterns,	and	Performance It	is	a	common	pattern	to	use	Amazon	S3	storage	in	hybrid	IT	environments	and	applications. For	example,	data	in	on-premises	file	systems,	databases,	and	compliance	archives	can	easily be	backed	up	over	the	Internet	to	Amazon	S3	or	Amazon	Glacier,	while	the	primary application	or	database	storage	remains	on-premises. Another	common	pattern	is	to	use	Amazon	S3	as	bulk	“blob”	storage	for	data,	while	keeping an	index	to	that	data	in	another	service,	such	as	Amazon	DynamoDB	or	Amazon	RDS.	This allows	quick	searches	and	complex	queries	on	key	names	without	listing	keys	continually. Amazon	S3	will	scale	automatically	to	support	very	high	request	rates,	automatically	repartitioning	your	buckets	as	needed.	If	you	need	request	rates	higher	than	100	requests	per second,	you	may	want	to	review	the	Amazon	S3	best	practices	guidelines	in	the	Developer Guide.	To	support	higher	request	rates,	it	is	best	to	ensure	some	level	of	random	distribution of	keys,	for	example	by	including	a	hash	as	a	prefix	to	key	names.
	If	you	are	using	Amazon	S3	in	a	GET-intensive	mode,	such	as	a	static	website hosting,	for	best	performance	you	should	consider	using	an	Amazon	CloudFront distribution	as	a	caching	layer	in	front	of	your	Amazon	S3	bucket.