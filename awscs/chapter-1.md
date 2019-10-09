# AWS ���
## ʲô���Ƽ���
�Ƽ�����ͨ�����������轻��IT��Դ��Ӧ�ó��򣬲����踶�ѡ��������������������ƶ��û�������Ƭ��Ӧ�ó��򣬻����ṩ֧��ҵ��ؼ���Ӫ�ķ������ṩ�˶����͵ͳɱ�IT��Դ�Ŀ��ٷ��ʡ�ʹ���Ƽ��㣬������Ҫ��Ӳ���Ͻ��д�����ǰ��Ͷ�ʣ�Ҳ����Ҫ���Ѵ���ʱ�����Ӳ�����෴���������ṩ��ȷ���ͺͺ��ʴ�С�ļ�����Դ����֧�������µĴ����뷨����Ӫ����IT���š�ʹ���Ƽ��㣬�����������������������������������Դ������ֻ��֧����ʹ�õ���Դ�ķ��á�
�Ƽ�����ŵ�
Cloud	computing	introduces	a	revolutionary	shift	in	how	technology	is	obtained,	used,	and managed,	and	in	how	organizations	budget	and	pay	for	technology	services.	With	the	ability to	reconfigure	the	computing	environment	quickly	to	adapt	to	changing	business requirements,	organizations	can	optimize	spending.	Capacity	can	be	automatically	scaled	up or	down	to	meet	fluctuating	usage	patterns.	Services	can	be	temporarily	taken	offline	or	shut down	permanently	as	business	demands	dictate.	In	addition,	with	pay-per-use	billing,	AWS Cloud	services	become	an	operational	expense	instead	of	a	capital	expense. While	each	organization	experiences	a	unique	journey	to	the	cloud	with	numerous	benefits, six	advantages	become	apparent	time	and	time	again,	as	illustrated	in	Figure	1.1.

�Ƽ�������˼�����ȡ��ʹ�ú͹���ʽ�ĸ�����ת�䣬�Լ���֯���Ϊ�����������Ԥ���֧�����Ƽ����ܹ������������ü��㻷��������Ӧ���ϱ仯��ҵ��������֯�����Ż�֧�������������Զ����ӻ���٣������㲨����ʹ��ģʽ�����������ʱ�ѻ������ҵ���������ùرա����⣬ʹ�ð��μƷѣ�aws�Ʒ����Ϊһ����Ӫ���ã��������ʱ����á���Ȼÿ����֯��������һ�ζ��ص��ƶ�֮�ã����������ô����������ô�ȴһ����һ�ε����ֳ�������ͼ-1.1��ʾ��

Global in minutes
Variable VS.capital expense
Economies of Scale
Increace speed and ingility
Focus on business differentiators
Stop guessing capacity


## AWS ����ԭ��

aws�ĺ���ּ�ڰ�ȫ���Ʒ���ƽ̨��ͨ���������ṩit��Դ�İ��轻�����ṩ�����������洢�����ݿ⡢���ݽ������������ܣ��԰�����ҵ��չ��������
At	its	core,	AWS	provides	on-demand	delivery	of	IT	resources	via	the	Internet	on	a	secure cloud	services	platform,	offering	compute	power,	storage,	databases,	content	delivery,	and other	functionality	to	help	businesses	scale	and	grow.	Using	AWS	resources	instead	of	your own	is	like	purchasing	electricity	from	a	power	company	instead	of	running	your	own generator,	and	it	provides	the	key	advantages	of	cloud	computing:	Capacity	exactly	matches your	need,	you	pay	only	for	what	you	use,	economies	of	scale	result	in	lower	costs,	and	the service	is	provided	by	a	vendor	experienced	in	running	large-scale	networks. AWS	global	infrastructure	and	AWS	approach	to	security	and	compliance	are	key foundational	concepts	to	understand	as	you	prepare	for	the	exam. Global	Infrastructure AWS	serves	over	one	million	active	customers	in	more	than	190	countries,	and	it	continues	to expand	its	global	infrastructure	steadily	to	help	organizations	achieve	lower	latency	and higher	throughput	for	their	business	needs. AWS	provides	a	highly	available	technology	infrastructure	platform	with	multiple	locations worldwide.	These	locations	are	composed	of	regions	and	Availability	Zones.	Each	region	is	a separate	geographic	area.	Each	region	has	multiple,	isolated	locations	known	as	Availability Zones.	AWS	enables	the	placement	of	resources	and	data	in	multiple	locations.	Resources aren��t	replicated	across	regions	unless	organizations	choose	to	do	so. Each	region	is	completely	independent	and	is	designed	to	be	completely	isolated	from	the other	regions.	This	achieves	the	greatest	possible	fault	tolerance	and	stability.	Each Availability	Zone	is	also	isolated,	but	the	Availability	Zones	in	a	region	are	connected	through low-latency	links.	Availability	Zones	are	physically	separated	within	a	typical	metropolitan region	and	are	located	in	lower-risk	flood	plains	(specific	flood	zone	categorization	varies	by region).	In	addition	to	using	a	discrete	uninterruptable	power	supply	(UPS)	and	on-site backup	generators,	they	are	each	fed	via	different	grids	from	independent	utilities	(when available)	to	reduce	single	points	of	failure	further.	Availability	Zones	are	all	redundantly connected	to	multiple	tier-1	transit	providers.	By	placing	resources	in	separate	Availability Zones,	you	can	protect	your	website	or	application	from	a	service	disruption	impacting	a single	location.
	You	can	achieve	high	availability	by	deploying	your	application	across	multiple Availability	Zones.	Redundant	instances	for	each	tier	(for	example,	web,	application,	and database)	of	an	application	should	be	placed	in	distinct	Availability	Zones,	thereby creating	a	multisite	solution.	At	a	minimum,	the	goal	is	to	have	an	independent	copy	of each	application	stack	in	two	or	more	Availability	Zones.
