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
```

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

* �������Է�Ϊ�����ģ�˽�еģ������VPN�����������ǹ���·�ɱ��Ժ����ۣ�����������������Amazon VPC��IGW���Ժ����ۣ���������private�����ǹ���·�ɱ�����������������Amazon VPC��IGW������������VPN�����������й�����·�ɱ���������������Amazon VPC��VPG���Ժ����ۣ�������û�е�IGW��·�ɡ�����������������Σ��������ڲ�IP��ַ��Χʼ����˽�еģ�������Internet�ϲ���·�ɣ���

* Ĭ�ϵ�Amazon vpc�������ڵ�ÿ�����������ж�����һ��������������������Ϊ/20��

## ·�ɱ�Route Tables��
* ·�ɱ���Amazon VPC�е�һ���߼��ṹ��������һ��Ӧ���������Ĺ��򣨳�Ϊ·�ɣ�������ȷ�����������Ķ���λ��Amazon VPC�е����������໥ͨ�š��������޸�·�ɱ�����Լ����Զ���·�ɡ���������ʹ��·�ɱ�ָ����Щ�����ǹ��õģ�ͨ����Internet��������IGW����Щ������ר�õģ�ͨ��û�н���������IGW��·�ɣ���

* ÿһ��·�ɱ����һ������·�ɡ�ͨ���������·�ɿ��Ժ�Amazon VPC����ͨ�ţ��������·�ɲ���ɾ��Ҳ�����޸ġ�������Ӷ����·������������ͨ��IGW���Ժ����ۣ���VPG���Ժ����ۣ���NATʵ�����Ժ����ۣ��˳�Amazon VPC���ڱ���ĩβ����ϰ�У�������ʵ���������ʵ�ֵġ�

* ����·�ɱ���Ӧ�ü�ס���¼��㣺
```
 * ���VPC��һ������·��
 * ���VPC���Զ�����һ����·�ɱ�������޸���
 * ������ΪVPC���������Զ���·�ɱ�
 * ÿ���������������������·�ɵ�·�ɱ�����������δ���������ض�·�ɱ���ʽ������������ʹ����·�ɱ�
 * ���������Ѵ������Զ�����滻��·�ɱ��Ա�ÿ���������Զ��������
 * ���е�ÿ��·��ָ��һ��Ŀ�ĵ�CIDR��һ��Ŀ�ꣻ���磬Ŀ�ĵ�Ϊ172.16.0.0/12��������VPG��Ŀ�ꡣAWSʹ��������ƥ������ض�·����ȷ�����·������ 
```

## ���أ�Internet Gateways��
* Internet���أ�IGW����һ��ˮƽ��չ�������Ҹ߶ȿ��õ�Amazon VPC���������Amazon VPC�е�ʵ����Internet֮�����ͨ�š�IGW��Amazon VPC·�ɱ���ΪInternet��·�������ṩĿ�꣬�����ѷ��乫��IP��ַ��ʵ��ִ�������ַת����

* Amazon VPC�е�Amazon EC2ʵ��ֻ֪�����ǵ�˽��IP��ַ����������ʵ�����͵�Internetʱ��IGW��Ӧ���ַת��Ϊʵ���Ĺ���IP��ַ����EIP��ַ���Ժ���ܣ�����ά��ʵ��˽��IP��ַ�͹���IP��ַ��һ��һӳ�䡣��ʵ�����յ�����Internet������ʱ��IGW��Ŀ���ַ������IP��ַ��ת��Ϊʵ����˽��IP��ַ����������ת����Amazon VPC��

* ����ִ�����²������ܴ�������Internet����Ȩ�޵Ĺ�������
```
 * ����һ��IGW�����Amazon VPC
 * ����һ������·�ɱ�������ڷ������еķǱ���������0.0.0.0/0����IGW
 * �����������ACLs�Ͱ�ȫ������������������������������ʵ��
```

* �����ִ�����²������Ա���Amazon EC2ʵ���ܹ�����������Internet�ͽ�������Internet��������
```
 * ����һ��public IP��ַ����EIP��ַ
```

* �����Խ�·�ɷ�Χ����Ϊ·�ɱ�0.0.0.0/0��δ��ȷ֪��������Ŀ�ĵأ�Ҳ���Խ�·�ɷ�Χ����Ϊ��խ��IP��ַ��Χ�����磺AWS֮�⹫˾�����ս��Ĺ���IP��ַ��Amazon VPC֮�������Amazon EC2ʵ����EIP��ַ��

* ͼ4.2չʾ��һ����ַ�ռ�Ϊ10.0.0.0/16��Amazon VPC��һ��������ַ��ΧΪ10.0.0.0/24��һ��·�ɱ�һ�����ӵ�IGW���Լ�һ������˽��IP��ַ��EIP��ַ��Amazon EC2ʵ����·�ɱ��������·�ɣ������VPCͨ�ŵı���·�ɺͽ����зǱ����������͵�IGW��IGW id����·�ɣ�ע��Amazon EC2ʵ����һ������IP��ַ��EIP=198.51.100.2�������Դ�Internet���ʴ�ʵ�����������ܻ���������ص���ʵ����

## ��̬��������Э�飨DHCP��
* ��̬��������Э��DHCPΪ��TCP/IP�����ϵ���������������Ϣ�ṩ�˱�׼��DCCP��Ϣ��ѡ���ֶΰ��������ò����������а��������������������Լ�netbios-node-type��

* AWS���Զ�Ϊ�㴴����Amazon VPC�����͹���һ��DCCPѡ���������������ѡ���������Ĭ���ǣ�AmazonProvidedDNS����������Ĭ�������region����������AmazonProvidedDNS��Amazon��һ������ϵͳ���񣬴�ѡ����������Ҫ��������VPC��ͨ�ŵ�ʵ����

* Amazon VPC��DHCP option setsԪ����������Amazon EC2���������䶨���Լ�����Դ��Ҫ���Լ������������ʵ�����봴���Զ���DHCPѡ�����������Amazon VPC��������DHCPѡ�����������ֵ��
```
 * domain-name-servers ����ĸ�������������IP��ַ���ö��ŷָ���Ĭ��ֵΪAmazonProvidedDNS��
 * domain-name �ڴ˴�ָ�����������
 * ntp-servers ����ĸ�����ʱ��Э���������IP��ַ���ö��ŷָ���
 * netbios-name-servers ����ĸ�NetBIOS���ַ�������IP��ַ���ö��ŷָ���
 * netbios-node-type ����ֵ����Ϊ��2��
```
* ֻ��Ϊÿ��Amazon VPC����һ��DHCPѡ���

## ����IP��ַ��Elastic IP Addresses(EIPs)��
AWS ��ÿ��Regionά��һ������IP��ַ�أ���ʹ���ǿɹ�����Amazon VPCs�е���Դ����������IP��ַ��EIP���ǳ��еľ�̬����IP��ַ�������Խ������������ʻ����ӳ�����ȡ�����ͷţ����سأ���EIP������ά��һ�鱣�̶ֹ���IP��ַ�����ײ������ʩ���ܻ�����ʱ����ı䡣�����ǿ������й�EIP����ҪҪ��:
```
 * �����ȷ���һ��EIP��VPCʹ�ã�Ȼ���ٽ�������һ��ʵ����
 * EIP���ض���һ������ģ�Ҳ����˵�����ܽ�һ�������е�EIP�������һ��������Amazon VPC�ڵ�ʵ������
 * ����ӿں�EIP��һһ��Ӧ�Ĺ�ϵ
 * ���Խ�EIP��һ��ʵ���Ƶ�����һ��ʵ����������ͬһ��Amazon VPC��Ҳ������ͬһ��Region�Ĳ�ͬAmazon VPC��
 * ������ȷ�ͷ�EIP֮ǰ��EIP��������AWS�ʻ�������
 * Ϊ�����ʻ������EIP����ȡ���ã���ʹ��������Դû�й�����
```

## ��������ӿڣ�Elastic Network Interfaces(ENIs)��
* ��������ӿڣ�ENI����һ����������ӿڣ����Ը��ӵ�Amazon VPC�е�ʵ����ENIs����Amazon VPC�п��ã����������ڴ���ʱ����������������ǿ�����һ������IP��ַ�Ͷ��˽��IP��ַ������ж��ר��IP��ַ������һ������IP��ַ��ͨ��ENIΪʵ������ڶ�������ӿ���������˫�޵ģ��ڲ�ͬ����������������ڣ����������ض�ʵ��������ENI���������ڣ������������ӵ����κ�ʵ������������Σ��������ʵ��ʧ�ܣ������ͨ����ENI���ӵ��滻ʵ��������IP��ַ��              

* ENIs����������һ���������磬��Amazon VPC��ʹ������Ͱ�ȫ�豸���ڲ�ͬ�������ϴ������й�������/��ɫ��˫��ʵ�������ߴ���һ���ͳɱ����߿����ԵĽ������


## �˵㣨Endpoints��
* Amazon VPC�˵���������Amazon VPC����һ��AWS����֮�䴴��˽�����ӣ�������ͨ��Internet��NATʵ����VPN���ӻ�AWSֱ�����ӽ��з��ʡ�����Ϊ�������񴴽�����ս�㣬������ʹ�ò�ͬ��·�ɱ�Ӳ�ͬ��������ͬһ����ǿ��ʵʩ��ͬ�ķ��ʲ��ԡ�

* Amazon VPC�˵�Ŀǰ֧����Amazon Simple Storage Service��Amazon S3����ͨ�ţ�δ������������������Ҫ����Amazon VPC�˵㣬����ִ�����²�����
```
 * ָ��Amazon VPC
 * ָ������һ��������ͨ����������ǰ׺�б����ʽ���壺com.amazonaws.<region>.<service>��
 * ָ�����ԡ�������������ȫ���ʻ򴴽��Զ�����ԡ��˲��Կ�����ʱ���ġ�
 * ָ��·�ɱ�·�ɽ�����ӵ�ÿ��ָ����·�ɱ��У��ñ���������ΪĿ�꣬�˵�����ΪĿ�� 
