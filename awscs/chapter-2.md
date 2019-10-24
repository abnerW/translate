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

* REST API、包装器SDK、Aws Cli和Amazon管理控制台都支持使用分隔符和前缀。这个特性使您可以逻辑地组织新的数据，并容易地维护现有文件上传或备份的现有文件的层次结构文件夹和文件结构。与iam或amazon s3 bucket策略一起使用，前缀和分隔符还允许您在单个bucket中创建等同于部门"子目录"或用户"主目录"，根据需要限制或共享对这些"子目录"（由前缀定义）的访问。

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

* Amazon S3对象生命周期管理大致相当于传统IT存储基础架构中的自动化存储分层。在许多情况下，数据有一个自然的生命周期，从"热"（经常访问）数据开始，随着时间的推移移动到"热"（不常访问）数据，在最终删除之前以"冷"（长期备份或存档）数据的形式结束其生命。

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

#### SSE-S3 (AWS-Managed Keys) 

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

### Range GETs 

* 通过使用range get，可以在Amazon S3和Amazon Glacier中只下载（get）对象的一部分。指定对象的字节范围。这对于处理连接不良的大型对象或仅下载大型Amazon Glacier备份的已知部分非常有用

### Cross-Region Replication

* 跨区域复制是Amazon S3的一个特性，它允许您将一个AWS区域中源bucket中的所有新对象异步复制到另一个区域中的目标bucket中。与该对象关联的任何元数据和ACL也是复制的一部分。在源存储桶上设置跨区域复制后，对对象上的数据、元数据或ACL所做的任何更改都会触发对目标存储桶的新复制。若要启用跨区域复制，必须同时启用源存储桶和目标存储桶的版本控制，而且您必须使用IAM策略来授予Amazon S3代表您复制对象的权限。

* 跨区域复制通常用于减少访问Amazon S3中的对象所需的延迟，方法是将对象放置在更靠近一组用户的位置，或者满足在与原始源数据一定距离处存储备份数据的要求。

* 备注
```
  如果在现有的桶中打开，跨区域复制将只复制新对象。现有对象将不被复制，必须通过单独的命令复制到新的桶。
```

### 日志

* 为了跟踪你对Amazon S3桶的访问请求，可以启用Amazon S3 服务访问日志。默认此服务是关闭的，但可以轻松打开。当您为一个bucket（源bucket）启用日志记录时，您必须选择日志的存储位置（目标bucket）。您可以将访问日志存储在同一个bucket或不同的bucket中。无论哪种方式，都可以指定前缀，如logs/或bucketname/logs/，以便更容易识别日志。

* 一旦启用，日志将在尽最大努力的基础上交付，并有轻微的延迟，日志包括如下信息：。
```
  * 请求者账号和IP地址
  * Bucket名字
  * 请求时间
  * 动作(GET, PUT, LIST, and so forth) 
  * 返回状态和错误码
```

### 事件通知

* Amazon S3事件通知可以响应对Amazon S3中上载或存储的对象执行的操作而发送。事件通知使您能够运行工作流、发送警报或执行其他操作以响应存储在Amazon S3中的对象中的更改。您可以使用Amazon S3事件通知设置触发器来执行操作，例如，在上传媒体文件时对其进行转码，在数据文件可用时对其进行处理，以及将amazon S3对象与其他数据存储同步。

* Amazon S3事件通知是在bucket级别设置的，您可以通过Amazon S3控制台、rest api或使用aws sdk配置它们。Amazon S3可以在创建新对象（通过put、post、copy或multipart upload完成）、删除对象（通过delete）时发布通知，或者当Amazon S3检测到RRS对象丢失时。您还可以基于对象名前缀和后缀设置事件通知。通知消息可以通过Amazon简单通知服务（Amazon SNS）或Amazon简单队列服务（Amazon SQS）发送，或者直接传递到AWS lambda以调用AWS lambda函数。


### 最佳实践、模式和性能

* 在混合It环境和应用程序中使用Amazon S3存储是一种常见的模式。例如，本地文件系统、数据库和法规遵从性存档中的数据可以通过Internet轻松备份到Amazon S3或Amazon Glacier，而主应用程序或数据库存储仍在本地。