Security	and	Compliance Whether	on-premises	or	on	AWS,	information	security	is	of	paramount	importance	to
organizations	running	critical	workloads.	Security	is	a	core	functional	requirement	that protects	mission-critical	information	from	accidental	or	deliberate	theft,	leakage,	integrity compromise,	and	deletion.	Helping	to	protect	the	confidentiality,	integrity,	and	availability	of systems	and	data	is	of	the	utmost	importance	to	AWS,	as	is	maintaining	your	trust	and confidence. This	section	is	intended	to	provide	a	very	brief	introduction	to	AWS	approach	to	security	and compliance.	Chapter	12,	��Security	on	AWS,��	and	Chapter	13,	��AWS	Risk	and	Compliance,��	will address	these	topics	in	greater	detail,	including	the	importance	of	each	on	the	exam. Security Cloud	security	at	AWS	is	the	number	one	priority.	All	AWS	customers	benefit	from	data center	and	network	architectures	built	to	satisfy	the	requirements	of	the	most	securitysensitive	organizations.	AWS	and	its	partners	offer	hundreds	of	tools	and	features	to	help organizations	meet	their	security	objectives	for	visibility,	auditability,	controllability,	and agility.	This	means	that	organizations	can	have	the	security	they	need,	but	without	the	capital outlay	and	with	much	lower	operational	overhead	than	in	an	on-premises	environment. Organizations	leveraging	AWS	inherit	all	the	best	practices	of	AWS	policies,	architecture,	and operational	processes	built	to	satisfy	the	requirements	of	the	most	security-sensitive customers.	The	AWS	infrastructure	has	been	designed	to	provide	the	highest	availability while	putting	strong	safeguards	in	place	regarding	customer	privacy	and	segregation.	When deploying	systems	on	the	AWS	Cloud	computing	platform,	AWS	helps	by	sharing	the	security responsibilities	with	the	organization.	AWS	manages	the	underlying	infrastructure,	and	the organization	can	secure	anything	it	deploys	on	AWS.	This	affords	each	organization	the flexibility	and	agility	they	need	in	security	controls. This	infrastructure	is	built	and	managed	not	only	according	to	security	best	practices	and standards,	but	also	with	the	unique	needs	of	the	cloud	in	mind.	AWS	uses	redundant	and layered	controls,	continuous	validation	and	testing,	and	a	substantial	amount	of	automation to	ensure	that	the	underlying	infrastructure	is	monitored	and	protected	24/7.	AWS	ensures that	these	controls	are	consistently	applied	in	every	new	data	center	or	service. Compliance When	customers	move	their	production	workloads	to	the	AWS	Cloud,	both	parties	become responsible	for	managing	the	IT	environment.	Customers	are	responsible	for	setting	up	their environment	in	a	secure	and	controlled	manner.	Customers	also	need	to	maintain	adequate governance	over	their	entire	IT	control	environment.	By	tying	together	governance-focused, audit-friendly	service	features	with	applicable	compliance	or	audit	standards,	AWS	enables customers	to	build	on	traditional	compliance	programs.	This	helps	organizations	establish and	operate	in	an	AWS	security	control	environment.
	Organizations	retain	complete	control	and	ownership	over	the	region	in	which their	data	is	physically	located,	allowing	them	to	meet	regional	compliance	and	data residency	requirements.
