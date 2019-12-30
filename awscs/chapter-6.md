# 第六章 AWS Identity and Access Management (IAM)
**《AWS认证解决方案架构师-联合考试》中的本章节目标包括不限于如下内容：**

## 第二点 实现/部署
### 使用Amazon EC2、Amazon S3、Elastic Beanstalk、CloudFormation、Amazon Virtual Private Cloud（VPC）和AWS Identity and Access Management（IAM）识别适当的技术和方法来编码和实现云解决方案

**可能包含如下内容**
```
 * 配置IAM策略及最佳实践
```

## 第三点 数据安全
### 认识并实施安全实践以实现最佳的云部署和维护
**可能包含如下内容**
```
 * AWS Identity and Access Management（IAM）
```

## 简介
* 在本章中，您将了解AWS身份和访问管理（IAM）如何确保与您帐户中的AWS资源的交互，包括：
```
 * 哪些主体通过AWS管理控制台、命令行界面（CLI）和软件开发工具包（sdk）与AWS交互
 * 如何认证每个主体
 * 如何编写IAM策略以指定主体的访问权限
 * IAM策略如何与主体关联
 * 如何通过多因素身份验证（MFA）和密钥轮换进一步保护您的基础架构
 * 如何使用IAM角色来委派权限和联合用户
 * 如何解决多个可能存在冲突的IAM权限
```

* IAM是一个强大的服务，它允许您控制人们和程序如何被允许操作AWS基础设施。IAM使用传统的身份概念（如用户、组和访问控制策略）来控制谁可以使用您的AWS帐户、他们可以使用哪些服务和资源以及如何使用它们。IAM提供的控件足够精细，可以限制单个用户在特定时间窗口内对来自特定IP地址的特定资源执行单个操作的能力。应用程序可以被授予访问AWS资源的权限，无论它们是在本地运行还是在云中运行。这种灵活性创建了一个非常强大的系统，它将提供您所需的所有功率，以确保您的AWS帐户用户有能力满足您的业务需求，同时解决组织的所有安全问题。

* 本章将介绍可以与AWS交互的不同主体以及如何对它们进行身份验证。然后将讨论如何编写策略来定义对服务、操作和资源的允许访问，并将这些策略与经过身份验证的主体相关联。最后，它将介绍IAM的其他特性，这些特性将帮助您保护基础结构，包括MFA、旋转键、联合、解析多个权限和使用IAM角色。

* 了解IAM的确切含义与了解IAM的确切含义同样重要：

* 首先，IAM不是应用程序的标识存储/授权系统。您分配的权限是操作AWS基础结构的权限，而不是应用程序中的权限。如果您正在迁移已经拥有自己的用户存储库和身份验证/授权机制的现有Office应用程序，那么当您部署在AWS上时，应该继续工作，这可能是正确的选择。如果应用程序标识基于Active Directory，则可以将本地activedirectory扩展到云中，以继续满足该需要。在云中使用Active Directory的一个很好的解决方案是AWS目录服务，它是一个与activedirectory兼容的目录服务，可以独立工作或与本地activedirectory集成。最后，如果您使用的是移动应用程序，请考虑使用Amazon Cognito对移动应用程序进行身份管理。

* 其次，IAM不是操作系统身份管理。请记住，在共享责任模型下，您可以控制操作系统控制台和配置。无论您当前使用何种机制来控制对服务器基础设施的访问，都将继续在Amazon Elastic Compute Cloud（Amazon EC2）实例上工作，无论该实例是管理单个计算机登录帐户，还是管理目录服务（如活动目录或轻型目录访问协议（LDAP））。您可以在Amazon EC2上运行Active Directory或LDAP服务器，也可以将本地系统扩展到云中。AWS目录服务也将很好地提供云服务中的活动目录功能，无论是独立的还是与您现有的活动目录集成。

* 表6.1 总结了不同身份验证系统在您的awsen环境中可以发挥的作用。

