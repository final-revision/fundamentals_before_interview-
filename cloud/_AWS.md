# AWS + Cloud Fundamentals --- Fresher Interview Questions & Answers

A practical interview-preparation guide covering the **fundamentals of
cloud computing and AWS** that every fresher should know.

------------------------------------------------------------------------

## 1. Cloud Computing Fundamentals

### Q1. What is Cloud Computing?

**Answer:** Cloud computing is the delivery of computing resources such
as servers, storage, databases, networking, and software over the
internet on demand. Instead of purchasing and maintaining physical
infrastructure, organizations can use cloud resources and pay according
to usage.

### Q2. Why do companies use Cloud Computing?

**Answer:** - Reduces infrastructure cost - Provides scalability -
Enables faster deployment - Improves availability and reliability -
Provides global access - Reduces the need to maintain physical servers -
Supports backup and disaster recovery

### Q3. What are the main characteristics of Cloud Computing?

**Answer:** 1. On-demand self-service 2. Broad network access 3.
Resource pooling 4. Rapid elasticity 5. Measured service

### Q4. What is scalability?

**Answer:** Scalability is the ability of a system to handle increased
workload by increasing available resources.

**Example:** Increasing the CPU and RAM of a server when traffic
increases.

### Q5. What is elasticity?

**Answer:** Elasticity is the ability to automatically add or remove
resources according to workload demand.

**Simple difference:** - **Scalability:** ability to grow -
**Elasticity:** automatically grow and shrink as demand changes

### Q6. What is high availability?

**Answer:** High availability means designing a system so that it
remains operational with minimal downtime, even when some components
fail.

### Q7. What is fault tolerance?

**Answer:** Fault tolerance is the ability of a system to continue
operating even when one or more components fail.

### Q8. What is a data center?

**Answer:** A data center is a physical facility containing servers,
storage systems, networking equipment, power systems, and cooling
infrastructure used to run IT workloads.

### Q9. What is virtualization?

**Answer:** Virtualization is the technology of creating virtual
versions of computing resources such as servers, operating systems,
storage, or networks using software.

### Q10. What is a Virtual Machine (VM)?

**Answer:** A VM is a software-based computer that runs an operating
system and applications using virtualized hardware resources.

### Q11. What is a container?

**Answer:** A container packages an application and its dependencies
into an isolated, lightweight environment that can run consistently
across systems.

### Q12. VM vs Container?

**Answer:**

  VM                             Container
  ------------------------------ ---------------------------
  Includes a complete guest OS   Shares the host OS kernel
  Heavier                        Lightweight
  Slower startup                 Fast startup
  More resource usage            Less resource usage
  Strong isolation               Process-level isolation

------------------------------------------------------------------------

# 2. Cloud Service Models

### Q13. What are IaaS, PaaS, and SaaS?

**Answer:**

**IaaS --- Infrastructure as a Service:** Provides virtual
infrastructure such as servers, storage, and networking.

**PaaS --- Platform as a Service:** Provides a platform for developers
to build and deploy applications without managing the underlying
infrastructure.

**SaaS --- Software as a Service:** Provides complete software
applications over the internet.

### Q14. Give examples of IaaS, PaaS, and SaaS.

**Answer:** - **IaaS:** AWS EC2 - **PaaS:** AWS Elastic Beanstalk -
**SaaS:** Gmail, Microsoft 365, Salesforce

### Q15. What is the difference between IaaS and PaaS?

**Answer:** With IaaS, the customer manages more of the infrastructure
and operating system. With PaaS, the cloud provider manages more of the
underlying platform so developers can focus mainly on application code.

### Q16. What is the difference between SaaS and PaaS?

**Answer:** SaaS is ready-to-use software for end users, while PaaS is a
development and deployment platform for developers.

------------------------------------------------------------------------

# 3. Cloud Deployment Models

### Q17. What is a Public Cloud?

**Answer:** A public cloud is infrastructure operated by a cloud
provider and shared among multiple customers using logical isolation.