* 另一个常见的模式是使用Amazon S3作为数据的大容量"blob"存储，同时在另一个服务（如amazon dynamodb或amazon rds）中保存该数据的索引，这允许快速搜索和复杂查询密钥名，而无需连续列出密钥。

* Amazon S3将自动缩放以支持非常高的请求率，并根据需要自动重新分配存储桶。如果您需要的请求率高于每秒100个请求，您可能需要查看《开发人员指南》中的Amazon S3最佳实践指南。若要支持更高的请求率，最好确保密钥的某种程度的随机分布，例如，将散列作为密钥名的前缀。

* 备注
```
  如果您正在使用GET密集模式的Amazon S3，比如静态网站托管，为了获得最佳性能，您应该考虑在Amazon S3存储桶前面使用Amazon Cloudfront发行版作为缓存层。
``` 

## Amazon Glacier

* Amazon Glacier 是一种极低成本的存储服务，为数据归档和在线备份提供持久、安全和灵活的存储。为了保持低成本，mazon Glacier被设计用于不频繁访问的数据，其中三至五小时的检索时间是可接受的。

* Amazon Glacier可以以任何格式存储无限量的几乎任何类型的数据。Amazon Glacier的常见用例包括替换传统的磁带解决方案，用于长期备份、存档和存储法规遵从性所需的数据。在大多数情况下，存储在Amazon Glacier中的数据由大型tar（磁带存档）或zip文件组成。

* 和AmazonS3一样，Amazon Glacier非常耐用，在一个地区的多个设备上存储数据。Amazon Glacier是为99.999999999%的物体在给定年份的耐久性而设计的。

#### 归档

* 在Amazon Glacier中，数据存储在归档文件中。一个归档文件最多可包含40TB的数据，并且您可以拥有无限数量的归档文件。每个归档文件在创建时都被分配了一个唯一的归档ID。（与Amazon S3对象密钥不同，您不能指定一个用户友好的归档文件名。）所有归档文件都会自动加密，并且存档在创建后是不可变的，不能修改。

#### Vaults

* 保管库是存档的容器。每个AWS帐户最多可以有1000个保管库。您可以使用IAM策略或保管库访问策略控制对保管库的访问和允许的操作。

#### Vaults Locks

* 您可以使用保管库锁定策略轻松地为单个Amazon Glacier保管库部署和强制执行符合性控制。您可以在保管库锁定策略中指定诸如"一次写入多次读取"（WORM）之类的控件，并将该策略从以后的编辑中锁定。锁定后，将无法再更改该策略。

#### Data Retrieval

* 你可以每月从Amazon Glacier 中获取多达5%的数据，每天按比例计算。如果你检索超过5%，你将根据你的最大检索率而得到检索费。可以在保管库上设置数据检索策略，以将检索限制在可用层或指定的数据区域。

#### Amazon Glacier 与 Amazon Simple Storage Service(Amazon S3)

* Amazon Glacier与Amazon S3类似，但在几个关键方面有所不同。
```
  * Amazon Glacier支持40TB的存档，而Amazon S3支持5TB的对象
  * 由系统生成的存档ID标识，而Amazon S3允许您使用"友好的"密钥名称
  * Amazon Glacier存档是自动加密的，而在Amazon S3中，静态加密是可选的
  * 但是，通过将Amazon Glacier与对象生命周期策略一起用作Amazon S3存储类，您可以使用Amazon S3接口来获得Amazon Glacier的大部分好处，而无需学习新的接口。
```

## 总结

* Amazon S3是AWS的核心对象存储服务。允许您以非常高的持久性存储无限量的数据

* 常见的Amazon S3使用场景包括：备份和归档、web内容、大数据分析、静态网站托管、移动和云本机应用程序托管以及灾难恢复。

* Amazon S3与许多其他AWS云服务集成，包括Aws Iam、Aws KMS、Amazon Ec2、Amazon EBS、Amazon EMR、Amazon Dynamodb、Amazon Redshift、Amazon SQS、Aws Lambda和Amazon Cloudfront。

* 对象存储不同于传统的块和文件存储。块存储将设备级的数据作为可寻址块管理，而文件存储将操作系统级的数据作为文件和文件夹管理。对象存储将数据作为包含数据和元数据的对象管理，由API操作。

* Amazon S3 Bucket是存储在Amazon S3中的对象的容器。bucket名称必须是全局唯一的。每个bucket都是在特定的区域中创建的，除非用户显式地复制，否则数据不会离开该区域。