|---|---|
|使用场景|技术方案|
|操作系统权限访问|AD-LDAP Machine-specific accounts|
|应用权限访问|AD，应用用户 Repositories，Amazon Cognito|
|AWS 资源| IAM|

* IAM与大多数其他AWS云服务一样受控制：

* 与其他服务一样，通过AWS管理控制台，AWS管理控制台是开始学习和操作服务的最简单方式。
* 使用CLI学习系统时，可以使用CLI开始编写重复任务的脚本。
* 通过AWS sdk，您最终可以通过几个sdk中的一个直接通过REST API操纵IAM，开始编写自己的工具和复杂的流程。

* 所有这些方法都可以像控制其他服务一样控制IAM。此外，AWS合作伙伴网络（APN）还包括管理和扩展IAM的丰富的工具生态系统

## Principals
* 首先要理解的IAM概念是主体。主体是允许与AWS资源交互的IAM实体。主体可以是永久的，也可以是临时的，它可以表示人或应用程序。主体有三种类型：根用户、IAM用户和角色/临时安全令牌。

### root 用户
* 当您第一次创建AWS帐户时，您只能从一个单一登录主体开始，该主体可以完全访问该帐户中的所有AWS云服务和资源。此主体称为根用户。只要您在AWS有一个开放帐户，该关系的根用户就将持续存在。根用户可以用于控制台和程序访问AWS资源。

* 根用户在概念上类似于UNIX根或Windows管理员帐户，它拥有在该帐户中执行任何操作的完全权限，包括关闭该帐户。强烈建议您不要将根用户用于日常任务，甚至是管理任务。相反，请遵循以下最佳实践：仅使用根用户创建第一个IAM用户，然后安全地锁定根用户凭据

### IAM 用户
* 用户是通过IAM服务设置的持久标识，用于表示个人或应用程序。您可以为操作团队的每个成员创建单独的IAM用户，以便他们可以与控制台交互并使用CLI。您还可以为需要访问AWS云服务的应用程序创建开发、测试和生产用户（尽管您将在本章后面看到IAM角色可能是该用例的更好解决方案）。

* IAM用户可以由具有IAM管理权限的主体随时通过AWS管理控制台、CLI或sdk创建。用户是持久的，因为没有到期期限；它们是永久性实体，直到IAM管理员采取行动删除它们为止。

* 备注
```
 用户是执行最小特权主体的一个极好的方法；也就是说，允许与AWS资源交互的人员或流程准确地执行他们所需的任务，而不执行其他任务。用户可以与定义这些权限的非常精细的策略相关联。策略将在后面的章节中介绍
```

### 角色/临时安全令牌
* 角色和临时安全令牌对于高级IAM的使用非常重要，但是许多AWS用户发现它们令人困惑。角色用于在一段时间内将特定权限授予特定的参与者。这些参与者可以通过AWS或一些可信的外部系统进行身份验证。当其中一个参与者承担角色时，AWS从AWS安全令牌服务（STS）向参与者提供一个临时安全令牌，参与者可以使用它来访问AWS云服务。请求临时安全令牌需要指定令牌将在到期之前存在多长时间。临时安全令牌生存期的范围是15分钟到36小时。

* 角色和临时安全令牌支持许多用例：
```
 * Amazon EC2角色-向运行在amazonec2实例上的应用程序授予权限。
 * 跨帐户访问-将权限授予来自其他AWS帐户的用户，无论您是否控制这些帐户。
 * Federation-向通过受信任的外部系统认证的用户授予权限
```

### Amazon EC2 角色
* 授予应用程序权限总是很棘手的，因为它通常需要在安装时使用某种凭据配置应用程序。这会导致在使用前安全存储凭据、如何在安装期间安全访问凭据以及如何在配置中保护凭据等问题。假设运行在Amazon EC2实例上的应用程序需要访问amazonsimplestorageservice（Amazon S3）bucket。可以创建一个授予读写该bucket权限的策略，并将其分配给IAM用户，应用程序可以使用该IAM用户的访问密钥来访问Amazon S3 bucket。这种方法的问题是，用户的访问密钥必须能够被应用程序访问，可能需要将其存储在某种配置文件中。获取访问密钥并将其加密存储在配置中的过程通常很复杂，这是敏捷开发的障碍。此外，访问密钥在被传递时存在风险。最后，当轮换访问键的时候，轮换涉及到再次执行整个过程。