**Examples:** AWS, Microsoft Azure, Google Cloud.

### Q18. What is a Private Cloud?

**Answer:** A private cloud is cloud infrastructure dedicated to a
single organization.

### Q19. What is a Hybrid Cloud?

**Answer:** Hybrid cloud combines private infrastructure with public
cloud services, allowing workloads or data to operate across both
environments.

### Q20. What is a Multi-Cloud strategy?

**Answer:** Multi-cloud means using cloud services from multiple cloud
providers, such as AWS and Azure, rather than depending on only one
provider.

------------------------------------------------------------------------

# 4. AWS Fundamentals

### Q21. What is AWS?

**Answer:** AWS (Amazon Web Services) is a cloud platform that provides
a large collection of services for computing, storage, databases,
networking, security, analytics, AI/ML, monitoring, and more.

### Q22. Why is AWS popular?

**Answer:** - Large number of cloud services - Global infrastructure -
Flexible pricing - Scalability - High availability options - Strong
security features - Extensive ecosystem - Large developer and job market

### Q23. What is an AWS Region?

**Answer:** An AWS Region is a geographical area containing multiple
isolated data-center locations called Availability Zones.

**Example:** Mumbai is an AWS Region in India.

### Q24. What is an Availability Zone (AZ)?

**Answer:** An Availability Zone is an isolated location within an AWS
Region. A Region normally contains multiple AZs to improve availability
and fault tolerance.

### Q25. Region vs Availability Zone?

**Answer:** - **Region:** geographical area - **Availability Zone:**
isolated infrastructure location inside a Region

### Q26. Why does AWS have multiple Regions?

**Answer:** - Reduce latency for users - Meet data residency
requirements - Improve disaster recovery - Provide geographical
redundancy - Support global applications

### Q27. What is an Edge Location?

**Answer:** An edge location is an AWS point of presence used by
services such as Amazon CloudFront to deliver content closer to end
users.

------------------------------------------------------------------------

# 5. AWS Core Services

## EC2

### Q28. What is Amazon EC2?

**Answer:** Amazon EC2 (Elastic Compute Cloud) provides resizable
virtual servers called instances in the AWS cloud.

### Q29. What is an EC2 instance?

**Answer:** An EC2 instance is a virtual server running in AWS. It can
be configured with a selected CPU, memory, storage, networking, and
operating system.

### Q30. What is an AMI?

**Answer:** AMI stands for Amazon Machine Image. It is a template
containing the information required to launch an EC2 instance, including
the operating system and software configuration.

### Q31. What is an EC2 instance type?

**Answer:** An instance type defines the hardware characteristics
available to an EC2 instance, such as CPU, memory, networking, and
sometimes specialized accelerators.

### Q32. What is a Security Group?

**Answer:** A Security Group is a virtual firewall associated with AWS
resources such as EC2 instances. It controls inbound and outbound
network traffic using rules.

### Q33. Are Security Groups stateful or stateless?

**Answer:** Security Groups are **stateful**. If inbound traffic is
allowed, the corresponding response traffic is automatically allowed.

### Q34. What is an Elastic IP?

**Answer:** An Elastic IP is a static public IPv4 address that can be
associated with an AWS resource such as an EC2 instance.

------------------------------------------------------------------------

# 6. AWS Storage

### Q35. What is Amazon S3?

**Answer:** Amazon S3 (Simple Storage Service) is an object storage
service used to store and retrieve files and other objects at scale.

### Q36. What is an S3 bucket?

**Answer:** An S3 bucket is a logical container in which objects are
stored.

### Q37. What is an S3 object?

**Answer:** An object is the actual data stored in S3 along with
metadata and a unique key.

### Q38. What are common uses of S3?

**Answer:** - File storage - Backup - Static website assets - Logs -
Data lakes - Media storage - Application-generated files

### Q39. S3 vs EBS?

**Answer:** - **S3:** object storage accessed through APIs - **EBS:**
block storage designed primarily for use with EC2 instances

### Q40. What is EBS?