The	IT	infrastructure	that	AWS	provides	to	organizations	is	designed	and	managed	in alignment	with	security	best	practices	and	a	variety	of	IT	security	standards.	The	following	is a	partial	list	of	the	many	certifications	and	standards	with	which	AWS	complies: Service	Organization	Controls	(SOC)	1/International	Standard	on	Assurance Engagements	(ISAE)	3402,	SOC	2,	and	SOC	3 Federal	Information	Security	Management	Act	(FISMA),	Department	of	Defense Information	Assurance	Certification	and	Accreditation	Process	(DIACAP),	and	Federal Risk	and	Authorization	Management	Program	(FedRAMP) Payment	Card	Industry	Data	Security	Standard	(PCI	DSS)	Level	1 International	Organization	for	Standardization	(ISO)	9001,	ISO	27001,	and	ISO	27018 AWS	provides	a	wide	range	of	information	regarding	its	IT	control	environment	to	help organizations	achieve	regulatory	commitments	in	the	form	of	reports,	certifications, accreditations,	and	other	third-party	attestations.


## AWS	�Ƽ���ƽ̨ 

  aws�ṩ������Ʒ��������Խ����ǽ������������ҵ�����֯������μ�ͼ1.2�����˽����е�ƽ̨����ʹ����Ϊһ��ȫ��Ľ�������ܹ�ʦ���˽Ȿ���и����ķ���ͻ��������������Ϊ��AWS��֤��������ܹ�ʦ-���Ͽ��ԡ�����׼����


���ڰ���������Ҫ��aws�Ʒ��������½��ṩ���뿼����صķ���ĸ��������ͼ��

### ƽ̨����

  Ҫ����aws�Ʒ��񣬿���ʹ��aws�������̨��aws�����н��棨cli����aws����������߰���sdk����

* aws�������̨��һ�����ڹ���aws�Ʒ����webӦ�ó��򡣿���̨Ϊִ����������ṩֱ�۵��û����档ÿ���������Լ��Ŀ���̨�����Դ�aws�������̨���ʡ�����̨���ṩ�й��ʻ����ʵ�����Ϣ��

* aws�����н��棨cli�������ڹ���aws�Ʒ����ͳһ���ߣ�ֻ�����غ�����һ�����ߣ��Ϳ��Դ������п��ƶ�����񣬲�ͨ���ű�ʵ���Զ�����

* aws����������߰���sdk���ṩ��һ��Ӧ�ó����̽ӿڣ�api���������������awsƽ̨��web������н�����sdkΪ��಻ͬ�ı�����Ժ�ƽ̨�ṩ֧�֣�������ʹ����ѡ���ԡ�

����Web����˵㣬ʹ��SDK����ͨ���ṩ��������ı�̷��������ٱ���ĸ����ԡ� 

### ������������

  aws�ṩ���ּ�����������Ϊ��ҵ�����������乤�������ṩ���Ĺ��ܡ���Щ���������������洢�����ݿ��Ӧ�ó������һ��ʹ�ã�Ϊ���㡢��ѯ�����ṩ�����Ľ���������Լ��㷺Ӧ�õĴ洢�������ṩ���ļ�����������ĸ߼�����

### Amazon Elastic Compute Cloud��Amazon EC2)

  Amazon Elastic Compute Cloud��Amazon EC2����һ���������ṩ�ɵ�����С�ļ���������Web������������֯��ȡ������Amazon�������ĵ��������������������Щ��Դ���������й����ϵͳ����֯���ԴӸ��ֲ���ϵͳ����Դ���ã��ڴ桢CPU���洢�ȣ���ѡ�����ʺ�ÿ���������ص�Ӧ�ó��������ļ���Amazon EC2�ṩ��һ��������������㻷����������֯ʹ�ø��ֲ���ϵͳ����������Դ��ʹ���Զ���Ӧ�ó���������ǣ����ڱ�����ȫ���Ƶ�ͬʱ�����������Ȩ��

### aws lambda

  ��һ��������web������Ա����������ƽ̨������aws����Ϊ�����д��룬��Ϊ���ṩϸ���ȵĶ��۽ṹ��aws lambda��һ������Ķ�������������������Լ���aws������amazon ec2ʵ�������ṩ��aws������ʩ�ĸ߿����ԡ���ȫ�ԡ����ܺͿ���չ�� 