* 备注
```
 使用Amazon EC2的IAM角色，无需在配置文件中存储AWS凭据
```

* 另一种方法是创建一个IAM角色，该角色授予对Amazon S3存储桶的所需访问权限。启动Amazon EC2实例时，会将角色分配给该实例。当在实例上运行的应用程序使用应用程序编程接口（API）访问Amazon S3 bucket时，它将承担分配给实例的角色，并获取发送给API的临时令牌。获取临时令牌并将其传递给API的过程由大多数AWS sdk自动处理，允许应用程序调用Amazon S3 bucket而无需担心身份验证。除了对开发人员来说很容易，这还消除了在配置文件中存储访问密钥的任何需要。另外，由于API访问使用一个临时令牌，因此没有必须旋转的固定访问密钥。

### 跨账号访问
* IAM角色的另一个常见用例是将AWS资源的访问权授予其他AWS帐户中的IAM用户。这些账户可能是由贵公司或客户或供应商等外部代理控制的其他AWS账户。您可以使用要授予其他帐户中的用户的权限设置IAM角色，然后其他帐户中的用户可以使用该角色来访问您的资源。强烈建议将此作为最佳实践，而不是在组织外部分发访问密钥。

### 联邦
* 许多组织已经在AWS之外拥有了一个身份存储库，他们宁愿利用这个存储库，也不愿创建一个新的、大量重复的IAM用户存储库。类似地，基于web的应用程序可能希望利用基于web的身份，如Facebook、Google或登录Amazon。IAM身份提供程序提供了将这些外部身份与IAM联合起来并将权限分配给在IAM外部进行身份验证的用户的能力。IAM可以与两种不同类型的外部身份提供者（IdP）集成。为了联合Facebook、Google或登录Amazon等web身份，IAM支持通过OpenID Connect（OIDC）进行集成。这允许IAM向通过某些主要基于web的idp验证的用户授予特权。对于联合内部标识（如Active Directory或LDAP），IAM支持通过安全断言标记语言2.0（SAML）进行集成。与SAML兼容的IdP（如Active Directory Federation Services（ADFS））用于将内部目录联合到IAM。（配置许多兼容产品的说明可以在AWS网站上找到。）在每种情况下，联合都是通过将与角色相关联的临时令牌返回到IdP以获得用于调用AWS API的身份验证标识。返回的实际角色是通过从IdP接收的信息来确定的，这些信息可以是本地标识存储中用户的属性，也可以是web标识存储的用户名和身份验证服务。表6.2列出了这三类主体及其一般特征。

* 表6.2 AWS主体特征
|---|---|
|主体|特征|
|根用户|不受限制，永久|
|IAM用户|通过策略控制权限访问，Durable，可以通过IAM管理员移除|
|角色/临时安全令牌|策略控制的访问在特定时间间隔后临时过期|


## Authentication
IAM对主体进行身份验证有三种方法：

* 用户名/密码-当主体表示与控制台交互的人员时，该人员将提供用户名/密码对以验证其身份。IAM允许您创建密码策略，强制执行密码复杂度和过期时间。

* 访问密钥-访问密钥是访问密钥ID（20个字符）和访问密钥（40个字符）的组合。当程序通过API操作AWS基础设施时，它将使用这些值来对服务的底层REST调用进行签名。AWS SDK和工具处理所有复杂的REST调用签名，因此使用访问密钥几乎总是向SDK或工具提供值的问题。

* 访问密钥/会话令牌-当进程在假定角色下运行时，临时安全令牌提供用于身份验证的访问密钥。除了访问密钥（记住它由两部分组成），令牌还包括会话令牌。对AWS的调用必须同时包含两部分的访问密钥和会话令牌才能进行身份验证。

