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

* 子网可以分为公共的，私有的，或仅限VPN。公用子网是关联路由表（稍后讨论）将子网的流量定向到Amazon VPC的IGW（稍后讨论）的子网。专用子网是关联路由表不将子网的流量定向到Amazon VPC的IGW的子网。仅限VPN的子网是其中关联的路由表将子网的流量定向到Amazon VPC的VPG（稍后讨论），并且没有到IGW的路由。无论子网的类型如何，子网的内部IP地址范围始终是私有的（即，在Internet上不可路由）。

* 默认的Amazon vpc在区域内的每个可用区域中都包含一个公共子网，网络掩码为/20。

## 路由表（Route Tables）


## 网关（Internet Gateways）


## 动态主机配置协议（DHCP）


## 弹性IP地址（Elastic IP Addresses(EIPs)）


## 弹性网络接口（Elastic Network Interfaces(ENIs)）


## 终点（Endpoints）


## Peering



## 安全组



## 网络访问控制列表（ACLs）



## 网络地址转换（NAT）实例


## 虚拟私有网关（VPGs），客户网关（CGWs），以及虚拟私有网络（VPNs）




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