```

* ��-4.1 ��һ��·�ɱ��ʾ������·�ɱ���н�����Internetҵ��0.0.0.0/0��������IGW������·�ɡ�����һ��AWS�������磬Amazon S3��Amazon DynamoDB���������е��κ�ҵ�񽫱����͵�IGW���Ա�ﵽ�÷��� 

��-4.1 ����IGW·�ɹ����·�ɱ�
|---|---|
|Destination|Target|
|10.0.0.0/16|Local|
|0.0.0.0/0|igw-1a2b3c4d|

* ��4.2��һ��ʾ��·�ɱ������н�����Internet����������IGW������Amazon S3������Amazon VPC�˵������·�ɡ� 

��-4.2 ����IGW·�ɹ����VPC�˵�����·�ɱ�
|---|---|
|Destination|Target|
|10.0.0.0/16|Local|
|0.0.0.0/0|igw-1a2b3c4d|
|p1-1a2b3c4d|vpce-11bb22cc|

* ��4.2��������·�ɱ��Ѵ�ͬһ�����е�Amazon S3���������κ�ͨ�������򵽶˵㡣����������������������������IGW�����������������������������Amazon S3��������

## Peering
* һ��Amazon VPC�Ե�����������Amazon VPC֮����������ӣ���ʹ�κ�һ��Amazon VPC�е�ʵ���ܹ��˴�ͨ�ţ��ͺ���������ͬһ��������һ�������������Լ���Amazon VPC֮�䴴��һ��Amazon VPC�Ե����ӣ�Ҳ�����ڵ��������ڵ���һ��AWS�ʻ��д���һ��Amazon VPC�Ե����ӡ��Ե����ӼȲ�������Ҳ����Amazon VPN���ӣ����Ҳ�������ͨ�ŵĵ�����ϡ�              
* �Ե�������ͨ������/����Э�鴴���ġ������Amazon VPC����������Եȵ�Amazon VPC�������߷�������peer������Եȵ�Amazon VPC��ͬһ���˻��ڣ�������VPC ID��ʶ������Եȵ�VPC�ڲ�ͬ���˻��ڣ������˻�ID��VPC ID��ʶ���Եȵ�Amazon VPC���������ڶԵ�������ǰ��һ��ʱ����ܻ�ܾ��������Amazon VPC�Եȵ�����              һ��

* Amazon VPC�����ж���Ե����ӣ��Ե���Amazon VPC֮���һ��һ��ϵ������ζ������Amazon VPC֮�䲻���������Ե�Э�顣���⣬�Ե����Ӳ�֧�ִ���·�ɡ�ͼ4.3�����˴���·�ɡ�

* ͼ-4.3 VPC�Ե����Ӳ�֧�ִ���·�ɣ�������ͼ��

* ��ͼ4.3�У�VPC A�������Ե����ӣ��ֱ���VPC B��VPC����ˣ�VPC A����ֱ����VPC B��Cͨ�š����ڶԵ����Ӳ�֧�ִ���·�ɣ�����VPC A������ΪVPC B��C֮��ͨ�ŵĴ���㡣Ϊ��ʹVPC B��C�໥ͨ�ţ��Ե����ӱ���������֮����ʽ�������ӡ������ǹ��ڿ��ӿ��Ե�Ҫ�㣺              
```
 * �����ھ���ƥ����ص�CIDR���Amazon vpc֮�䴴���Ե�����
 * �����ڲ�ͬ�����Amazon VPC֮�䴴���Ե�����
 * Amazon VPC�Ե����Ӳ�֧�ִ���·��
 * ͬһʱ��ͬһ��Amazon VPC֮�䲻���ж���Ե�����
```

## ��ȫ��
* ��ȫ����һ��������״̬����ǽ�������Ƶ�AWS��Դ��Amazon EC2ʵ������վ�ͳ�վ��������������Amazon EC2ʵ��������������һ����ȫ���С��������ʱδָ����ȫ�飬��ʵ������������Amazon VPC��Ĭ�ϰ�ȫ���С�Ĭ�ϰ�ȫ������ȫ����������Դ֮���ͨ�ţ��������г�վͨ�ţ����ܾ���������ͨ�š������Ը���Ĭ�ϰ�ȫ��Ĺ��򣬵�����ɾ��Ĭ�ϰ�ȫ�顣��4.3������Ĭ�ϰ�ȫ������á�

* ��-4.3 ��ȫ����򣨴����ӣ�

* ����ÿ����ȫ�飬������ӿ���ʵ������վ�����Ĺ���Ϳ��Ƴ�վ�����ĵ������򼯡����磬��4.4������web�������İ�ȫ�顣

*��-4.4 Web ����İ�ȫ����򣨴����ӣ�
* �����ǹ��ڿ��ӿ��Ե�Ҫ�㣺
```
 * ��������Ϊÿ��Amazon VPC����500����ȫ�顣
 * ÿ����ȫ�����������50����վ��50����վ���������Ҫ��һ��ʵ��Ӧ��100��������������Խ������ȫ����ÿ������ӿڹ�����
 * ����ָ��������򣬵�����ָ���ܾ��������ǰ�ȫ���acl֮���һ����Ҫ����
 * ������Ϊ��վ�ͳ�վ����ָ�������Ĺ���
 * Ĭ������£��ڽ���վ������ӵ���ȫ��֮ǰ����������վ������
 * Ĭ������£��°�ȫ������������г�վ�����ĳ�վ����������ɾ���ù�����ӽ������ض���վ�����ĳ�վ����
 * ��ȫ������״̬�ġ�����ζ�����۳�վ������Σ����������վ��������Ӧ��������������֮��Ȼ�����ǰ�ȫ�������ACL֮���һ����Ҫ����
 * ��ͬһ��ȫ�������ʵ�������໥ͨ�ţ�������������������Ĺ���Ĭ�ϰ�ȫ����⣩��
 * �������������������ʵ�������İ�ȫ�飬��Щ���Ľ�������Ч��
```

## ������ʿ����б�ACLs��
* ������ʿ����б�ACL������һ����ȫ�㣬����������䵱��״̬����ǽ������ACL��AWS��˳�����Ĺ���ı���б��ӱ����͵Ĺ���ʼ����ȷ��������ACL�������κ��������Ƿ�����ͨ�š�Amazon vpc����һ�����޸ĵ�Ĭ������ACL�����ģ���ACL������������վ�ͳ�վ������ÿ����������������������Զ�������ACLʱ�����ʼ���ý��ܾ�������վ�ͳ�վͨ�ţ�ֱ������������������ʽ�Ĺ���������ʹ���밲ȫ�����ƵĹ�����������ACL���Ա���Amazon VPC��Ӱ�ȫ�㣬Ҳ����ѡ��ʹ��Ĭ�ϵ�����ACL����ACL������ͨ�������߽���������ܵ���˵��ÿ������������������ACL�������

* ��-4.5 չʾ�˰�ȫ�������ACL֮��Ĳ�ͬ��Ӧ�Կ��ԣ���Ӧ�ü�ס��ȫ�������ACL֮�����µĲ�ͬ�㡣
* ��-4.5 ��ȫ�������ACLs�Ա�
|---|---|
|��ȫ��|����ACL|
|ʵ���Ǽǲ����������ĵ�һ��|�������Ǽǣ������ĵڶ���|
|��֧������Ĺ���|֧���������;ܾ�����|
|״̬�ȶ��������Զ����������������κι���|״̬���ȶ����������������������屻����|
|�ھ����Ƿ���������֮ǰ��AWS���������й���|AWS�ھ����Ƿ���������ʱ������˳�������|
|ѡ���Ե�Ӧ���ڵ���ʵ��|�Զ�Ӧ���ڹ��������е�����ʵ�������Ƿ����ı��ݲ㣬���������������ָ����ȫ�����|


## �����ַת����NAT��ʵ���Լ�NAT����
* Ĭ������£���Amazon VPC��������˽���������κ�ʵ�����޷�ͨ��IGW��Internetͨ�š����˽�������е�ʵ����Ҫ��Amazon VPCֱ�ӷ���Internet����Ӧ�ð�ȫ���¡������޲���������Ӧ�ó�������������ִ����⡣AWS�ṩ��NATʵ����NAT���أ���������˽�������е�ʵ������Internet�����ڳ��������������ǽ�����ʹ��NAT���ض�����NATʵ����NAT�����ṩ�˸��õĿ����Ժ͸��ߵĴ������ұ�NATʵ����Ҫ���ٵĹ�������

### NATʵ��
* �����ַת����NAT��ʵ����Amazon-Linux Amazon����ӳ��AMI������������ڽ�������˽��������ʵ������������ԴIP��ַת��ΪNATʵ���Ĺ���IP��ַ����������ת����IGW�����⣬NATʵ��ά��ת��������״̬���Ա㽫��Ӧ������Internet���ص�˽�������е��ʵ�ʵ������Щʵ�������������ַ���amzn-ami-p-vpc-nat��������Amazon EC2����̨�н�������

* ��Ҫ����ר�������е�ʵ��ͨ��NATʵ��ͨ��IGW����Internet��Դ������ִ�����²�����
```
 * ʹ�ó�վ����ΪNAT������ȫ�飬�ó�վ���򰴶˿ڡ�Э���IP��ַָ�������Internet��Դ��
 * ��Amazon Liinux Nat AMI ��Ϊ���������е�ʵ����������������NAT��ȫ�������
 * ����NAT��Դ/Ŀ�������ԡ�
 * ������ר������������·�ɱ��Խ��󶨵�Internet����������NATʵ�������磬i-1a2b3c4d����
 * ����EIP��������NATʵ��������
```
* ����������˽�������е�ʵ�����ͳ�վInternetͨ�ţ�������ֹʵ��������Internet�ϵ�ĳ�˷������վͨ�š�

### NAT����
* NAT������Amazon�������Դ�����������NATʵ��һ�������������ڹ��������ڿ����������ڸ߶ȿ��á���Ҫ����ר�������е�ʵ��ͨ��NAT����ͨ��IGW����Internet��Դ������ִ�����²�����
```
 * ����ר������������·�ɱ�����Ϊֱ�Ӱ󶨵�Internet��NAT���ص����������磬NAT-1a2b3c4d����
 * ����EIP��������NAT���ع�����
```

* ��NATʵ��һ�������йܷ��������վInternetͨ�ţ�����ֹʵ��������Internet�ϵ�ĳ�˷������վͨ��

* ��ע
``` 
 Ҫ���������ڿ���������ϵ�ṹ������ÿ���������д���һ��NAT���أ�������·����ȷ����Դ��ͬһ��������ʹ��NAT����
```
����ϰ�н���֤��NAT������ι�����

## ����˽�����أ�VPGs�����ͻ����أ�CGWs�����Լ�����˽�����磨VPNs��
* ������ʹ��Ӳ�������VPN���ӽ����е������������ӵ�Amazon VPC���⽫ʹAmazon VPC��Ϊ�������ĵ���չ��Amazon VPC�ṩ�����ֽ���ҵ�������ӵ�VPC�ķ�����VPG��CGW��              
* ����ר�����أ�VPG������������֮��VPN���ӵ�AWS�˵�����ר������VPN�����������ͻ����أ�CGW����ʾVPN���ӿͻ��˵������豸�����Ӧ�ó����ڴ�����Amazon VPC��������Ԫ��֮�����һ���Ǵ���VPN�����VPN������ڴ�VPN���ӵĿͻ�����������֮�����ġ�ͼ4.4��ʾ�˹�˾�����Amazon VPC֮��ĵ���VPN���ӡ�

* ͼ4.4 ��ͻ����罨��VPN���ӵ�VPC�������ӣ�

* ����ָ������VPN����ʱ�ƻ�ʹ�õ�·�����͡����CGW֧�ֱ߽�����Э�飨BGP������Ϊ��̬·������VPN���ӡ�������Ϊ��̬·���������ӡ����Ҫʹ�þ�̬·�ɣ����������Ӧ��VPGͨ�ŵ�����·�ɡ�·�ɽ�������Amazon VPC��������������Դͨ��VGW��VPN�������������·�ɻع�˾����Amazon VPC��֧�ֶ��cgw��ÿ��cgw����һ��VPN���ӵ�һ��VPG�����һ��ƣ���Ϊ��֧���������˽ṹ��CGW IP��ַ�������ڱ�����Ψһ�ġ�

* Amazon VPC���ṩ�������Ա����CGW�������Ϣ������VPG����VPN���ӡ�VPN����������InternetЭ�鰲ȫ��IPSec�������ɣ������Amazon VPC�Ŀ����ԡ������ǿ�������Ҫ�˽���й�VPG��CGW��VPN��Ҫ�㣺
```
 * VPG��VPN�����AWS�ˡ�
 * CGW��VPN����ͻ��˵�Ӳ�������Ӧ�ó���
 * ������������CGW��VPG��VPN�����
 * vpg֧��BGP��̬·�ɺ;�̬·�ɡ�
 * VPN���������������ɣ������VPC�Ŀ����ԡ�
```

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