* Amazon S3对象是存储在bucket中的文件。对象可以高达5tb，并且可以包含任何类型的数据。对象既包含数据又包含元数据，并由密钥标识。每个Amazon S3对象都可以由web服务端点、bucket名称和对象密钥形成的唯一url寻址。

* Amazon S3有一个极简的API create/delete a bucket、read/write/delete objects、列出bucket中的键，并使用基于标准http动词get、put、post和delete的rest接口。

* AmazonS3是一款高度耐用和高可用的产品，专为特定年份的11个9的耐久性和4个9的可用性而设计。

* Amazon S3最终是一致的，但是为新的对象puts提供了读写一致性。

* 默认情况下，Amazon S3对象是私有的，只能由所有者访问。对象可以标记为公共可读，以便在web上访问。可以使用acl、AWS IAM和Amazon S3 Bucket策略将受控访问提供给其他人。

* 静态网站可以托管在Amazon S3存储桶中。前缀和分隔符可用于键名中，以分层方式组织和导航数据，这与传统的文件系统非常相似。

* Amazon S3提供了几个适合不同用例的存储类：Standard是为需要高性能和低延迟的通用数据而设计的；Standard-IA是为访问频率较低的数据而设计的；RRS以较低的成本提供较低的冗余，以便于复制Amazon Glacier为存档和长期备份提供了低成本的持久存储，这些备份很少被访问，可以接受3到5个小时的检索时间。

* 对象生命周期管理策略可用于根据时间在存储类之间自动移动数据。

* Amazon S3数据可以使用服务器端或客户端加密进行加密，加密密钥可以使用Amazon KMS进行管理。

* 版本控制和MFA delete可用于防止意外删除。

* 跨区域复制可用于自动将新对象从一个区域的源存储桶复制到另一个区域的目标存储桶。

* 预签名的url授予下载对象的时间限制权限，可用于保护媒体和其他web内容免受未经授权的"web抓取"。

* 多部分上传可用于上传大型对象，Range Gets可用于下载Amazon S3对象或Amazon Glacier归档文件的一部分。

* 可以在bucket上启用服务器访问日志来跟踪请求者、对象、操作和响应。

* Amazon S3事件通知可用于发送Amazon SQS或Amazon SNS消息，或在创建或删除对象时触发Aws Lambda函数。

* Amazon Glacier可以用作Amazon S3中的独立服务或存储类。

* Amazon Glacier将数据存储在包含在保险库中的档案中。最多可以有1000个保险库，每个保险库可以存储无限数量的档案。

* Amazon Glacier vaults可以锁定，以达到合规目的。

## 考试要点

* 知道什么是Amazon S3以及常见使用场景
```
 Amazon S3是一种安全、持久且高度可扩展的云存储，可以使用简单的Web服务接口以几乎任何格式存储无限量的数据。常见的用例包括备份和存档、内容存储和分发、大数据分析、静态网站托管、云本机应用程序托管，以及灾难恢复。
```

* 理解对象存储和块存储、文件存储的不同
```
 Amazon S3云对象存储将应用程序级的数据作为对象进行管理，使用构建在HTTP上的Rest Api。块存储使用SCSI或光纤通道等协议将操作系统级的数据作为编号的可寻址块进行管理。文件存储将数据作为共享数据进行管理使用CIFS或NFS等协议的操作系统级文件。
```

* 了解Amazon S3的基本知识。
```
 Amazon S3将数据存储在包含数据和元数据的对象中。对象由用户定义的密钥标识，并存储在一个称为bucket的简单平面文件夹中。接口包括本机rest接口、多种语言的sdk、AWS cli和AWS管理控制台。

 了解如何创建bucket；如何上载、下载和删除对象；如何公开对象；以及如何打开对象url
```

* 了解amazon s3的持久性、可用性和数据一致性模型。
```
 Amazon S3标准存储是为11个9的持久性和一年内4个9的对象可用性而设计的。其他存储类不同。Amazon S3最终是一致的，但为放入新对象提供了读写一致性。
```

* 知道如何在Amazon S3上启动静态网站托管
```
 要在Amazon S3上创建静态网站，必须使用网站主机名创建一个bucket，上载静态内容并将其公开，在bucket上启用静态网站宿主，并指示索引和错误页面对象。
```