### �Զ�����

* Auto Scaling������֯����Ϊ�ض��������ض���������Զ����ϻ�������չAmazon EC2��������ͼ1.3�������������԰���ά��Ӧ�ó�������Բ�ȷ������������Amazon EC2ʵ���������У�����Ҳ������Դ������չ�����㶯̬�������ص�������֯�����Ż��ɱ���������Ϊ��ֵ�����ṩ��Դ��ֻʹ��ʵ����Ҫ��������

* �Զ������ǳ��ʺ��ھ����ȶ�����ģʽ��Ӧ�ó���Ҳ�ʺ�����ʹ��������ÿСʱ��ÿ���ÿ�ܱ仯��Ӧ�ó��� 

### ���Ը��ؾ���

* ���Ը���ƽ�������п���Amazon EC2ʵ���Զ����䴫���Ӧ�ó�����������ʹ��֯�ܹ�����Ӧ�ó�����ʵ�ָ��߼�����ݴ��޷���ṩ����Ӧ�ó�����������ĸ���ƽ��������

### AWS Elastic Beanstalk 

* AWS Elastic Beanstalk����AWS������������WebӦ�ó����������򵥵ķ�ʽ��������Աֻ���ϴ����ǵ�Ӧ�ó�����룬�÷���ͻ��Զ���������ϸ�ڣ�����Դ���á�����ƽ�⡢�Զ���������Ϊ����ƽ̨�ṩ֧�֣�����php��java��python��ruby��node.js��.net��go��ʹ��aws����beanstalk����֯������ȫ����ΪӦ�ó����ṩ������aws��Դ����������ʱ���ʵײ���Դ��

### Amazon����˽���ƣ�Amazon VPC��

* amazon����˽���ƣ�amazon vpc��������֯�ṩaws�Ƶ��߼����벿�֣����������ǿ������Լ��������������������aws��Դ����֯������ȫ�������⻷��������ѡ��ip��ַ��Χ�������������Լ�·�ɱ�����ú��������ء����⣬��֯����ʹ��Ӳ�����������ר������VPN�����ӻ�ר�õ�·ʹ��AWSֱ�����ӽ��乫˾��������������չ��AWS

### AWS Direct Connect

* aws direct connect������֯���������������ĵ�aws��ר���������ӡ�ʹ��aws direct connect����֯������aws�����������ġ��칫�һ��йܻ���֮�佨��ר�����ӣ������������¿��Խ�������ɱ������Ӵ������������ṩ�Ȼ���Internet��VPN���Ӹ�һ�µ���������

### Amazon	Route	53 

* ����ѷRoute53��һ���߶ȿ��úͿ���չ������ϵͳ��DNS�������������Ŀ����ͨ��������ɶ������ƣ���www.example.com��ת��Ϊ����������໥���ӵ�����IP��ַ����192.0.2.1����Ϊ������Ա����ҵ�ṩһ�ּ���ɿ��;��ø�Ч�ķ�ʽ���������û�·�ɵ�InternetӦ�ó���������ֱ�Ӵ�aws����͹�����

### �洢�����ݷַ�

AWS�ṩ����������Ҫ�Ĵ洢�������磺Amazon�򵥴洢����Amzzon CloudFront��Amazon���Կ���񡣱��½�ֻ�Ǵ洢�����ݷַ�����ĸ�����

#### Amazon S3

* Amazon Simple Storage Service��Amazon S3��Ϊ������Ա��IT�Ŷ��ṩ�˸߶ȳ־úͿ���չ�Ķ���洢�����Դ����������������ݺʹ��������û�����֯���Դ洢�κ����͵Ķ�����HTMLҳ�桢Դ�����ļ���ͼ���ļ��ͼ������ݣ���ʹ�û���http��Э��������ǡ�amazon s3Ϊ���ָ����������ṩ���ø�Ч�Ķ���洢���������ݺͻָ������߹鵵�������ݷ��������ѻָ�����Ӧ�ó�������ݷַ���

#### Amazon Glacier

* Amazon Glacier��һ�ְ�ȫ�����á��ɱ����͵Ĵ洢�����������ݴ浵�ͳ��ڱ��ݡ���֯�����Էǳ��͵�ÿ��ÿGB�ɱ��ɿ��ش洢�������������ݡ�Ϊ��ʹ�ͻ��ĳɱ������ڽϵ�ˮƽ��AmazonGlacier��Բ������ʵ����ݽ������Ż�������������£�����ʱ���ʺϼ���Сʱ��AmazonS3��AmazonGlacier���ܼ��ɣ�������֯Ϊ�乤������ѡ����ȷ�Ĵ洢�� 