**Answer:** Amazon Elastic Block Store (EBS) provides persistent block
storage volumes for EC2 instances.

### Q41. What is EFS?

**Answer:** Amazon Elastic File System (EFS) provides scalable shared
file storage that can be mounted by multiple compute resources.

------------------------------------------------------------------------

# 7. AWS Databases

### Q42. What is Amazon RDS?

**Answer:** Amazon RDS (Relational Database Service) is a managed
service for relational databases. AWS handles many administrative tasks
such as provisioning, backups, patching, and infrastructure management.

### Q43. What databases can RDS support?

**Answer:** Depending on AWS's currently supported engines, RDS can
support engines such as PostgreSQL, MySQL, MariaDB, Oracle, SQL Server,
and Amazon Aurora.

### Q44. What is Amazon DynamoDB?

**Answer:** DynamoDB is a fully managed NoSQL database designed for
low-latency performance and automatic scaling.

### Q45. RDS vs DynamoDB?

**Answer:** - **RDS:** relational, SQL-based, structured schema -
**DynamoDB:** NoSQL, key-value/document model, highly scalable

------------------------------------------------------------------------

# 8. AWS Networking

### Q46. What is Amazon VPC?

**Answer:** Amazon VPC (Virtual Private Cloud) lets you create a
logically isolated virtual network in AWS where you can launch resources
and control networking.

### Q47. What is a subnet?

**Answer:** A subnet is a range of IP addresses within a VPC. Subnets
are associated with a specific Availability Zone.

### Q48. What is a public subnet?

**Answer:** A subnet is considered public when its routing configuration
provides a path to an Internet Gateway.

### Q49. What is a private subnet?

**Answer:** A private subnet does not have a direct route to an Internet
Gateway for its resources. It is commonly used for internal application
servers and databases.

### Q50. What is an Internet Gateway?

**Answer:** An Internet Gateway is a VPC component that enables
communication between resources in a VPC and the internet when routing
and security rules allow it.

### Q51. What is a Route Table?

**Answer:** A route table contains rules that determine where network
traffic from a subnet or network interface should be directed.

### Q52. What is NAT Gateway?

**Answer:** A NAT Gateway allows resources in a private subnet to
initiate outbound connections to the internet while preventing
unsolicited inbound internet connections to those resources.

### Q53. What is a Load Balancer?

**Answer:** A load balancer distributes incoming traffic across multiple
targets such as EC2 instances.

### Q54. What is Elastic Load Balancing (ELB)?

**Answer:** Elastic Load Balancing is AWS's managed load-balancing
service family. Common types include Application Load Balancer, Network
Load Balancer, and Gateway Load Balancer.

------------------------------------------------------------------------

# 9. AWS IAM and Security

### Q55. What is IAM?

**Answer:** IAM (Identity and Access Management) controls who can access
AWS resources and what actions they are allowed to perform.

### Q56. What is an IAM User?

**Answer:** An IAM user represents an identity that can have credentials
and permissions for interacting with AWS resources.

### Q57. What is an IAM Group?

**Answer:** An IAM group is a collection of IAM users to which
permissions can be assigned through policies.

### Q58. What is an IAM Role?

**Answer:** An IAM role is an identity with permissions that can be
assumed by trusted entities, such as AWS services, applications, or
users.

### Q59. What is an IAM Policy?

**Answer:** An IAM policy is a document that defines permissions,
specifying which actions are allowed or denied on which resources under
particular conditions.

### Q60. What is the Principle of Least Privilege?

**Answer:** Give a user, application, or service only the permissions it
actually needs to perform its task.

### Q61. What is MFA?

**Answer:** Multi-Factor Authentication adds an additional verification
factor beyond a password or access key, improving account security.

### Q62. IAM User vs IAM Role?

**Answer:** - **User:** represents a persistent identity - **Role:**
provides temporary credentials when assumed by a trusted entity

------------------------------------------------------------------------

# 10. AWS Serverless and Application Services

### Q63. What is AWS Lambda?

**Answer:** AWS Lambda is a serverless compute service that runs code in
response to events without requiring the user to manage servers.

### Q64. What is serverless computing?

**Answer:** Serverless computing means the cloud provider manages the
underlying server infrastructure while developers focus on application
code. Servers still exist, but their management is abstracted away.

### Q65. What is Amazon API Gateway?

**Answer:** API Gateway is a managed service for creating, publishing,
securing, monitoring, and managing APIs.

### Q66. What is Amazon SQS?

**Answer:** Amazon Simple Queue Service (SQS) is a managed message
queuing service that helps decouple application components.

### Q67. What is Amazon SNS?

**Answer:** Amazon Simple Notification Service (SNS) is a managed
publish/subscribe messaging service used to send notifications and
distribute messages to subscribers or other systems.

### Q68. SQS vs SNS?

**Answer:** - **SQS:** message queue; consumers process messages from a
queue - **SNS:** publish/subscribe; one message can be delivered to
multiple subscribers

------------------------------------------------------------------------

# 11. AWS Monitoring and Management

### Q69. What is Amazon CloudWatch?

**Answer:** CloudWatch is an AWS monitoring and observability service
used for metrics, logs, alarms, and monitoring AWS resources and
applications.

### Q70. What is AWS CloudTrail?

**Answer:** CloudTrail records AWS API activity and account actions,
helping with auditing, security analysis, and troubleshooting.

### Q71. CloudWatch vs CloudTrail?

**Answer:** - **CloudWatch:** monitors performance, metrics, logs, and
alarms - **CloudTrail:** records API calls and account activity

### Q72. What is AWS CloudFormation?

**Answer:** CloudFormation is an infrastructure-as-code service used to
define and provision AWS resources through templates.

------------------------------------------------------------------------

# 12. AWS Pricing Fundamentals

### Q73. What is pay-as-you-go pricing?

**Answer:** Pay-as-you-go means you generally pay for the cloud
resources you consume rather than purchasing all infrastructure upfront.

### Q74. What are AWS Free Tier offerings?

**Answer:** AWS provides certain free usage allowances for eligible
services and accounts. Exact limits and eligibility can change, so
candidates should check current AWS documentation before relying on a
specific limit.

### Q75. What are Reserved Instances?

**Answer:** Reserved Instances are a pricing option that can provide
discounts compared with On-Demand pricing when you commit to specified
usage terms for eligible services such as EC2.

### Q76. What are Spot Instances?

**Answer:** Spot Instances use spare AWS compute capacity and can offer
significant discounts, but AWS can interrupt them when the capacity is
needed back.

### Q77. On-Demand vs Reserved vs Spot?

**Answer:**

  Option      Best for
  ----------- --------------------------------------------------------
  On-Demand   Flexible workloads with no long commitment
  Reserved    Predictable workloads requiring longer-term commitment
  Spot        Flexible, interruption-tolerant workloads

------------------------------------------------------------------------

# 13. AWS Architecture Concepts

### Q78. What is horizontal scaling?

**Answer:** Horizontal scaling means adding or removing multiple
instances to handle workload.

**Example:** Going from 2 EC2 instances to 5 EC2 instances.

### Q79. What is vertical scaling?

**Answer:** Vertical scaling means increasing or decreasing the
resources of an existing instance.

**Example:** Moving from a smaller EC2 instance type to a larger one.

### Q80. What is Auto Scaling?

**Answer:** Auto Scaling automatically adjusts compute capacity
according to demand, policies, health, or schedules.

### Q81. What is an Auto Scaling Group?

**Answer:** An Auto Scaling Group manages a collection of EC2 instances
and can automatically launch or terminate instances according to
configured rules.

### Q82. What is a highly available architecture?

**Answer:** It is an architecture designed to minimize downtime by
avoiding single points of failure and distributing workloads across
multiple failure domains.

### Q83. What is a single point of failure?

**Answer:** A single point of failure is a component whose failure can
cause the entire system or a critical part of it to become unavailable.

### Q84. What is disaster recovery?

**Answer:** Disaster recovery is the process and architecture used to
restore applications and data after a major failure or disaster.

------------------------------------------------------------------------

# 14. AWS DevOps Basics

### Q85. What is DevOps?

**Answer:** DevOps is a set of practices and a culture that brings
development and operations closer together to automate and improve
software delivery, reliability, and collaboration.

### Q86. What is CI/CD?

**Answer:** - **CI --- Continuous Integration:** Frequently integrate
and test code changes. - **CD --- Continuous Delivery/Deployment:**
Automate the process of preparing or deploying software releases.

### Q87. What is Infrastructure as Code (IaC)?

**Answer:** IaC means defining infrastructure using code or
configuration files instead of manually creating resources.

**AWS example:** CloudFormation or AWS CDK.

### Q88. What is AWS CodePipeline?

**Answer:** AWS CodePipeline is a service for automating software
release workflows and connecting stages such as source, build, test, and
deployment.

------------------------------------------------------------------------

# 15. Important Cloud Interview Concepts

### Q89. What is multi-tenancy?

**Answer:** Multi-tenancy means multiple customers share underlying
cloud infrastructure while logical isolation keeps their resources and
data separated.

### Q90. What is vendor lock-in?

**Answer:** Vendor lock-in occurs when moving an application, workload,
or data from one cloud provider to another becomes difficult or
expensive because of provider-specific technologies or dependencies.

### Q91. What is latency?

**Answer:** Latency is the time taken for data or a request to travel
between two points.

### Q92. What is bandwidth?

**Answer:** Bandwidth is the amount of data that can be transferred over
a network in a given period.

### Q93. What is an API?

**Answer:** An API (Application Programming Interface) is a defined
interface that allows software systems to communicate with each other.

### Q94. What is an endpoint?

**Answer:** An endpoint is a specific network address or API location
through which a service can be accessed.

### Q95. What is a CDN?

**Answer:** A Content Delivery Network distributes cached content
through geographically distributed edge locations so users can receive
content from a location closer to them.

### Q96. What is caching?

**Answer:** Caching stores frequently accessed data in a faster storage
layer so that future requests can be served more quickly.

------------------------------------------------------------------------

# 16. Scenario-Based Fresher Questions

### Q97. Your website suddenly receives 10x traffic. What would you do?

**Answer:** 1. Put the application behind a load balancer. 2. Use Auto
Scaling to add compute instances. 3. Monitor CPU, memory, latency, and
request metrics. 4. Use caching where appropriate. 5. Check database
capacity and scaling options. 6. Review logs and errors using monitoring
tools.

### Q98. Your EC2 instance is unreachable. What would you check?

**Answer:** 1. Instance state 2. Security Group rules 3. Network ACLs 4.
Route table 5. Internet Gateway or NAT configuration 6. Public/private
IP configuration 7. Operating-system firewall 8. Application/service
status 9. CPU and memory conditions

### Q99. Your application needs to store images uploaded by users. Which AWS service would you consider?

**Answer:** Amazon S3 is a common choice because it is designed for
scalable object storage.

### Q100. Your application has a frontend, backend, and database. How could you design it on AWS?

**Answer:** A basic architecture could use: - **Frontend:** S3 +
CloudFront - **Backend:** EC2, containers, or Lambda depending on
requirements - **Database:** RDS or DynamoDB depending on the data
model - **Networking:** VPC - **Security:** IAM + Security Groups -
**Monitoring:** CloudWatch - **DNS:** Route 53

### Q101. How would you secure an AWS application?

**Answer:** - Apply least-privilege IAM policies - Enable MFA for
appropriate identities - Avoid exposing databases directly to the
internet - Use private subnets where appropriate - Restrict Security
Group rules - Encrypt sensitive data - Monitor API activity with
CloudTrail - Monitor resources with CloudWatch - Regularly review
permissions and security configuration

### Q102. How would you reduce AWS cost?

**Answer:** - Remove unused resources - Right-size compute resources -
Use appropriate purchasing models - Use lifecycle policies for storage -
Monitor resource usage - Use Auto Scaling - Select appropriate storage
classes - Set budgets and cost alerts - Review architecture for
unnecessary data transfer and compute