* 知道如何保护存在Amazon S3上的数据
```
 使用Https加密飞行中的数据，使用SSE或客户端加密对静止数据进行加密。启用版本控制以将对象的多个版本保存在存储桶中。启用MFA delete以防止意外删除。使用Acls Amazon S3存储桶策略和AWS IAM策略进行访问控制。使用预签名的URL有时间限制的下载访问。使用跨区域复制将数据自动复制到另一个区域.
```
* 知道每种Amazon S3 存储类的使用场景
```
 Standard 是针对需要高耐久性、高性能和低延迟访问的通用数据。Standard-IA是针对访问频率较低但在访问时需要相同性能和可用性的数据。RRS以较低的成本为易于复制的数据提供较低的耐久性。Amazon Glacier用于以最低的成本存储很少访问的存档数据，而三到五小时的检索时间是可以接受的。
```
* 知道如何使用生命周期配置规则。
```
 生命周期规则可以在AWS管理控制台或API中配置。生命周期配置规则定义了根据时间将对象从一个存储类转换到另一个存储类的操作。
```

* 知道如何使用Amazon S3事件通知
```
 事件通知设置在bucket级别，可以在Amazon SNS或Amazon SQS中触发消息，或者在AWS Lambda中触发动作以响应对象的上载或删除
```

* 知道Amazon Glacier作为独立服务的基础知识。
```
 数据存储在加密的存档中，其大小可达40TB。存档通常包含tar或zip文件。保险库是存档的容器，可以锁定保险库以实现法规遵从性。
```

## 练习

为了帮助完成以下练习，请参考以下文档

* Amazon S3 入门
```
http://docs.aws.amazon.com/AmazonS3/latest/gsg/GetStartedWithS3.html
```

* 建立一个静态网站
```
 http://docs.aws.amazon.com/AmazonS3/latest/dev/HostingWebsiteOnS3Setup.html
```

* 使用版本: 
```
 http://docs.aws.amazon.com/AmazonS3/latest/dev/Versioning.html
```

* 对象生命周期管理
```
 http://docs.aws.amazon.com/AmazonS3/latest/dev/object-lifecycle-mgmt.html
```

### 练习 2.1
* 在这个练习中：创建一个Amazon S3 bucket：在选定的region中创建一个Amazon S3 bucket，后面的练习会用到此bucket：
```
    1. 登陆AWS 管理控制台；
    2. 选择一个合适得region，例如：US West（Oregon）；
    3. 导航到Amazon S3控制台，注意：默认的region 指示符显示为：Global。记住Amazon S3 Bucket形成了一个全局命名空间，即使每个bucket都是在特定的区域中创建的；
    4. 启动创建bucket的进程；
    5. 当提示输入bucket名字时，输入：mynewbucket；
    6. 选择一个合适得region，例如：US West（Oregon）；
    7. 尝试创建bucket。您几乎肯定会收到一条消息，即请求的bucket名称不可用。请记住，bucket名称必须是全局唯一的；
    8. 再次尝试使用你的姓氏，然后使用连字符，然后将今天的日期作为桶名（一个不太可能存在的桶名）以六位数格式进行。

现在应该有一个新的amazon s3存储桶了

```


### 练习 2.2

* 上传、公开、重命名和删除bucket中的对象：在这个练习中，你会向bucket中上传一个对象，然后公开对象，并用浏览器访问对象，然后给对象重命名，最终从bucket中删除对象。