#### Amazon Elastic Block Storage��Amazon EBS��

* Amazon���Կ�洢��Amazon EBS��ΪAmazon EC2ʵ���ṩ�־õĿ鼶�洢��ÿ��Amazon EBS��������������Զ����ƣ��Ա�����֯����������ϵ�Ӱ�죬�ṩ�߿����Ժ������ԡ�ͨ���ṩһ�º͵��ӳٵ����ܣ�Amazon EBS�ṩ�����и��ֹ�����������Ĵ��̴洢��

#### AWS Storage Gateway

* AWS�洢������һ��ڲ�����豸������ƵĴ洢���������ķ��񣬿�����֯���ڲ�IT������AWS�洢������ʩ֮���ṩ�޷�Ͱ�ȫ�ļ��ɡ��÷���֧��������Ӧ�ó���һ��������ҵ��׼�洢Э�顣���ṩ�͹��ĵ�ͨ���ڱ���ά��Ƶ�����ʵ����ݵĻ��棬ͬʱ��AmazonS3��AmazonGlacie�а�ȫ�ش洢���ܵ��������ݣ��Ӷ������ȶ������ܡ�

#### AWS CloudFront

* amazon cloudfront��һ�����ݽ���web������������aws�Ʒ��񼯳ɣ�ʹ������Ա����ҵ�ܹ��Ե��ӳ١������ݴ����ٶȺ������ʹ�ó�ŵ�ķ�ʽ��ȫ���û��ַ����ݡ�Amazon CloudFront����ʹ�ñ�Եλ�õ�ȫ����������������������վ��������̬����̬����ʽ�ͽ���ʽ���ݡ������ݵ�������Զ�·�ɵ�����ı�Եλ�ã�������ݻ���������ܽ�����ȫ����ص������û�

### ���ݿ����

* aws�ṩ����ȫ�йܵĹ�ϵ���ݿ�����nosql���ݿ�����Լ���Ϊ������ڴ滺���PB�������ݲֿ�����������С�ڸ��������ݿ���������Щ��Ʒ��

#### Amazon RDS

* amazon��ϵ���ݿ����amazon rds���ṩ��һ����ȫ�йܵĹ�ϵ���ݿ⣬֧��������еĿ�Դ���������ݿ����档����һ�����ø�Ч�ķ���������֯������ȫ���߿��á��ݴ�����ݿ⡣�ڼ������ھͿ����������ݿ��ˡ�����amazon rds�����ʱ�Ĺ������񣬰������ݡ�����޲������ӡ���չ�͸��ƣ������֯��Դ���Լ����ڲ��������Ӧ�ó����ҵ�񣬶�������ͨ�Ĳ�������

#### Amazon	DynamoDB

* Amazon DYNAMODB��һ�ֿ�������NoSQL���ݿ�����������κι�ģ����Ҫһ�µġ����뼶�ӳٵ�����Ӧ�ó�������һ����ȫ�йܵ����ݿ⣬֧���ĵ��ͼ�/ֵ����ģ�͡�����������ģ�ͺͿɿ�������ʹ���ǳ��ʺ��ƶ���Web����Ϸ����漼�������������������Ӧ�á�

#### Amazon	Redshift

* Amazon Redshift��һ�����١���ȫ����PB�������ݲֿ������ʹ�����ṹ�����ݱ�ü��Ҿ��ø�Ч��Amazon Redshift�ṩ��һ����׼��SQL�ӿڣ�������֯ʹ�����е���ҵ���ܹ��ߡ�ͨ���������I/OЧ�ʺͿ����ڵ㲢�в�ѯ����״�洢������Amazon Redshift�ܹ��ṩ���ٵĲ�ѯ���ܡ�Amazon Redshift��ϵ�ṹ������֯�Զ�ִ�����ṩ�����úͼ��������ݲֿ���صĴ����������������

#### Amazon	ElastiCache 

* Amazon Elasticache��һ��Web���������������ڴ滺��Ĳ��𡢲�������չ���÷���������֯�ӿ��١��йܵ��ڴ滺���м�����Ϣ����������ȫ�����ٶȽ����Ļ��ڴ��̵����ݿ⣬�Ӷ������WebӦ�ó�������ܡ���׫д����ʱ��Amazon Elasticache֧��memcached��redis�������档

### ������

* AWS�ṩ���ֹ��ߣ�������ҵ�����Լ���AWS��Դ�����½ڸ�����AWS�ṩ����ҵ�Ĺ����ߡ�

#### Amazon CloudWatch

* amazon cloudwatch��һ�����aws����Դ��aws�����е�Ӧ�ó���ļ��ӷ�����������֯�ռ��͸��ٶ������ռ��ͼ�����־�ļ��Լ����þ�����ͨ������amazon cloudwatch����֯������ϵͳ��Χ���˽���Դ�����ʡ�Ӧ�ó������ܣ��Լ���Ӫ������ͨ��ʹ����Щ����������֯���Ը�����Ҫ������Ӧ���Ա���Ӧ�ó����ƽ�����С� 

#### AWS CloudFormation

* aws cloudformationΪ������Ա��ϵͳ����Ա�ṩ�˴����͹������aws��Դ���ϵ���Ч������������Ϳ�Ԥ��ķ�ʽ�ṩ�͸������ǡ�aws cloudformation������һ�ֻ���json��ģ�����ԣ����������������������������aws��Դ��ģ������ύ��aws cloudformation�����񽫸������ʵ���˳�����ú�������Щ��Դ���μ�ͼ1.4����

#### AWS CloudTrail

* aws cloudtrail��һ��web��������¼aws api��ĳ���ʻ��ĵ��ã����ṩ��־�ļ�����ƺ���顣��¼����Ϣ����api���÷�����ݡ�api���õ�ʱ�䡢api���÷���Դip��ַ����������ͷ��񷵻ص���ӦԪ�ء�

#### AWS Config

* aws config��һ����ȫ�йܵķ���������֯�ṩaws��Դ�嵥��������ʷ��¼�����ø���֪ͨ�������ð�ȫ�Ժ�����ʹ��aws config��֯���Է������е�aws��Դ��������������������ϸ��Ϣ��aws��Դ�嵥����ȷ����Դ���κ�ʱ�������÷�ʽ����Щ����֧�ֺϹ���ˡ���ȫ�Է�������Դ���ĸ��ٺ͹����ų� 


### ��ȫ�����

* aws�ṩ��ȫ����ݷ��񣬰�����֯�����ϱ������ǵ����ݺ�ϵͳ����һ�ڽ���һ���ϸߵȼ�������Щ����

#### AWS Identity and Access Management ��IAM)

* aws��ݺͷ��ʹ���IAM��ʹ��֯�ܹ���ȫ�ؿ������û���aws�Ʒ������Դ�ķ��ʡ�ʹ��IAM����֯���Դ����͹���aws�û����飬��ʹ��Ȩ������;ܾ����aws��Դ�ķ��ʡ�

#### AWS Key Management Service(KMS)

* aws��Կ�������kms����һ���йܷ�����ʹ��֯�ܹ����ɴ����Ϳ������ڼ��������ݵļ�����Կ����ʹ��Ӳ����ȫģ�飨hsms��������Կ�İ�ȫ�ԡ�aws kms����������aws�Ʒ��񼯳ɣ��԰�����������Щ����һ��洢�����ݡ�

#### AWS Directory Service

* AWSĿ¼����������֯��AWS�������ú�����Microsoft Active Directory������AWS��Դ���ӵ����е��ڲ�����Microsoft Active Directory����֯����ʹ�����������û����顢�ṩ��Ӧ�ó���ͷ���ĵ����¼��������Ӧ������ԣ������amazon ec2ʵ�����򻯻����Ƶ�linux��microsoft windows�������صĲ���͹���


#### AWS Certificate Manager

* aws֤���������һ�ַ���������֯���ɵ����á�����Ͳ���ȫ�׽��ֲ�/����㰲ȫ��ssl/tls��֤�飬�Ա���aws�Ʒ���һ��ʹ�á��������˹������غ�����ssl/tls֤��ĺ�ʱ���ֶ����̡�ʹ��aws֤�����������֯���Կ�������֤�飬���䲿��aws��Դ���絯�Ը���ƽ���amazon cloudfront���а棩�ϣ�����aws֤�����������֤��������

#### AWS Web Application Firewall (WAF)

* AWS WebӦ�ó������ǽ��WAF�������ڱ���WebӦ�ó������ܿ���Ӱ��Ӧ�ó�������ԡ�Σ����ȫ�Ի����Ĺ�����Դ�ĳ������������á�AWS WAFͨ��������Զ����Web��ȫ����ʹ��֯�ܹ������������ֹ��Щͨ��������WebӦ�ó���


