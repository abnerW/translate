# ������ Amazon Virtual Private Cloud(Amazon VPC)
**��AWS��֤��������ܹ�ʦ-���Ͽ��ԡ��еı��½�Ŀ������������������ݣ�**

## ��һ�� ��Ƹ߿��á��ͳɱ����ݴ�����չ��ϵͳ
### �ҳ���ʶ���Ƽܹ��������أ����磺�����������Ч�����

**�����������ݣ�**
```
  * ��ô����Ʒ���
  * �ƻ������
  * ��Ϥ�������ݣ�
    AWS�ܹ�����¼�
    �ܹ�Ȩ����ߣ����磺�߿��� vs �ɱ���Amazon ��ϵ���ݿ����[RDS] VS ��Amazon EC2�ϰ�װ���Լ������ݿ⣩
  * ���IT�ܹ������磬ֱ�����ӣ��洢���أ�VPC��Ŀ¼����
```
## �ڶ��� ʵ��/����

### ʹ��Amazon Ec2��Amazon Simple Storage Service��Amazon S3����AWS Elastic Beanstalk��AWS Cloudformation��AWS Opsworks��Amazon Virtual Private Cloud��Amazon VPC����AWS Identity And Access Management��IAM��ȷ���ʵ��ļ����ͷ����������ʵ���ƽ��������

**������������**
```
  * �ڻ��IT�ܹ��в�������չ�������
  * ���÷�����֧�����еĺϹ���Ҫ��
```
## ������ ���ݰ�ȫ

### ��ʶ��ʵʩ��ȫʵ����ʵ����ѵ��Ʋ����ά��
**���ܰ�����������**
```
 * AWS��ȫ���ԣ��ͻ�����������������㣩
 * Amazon Virtual Private Cloud (VPC) 
 * ��ںͳ��ڹ��ˣ��Լ���ЩAWS����͹����ʺ�
 * "����"Amazon EC2��S3��ȫ���Լ�
 * ����ͨ�ó��氲ȫ��Ʒ������ǽ��VPN��
 * ���ӵķ��ʿ��ƣ��������ӵİ�ȫ�顢ACL�ȣ� 

## ���
* Amazon����˽���ƣ�Amazon VPC����AWS�����Զ�����������硣�������ṩ�Լ���AWS�߼����벿�֣���������ƺ�ʵ�ֽ��ڱ����������������еĶ������硣����̽��Amazon VPC�ĺ������������ϰ�У�����ѧϰ��������й����Լ���Amazon VPC��ͨ��������Ҫ��Amazon VPC�����˽ṹ�͹����ų��к�ǿ���˽⣬����ǿ�ҽ�������ɱ����е���ϰ

## Amazon Virtual Private Cloud(Amazon VPC)
* Amazon VPC��Amazon���Լ����ƣ�Amazon EC2��������㣬����������AWS�й����Լ����������硣�����Կ���Amazon VPC�ĸ������棬����ѡ���Լ���IP��ַ��Χ�������Լ��������������Լ���·�ɱ��������غͰ�ȫ���á���һ�������ڣ������Դ������Amazon VPC������ÿ��Amazon VPC���߼����Ǹ���ģ���ʹ��������IP��ַ�ռ䡣

* ����Amazon VPCʱ������ͨ��ѡ���������·�ɣ�CIDR���飨��10.0.0.0/16����ָ��IPv4��ַ��Χ��Amazon VPC������֮��Amazon VPC�ĵ�ַ��Χ���ܸı䡣һ��Amazon VPC����ַ��Χ�ɴ�/16(65536�����õ�ַ)����С��ַ��Χ/28(16�����õ�ַ)�����Һ����ǽ�Ҫ���ӵ������κ������ص���

* Amazon VPC��������Amazon EC2����֮�󷢲��ģ���ˣ�AWS����������ͬ������ƽ̨��EC2 Classic��EC2-VPC��Amazon EC2�����������AWS�ͻ�����ĵ�һƽ������EC2 Classicһ�𷢲��ġ���ˣ���Amazon VPC���񵽴�֮ǰ������AWS�ʻ����Խ�ʵ��������EC2 Classic network��EC2-VPC�С�֧��EC2-VPC��AWS�ʻ�����ÿ�������д���һ��Ĭ��VPC����ÿ�������������д���һ��Ĭ��������VPC�����CIDR�齫��172.31.0.0/16��

* ͼ4.1 ˵��һ����ַ�ռ䣺10.0.0.0/16����������ͬ������10.0.0.0/24��10.0.1.0/24����Amazon VPC�����������ֱ��ڲ�ͨ�Ŀ������򣬲���ָ���˱���·�ɵ�·�ɱ�

* һ��Amazon VPC�������µ������
```
 * ����
 * ·�ɱ�
 * ��̬����Э�飨DHCP��ѡ�
 * ��ȫ��
 * ��������б�(ACLs)