```
 * 上传对象
    1. 在Amazon S3 控制台加载2.1中创建得buckt；
    2. 点击：Upload，然后新增文件；
    3. 在本地PC上选择一个文件，此文件可以上传到Amazon S3 并且面向Internet公开（为练习得目的：建议使用非个人得镜像文件）；
    4. 选择一个合适得文件，然后开始上传，你可以在传输段看到文件上传进度；
    5. 文件上传结束，可以看到状态变为：Done；

* 你上传得对象应该已经成为Amazon S3得对象，并在bucket中能列表展示出来；

* 打开Amazon S3 URL
    6. 打开对象属性，应该包括：bucket，名字，link；
    7. 复制Amazon S3 中对象对应得URL；
    8. 粘贴到浏览器得地址栏；
* 应该看到一个xml格式包含：AccessDenied 错误的信息；对象已经有一个URL，但对象默认是private，因此不能通过web浏览器访问。

* 公开对象
    9. 回到Amazon S3 控制台，选择：Make Public（相当于，您可以更改对象的权限，并添加被授予者Everyone和打开/下载权限）
    10. 复制URL到浏览器，并尝试打开；现在你的镜像文件会展示在浏览器里。

* 对象重命名
    11. 在Amazon S3 控制台，选择：Rename；
    12. 给对象重命名，但不要修改文件扩展名；
    13. 复制新得Amazon S3 URL到浏览器，你应该也可以访问到同样得镜像文件。

* 删除对象
    14. 在Amazon S3 控制台，选择：Delete，当提示你是否想要删除对象时，选择：OK；
    15. 此时对象已经删除；
    16. 为了验证对象已经删除，用对象的Amazon S3 URL重新加载。

你应该看到一个xml格式包含：AccessDenied 错误的信息
```

### 练习 2.3
* 启用版本控制：在这个练习中，你将会在最新创建得bucket上启用版本控制。
```
* 启用版本
    1. 在Amazon S3 控制台，加载你的bucket得属性。不要打开bucket；
    2. 启用属性中得 versioning ，并选择OK进行验证。现在你得bucket已经启用了版本控制（
请注意，版本控制可以挂起，但不能关闭。）；创建一个对象得多个版本；
    3. 在你得电脑上创基爱你一个文件：foo.txt，并写入：blue；
    4. 保存文件到电脑得某个位置；
    5. 上传文件到你得bucket，这是版本：1；
    6. 上传文件到bucket之后，在你得电脑上打开文件副本，blue 为 red，保存文件，文件名仍然为：foo.txt；
    7. 上传修改后得文件到你得bucket；
    8. 在上传得对象上选择：Show Versions；现在你看到对喜爱那个得两个不通版本，并且有不通得IDs，可能大小也不一样；

* 注意，当您选择Show Version时，Amazon S3 URL现在在查询字符串中的对象名后面包含版本ID;

```

### 练习 2.4 
* 删除对象并恢复：在这个练习中，你将在你得Amazon S3 bucket中删除一个对象并恢复它。

```
* 删除一个对象
    1. 打开在2.3中上传得包含两个版本得文本文件得bucket；
    2. 选择：Hide Versions；
    3. 选择：Delete，然后选择：OK进行验证；
    4. 你得对象将会被删除，你也不能再看见这个对象；
    5. 选择：Show Versions；
对象的两个版本现在都显示其版本ID

* 恢复一个对象
    6. 打开你得bucket；
    7. 选择：Show Versions；
    8. 选择最旧得版本下载对象，注意：文件名只是foo.txt，没有版本指示器；
    9. 上传foo.txt到统一个bucket；
    10. 选择：Hide Versions，文件foo.txt应该重新出现了；

* 备注：
    若要还原版本，请将所需版本复制到同一个bucket中。在Amazon S3控制台中，这需要下载然后重新上载对象。使用API、SDK或AWS CLI，可以直接复制版本，而无需下载和重新加载。
```

### 练习 2.5
* 生命周期管理：在这个练习中，你将会探索生命周期管理得各种选项。
```
    1. 通过Amazon S3 控制台选择你的bucket；
    2. 在属性下，增加一个生命周期规则；
    3. 探索各种选项以将生命周期规则添加到此bucket中的对象。建议不要实现这些选项中的任何一个，因为可能会产生额外的成本。完成后，单击"取消"按钮。

备注：
    大多数生命周期规则在转换生效之前都需要一定的过期天数。例如，从Amazon S3 Standard 转换到Amazon S3 Standard-IA至少需要30天。这使得创建生命周期规则并在练习中查看实际结果变得不实际
```


### 练习 2.6
* 在你的bucket上启用静态托管：在这个练习中，你将会在你创建得bucket上启用静态托管。