------------------------------------------------------------------------

# 17. Most Important AWS Services to Remember

For fresher interviews, understand the **purpose** of these services
rather than trying to memorize every AWS service.

  Service          What it does
  ---------------- --------------------------------
  EC2              Virtual servers
  S3               Object storage
  EBS              Block storage
  EFS              Shared file storage
  RDS              Managed relational databases
  DynamoDB         Managed NoSQL database
  VPC              Virtual networking
  IAM              Identity and access management
  Lambda           Serverless compute
  CloudWatch       Monitoring and observability
  CloudTrail       API/account activity auditing
  CloudFront       CDN
  Route 53         DNS and domain routing
  ELB              Load balancing
  Auto Scaling     Automatic capacity adjustment
  SQS              Message queue
  SNS              Pub/sub notifications
  CloudFormation   Infrastructure as Code
  API Gateway      API management

------------------------------------------------------------------------

# 18. Quick Revision --- One-Line Answers

### What is Cloud?

Using computing resources over a network on demand.

### What is AWS?

Amazon's cloud computing platform.

### What is EC2?

A service for running virtual servers.

### What is S3?

Object storage.

### What is RDS?

Managed relational database service.

### What is DynamoDB?

Managed NoSQL database service.

### What is VPC?

A logically isolated virtual network in AWS.

### What is IAM?

AWS identity and permission management.

### What is Lambda?

Serverless code execution.

### What is CloudWatch?

Monitoring and observability.

### What is CloudTrail?

AWS API/account activity auditing.

### What is CloudFront?

A content delivery network.

### What is Route 53?

AWS DNS and domain routing service.

### What is a Region?

A geographical AWS infrastructure area.

### What is an Availability Zone?

An isolated location within an AWS Region.

### What is a Security Group?

A stateful virtual firewall for AWS resources.

### What is a Load Balancer?

A service that distributes traffic across targets.

### What is Auto Scaling?

Automatic adjustment of compute capacity.

### What is IaaS?

Infrastructure as a Service.

### What is PaaS?

Platform as a Service.

### What is SaaS?

Software as a Service.

------------------------------------------------------------------------

# 19. Fresher Interview Checklist

Before an AWS/cloud interview, make sure you can explain these without
memorizing definitions word-for-word:

-   [ ] What is cloud computing?
-   [ ] Benefits of cloud
-   [ ] Scalability vs elasticity
-   [ ] Availability vs fault tolerance
-   [ ] IaaS vs PaaS vs SaaS
-   [ ] Public vs private vs hybrid cloud
-   [ ] Region vs Availability Zone
-   [ ] EC2
-   [ ] AMI
-   [ ] Security Groups
-   [ ] S3
-   [ ] EBS
-   [ ] RDS
-   [ ] DynamoDB
-   [ ] VPC
-   [ ] Subnet
-   [ ] Internet Gateway
-   [ ] NAT Gateway
-   [ ] Route Table
-   [ ] Load Balancer
-   [ ] Auto Scaling
-   [ ] IAM
-   [ ] IAM User vs Role
-   [ ] Least privilege
-   [ ] Lambda
-   [ ] SQS vs SNS
-   [ ] CloudWatch vs CloudTrail
-   [ ] CloudFront
-   [ ] Route 53
-   [ ] Basic AWS pricing models
-   [ ] Backup and disaster recovery
-   [ ] Basic cloud security
-   [ ] Basic CI/CD and IaC concepts

------------------------------------------------------------------------

# 20. Final Interview Tip

For fresher interviews, do not try to memorize hundreds of AWS services.

Focus on understanding:

**Cloud Fundamentals → AWS Global Infrastructure → Compute → Storage →
Database → Networking → Security → Monitoring → Scaling → Pricing →
Basic Architecture**

If you can explain these concepts in your own words and answer simple
scenario-based questions, you will have a strong foundation for
AWS/cloud interviews.