需要注意的是，创建IAM用户时，它既没有访问密钥也没有密码，IAM管理员可以设置其中一个，也可以同时设置这两个。这增加了一个额外的安全层，因为控制台用户不能使用他们的凭据运行访问您的AWS基础设施的程序。

* 图6.1显示了不同身份验证方法的汇总。

## Authorization
* IAM对主体进行身份验证后，必须管理该主体的访问，以保护您的AWS基础结构。确切指定主体可以执行和不能执行的操作的过程称为授权。在IAM中，通过定义策略中的特定权限并将这些策略与主体关联来处理授权。

### 策略
了解访问管理在IAM下是如何工作的，首先要了解策略。策略是一个JSON文档，它完全定义了一组访问和操作AWS资源的权限。策略文档包含一个或多个权限，每个权限定义为：

* Effect-单个单词：Allow或Deny。
* 服务-此权限适用于哪些服务？大多数AWS云服务支持通过IAM授予访问权限，包括IAM本身。
* 资源-Resource资源值指定应用此权限的特定AWS基础结构。它被指定为Amazon资源名（ARN）。ARN的格式在服务之间略有不同，但基本格式是：“ARN:aws:service:region:account id:[resourcetype:]resource”

* 对于某些服务，允许使用通配符值；例如，Amazon S3 ARN可以使用foldername\*资源来指示指定文件夹中的所有对象。表6.3显示了一些示例ARNs

* 表 6.3 样例 ARNs
|---|---|
|资源|ARN格式|
|Amazon S3 桶|arn:aws:s3:us-east-1:123456789012:my_corporate_bucket/*|
|IAM 用户|arn:aws:iam:us-east-1:123456789012:user/David|
|Amazon DynamoDB 表|arn:aws:dynamodb:us-east-1:123456789012:table/tablename|

* Action-操作值指定权限允许或拒绝的服务内操作的子集。例如，权限可以授予Amazon S3访问任何基于read的操作的权限。可以使用枚举列表或通配符（Read*）指定一组操作。

* Condition-条件值可选择地定义一个或多个限制权限允许的操作的附加限制。例如，权限可能包含一个条件，该条件将访问资源的能力限制为来自特定IP地址范围的调用。另一个条件可能会将权限限制为仅在特定时间间隔内应用。有许多类型的权限允许各种各样的功能，这些功能因服务而异。有关每个服务支持的条件的列表，请参阅IAM文档。

* 下表显示了一个示例策略。此策略允许主体在特定的存储桶中列出对象并检索这些对象，但前提是调用来自特定的IP地址
```
{
  "Version": "2012–10–17",
  "Statement": [
    {
      "Sid": "Stmt1441716043000",
      "Effect": "Allow", <- This policy grants access
      "Action": [ <- Allows identities to list
      "s3:GetObject", <- and get objects in
      "s3:ListBucket" <- the S3 bucket
    ],
    "Condition": {
      "IpAddress": { <- Only from a specific
        "aws:SourceIp": "192.168.0.1" <- IP Address
      }
    },
    "Resource": [
      "arn:aws:s3:::my_public_bucket/*" <- Only this bucket
    ]
   }
 ]
}
```

### 将策略与主体关联
有许多方法可以将IAM用户和策略关联，本节值介绍最常用的。

通过如下方法中的一个，可以将一个策略直接和IAM用户关联：
* 用户策略-这些策略只存在于它们所依附的用户的上下文中。在控制台中，用户策略被输入到IAM用户页上的用户界面中
* 托管策略-这些策略是在IAM页面上的策略选项卡（或通过CLI等）创建的，并且独立于任何单个用户而存在。这样，同一策略可以与许多用户或用户组相关联。您可以在AWS管理控制台的IAM页面的policies选项卡上查看大量预定义的托管策略。此外，您可以针对您的用例编写自己的策略。

* 备注
```
 使用预定义的托管策略可确保在为新功能添加新权限时，您的用户仍具有正确的访问权限
```

* 将策略与用户关联的另一种常见方法是使用IAM组功能。组简化了对大量用户的权限管理。将策略分配给组后，作为该组成员的任何用户都将拥有这些权限。这使得将策略分配给组织中的整个团队更加简单。例如，如果您为分配给该组的操作组创建了一个“操作”组，则将所需权限与该组相关联是一件简单的事情，并且该组的所有IAM用户都将拥有这些权限。然后可以将新的IAM用户直接分配给组。

这是一个比审查操作团队的新IAM用户应该接收哪些策略并手动将这些策略添加到用户中要简单得多的管理过程。策略可以通过两种方式与IAM组关联：
* 组策略-这些策略只存在于它们所连接的组的上下文中。在AWS管理控制台中，在IAM group页面的用户界面中输入组策略。
* 托管策略-与托管策略（在“授权”部分中讨论）可以与IAM用户关联的方式相同，它们也可以与IAM组关联。

图6.2显示了策略与IAM用户关联的不同方式。

* 备注
```
  一个好的第一步是使用根用户创建名为“IAM Administrators”的新IAM组
  并分配受管策略“IAMFullAccess”。
  然后创建名为“Administrator”的新IAM用户，分配密码，
  并将其添加到IAM Administrators组。
  此时，您可以作为根用户注销，并使用IAM用户帐户执行所有进一步的管理
```

* 参与者与策略关联的最后一种方式是假设角色。在这种情况下，参与者可以是：
```
 * 经过身份验证的IAM用户（个人或进程）。
 在这种情况下，IAM用户必须具有承担该角色的权限。
 
 * 由AWS以外的可信服务（如本地LDAP目录或web身份验证服务）进行身份验证的人或进程。
 在这种情况下，AWS云服务将代表参与者承担角色，并向参与者返回一个令牌。
``` 
 
* 在参与者承担角色后，将为其提供与该角色的策略关联的临时安全令牌。令牌包含验证API调用所需的所有信息。此信息包括一个标准访问密钥和一个附加的会话令牌，用于对假定角色下的调用进行身份验证。

## 其他的关键特性
* 除了主体、身份验证和授权等关键概念之外，IAM服务还有一些其他特性，这些特性对于了解IAM的全部好处非常重要

### Multi-Factor Authentication(MFA)
* 多因素身份验证（MFA）可以通过添加第二种身份验证方法（不只是密码或访问密钥）向基础结构添加额外的安全层。对于MFA，身份验证还需要从小型设备输入一次性密码（OTP）。MFA设备可以是随身携带的小型硬件设备，也可以是通过智能手机上的应用程序（例如，AWS虚拟MFA应用程序）实现的虚拟设备。

* 备注
```
MFA要求你用你知道的和你拥有的东西来验证你的身份。
```
* 可以将MFA分配给任何IAM用户帐户，无论该帐户代表个人还是应用程序。当使用配置有MFA的IAM用户的人试图访问AWS管理控制台时，在提供密码后，系统将提示他们在被授予访问权限之前输入显示在MFA设备上的当前代码。使用配置了MFA的IAM用户的应用程序必须查询应用程序用户以提供当前代码，然后应用程序将这些代码传递给API。

* 强烈建议AWS客户向其根用户添加MFA保护。

### Rotating Keys
* 任何凭证的安全风险都会随着凭证的使用年限而增加。为此，旋转与IAM用户关联的访问密钥是安全性最佳实践。IAM通过一次允许两个活动的访问密钥来简化此过程。可以通过控制台、CLI或SDKs执行密钥旋转过程:
```
 1. 为用户创建新的访问密钥。
 2. 重新配置所有应用程序以使用新的访问密钥。
 3. 禁用原始访问密钥（在此阶段禁用而不是删除非常关键，因为如果旋转有问题，它允许回滚到原始密钥）。
 4. 验证所有应用程序的操作。
 5. 删除原始访问密钥。
```
* 备注
```
 应定期旋转访问键
```
### 解析多个权限
* 有时，在确定主体是否具有执行某些操作的权限时，会应用多个权限。这些权限可能来自与主体相关联的多个策略或附加到相关AWS资源的资源策略。了解如何解决这些权限之间的冲突很重要：
```
 1. 最初，默认情况下请求被拒绝。
 2. 对所有适当的策略进行评估；如果在任何策略中发现显式的“拒绝”，则拒绝请求并停止评估。
 3. 如果未找到显式“拒绝”，并且在任何策略中都找到显式“允许”，则允许该请求。
 4. 如果找不到明确的“允许”或“拒绝”权限，则保持默认的“拒绝”并拒绝请求。
```

* 此规则的唯一例外是，如果AssumeRole调用包含角色和策略，则该策略无法扩展角色的权限（例如，该策略无法覆盖默认情况下在角色中被拒绝的任何权限）。

## 总结
* IAM是一个强大的服务，它使您能够控制哪些人和应用程序可以在非常精细的级别访问您的AWS帐户。因为不能限制AWS帐户中的根用户，所以您应该为您的人员和进程设置IAM用户和临时安全令牌，以便与AWS交互。
* 策略定义可以和不能采取的操作。策略直接或通过组成员身份与IAM用户关联。临时安全令牌通过承担IAM角色与策略关联。您可以编写自己的策略或使用AWS提供的一个托管策略。
* IAM角色的常见用例包括从外部idp联合身份、将权限分配给Amazon EC2实例（在该实例上运行的应用程序可以在该实例上承担这些权限），以及跨帐户访问。
* 可以通过旋转密钥、实现MFA和向策略添加条件来进一步保护IAM用户帐户。MFA确保身份验证是基于您所知道的内容之外的其他内容，并且条件可以添加进一步的限制，例如限制客户端IP地址范围或设置特定的时间间隔。

## 考试基础
* 了解IAM的不同原则。可以验证AWS资源并与之交互的三个主体是根用户、IAM用户和角色。根用户与实际的AWS帐户关联，不能以任何方式进行限制。IAM用户是可以通过IAM控制的持久标识。角色允许人们或流程使用不同的身份进行临时操作。人员或进程通过被授予将在指定时间段后过期的临时安全令牌来承担角色。

* 了解如何在IAM中验证主体。以IAM用户或根用户身份登录到AWS管理控制台时，将使用用户名/密码组合。使用IAM用户或根用户访问API的程序使用由两部分组成的访问密钥。临时安全令牌使用访问密钥和该临时安全令牌唯一的附加会话令牌进行身份验证。

* 了解政策的各个部分。策略是一个JSON文档，它定义了一个或多个与AWS资源交互的权限。每个权限包括效果、服务、操作和资源。它还可以包括一个或多个条件。AWS将许多预定义的策略作为托管策略提供。

* 了解策略如何与主体关联。经过身份验证的主体与零对多策略关联。对于IAM用户，这些策略可以直接附加到用户帐户，也可以附加到用户帐户是其成员的IAM组。临时安全令牌通过承担IAM角色与策略关联。

* 了解MFA。MFA通过从一个小设备（你有的东西）使用一个旋转的OTP来增加密码（你知道的东西）来增加AWS帐户的安全性，确保任何验证帐户的人都知道密码和拥有该设备。AWS支持Gemalto硬件MFA设备和许多虚拟MFA应用程序。

* 了解关键点旋转。为了保护您的AWS基础设施，访问密钥应该定期轮换。AWS允许两个访问密钥同时有效，以使旋转过程简单明了：生成新的访问密钥，将应用程序配置为使用新的访问密钥，测试，禁用原始访问密钥，测试，删除原始访问密钥，然后再次测试。

* 了解IAM角色和联盟。IAM角色是预先打包的权限集，没有凭据。主体可以承担一个角色，然后使用关联的权限。创建临时安全令牌时，它将承担定义分配给该令牌的权限的角色。当Amazon EC2实例与IAM角色关联时，SDK调用根据与实例关联的角色获取临时安全令牌，并使用该令牌访问AWS资源。角色是将外部idp与AWS联合的基础。将IAM IdP配置为与外部IdP交互，来自IdP的经过身份验证的标识将映射到角色，并返回已假定该角色的临时安全令牌。AWS同时支持SAML和OIDC idp。

* 知道如何解决权限冲突。解析多个权限相对简单。如果策略未明确允许对资源执行操作，则拒绝该操作。如果两个策略相互矛盾，也就是说，如果一个策略允许对资源执行操作，而另一个策略拒绝该操作，则该操作被拒绝。虽然这听起来不太可能，但可能是由于策略中的范围差异造成的。一个策略可以公开整个Amazon EC2实例，另一个策略可以显式地锁定一个特定实例。

## 练习
为辅助完成下面的练习，参考IAM用户指导手册：http://docs.aws.amazon.com/IAM/latest/UserGuide/

### 练习 6.1
#### Create an IAM Group
* In this exercise, you will create a group for all IAM administrator users and assign the
proper permissions to the new group. This will allow you to avoid assigning policies
directly to a user later in these exercises.
1. Log in as the root user.
2. Create an IAM group called Administrators.
3. Attach the managed policy, IAMFullAccess, to the Administrators group.

### 练习 6.2
#### Create a Customized Sign-In Link and Password Policy
* In this exercise, you will set up your account with some basic IAM safeguards. The
password policy is a recommended security practice, and the sign-in link makes it easier
for your users to log in to the AWS Management Console.
1. Customize a sign-in link, and write down the new link name in full.
2. Create a password policy for your account.

### 练习 6.3
#### Create an IAM User
* In this exercise, you will create an IAM user who can perform all administrative IAM
functions. Then you will log in as that user so that you no longer need to use the root
user login. Using the root user login only when explicitly required is a recommended
security practice (along with adding MFA to your root user).
1. While logged in as the root user, create a new IAM user called Administrator.
2. Add your new user to the Administrators group.
3. On the Details page for the administrator user, create a password.
4. Log out as the root user.
5. Use the customized sign-in link to sign in as Administrator.

### 练习 6.4
#### Create and Use an IAM Role
* In this exercise, you will create an IAM role, associate it with a new instance, and verify
that applications running on the instance assume the permissions of the role. IAM roles
allow you to avoid storing access keys on your Amazon EC2 instances.
1. While signed in as administrator, create an Amazon EC2-type role named S3Client.
2. Attach the managed policy, AmazonS3ReadOnlyAccess, to S3Client.
3. Launch an Amazon Linux EC2 instance with the new role attached (Amazon Linux
AMIs come with CLI installed).
4. SSH into the new instance, and use the CLI to list the contents of an Amazon S3
bucket.

### 练习 6.5
#### Rotate Keys
* In this exercise, you will go through the process of rotating access keys, a recommended
security practice.
1. Select the administrator, and create a two-part access key.
2. Download the access key.
3. Download and install the CLI to your desktop.
4. Configure the CLI to use the access key with the AWS Configure command.
5. Use the CLI to list the contents of an Amazon S3 bucket.
6. Return to the console, and create a new access key for the administrator account.
7. Download the access key, and reconfigure the CLI to use the new access key.
8. In the console, make the original access key inactive.
9. Confirm that you are using the new access key by once again listing the contents of
the Amazon S3 bucket.
10. Delete the original access key.

### 练习 6.6
#### Set Up MFA
* In this exercise, you will add MFA to your IAM administrator. You will use a virtual MFA
application for your phone. MFA is a security recommendation on powerful accounts
such as IAM administrators.
1. Download the AWS Virtual MFA app to your phone.
2. Select the administrator user, and manage the MFA device.
3. Go through the steps to activate a Virtual MFA device.
4. Log off as administrator.
5. Log in as administrator, and enter the MFA value to complete the authentication
process.

### 练习 6.7
Resolve Conflicting Permissions
In this exercise, you will add a policy to your IAM administrator user with a conflicting
permission. You will then attempt actions that verify how IAM resolves conflicting
permissions.
1. Use the policy generator to create a new policy.
2. Create the policy with Effect: Deny; AWS Service: Amazon S3; Actions: *; and ARN:
*.
3. Attach the new policy to the Administrators group.
4. Use the CLI to attempt to list the contents of an Amazon S3 bucket. The policy that
allows access and the policy that denies access should resolve to deny access.

## 复习题

### 1. Which of the following methods will allow an application using an AWS SDK to be authenticated as a principal to access AWS Cloud services? (Choose 2 answers)
 * A. Create an IAM user and store the user name and password for the user in the application’s configuration.
 * B. Create an IAM user and store both parts of the access key for the user in the application’s configuration.
 * C. Run the application on an Amazon EC2 instance with an assigned IAM role.
 * D. Make all the API calls over an SSL connection.

### 2. Which of the following are found in an IAM policy? (Choose 2 answers)
 * A. Service Name
 * B. Region
 * C. Action
 * D. Password

### 3. Your AWS account administrator left your company today. The administrator had access to the root user and a personal IAM administrator account. With these accounts, he generated other IAM accounts and keys. Which of the following should you do today to protect your AWS infrastructure? (Choose 4 answers)
 * A. Change the password and add MFA to the root user.
 * B. Put an IP restriction on the root user.
 * C. Rotate keys and change passwords for IAM accounts.
 * D. Delete all IAM accounts.
 * E. Delete the administrator’s personal IAM account.
 * F. Relaunch all Amazon EC2 instances with new roles.

### 4. Which of the following actions can be authorized by IAM? (Choose 2 answers)
 * A. Installing ASP.NET on a Windows Server
 * B. Launching an Amazon Linux EC2 instance
 * C. Querying an Oracle database
 * D. Adding a message to an Amazon Simple Queue Service (Amazon SQS) queue

### 5. Which of the following are IAM security features? (Choose 2 answers)
 * A. Password policies
 * B. Amazon DynamoDB global secondary indexes
 * C. MFA
 * D. Consolidated Billing

### 6. Which of the following are benefits of using Amazon EC2 roles? (Choose 2 answers)
 * A. No policies are required.
 * B. Credentials do not need to be stored on the Amazon EC2 instance.
 * C. Key rotation is not necessary.
 * D. Integration with Active Directory is automatic.

### 7. Which of the following are based on temporary security tokens? (Choose 2 answers)
 * A. Amazon EC2 roles
 * B. MFA
 * C. Root user
 * D. Federation

### 8. Your security team is very concerned about the vulnerability of the IAM administrator user accounts (the accounts used to configure all IAM features and accounts). What steps can be taken to lock down these accounts? (Choose 3 answers)
 * A. Add multi-factor authentication (MFA) to the accounts.
 * B. Limit logins to a particular U.S. state.
 * C. Implement a password policy on the AWS account.
 * D. Apply a source IP address condition to the policy that only grants permissions when the user is on the corporate network.
 * E. Add a CAPTCHA test to the accounts.

### 9. You want to grant the individuals on your network team the ability to fully manipulate Amazon EC2 instances. Which of the following accomplish this goal? (Choose 2 answers)
 * A. Create a new policy allowing EC2:* actions, and name the policy NetworkTeam.
 * B. Assign the managed policy, EC2FullAccess, to a group named NetworkTeam, and assign all the team members’ IAM user accounts to that group.
 * C. Create a new policy that grants EC2:* actions on all resources, and assign that policy to each individual’s IAM user account on the network team.
 * D. Create a NetworkTeam IAM group, and have each team member log in to the AWS Management Console using the user name/password for the group.

### 10. What is the format of an IAM policy?
 * A. XML
 * B. Key/value pairs
 * C. JSON
 * D. Tab-delimited text