```
    1. 在Amazon S3 控制台上选择你的bucket；
    2. 在属性段，选择：Enable Website Hosting；
    3. 输入index.txt作为索引文档名，输入error.txt作为错误文档名；
    4. 使用文本编辑器创建两个文本文件，并将它们保存为index.txt和error.txt。在index.txt文件中，写下短语"hello world"，在error.txt文件中，写下短语"error page"。上传两个文件到你的bucket；
    5. 公开这两个文件；
    6. 复制"静态网站宿主"下的"端点：链接"，并将其粘贴到浏览器窗口或选项卡中。现在应该可以看到显示的短语"hello world"；
    7. 在你浏览器得地址栏，尝试添加一个正斜杠，后跟一个虚构的文件名（例如，/test.html），现在应该可以看到显示的短语"error page"。
    8. 为了清理：删除bucket中的对象，同时删除你的bucket。

```

## 复习题
1. In what ways does Amazon Simple Storage Service (Amazon S3) object storage differ from block and file storage? (Choose 2 answers)
 A. Amazon S3 stores data in fixed size blocks.
 B. Objects are identified by a numbered address.
 C. Objects can be any size.
 D. Objects contain both data and metadata.
 E. Objects are stored in buckets. 

2. Which of the following are not appropriates use cases for Amazon Simple Storage Service (Amazon S3)? (Choose 2 answers)
 A. Storing web content
 B. Storing a file system mounted to an Amazon Elastic Compute Cloud (Amazon EC2) instance
 C. Storing backups for a relational database
 D. Primary storage for a database E. Storing logs for analytics 

3. What are some of the key characteristics of Amazon Simple Storage Service (Amazon S3)? (Choose 3 answers)
 A. All objects have a URL.
 B. Amazon S3 can store unlimited amounts of data.
 C. Objects are world-readable by default.
 D. Amazon S3 uses a REST (Representational State Transfer) Application Program Interface (API).
 E. You must pre-allocate the storage in a bucket. 

4. Which features can be used to restrict access to Amazon Simple Storage Service (Amazon S3) data? (Choose 3 answers)
 A. Enable static website hosting on the bucket.
 B. Create a pre-signed URL for an object.
 C. Use an Amazon S3 Access Control List (ACL) on a bucket or object.
 D. Use a lifecycle policy.
 E. Use an Amazon S3 bucket policy. 

5. Your application stores critical data in Amazon Simple Storage Service (Amazon S3), which must be protected against inadvertent or intentional deletion. How can this data be protected? (Choose 2 answers)
 A. Use cross-region replication to copy data to another bucket automatically.
 B. Set a vault lock.
 C. Enable versioning on the bucket.
 D. Use a lifecycle policy to migrate data to Amazon Glacier.
 E. Enable MFA Delete on the bucket. 

6. Your company stores documents in Amazon Simple Storage Service (Amazon S3), but it wants to minimize cost. Most documents are used actively for only about a month, then much less frequently. However, all data needs to be available within minutes when requested. How can you meet these requirements?
 A. Migrate the data to Amazon S3 Reduced Redundancy Storage (RRS) after 30 days.
 B. Migrate the data to Amazon Glacier after 30 days.
 C. Migrate the data to Amazon S3 Standard – Infrequent Access (IA) after 30 days.
 D. Turn on versioning, then migrate the older version to Amazon Glacier. 

7. How is data stored in Amazon Simple Storage Service (Amazon S3) for high durability? 
 A. Data is automatically replicated to other regions. 
 B. Data is automatically replicated within a region. 
 C. Data is replicated only if versioning is enabled on the bucket. 
 D. Data is automatically backed up on tape and restored if needed. 

8. Based on the following Amazon Simple Storage Service (Amazon S3) URL, which one of the following statements is correct? https://bucket1.abc.com.s3.amazonaws.com/folderx/myfile.doc
 A. The object “myfile.doc” is stored in the folder “folderx” in the bucket “bucket1.abc.com.”
 B. The object “myfile.doc” is stored in the bucket “bucket1.abc.com.”
 C. The object “folderx/myfile.doc” is stored in the bucket “bucket1.abc.com.”
 D. The object “myfile.doc” is stored in the bucket “bucket1.”

9. To have a record of who accessed your Amazon Simple Storage Service (Amazon S3) data and from where, you should do what?
 A. Enable versioning on the bucket.
 B. Enable website hosting on the bucket.
 C. Enable server access logs on the bucket.
 D. Create an AWS Identity and Access Management (IAM) bucket policy.
 E. Enable Amazon CloudWatch logs. 

10. What are some reasons to enable cross-region replication on an Amazon Simple Storage Service (Amazon S3) bucket? (Choose 2 answers)
 A. You want a backup of your data in case of accidental deletion.
 B. You have a set of users or customers who can access the second bucket with lower latency.
 C. For compliance reasons, you need to store data in a location at least 300 miles away from the first region.
 D. Your data needs at least five nines of durability. 

11. Your company requires that all data sent to external storage be encrypted before being sent. Which Amazon Simple Storage Service (Amazon S3) encryption solution will meet this requirement?
 A. Server-Side Encryption (SSE) with AWS-managed keys (SSE-S3)
 B. SSE with customer-provided keys (SSE-C)
 C. Client-side encryption with customer-managed keys
 D. Server-side encryption with AWS Key Management Service (AWS KMS) keys (SSEKMS) 

12. You have a popular web application that accesses data stored in an Amazon Simple Storage Service (Amazon S3) bucket. You expect the access to be very read-intensive, with expected request rates of up to 500 GETs per second from many clients. How can you increase the performance and scalability of Amazon S3 in this case? 
 A. Turn on cross-region replication to ensure that data is served from multiple locations.
 B. Ensure randomness in the namespace by including a hash prefix to key names.
 C. Turn on server access logging.
 D. Ensure that key names are sequential to enable pre-fetch.

13. What is needed before you can enable cross-region replication on an Amazon Simple Storage Service (Amazon S3) bucket? (Choose 2 answers) 
 A. Enable versioning on the bucket.
 B. Enable a lifecycle rule to migrate data to the second region.
 C. Enable static website hosting.
 D. Create an AWS Identity and Access Management (IAM) policy to allow Amazon S3 to replicate objects on your behalf. 

14. Your company has 100TB of financial records that need to be stored for seven years by law. Experience has shown that any record more than one-year old is unlikely to be accessed. Which of the following storage plans meets these needs in the most cost efficient manner?
 A. Store the data on Amazon Elastic Block Store (Amazon EBS) volumes attached to t2.micro instances.
 B. Store the data on Amazon Simple Storage Service (Amazon S3) with lifecycle policies that change the storage class to Amazon Glacier after one year and delete the object
after seven years.
 C. Store the data in Amazon DynamoDB and run daily script to delete data older than seven years.
 D. Store the data in Amazon Elastic MapReduce (Amazon EMR). 

15. Amazon Simple Storage Service (S3) bucket policies can restrict access to an Amazon S3 bucket and objects by which of the following? (Choose 3 answers)
 A. Company name
 B. IP address range
 C. AWS account
 D. Country of origin
 E. Objects with a specific prefix 

16. Amazon Simple Storage Service (Amazon S3) is an eventually consistent storage system. For what kinds of operations is it possible to get stale data as a result of eventual consistency? (Choose 2 answers)
 A. GET after PUT of a new object
 B. GET or LIST after a DELETE
 C. GET after overwrite PUT (PUT to an existing key)
 D. DELETE after PUT of new object 

17. What must be done to host a static website in an Amazon Simple Storage Service (Amazon S3) bucket? (Choose 3 answers)
 A. Configure the bucket for static hosting and specify an index and error document.
 B. Create a bucket with the same name as the website.
 C. Enable File Transfer Protocol (FTP) on the bucket.
 D. Make the objects in the bucket world-readable.
 E. Enable HTTP on the bucket. 

18. You have valuable media files hosted on AWS and want them to be served only to authenticated users of your web application. You are concerned that your content could be stolen and distributed for free. How can you protect your content?
 A. Use static web hosting.
 B. Generate pre-signed URLs for content in the web application.
 C. Use AWS Identity and Access Management (IAM) policies to restrict access.
 D. Use logging to track your content. 

19. Amazon Glacier is well-suited to data that is which of the following? (Choose 2 answers)
 A. Is infrequently or rarely accessed
 B. Must be immediately available when needed
 C. Is available after a three- to five-hour restore period
 D. Is frequently erased within 30 days 

20. Which statements about Amazon Glacier are true? (Choose 3 answers)
 A. Amazon Glacier stores data in objects that live in archives.
 B. Amazon Glacier archives are identified by user-specified key names.
 C. Amazon Glacier archives take three to five hours to restore.
 D. Amazon Glacier vaults can be locked.
 E. Amazon Glacier can be used as a standalone service and as an Amazon S3 storage class.