```

* һ�� Amazon VPC �������¿�ѡ�����
```
 * Internet ����(IGWs)
 * ����IP��ַ(EIP��
 * ��������ӿڣ�ENIs)
 * Endpoints
 * Peering
 * �����ַת��ʵ����NAT����
 * VPG,CGWs,VPNs
```

## Subnets
* ������Amazon VPC��IP��ַ��Χ��һ���֣���������������Amazon EC2ʵ����Amazon��ϵ���ݿ����Amazon RDS�����ݿ������AWS��Դ��CIDR�鶨�����������磬10.0.1.0/24��192.168.0.0/24���������Դ�������С������/28��16��IP��ַ����AWS����ÿ��������ǰ�ĸ�IP��ַ�����һ��IP��ַ�������ڲ����硣���磬����Ϊ/28��������16������IP��ַ����ȥAWS�����5��IP���õ�11��IP��ַ��������������ʹ�á�

* ����Amazon VPC�󣬿�����ÿ���������������һ����������������λ��һ�����������ڣ����ܿ�Խ�������Ǽ���п��ܳ��ֵ�һ����Ҫ�㣬���ס��һ����������һ���������򡣵��ǣ���������һ�������������ж��������

* �������Է�Ϊ�����ģ�˽�еģ������VPN�����������ǹ���·�ɱ��Ժ����ۣ�����������������Amazon VPC��IGW���Ժ����ۣ���������ר�������ǹ���·�ɱ�����������������Amazon VPC��IGW������������VPN�����������й�����·�ɱ���������������Amazon VPC��VPG���Ժ����ۣ�������û�е�IGW��·�ɡ�����������������Σ��������ڲ�IP��ַ��Χʼ����˽�еģ�������Internet�ϲ���·�ɣ���

* Ĭ�ϵ�Amazon vpc�������ڵ�ÿ�����������ж�����һ��������������������Ϊ/20��

## ·�ɱ�Route Tables��


## ���أ�Internet Gateways��


## ��̬��������Э�飨DHCP��


## ����IP��ַ��Elastic IP Addresses(EIPs)��


## ��������ӿڣ�Elastic Network Interfaces(ENIs)��


## �յ㣨Endpoints��


## Peering



## ��ȫ��



## ������ʿ����б�ACLs��



## �����ַת����NAT��ʵ��


## ����˽�����أ�VPGs�����ͻ����أ�CGWs�����Լ�����˽�����磨VPNs��




## �ܽ�




## ���Ի���




## ��ϰ




## ��ϰ��

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
 * B. Three subnets are created by default��one for each Availability Zone. 
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

### 16. You are responsible for your company��s AWS resources, and you notice a significant amount of traffic from an IP address in a foreign country in which your company does not have customers. Further investigation of the traffic indicates the source of the traffic is scanning for open ports on your EC2-VPC instances. Which one of the following resources can deny the traffic from reaching the instances? 
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









