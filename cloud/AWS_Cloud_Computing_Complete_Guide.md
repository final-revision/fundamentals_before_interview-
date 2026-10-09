# AWS Cloud Computing: Complete Fundamentals to Advanced Services

*A single study guide for learning AWS from the ground up*

> **Purpose:** Learn the core ideas behind cloud computing, understand
> the AWS services used most often, and develop the judgment needed to
> design, secure, deploy, monitor, and discuss real applications.
>
> **How to study:** Read Sections 1--8 first. Then study the service
> families, architecture patterns, practical labs, interview questions,
> and glossary. Do the labs in an AWS account only after setting billing
> alerts and using the Free Tier/Free Plan details currently shown in
> your account. AWS pricing and free offers change, so always verify
> them before creating resources.

------------------------------------------------------------------------

## Contents

1.  Cloud computing fundamentals
2.  AWS global infrastructure and account structure
3.  Identity, security, and shared responsibility
4.  Networking fundamentals and Amazon VPC
5.  Compute services
6.  Storage services
7.  Databases and caching
8.  Application integration and messaging
9.  Containers and serverless
10. Data, analytics, AI, and machine learning
11. Monitoring, logging, auditing, and operations
12. Infrastructure as Code and developer tools
13. High availability, disaster recovery, and reliability
14. Security architecture and common mistakes
15. Cost management and optimization
16. A practical architecture walkthrough
17. Hands-on learning roadmap
18. Interview questions with answers
19. Glossary and quick revision sheet

------------------------------------------------------------------------

# 1. Cloud Computing Fundamentals

## 1.1 What is cloud computing?

Cloud computing is the on-demand delivery of computing resources---such
as servers, storage, databases, networking, analytics, and AI---over a
network, usually the internet. Instead of purchasing and maintaining all
hardware yourself, you provision resources from a cloud provider and pay
according to the pricing model.

**Example:** Suppose you build a job portal. Traditionally, you might
purchase a physical server, install an operating system, configure
networking, maintain hardware, and plan for peak traffic. In AWS, you
could run the backend on Amazon EC2, store uploaded resumes in Amazon
S3, use Amazon RDS for a relational database, and use Amazon CloudFront
to distribute static files.

## 1.2 Why organizations use cloud

-   **Speed:** Create infrastructure in minutes rather than waiting for
    hardware procurement.
-   **Elasticity:** Add or remove resources as demand changes.
-   **Pay-as-you-go:** Pay for measured usage rather than owning all
    capacity upfront.
-   **Global reach:** Deploy in multiple geographic regions.
-   **Managed services:** Let AWS operate parts of the infrastructure.
-   **Resilience options:** Design across Availability Zones and
    regions.
-   **Automation:** Re-create infrastructure through templates and APIs.

Cloud does not automatically mean cheap, secure, or highly available.
Those outcomes depend on architecture, configuration, monitoring, and
operational discipline.

## 1.3 Cloud service models

### IaaS --- Infrastructure as a Service

You manage more of the software stack, while the provider manages
physical infrastructure.

**AWS example:** Amazon EC2 virtual machines. You generally manage the
guest operating system, installed packages, application, and much of the
configuration.

### PaaS --- Platform as a Service

The provider manages more of the platform so you can focus on deploying
code.

**AWS examples:** AWS Elastic Beanstalk provides an application
deployment and environment-management experience; Amazon RDS manages
many database administration tasks. These services still require
configuration and operational responsibility.

### SaaS --- Software as a Service

You use a complete application managed by its provider.

**General examples:** Email, online office suites, and customer
relationship management applications. AWS itself also offers SaaS-like
services, but the key idea is that you consume a finished application
rather than manage its underlying stack.

### Serverless

Serverless means the provider manages server provisioning and much of
the scaling/availability work. It does **not** mean servers do not
exist, nor does it mean applications have no operational concerns.

**AWS examples:** AWS Lambda, Amazon DynamoDB on-demand capacity, Amazon
S3, and Amazon API Gateway.

## 1.4 Deployment models

-   **Public cloud:** Resources run on a cloud provider's
    infrastructure.
-   **Private cloud:** Cloud-like infrastructure dedicated to one
    organization.
-   **Hybrid cloud:** Connects on-premises infrastructure and cloud
    resources.
-   **Multi-cloud:** Uses services from multiple cloud providers.

These models describe where or across which environments workloads run;
IaaS/PaaS/SaaS describe how services are consumed.

## 1.5 Scalability vs. elasticity

-   **Scalability:** Ability to handle growth by increasing capacity.
-   **Vertical scaling (scale up/down):** Change the size of one
    machine, for example use a larger EC2 instance.
-   **Horizontal scaling (scale out/in):** Add or remove instances,
    containers, or function executions.
-   **Elasticity:** Automatically or dynamically match capacity to
    demand.

Horizontal scaling often improves resilience, but the application must
be designed for it. For example, local files stored on one instance may
not be available to other instances.

## 1.6 High availability, fault tolerance, and disaster recovery

-   **High availability (HA):** Reduce downtime, often by distributing
    components across failure domains.
-   **Fault tolerance:** Continue operating through certain failures
    with little or no interruption.
-   **Disaster recovery (DR):** Restore service after a major
    disruption.
-   **Backup:** A recoverable copy of data; a backup alone does not
    guarantee a quick recovery.
-   **Business continuity:** The broader plan for continuing critical
    operations.

## 1.7 CapEx and OpEx

-   **CapEx:** Upfront capital expenditure, such as purchasing physical
    servers.
-   **OpEx:** Operating expenditure, such as ongoing cloud usage
    charges.

Cloud shifts many costs toward operating expenditure, but organizations
still need budgets, forecasts, tagging, and cost controls.

## 1.8 Shared responsibility model

AWS is responsible for **security of the cloud**---the physical
facilities, hardware, foundational networking, and underlying
infrastructure that AWS operates.

Customers are responsible for **security in the cloud**---including
identities and permissions, data classification, network configuration,
application security, and guest operating systems where applicable.

The exact split changes by service. With EC2, the customer manages the
guest OS and installed software. With a managed service such as
DynamoDB, AWS manages much more of the underlying infrastructure, while
the customer still controls access, data, and configuration.

**Memory aid:** AWS protects the infrastructure it operates; you protect
your workloads, data, identities, and configuration within it.

------------------------------------------------------------------------

# 2. AWS Global Infrastructure and Account Structure

## 2.1 Regions

An AWS Region is a separate geographic area containing multiple
Availability Zones. Choose a Region based on latency to users, service
availability, legal/data-residency requirements, resilience needs, and
cost.

A Region is not simply a billing label. Resources are often regional: a
VPC, RDS database, or Lambda function is created in a particular Region.
Some services and features have different regional availability.

## 2.2 Availability Zones (AZs)

An Availability Zone is an isolated location within a Region, made up of
one or more data centers with independent infrastructure. AZs are
designed to reduce the chance that one localized failure affects all
zones.

For production workloads, distribute suitable components across multiple
AZs. Two subnets in different AZs are not the same as two Regions.

## 2.3 Edge locations and Points of Presence

AWS operates edge infrastructure that can bring content or network
services closer to users. Amazon CloudFront uses a global edge network
to cache and deliver content. Route 53 provides DNS services. AWS Global
Accelerator uses the AWS global network to improve access to
applications.

An edge location is not a replacement for choosing the correct Region
for compute and data.

## 2.4 Region vs. AZ vs. edge location

  -----------------------------------------------------------------------
  Concept                 Main purpose            Example use
  ----------------------- ----------------------- -----------------------
  Region                  Geographic deployment   Host an application
                          boundary                near its users

  Availability Zone       Isolated failure domain Run redundant
                          inside a Region         app/database components

  Edge location           Serve content or        Cache website images
                          network traffic closer  through CloudFront
                          to users                
  -----------------------------------------------------------------------

## 2.5 AWS account, organization, and organizational units

An **AWS account** is a resource and security boundary with its own
identities/configuration, quotas, and billing context. An **AWS
Organization** can centrally manage multiple accounts. Organizational
Units (OUs) group accounts, such as production, development, and
security.

A common setup separates: - Management account for organization-level
management (avoid using it for ordinary workloads). -
Security/log-archive accounts for security tooling and centralized
logs. - Development/test accounts. - Production accounts.

Use separate accounts to limit blast radius and simplify governance. Do
not treat separate accounts as a substitute for proper IAM policies.

## 2.6 Resource naming and tagging

Use consistent names and tags such as `Project`, `Environment`, `Owner`,
`CostCenter`, and `DataClassification`. Tags support cost allocation,
inventory, automation, and ownership. Not every AWS resource supports
every tag operation, so verify service-specific behavior.

## 2.7 AWS Console, CLI, SDKs, and APIs

-   **AWS Management Console:** Browser-based interface.
-   **AWS CLI:** Command-line interface for scripts and operations.
-   **AWS SDKs:** Libraries for applications written in languages such
    as Python, JavaScript, Java, and C#.
-   **AWS APIs:** Programmatic operations exposed by services.

Prefer temporary credentials and IAM roles over embedding long-lived
access keys in source code.

------------------------------------------------------------------------

# 3. Identity, Security, and Shared Responsibility

## 3.1 IAM: users, groups, roles, and policies

AWS Identity and Access Management (IAM) controls who can do what.

-   **IAM user:** An identity that can have long-term credentials. Avoid
    creating long-lived users for workloads when roles are suitable.
-   **IAM group:** Organizes IAM users and can have policies attached.
-   **IAM role:** An identity with permissions that can be assumed by a
    trusted principal or AWS service. It provides temporary credentials.
-   **IAM policy:** A JSON document defining allowed or denied actions
    on resources, optionally under conditions.
-   **Principal:** The identity making a request.
-   **Resource:** The AWS object being accessed.
-   **Action:** The operation, such as `s3:GetObject`.
-   **Condition:** Additional constraints, such as source network, tags,
    or encryption requirements.

## 3.2 Least privilege

Grant only the permissions required for a task, to the smallest
appropriate set of resources, for the necessary duration.

Bad practice: give every developer and application administrator access
to everything.

Better practice: 1. Start with the specific actions needed. 2. Restrict
resources using resource ARNs where supported. 3. Add conditions when
useful. 4. Test the workflow. 5. Review permissions regularly and remove
unused access.

The `AdministratorAccess` managed policy is powerful and should not be a
default for applications.

## 3.3 IAM policy evaluation basics

At a high level: 1. A request is evaluated against applicable
identity-based policies, resource-based policies, permissions
boundaries, session policies, service control policies, and other
relevant controls. 2. An explicit **Deny** overrides an Allow. 3. A
request must have an applicable Allow and must not be blocked by an
applicable Deny or other limiting control. 4. Cross-account access
usually requires the appropriate permissions on both sides, depending on
the service and access pattern.

Do not assume that attaching one Allow policy always guarantees access.

## 3.4 IAM roles for AWS services

For example, an EC2 application needs to read objects from a specific S3
bucket. Create an IAM role trusted by EC2 and attach a policy that
grants only the required S3 actions. Attach the role to the instance.
The application receives temporary credentials without a hard-coded
access key.

Similarly, Lambda functions can use execution roles, and GitHub Actions
or other external systems can use federation (often OIDC) to assume
roles without storing permanent AWS access keys.

## 3.5 Root user

The root user is the original identity for an AWS account and has
extensive privileges. Secure it with multi-factor authentication (MFA),
protect recovery methods, avoid using it for routine work, and do not
create root access keys. Use IAM roles or administrative identities for
normal administration.

## 3.6 Authentication vs. authorization

-   **Authentication:** Who are you?
-   **Authorization:** What are you allowed to do?

MFA strengthens authentication. IAM policies primarily control
authorization.

## 3.7 Encryption

-   **Encryption in transit:** Protects data moving across a network,
    commonly using TLS/HTTPS.
-   **Encryption at rest:** Protects stored data, for example S3 objects
    or EBS volumes.
-   **AWS Key Management Service (KMS):** Creates and manages
    cryptographic keys and integrates with many AWS services.
-   **AWS Certificate Manager (ACM):** Provisions and manages supported
    TLS certificates.
-   **Secrets Manager:** Stores and can rotate secrets such as database
    credentials.
-   **Systems Manager Parameter Store:** Stores configuration values and
    can store encrypted values; Secrets Manager is often preferred when
    managed secret rotation is needed.

Encryption does not replace access control. A user with authorized
access to decrypt data may still read it.

## 3.8 Important security services

-   **AWS CloudTrail:** Records account/API activity for auditing and
    investigations.
-   **Amazon GuardDuty:** Detects potential threats using supported log
    and telemetry sources.
-   **AWS Security Hub:** Aggregates and prioritizes security findings
    and checks across supported services and standards.
-   **Amazon Inspector:** Helps identify certain software
    vulnerabilities and unintended exposure in supported workloads.
-   **AWS WAF:** Filters web requests using rules.
-   **AWS Shield:** Provides DDoS protection, with different
    levels/capabilities.
-   **Amazon Macie:** Helps discover and protect sensitive data in
    Amazon S3.
-   **AWS Config:** Tracks resource configuration and evaluates it
    against rules.
-   **IAM Access Analyzer:** Helps identify external access and validate
    policies.

Use these tools as part of a security program; enabling a service does
not mean every risk is automatically solved.

------------------------------------------------------------------------

# 4. Networking Fundamentals and Amazon VPC

Networking is one of the most important AWS topics. Understand the
purpose of each component rather than memorizing names.

## 4.1 IP addresses, CIDR, and subnetting

An IP address identifies a network interface. IPv4 addresses have 32
bits. CIDR notation expresses a network range, such as `10.0.0.0/16`.

-   `10.0.0.0/16` contains a much larger range than `10.0.1.0/24`.
-   A `/24` IPv4 network has 256 total addresses before AWS-specific
    subnet reservations.
-   AWS reserves some IPv4 addresses in each subnet, so the usable count
    is lower than the total.

Plan non-overlapping ranges for VPCs, on-premises networks, VPNs, and
peered networks.

## 4.2 VPC

An Amazon Virtual Private Cloud (VPC) is a logically isolated virtual
network for your AWS resources in a Region. You define IP ranges,
subnets, route tables, gateways, and network controls.

A VPC spans multiple AZs, but each subnet belongs to exactly one AZ.

## 4.3 Public and private subnets

A subnet is considered public when its associated route table provides a
route to an Internet Gateway for internet-bound traffic. A private
subnet generally has no direct route to an Internet Gateway.

A resource does **not** become publicly reachable just because it is in
a public subnet. Reachability also depends on public IP addressing,
route tables, security groups, network ACLs, and the application
listening on the expected port.

Typical design: - Public subnets: load balancers, NAT Gateways, or
resources that intentionally need direct internet connectivity. -
Private application subnets: backend EC2 instances or application
components. - Private database subnets: databases with no direct public
exposure.

## 4.4 Internet Gateway (IGW)

An Internet Gateway connects a VPC to the internet. It is attached to
the VPC, and route tables direct appropriate traffic to it. An IGW alone
does not make every resource public.

## 4.5 NAT Gateway

A NAT Gateway allows resources in a private subnet to initiate supported
outbound IPv4 connections to the internet without accepting unsolicited
inbound internet connections through that NAT path.

Example: a private application instance downloads operating-system
updates. Its route table sends internet-bound traffic to a NAT Gateway
in a public subnet; the NAT Gateway uses the Internet Gateway.

NAT Gateways incur charges. For resilience, design placement and routing
deliberately, often with a NAT Gateway per AZ for workloads that need
AZ-independent outbound access. Alternatives such as VPC endpoints may
avoid routing some traffic through NAT.

## 4.6 Route tables

Route tables determine where network traffic is directed. A route has a
destination range and a target, such as a local VPC route, IGW, NAT
Gateway, Transit Gateway, or VPC endpoint.

A subnet uses an associated route table. If no more-specific route
matches, the default route may apply. Routes alone do not override
security group or network ACL restrictions.

## 4.7 Security groups vs. network ACLs

  -----------------------------------------------------------------------
  Feature                 Security Group          Network ACL (NACL)
  ----------------------- ----------------------- -----------------------
  Applies to              Network                 Subnets
                          interfaces/resources    

  State                   Stateful                Stateless

  Rules                   Allow rules; no         Allow and deny rules
                          explicit deny rules     

  Return traffic          Automatically allowed   Must be allowed by the
                          when it belongs to an   appropriate
                          allowed connection      inbound/outbound rules

  Typical use             Main workload-level     Additional subnet-level
                          traffic control         traffic guardrail
  -----------------------------------------------------------------------

Example: an application security group allows inbound HTTPS (443) only
from the load balancer's security group. The database security group
allows its database port only from the application security group.

## 4.8 Load balancing

Elastic Load Balancing distributes incoming traffic across registered
targets.

-   **Application Load Balancer (ALB):** Layer 7 HTTP/HTTPS routing;
    useful for path/host routing and web apps.
-   **Network Load Balancer (NLB):** Layer 4 TCP/UDP/TLS use cases
    requiring high performance or specific network behavior.
-   **Gateway Load Balancer (GWLB):** Helps deploy and scale virtual
    network appliances.

Health checks help the load balancer avoid sending traffic to unhealthy
targets. A load balancer does not itself make a single-AZ backend highly
available.

## 4.9 DNS and Route 53

DNS maps domain names to records such as IP addresses or aliases. Amazon
Route 53 provides DNS hosting, domain registration capabilities, and
health-check/routing features.

A typical website flow: 1. User requests `example.com`. 2. DNS resolves
the name to the relevant endpoint. 3. CloudFront or a load balancer
receives the request. 4. The application processes the request and
returns a response.

DNS caching means a routing change may not be reflected instantly
everywhere.

## 4.10 VPC endpoints

VPC endpoints allow supported services to be accessed privately from a
VPC without requiring the traffic to use a public internet route.

-   **Gateway endpoints:** Commonly used for S3 and DynamoDB.
-   **Interface endpoints:** Use AWS PrivateLink and endpoint network
    interfaces for supported services.

They can improve network design and reduce NAT usage, but review
endpoint policies, security groups, DNS behavior, and service-specific
charges.

## 4.11 VPN, Direct Connect, peering, and Transit Gateway

-   **Site-to-Site VPN:** Encrypted connectivity between a network and
    AWS over the internet.
-   **AWS Direct Connect:** Dedicated network connectivity; not
    inherently encrypted by itself.
-   **VPC peering:** Private connectivity between two VPCs; it is not
    transitive.
-   **AWS Transit Gateway:** A hub for connecting many VPCs and
    networks.
-   **AWS PrivateLink:** Private access to supported services without
    exposing them through a public endpoint.

Choose based on topology, scale, routing needs, cost, and security
requirements.

## 4.12 IPv6 note

IPv6 uses a much larger address space and has different routing/security
considerations. Do not assume IPv4 NAT behavior applies identically to
IPv6. Configure IPv6 routes and security rules intentionally.

------------------------------------------------------------------------

# 5. Compute Services

## 5.1 Amazon EC2

Amazon Elastic Compute Cloud (EC2) provides virtual servers called
instances.

Key concepts: - **AMI:** Amazon Machine Image, a template for launching
an instance. - **Instance type:** Defines CPU, memory, networking, and
other capacity characteristics. - **EBS volume:** Persistent block
storage often attached to an instance. - **Key pair:** Can support SSH
access to Linux instances; Windows access commonly uses different
mechanisms. - **Security group:** Controls network traffic. - **User
data:** Startup instructions that can run during instance
initialization. - **Placement group:** Options for influencing instance
placement for certain performance/availability goals. - **Elastic IP:**
Static public IPv4 address that can be associated with supported
resources; charges and restrictions may apply.

EC2 gives flexibility, but you are responsible for operating-system
patching, application deployment, hardening, and much of capacity
management.

### EC2 pricing options

-   **On-Demand:** Pay for use without a long-term commitment.
-   **Savings Plans:** Commit to a certain amount of eligible compute
    usage for a term in exchange for lower rates.
-   **Reserved Instances:** A billing discount/commitment model for
    eligible usage; they are not always a physical reservation.
-   **Spot Instances:** Use spare capacity at a discount, but
    interruptions can occur. Good for fault-tolerant batch jobs.
-   **Dedicated Hosts/Instances:** Options for specific isolation,
    licensing, or compliance requirements.

Always check current service-specific terms, commitment scope, and
regional pricing.

## 5.2 Auto Scaling

Amazon EC2 Auto Scaling can add or remove EC2 instances according to
policies, schedules, and health signals. Pair it with a load balancer
for common web application architectures.

Scaling policies may use target tracking, step scaling, or scheduled
actions. Scaling is not instantaneous, so applications need enough
capacity to handle demand while new capacity launches.

## 5.3 Elastic Beanstalk

AWS Elastic Beanstalk is a managed application deployment service that
provisions and coordinates supported infrastructure. It reduces the
amount of infrastructure setup developers must perform, while still
exposing configuration and operational responsibilities.

Use it when you want a simpler managed deployment path without designing
every resource manually.

## 5.4 AWS Lambda

Lambda runs code in response to events without requiring you to
provision or manage servers. It scales execution according to the
service's model and has runtime, timeout, concurrency, payload, and
other quotas that must be checked.

Common triggers include API Gateway, S3 events, EventBridge, SQS, and
DynamoDB Streams.

Good use cases: - API handlers - File processing after an S3 upload -
Scheduled jobs - Event-driven automation - Lightweight data
transformations

Consider cold-start latency, execution duration, concurrency, retries,
idempotency, and downstream database capacity. Lambda is not
automatically the best option for every long-running or stateful
workload.

## 5.5 EC2 vs. Lambda

  -----------------------------------------------------------------------
  Need                    Often a good starting   Why
                          point                   
  ----------------------- ----------------------- -----------------------
  Full OS control or      EC2                     More control over
  specialized software                            environment

  Event-triggered short   Lambda                  Managed execution and
  tasks                                           event integration

  Long-running service    EC2 or containers       More control over
  with custom runtime                             process lifetime
  needs                                           

  Variable, bursty API    Lambda or containers    Depends on latency,
  traffic                 with autoscaling        workload, and cost

  Predictable continuous  EC2 or containers       Compare operations and
  compute                                         total cost
  -----------------------------------------------------------------------

There is no universally cheapest option. Model actual usage and
operational needs.

------------------------------------------------------------------------

# 6. Storage Services

## 6.1 Amazon S3 --- object storage

Amazon Simple Storage Service (S3) stores objects inside buckets. It is
widely used for files, backups, logs, static website assets, data lakes,
and application uploads.

Core concepts: - **Bucket:** A container for objects; bucket names have
global naming constraints within a partition. - **Object:** Data plus
metadata and a key. - **Key:** The object's identifier within the
bucket; folder-like paths are key naming conventions. - **Versioning:**
Keeps multiple versions of an object. - **Lifecycle rules:** Transition
or expire objects based on age and conditions. - **Storage class:**
Trade-off between cost, retrieval time, and access pattern. - **Bucket
policy:** Resource-based policy controlling access. - **Presigned URL:**
Time-limited URL that grants a specific operation for an object under
the permissions used to sign it. - **Replication:** Copies objects
between supported buckets/locations according to configuration.

S3 is object storage, not a traditional mounted filesystem or block
device.

### S3 storage classes --- conceptual view

-   **S3 Standard:** Frequent access.
-   **S3 Intelligent-Tiering:** Can automatically move eligible objects
    between access tiers; monitoring and retrieval rules/charges depend
    on tier.
-   **S3 Standard-IA:** Infrequent access with retrieval and
    minimum-duration considerations.
-   **S3 One Zone-IA:** Infrequent access stored in one AZ; lower
    resilience than multi-AZ classes.
-   **S3 Glacier Instant Retrieval:** Archive-oriented storage with
    millisecond retrieval for suitable access patterns.
-   **S3 Glacier Flexible Retrieval:** Archive storage with retrieval
    options that may take minutes to hours.
-   **S3 Glacier Deep Archive:** Very low-cost long-term archive with
    longer retrieval times.

Verify current class names, minimum storage durations, retrieval fees,
and availability before selecting a class.

### S3 security checklist

1.  Keep Block Public Access enabled unless a carefully reviewed use
    case requires otherwise.
2.  Use least-privilege IAM and bucket policies.
3.  Enable encryption and choose KMS controls when required.
4.  Enable versioning for recovery from accidental overwrite/deletion
    where appropriate.
5.  Consider replication and Object Lock for specific recovery or
    retention requirements.
6.  Log and monitor access where needed.
7.  Avoid embedding permanent credentials in application code.

A public-read bucket is not the correct default for user-uploaded
resumes, documents, or private files.

## 6.2 Amazon EBS --- block storage

Elastic Block Store (EBS) provides block volumes for EC2 and other
supported uses. It behaves like a virtual disk that can be formatted
with a filesystem or used by a database.

-   Usually attached within the same AZ as the EC2 instance.
-   Suitable for OS disks, databases, and applications needing
    block-level storage.
-   Snapshots provide point-in-time backups stored through AWS-managed
    snapshot infrastructure.
-   Volume types offer different performance and cost characteristics.

An EBS volume is not the same as S3 object storage. Plan snapshots,
retention, encryption, and restore testing.

## 6.3 Amazon EFS --- shared file storage

Elastic File System (EFS) provides managed NFS file storage for
supported Linux workloads and can be mounted by multiple compute
clients. It is useful when multiple instances need a shared filesystem.

Choose EFS for shared file semantics, not simply because it is called
"storage." Consider performance mode, throughput, access points, network
access, and cost.

## 6.4 AWS Storage Gateway and AWS DataSync

-   **Storage Gateway:** Connects on-premises environments to supported
    AWS storage patterns.
-   **DataSync:** Automates and accelerates supported data transfers
    between storage systems and AWS.

Use them for hybrid storage or migration scenarios, not as
interchangeable services.

## 6.5 S3 vs. EBS vs. EFS

  --------------------------------------------------------------------------
  Property          S3                EBS                  EFS
  ----------------- ----------------- -------------------- -----------------
  Type              Object            Block volume         Shared file
                                                           system

  Common use        Files, backups,   OS/data disk for     Shared files
                    data lake, static compute              across clients
                    assets                                 

  Access style      API/object key    Mounted/attached     Mounted
                                      block device         filesystem

  Scaling           Managed object    Volume               Managed elastic
                    storage           sizing/performance   file storage
                                      choices              

  AZ considerations Regional service  Volume is AZ-scoped  Designed for
                    design and                             shared regional
                    storage class                          access patterns
                    matter                                 
  --------------------------------------------------------------------------

------------------------------------------------------------------------

# 7. Databases and Caching

## 7.1 Relational vs. NoSQL

### Relational database

Stores structured data in tables with defined relationships and commonly
supports SQL and transactions.

Use when relationships, joins, constraints, and transactional
consistency are central.

### NoSQL database

A broad category of data stores designed around models such as
key-value, document, wide-column, or graph. NoSQL does not mean "no
structure" or "no consistency."

Choose a database based on access patterns, data model, consistency
needs, scale, query requirements, and operational workload---not merely
because one is newer.

## 7.2 Amazon RDS

Amazon Relational Database Service (RDS) manages supported relational
database engines, including patching and backups according to the
selected configuration and service model.

Common uses: - Transactional applications - Job portals and e-commerce
systems - Structured records with relationships - SQL queries, joins,
and constraints

Know the distinction between: - **Multi-AZ deployment:** Primarily for
availability/failover, depending on deployment type. - **Read replica:**
Primarily for scaling read traffic or certain replication scenarios; not
a substitute for a Multi-AZ failover design. - **Automated backups and
snapshots:** Recovery mechanisms with different behaviors and retention
options.

Exact features depend on engine and deployment configuration.

## 7.3 Amazon Aurora

Amazon Aurora is a relational database service compatible with MySQL and
PostgreSQL in supported configurations. It separates aspects of compute
and distributed storage architecture and offers managed
availability/scaling features. It may cost more than standard RDS
options, so benchmark and compare total cost.

## 7.4 Amazon DynamoDB

DynamoDB is a managed NoSQL key-value/document database designed for
high scale and low-latency access patterns.

Key concepts: - **Partition key:** Helps determine how data is
distributed and accessed. - **Sort key:** Optional key that supports
ordered/range access within a partition-key value. - **Primary key:**
Partition key alone or partition key plus sort key. - **Secondary
indexes:** Additional query access patterns. - **Capacity modes:**
Provisioned or on-demand options, depending on workload. - **TTL:** Can
expire items asynchronously. - **Streams:** Capture item-level changes
for downstream processing. - **Global tables:** Multi-Region replication
options.

DynamoDB design starts with access patterns. It is not a relational
database where arbitrary joins are the normal model.

## 7.5 Amazon ElastiCache

ElastiCache provides managed in-memory caching using supported engines
such as Redis OSS/Valkey or Memcached depending on current service
options. It can reduce database load and improve latency.

Caching requires decisions about expiration (TTL), invalidation, stale
data, cache misses, memory sizing, and failure behavior. A cache should
not be the only durable copy of important data unless the system is
explicitly designed for that.

## 7.6 Amazon Redshift

Redshift is a managed cloud data warehouse for analytical workloads over
large datasets. It is designed for analytics and reporting, not as the
default transactional database for every web application.

## 7.7 Amazon DocumentDB and Neptune

-   **Amazon DocumentDB:** Managed document database service with
    MongoDB compatibility considerations; verify feature compatibility
    before migration.
-   **Amazon Neptune:** Managed graph database for graph-oriented
    relationship queries.

## 7.8 Database selection examples

  -----------------------------------------------------------------------
  Requirement             Candidate               Important caveat
  ----------------------- ----------------------- -----------------------
  Standard transactional  RDS or Aurora           Choose engine, HA,
  SQL application                                 backups, and instance
                                                  sizing

  Massive key-value       DynamoDB                Design keys and indexes
  access patterns                                 around queries

  Cache hot               ElastiCache             Plan invalidation and
  results/sessions                                failure behavior

  Business intelligence   Redshift                Optimize analytical
  warehouse                                       data model and workload

  Graph traversal         Neptune                 Use when graph query
                                                  patterns justify it

  Shared application      S3, not a database by   Store metadata in a
  documents/files         default                 database if needed
  -----------------------------------------------------------------------

## 7.9 Backups and recovery

A backup is useful only if it can be restored within the required time.
Define: - **RPO (Recovery Point Objective):** How much data loss in time
is acceptable? - **RTO (Recovery Time Objective):** How long can
recovery take? - Backup frequency and retention. -
Cross-account/cross-Region copies where appropriate. - Access controls
to prevent deletion or tampering. - Regular restore tests.

------------------------------------------------------------------------

# 8. Application Integration and Messaging

Modern applications often split work across components. Messaging
reduces tight coupling and helps absorb traffic spikes.

## 8.1 Amazon SQS

Simple Queue Service (SQS) is a managed message queue.

-   **Producer:** Sends messages.
-   **Queue:** Holds messages until consumers process them.
-   **Consumer:** Receives and handles messages.
-   **Visibility timeout:** Temporarily hides a received message while a
    consumer processes it.
-   **Dead-letter queue (DLQ):** Stores messages that repeatedly fail
    processing, according to configured redrive rules.

SQS Standard queues provide at-least-once delivery, so consumers should
be idempotent and tolerate duplicate messages. FIFO queues support
ordered processing and deduplication features within their documented
constraints.

## 8.2 Amazon SNS

Simple Notification Service (SNS) is a pub/sub messaging service. A
publisher sends to a topic and the topic fans messages out to subscribed
endpoints, which can include supported queues, functions, or
notification protocols.

**SNS vs. SQS:** - SNS is often used to broadcast an event to multiple
subscribers. - SQS is often used to buffer work for consumers. - SNS +
multiple SQS queues is a common fan-out pattern.

## 8.3 Amazon EventBridge

EventBridge routes events from AWS services, applications, and supported
partners to targets using rules and event patterns. It is useful for
event-driven architectures and scheduled rules.

Use EventBridge for routing events based on their content; use SQS for
durable work buffering and consumer decoupling. They can be combined.

## 8.4 AWS Step Functions

Step Functions coordinates workflows using states, transitions, retries,
error handling, and integrations. It is useful for multi-step processes
such as application approval, document processing, or order fulfillment.

A workflow orchestrator makes process state and failures explicit. It
does not eliminate the need to make individual steps safe to retry.

## 8.5 Amazon API Gateway

API Gateway creates and manages APIs and can integrate with Lambda and
other backends. It supports features such as authentication integration,
throttling, stages, and monitoring depending on API type.

A typical serverless API is: `Client → API Gateway → Lambda → DynamoDB`

Protect APIs with appropriate authentication/authorization, validation,
throttling, logging, and least-privilege permissions.

## 8.6 Amazon Kinesis

Kinesis services support streaming data ingestion and processing. Use
streaming services when records arrive continuously and low-latency
processing, replay, or stream consumers matter. Compare specific Kinesis
products and current capabilities before choosing.

------------------------------------------------------------------------

# 9. Containers and Serverless

## 9.1 What is a container?

A container packages an application and its dependencies into a portable
image. Containers share the host kernel, unlike traditional virtual
machines that generally run their own guest OS kernel.

-   **Image:** Immutable template used to create containers.
-   **Container:** Running instance of an image.
-   **Registry:** Stores container images.
-   **Orchestration:** Schedules containers, manages desired state,
    scaling, and service connectivity.

Containers improve packaging consistency, but they do not remove the
need for security patching, resource limits, monitoring, and deployment
controls.

## 9.2 Amazon ECR

Elastic Container Registry (ECR) stores container images. Build an
image, push it to ECR, then configure a supported compute platform to
pull and run it.

## 9.3 Amazon ECS

Elastic Container Service (ECS) is AWS's managed container orchestration
service. It runs containerized applications using task definitions,
services, clusters/capacity providers, and supported launch options.

-   **Task definition:** Describes containers, image, CPU/memory, ports,
    environment, roles, and logging.
-   **Task:** A running instance of a task definition.
-   **Service:** Maintains a desired number of tasks and integrates with
    deployment/scaling patterns.

ECS can be simpler to operate than a Kubernetes cluster for AWS-focused
applications.

## 9.4 Amazon EKS

Elastic Kubernetes Service (EKS) provides a managed Kubernetes control
plane. You still need to understand Kubernetes concepts such as pods,
deployments, services, namespaces, ingress, resource requests/limits,
and cluster security. AWS manages the control plane, but the customer
retains responsibility for much of workload configuration and
operations.

Choose EKS when Kubernetes compatibility, ecosystem, or organizational
requirements justify its added complexity.

## 9.5 AWS Fargate

Fargate provides serverless compute capacity for supported ECS and EKS
workloads. You do not manage the underlying EC2 hosts for the Fargate
tasks/pods, but you still configure networking, IAM, images, resources,
logging, and security.

## 9.6 ECS vs. EKS vs. Lambda

-   **Lambda:** Event-driven functions, short-lived execution within
    service limits.
-   **ECS:** AWS-native container orchestration with flexible compute
    options.
-   **EKS:** Kubernetes-based orchestration and ecosystem.
-   **Fargate:** A compute option for supported ECS/EKS workloads, not
    an orchestrator by itself.

Do not select Kubernetes merely because it is popular. Select it when
its capabilities and ecosystem outweigh its operational complexity.

------------------------------------------------------------------------

# 10. Data, Analytics, AI, and Machine Learning

## 10.1 Data lake

A data lake stores large volumes of raw and processed data, commonly in
S3, in multiple formats. Data is organized through cataloging, access
control, partitioning, and lifecycle management.

A data lake is not automatically well-governed. Poor naming, duplicated
datasets, unclear ownership, and excessive permissions make it difficult
to use safely.

## 10.2 Common AWS analytics services

-   **AWS Glue:** Managed data integration/ETL and Data Catalog
    capabilities.
-   **Amazon Athena:** Query data in S3 using SQL without managing
    traditional database servers for the query engine.
-   **Amazon Redshift:** Data warehouse for analytics.
-   **Amazon EMR:** Managed big-data frameworks for supported workloads.
-   **Amazon Kinesis:** Streaming data ingestion/processing options.
-   **AWS Lake Formation:** Helps manage data lake permissions and
    governance.
-   **Amazon QuickSight:** Business intelligence and dashboards.

A common pipeline:
`Applications/logs → S3 → Glue catalog/ETL → Athena or Redshift → QuickSight dashboard`

The right design depends on data volume, latency, format, query
patterns, governance, and budget.

## 10.3 AWS AI and ML services

-   **Amazon SageMaker AI:** Build, train, tune, deploy, and operate
    machine-learning models with managed tooling.
-   **Amazon Bedrock:** Build generative AI applications using supported
    foundation models and managed capabilities.
-   **Amazon Rekognition:** Image and video analysis.
-   **Amazon Textract:** Extracts text and structured information from
    documents.
-   **Amazon Transcribe:** Speech-to-text.
-   **Amazon Polly:** Text-to-speech.
-   **Amazon Comprehend:** Natural-language processing capabilities.
-   **Amazon Lex:** Build conversational interfaces.
-   **Amazon Translate:** Machine translation.

Service names and capabilities evolve; verify current regional
availability and pricing.

## 10.4 How to think about a generative AI application on AWS

A simplified architecture might include: 1. **Frontend:** Web/mobile
application. 2. **API layer:** API Gateway or a load-balanced backend.
3. **Identity:** Cognito or an existing identity provider. 4.
**Application logic:** Lambda or containers. 5. **Model access:**
Bedrock or a model deployed/managed through an appropriate ML service.
6. **Knowledge retrieval:** Ingestion pipeline, document storage,
embeddings, and a suitable vector search/retrieval store. 7. **Data:**
S3 and a database for application state. 8. **Observability/security:**
CloudWatch, CloudTrail, IAM, KMS, and service-specific controls.

For retrieval-augmented generation (RAG), document ingestion, chunking,
access filtering, retrieval quality, citations, prompt injection
defenses, model evaluation, latency, and cost all matter. A vector
database alone does not make a reliable RAG system.

------------------------------------------------------------------------

# 11. Monitoring, Logging, Auditing, and Operations

## 11.1 Amazon CloudWatch

CloudWatch collects metrics, logs, and events and supports alarms and
dashboards.

-   **Metrics:** Numeric measurements over time, such as CPU utilization
    or request count.
-   **Logs:** Event records from applications and services.
-   **Alarms:** Evaluate a metric against a condition and can trigger
    configured actions.
-   **Dashboards:** Visualize important operational metrics.
-   **Logs Insights:** Query and analyze supported log data.

Create alarms around user impact, not just resource activity. Examples
include elevated 5xx rates, high latency, queue backlog, failed jobs,
and database saturation.

## 11.2 AWS CloudTrail

CloudTrail records supported AWS API activity and is essential for audit
trails and incident investigations. It answers questions such as: which
identity called an API, when, and from where, subject to the events and
configuration recorded.

CloudTrail is not a substitute for application logs. Use both when
investigating user-facing behavior.

## 11.3 AWS Config

AWS Config records supported resource configuration changes and can
evaluate resources against rules. It helps answer questions such as
whether a storage bucket's configuration changed or whether resources
comply with a desired configuration.

## 11.4 AWS Systems Manager

Systems Manager provides capabilities for managing supported
infrastructure, including session access, patching, automation,
inventory, and parameter storage. Features depend on
agent/configuration, permissions, and resource type.

Prefer controlled management access such as Systems Manager Session
Manager when it fits, rather than exposing SSH/RDP broadly to the
internet.

## 11.5 AWS X-Ray and application tracing

Distributed tracing helps follow a request across multiple services,
exposing latency and failures between components. AWS X-Ray and
supported OpenTelemetry integrations can help, depending on the current
instrumentation approach.

Metrics show **what** is happening, logs show **what happened**, and
traces help show **where a request spent time**.

## 11.6 Operational excellence

Use: - Runbooks and playbooks. - Version-controlled configuration. -
Automated deployment and rollback. - Clear alerts with owners and
actions. - Incident reviews focused on learning. - Tested backups and
recovery procedures. - Capacity and quota monitoring. - Regular access
and cost reviews.

------------------------------------------------------------------------

# 12. Infrastructure as Code and Developer Tools

## 12.1 Infrastructure as Code (IaC)

IaC defines infrastructure in version-controlled files so environments
can be reviewed, reproduced, tested, and updated consistently.

Benefits: - Repeatability - Peer review - Change history - Reduced
manual configuration drift - Easier disaster recovery and environment
creation

IaC does not guarantee a secure result. Templates still need review,
testing, and controlled deployment.

## 12.2 AWS CloudFormation

CloudFormation uses templates to describe AWS resources and deploys them
as stacks. It is a foundational AWS-native IaC service.

## 12.3 AWS CDK

The AWS Cloud Development Kit (CDK) lets developers define cloud
infrastructure using supported programming languages and synthesizes it
into CloudFormation templates.

## 12.4 Terraform

Terraform is a popular third-party IaC tool that can manage AWS and
other platforms. It uses configuration and state to track managed
infrastructure. Secure the state file because it may contain sensitive
values.

CloudFormation/CDK and Terraform are both useful; learn one well first,
then understand the other conceptually.

## 12.5 CI/CD

Continuous Integration/Continuous Delivery (CI/CD) automates build,
test, security checks, and deployment.

A typical pipeline: 1. Developer pushes code. 2. Automated tests and
linting run. 3. Build a deployable artifact or container image. 4. Scan
dependencies/images and check policies. 5. Publish artifact to a
controlled registry or storage location. 6. Deploy to a test
environment. 7. Run validation tests. 8. Promote to production with an
approved strategy. 9. Monitor health and roll back if necessary.

AWS developer tools include CodeBuild, CodeDeploy, and CodePipeline.
GitHub Actions and other systems can also deploy to AWS using federation
and IAM roles.

## 12.6 Deployment strategies

-   **Rolling deployment:** Replace instances/tasks gradually.
-   **Blue/green:** Run two environments and shift traffic after
    validation.
-   **Canary:** Send a small portion of traffic to the new version, then
    increase gradually.
-   **Immutable deployment:** Launch new resources rather than changing
    existing ones in place.

Choose a strategy based on rollback speed, database compatibility, risk,
and cost. Database migrations often require special expand/contract
planning.

------------------------------------------------------------------------

# 13. High Availability, Disaster Recovery, and Reliability

## 13.1 Design for failure

Assume that instances, AZs, networks, dependencies, and deployments can
fail. Avoid single points of failure in components that must remain
available.

A common web architecture:
`Users → Route 53 → CloudFront/WAF (where suitable) → ALB across AZs → app instances/containers across AZs → database with suitable HA → S3 for files`

The exact path varies. Not every application needs every service.

## 13.2 Multi-AZ vs. Multi-Region

-   **Multi-AZ:** Improves resilience to failures within a Region and is
    often the first availability step.
-   **Multi-Region:** Can support regional disaster recovery, geographic
    latency, or data residency needs, but increases complexity and cost.

Multi-Region is not automatically better. Replication, failover, DNS,
data consistency, secrets, quotas, and operational procedures all need
planning.

## 13.3 Disaster recovery strategies

From simpler/cheaper to more complex/expensive in many cases: - **Backup
and restore:** Restore from backups after an incident. - **Pilot
light:** Keep core data/services prepared and scale up during
recovery. - **Warm standby:** Maintain a reduced but functional
environment. - **Multi-site active/active:** Run workloads in multiple
locations and distribute traffic.

Actual cost and recovery time depend on the workload. Set RTO/RPO
targets first, then test whether the design meets them.

## 13.4 Caching and resilience patterns

-   Cache suitable read-heavy data.
-   Set timeouts on network calls.
-   Retry only transient failures, with bounded exponential backoff and
    jitter.
-   Use circuit-breaker/bulkhead patterns where appropriate.
-   Make retried operations idempotent.
-   Use queues to absorb bursts.
-   Avoid unbounded retries that overload a failing dependency.
-   Apply rate limiting and quotas.
-   Monitor saturation and downstream dependencies.

## 13.5 AWS Well-Architected Framework

The AWS Well-Architected Framework organizes architecture review around
six pillars:

1.  **Operational Excellence:** Run and improve workloads effectively.
2.  **Security:** Protect systems, data, and access.
3.  **Reliability:** Recover from failures and meet demand.
4.  **Performance Efficiency:** Use resources and technologies
    effectively.
5.  **Cost Optimization:** Deliver value while controlling cost.
6.  **Sustainability:** Reduce environmental impact through efficient
    cloud use.

Use the pillars as a review checklist, not as a one-time certification
exercise.

------------------------------------------------------------------------

# 14. Security Architecture and Common Mistakes

## 14.1 Common dangerous mistakes

-   Making an S3 bucket public accidentally.
-   Storing AWS access keys in source code, GitHub, Docker images, or
    frontend JavaScript.
-   Giving all users administrator permissions.
-   Opening SSH/RDP or database ports to `0.0.0.0/0`.
-   Putting a database in a public subnet without a strong reason.
-   Ignoring CloudTrail, logs, and alerts.
-   Leaving test resources running indefinitely.
-   Using a single AZ for a production-critical workload without
    accepting the risk.
-   Assuming that backups are valid without restore testing.
-   Treating encryption as a replacement for authorization.
-   Ignoring application-level vulnerabilities because AWS
    infrastructure is managed.
-   Building multi-Region architecture without testing replication and
    failover.
-   Granting broad permissions to CI/CD roles.
-   Logging passwords, tokens, or sensitive personal data.

## 14.2 Secure web application pattern

For a typical web app: 1. Expose only the intended public entry point,
often CloudFront and/or an ALB/API Gateway. 2. Keep application and
database resources private when possible. 3. Use TLS for traffic. 4. Use
IAM roles for service-to-service access. 5. Store secrets in a managed
secret store. 6. Encrypt stored data and control KMS permissions. 7.
Validate input and use secure application coding practices. 8. Add logs,
metrics, alerts, and audit trails. 9. Patch and scan supported
systems/images. 10. Test backup restoration and incident response.

## 14.3 Identity federation

Federation allows users or external systems to use an existing identity
provider to access AWS without creating separate long-lived credentials
for every person or workflow. For workloads, use supported
role-assumption patterns such as OIDC where suitable.

------------------------------------------------------------------------

# 15. Cost Management and Optimization

## 15.1 Understand what drives AWS cost

Common cost dimensions: - Compute runtime and instance size - Storage
volume and storage class - Requests and data retrieval - Data transfer,
especially between regions or to the internet - NAT Gateway processing
and hourly use - Load balancers and public IPv4 usage where charged -
Database instance/storage/backup usage - Logs, metrics, and data
retention - Managed service capacity and requests

"Free" or low-cost resources can still create charges. Check current
pricing for your Region and exact configuration.

## 15.2 Cost-control tools

-   **AWS Budgets:** Set budgets and alerts.
-   **AWS Cost Explorer:** Explore historical cost and usage.
-   **Cost and Usage Reports / Data Exports:** Detailed billing and
    usage data options.
-   **Cost allocation tags:** Attribute costs to teams/projects where
    supported and activated.
-   **Compute Optimizer:** Recommendations for supported resource
    optimization.
-   **Trusted Advisor:** Recommendations across supported checks and
    plans.
-   **Savings Plans/Reserved Instances:** Commitments for eligible
    usage.
-   **Spot:** Discounted interruptible compute for suitable jobs.

## 15.3 Practical cost habits

1.  Set a budget and billing alerts before experimentation.
2.  Use tags for project, environment, and owner.
3.  Stop or delete unused compute.
4.  Delete unattached storage and stale snapshots when no longer needed.
5.  Avoid oversized instances; measure utilization.
6.  Use Auto Scaling where it suits the workload.
7.  Set log retention deliberately.
8.  Use lifecycle policies for old S3 objects.
9.  Minimize unnecessary cross-AZ, cross-Region, and internet data
    transfer.
10. Review bills regularly and investigate unexpected increases.

## 15.4 Cost vs. availability

A single small instance may be cheaper but introduces a single point of
failure. Multiple AZs, replicas, backups, and security services cost
money but may be necessary for business requirements.

The right question is not "What is the cheapest architecture?" but "What
is the lowest-cost architecture that satisfies the required performance,
reliability, security, and recovery objectives?"

------------------------------------------------------------------------

# 16. Practical Architecture Walkthrough: A Job Portal

Suppose you are building a job portal with user accounts, job listings,
applications, resume uploads, and an admin dashboard.

## 16.1 A reasonable starting architecture

-   **Frontend:** React static assets hosted in S3 and delivered via
    CloudFront, or another suitable hosting option.
-   **DNS:** Route 53 if using AWS DNS.
-   **HTTPS:** ACM certificates integrated with supported endpoints.
-   **Backend:** A Node.js/Express API on ECS/Fargate, EC2, Lambda, or a
    managed deployment platform depending on workload and experience.
-   **API entry:** ALB for container/EC2 web services or API Gateway for
    suitable API/serverless designs.
-   **Database:** RDS/Aurora for relational records, or DynamoDB if the
    data/access patterns suit its model.
-   **Resume uploads:** Private S3 bucket with short-lived presigned
    upload/download URLs where appropriate.
-   **Secrets:** Secrets Manager or Parameter Store.
-   **Identity:** A suitable identity provider; Amazon Cognito is an
    option, but a custom or external identity design may be appropriate.
-   **Logs/metrics:** CloudWatch; CloudTrail for AWS API auditing.
-   **Security:** IAM roles, private subnets, security groups,
    encryption, input validation, and least privilege.
-   **Delivery:** CI/CD pipeline with tests and staged deployment.
-   **Recovery:** Automated database backups, object versioning where
    appropriate, and tested recovery procedures.

## 16.2 Example request flow

1.  A candidate opens the website.
2.  DNS resolves the domain and CloudFront serves cached frontend files.
3.  The browser calls the backend over HTTPS.
4.  The API validates the identity and request.
5.  The backend reads or writes application data in the database.
6.  When a resume is uploaded, the backend authorizes a short-lived
    presigned URL; the browser uploads directly to a private S3 bucket.
7.  An event can trigger a background processing workflow, such as
    document scanning or metadata extraction.
8.  Logs and metrics capture failures and performance.
9.  Alerts notify the responsible team when service health degrades.

## 16.3 Why upload directly to S3?

Sending large files through the backend consumes application bandwidth
and compute. A presigned URL lets a client upload directly to S3 for a
limited time and permitted operation. The backend must still authorize
the upload and validate file size/type and downstream safety
requirements. Do not expose the bucket publicly.

## 16.4 What changes for production?

-   Run multiple application tasks/instances across AZs.
-   Add an appropriate load balancer and health checks.
-   Use a database configuration that meets availability and recovery
    targets.
-   Add rate limits, WAF where suitable, security scanning, and
    alerting.
-   Use controlled secrets and rotation.
-   Test rolling/blue-green deployments and rollback.
-   Configure retention and backup policies.
-   Review cost, data privacy, access boundaries, and threat model.
-   Document runbooks and test disaster recovery.

Do not deploy every possible AWS service just to make the architecture
look advanced. Add components to meet specific requirements.

------------------------------------------------------------------------

# 17. Hands-On Learning Roadmap

## Before using AWS

1.  Create or access an AWS account using the official AWS process.
2.  Secure the root identity with MFA and do not use it for routine
    work.
3.  Configure an administrative access method that follows current AWS
    guidance.
4.  Set a budget and billing alerts.
5.  Choose a single Region for initial practice.
6.  Read each service's pricing and free offer details before creating
    resources.
7.  Create a cleanup checklist and remove resources after each lab.

## Lab 1 --- IAM fundamentals

-   Inspect IAM roles and policies.
-   Read a simple JSON policy and identify Effect, Action, Resource, and
    Condition.
-   Create a least-privilege role for a test workload.
-   Learn how explicit Deny affects authorization.
-   Do not create permanent access keys unless a specific need requires
    them.

**Success criterion:** Explain why a role is generally preferable to
embedding credentials in code.

## Lab 2 --- S3 storage and permissions

-   Create a test bucket in your chosen Region.
-   Upload a non-sensitive file.
-   Inspect Block Public Access and encryption settings.
-   Enable versioning.
-   Create a lifecycle rule in a test environment if useful.
-   Test access with authorized and unauthorized identities.
-   Delete the test bucket and objects after finishing, if no longer
    needed.

**Success criterion:** Explain buckets, objects, keys, policies,
versioning, lifecycle rules, and public access controls.

## Lab 3 --- VPC networking

-   Inspect a VPC, subnets, route tables, and security groups.
-   Identify which subnets have routes to an Internet Gateway.
-   Explain how a private subnet can reach the internet through a NAT
    Gateway.
-   Understand why a public subnet alone does not guarantee inbound
    access.

**Cost caution:** NAT Gateways and other network resources can incur
charges. Prefer a diagram/simulation or clean up immediately when
appropriate.

## Lab 4 --- Launch a small EC2 test instance

-   Choose a suitable low-cost instance type and supported image.
-   Configure a security group with only required inbound traffic.
-   Prefer Session Manager when available and configured.
-   Learn instance status checks, EBS, user data, and stop
    vs. terminate.
-   Terminate the instance and remove unattached resources when done.

**Success criterion:** Explain AMI, instance type, EBS, security group,
IAM role, and Auto Scaling.

## Lab 5 --- Deploy a simple web app

-   Package a small Node.js application.
-   Deploy it to a suitable service, such as EC2, ECS, or a managed
    application platform.
-   Configure HTTPS and a health endpoint.
-   Send logs to CloudWatch.
-   Add an alarm for a meaningful failure signal.
-   Document how to roll back.

## Lab 6 --- S3 + Lambda event workflow

-   Create a Lambda function for a simple, non-sensitive file event.
-   Configure a supported S3 event notification.
-   Give Lambda only the permissions it needs.
-   Log the event safely.
-   Make the function idempotent to tolerate duplicate delivery.
-   Test failures and clean up.

## Lab 7 --- Database fundamentals

-   Compare RDS and DynamoDB using a small application data model.
-   For RDS, understand backups, Multi-AZ, and read replicas.
-   For DynamoDB, design a partition key and query pattern before
    creating a table.
-   Do not expose databases publicly for convenience.
-   Delete paid test resources after the lab.

## Lab 8 --- Infrastructure as Code

-   Write a small CloudFormation template or CDK app.
-   Deploy a harmless test resource.
-   Review the change set/diff before applying changes.
-   Update the template and observe the change.
-   Delete the stack and verify that resources were removed.

## Lab 9 --- Observability and audit

-   Inspect CloudWatch metrics and logs.
-   Create one meaningful alarm.
-   Find a supported API activity event in CloudTrail.
-   Explain the difference between application logs, metrics, traces,
    and audit events.

## Lab 10 --- Build a portfolio architecture

Document a small production-style application with: - Architecture
diagram - Threat model - VPC/subnet design - IAM roles and
least-privilege policies - Database and storage choices - CI/CD and
rollback - Monitoring/alerting - Backup and recovery targets - Estimated
monthly cost assumptions - Cleanup/deployment instructions

A well-explained, reproducible project is more valuable than a diagram
filled with services you cannot justify.

------------------------------------------------------------------------

# 18. Interview Questions with Answers

## Cloud fundamentals

### 1. What is cloud computing?

On-demand access to computing resources over a network with flexible
provisioning and usage-based pricing models.

### 2. What is the difference between scalability and elasticity?

Scalability is the ability to handle growth; elasticity is the ability
to adjust capacity as demand changes.

### 3. What is the difference between vertical and horizontal scaling?

Vertical scaling changes the capacity of one resource; horizontal
scaling adds or removes resources.

### 4. What is the shared responsibility model?

AWS secures the cloud infrastructure it operates; the customer secures
their workloads, data, identities, and configurations. The exact split
depends on the service.

### 5. What is a Region?

A separate geographic AWS area containing multiple Availability Zones.

### 6. What is an Availability Zone?

An isolated location within a Region designed to reduce correlated
failures.

### 7. What is high availability?

Designing a service to remain available through expected component
failures, often using redundancy and health-based failover.

### 8. What is the difference between IaaS, PaaS, and SaaS?

They represent increasing levels of managed abstraction: infrastructure,
application platform, and complete application.

## IAM and security

### 9. Why use IAM roles instead of hard-coded access keys?

Roles provide temporary credentials and avoid embedding long-lived
secrets in code.

### 10. What is least privilege?

Grant only the minimum permissions necessary for a task, resource scope,
and duration.

### 11. What happens if an Allow and an explicit Deny both apply?

The explicit Deny takes precedence.

### 12. What is MFA?

Multi-factor authentication requires an additional verification factor
beyond a password or single credential.

### 13. What is KMS used for?

Creating and controlling cryptographic keys and integrating key usage
with supported AWS services.

### 14. What is the difference between CloudTrail and CloudWatch?

CloudTrail records AWS API activity for auditing; CloudWatch focuses on
operational metrics, logs, alarms, and monitoring.

### 15. What is a security group?

A stateful virtual firewall associated with network
interfaces/resources.

## Networking

### 16. What is a VPC?

A logically isolated virtual network in AWS where you define IP ranges,
subnets, routes, and network controls.

### 17. What is the difference between a public and private subnet?

A public subnet has an appropriate route to an Internet Gateway. A
private subnet does not have that direct route. Actual reachability also
depends on IP addressing and security controls.

### 18. What does a NAT Gateway do?

It allows supported outbound IPv4 connections from private subnet
resources without allowing unsolicited inbound connections through that
NAT path.

### 19. Security group vs. NACL?

Security groups are stateful and operate at the
resource/network-interface level; NACLs are stateless and operate at the
subnet level.

### 20. What is an Internet Gateway?

A VPC component that enables internet connectivity for appropriately
routed and configured resources.

### 21. What is an ALB?

An Application Load Balancer distributes HTTP/HTTPS traffic and supports
Layer 7 routing features.

### 22. What is a VPC endpoint?

A way to privately connect a VPC to supported AWS services without
requiring public internet routing for that traffic.

## Compute and storage

### 23. What is EC2?

A service providing configurable virtual servers.

### 24. What is an AMI?

A template used to launch EC2 instances.

### 25. What is Auto Scaling?

A mechanism to adjust the number of compute instances according to
policies, schedules, and health signals.

### 26. What is Lambda?

A managed serverless compute service that runs code in response to
events.

### 27. S3 vs. EBS?

S3 is object storage accessed through APIs; EBS is block storage
commonly attached to EC2.

### 28. S3 vs. EFS?

S3 stores objects; EFS provides a shared file system for supported
clients.

### 29. What is S3 versioning?

A feature that keeps multiple versions of an object, helping recover
from some overwrites or deletions.

### 30. What is a presigned URL?

A time-limited URL that grants a specific S3 operation based on the
signer's permissions and the URL's parameters.

## Databases and integration

### 31. RDS vs. DynamoDB?

RDS is a managed relational database service; DynamoDB is a managed
key-value/document database designed around access patterns.

### 32. Multi-AZ vs. read replica?

Multi-AZ primarily supports availability/failover, while read replicas
primarily support read scaling and certain replication scenarios. Exact
behavior depends on engine/configuration.

### 33. What is SQS?

A managed message queue that buffers work between producers and
consumers.

### 34. What is SNS?

A pub/sub notification service that distributes messages to subscribers.

### 35. SNS vs. SQS?

SNS broadcasts to subscribers; SQS queues work for consumers. They are
often combined for fan-out and buffering.

### 36. What is EventBridge?

An event bus/routing service that directs events to targets based on
rules and event patterns.

### 37. Why must queue consumers be idempotent?

Messages may be delivered more than once, retried, or processed after
uncertain failures. Idempotency prevents duplicate side effects.

## Containers, operations, and cost

### 38. ECS vs. EKS?

ECS is AWS-native container orchestration; EKS provides managed
Kubernetes. EKS is useful when Kubernetes capabilities justify its
additional complexity.

### 39. What is Fargate?

Serverless compute capacity for supported ECS and EKS workloads; it is
not an orchestrator by itself.

### 40. What is CloudFormation?

An AWS IaC service that provisions and manages resources from templates.

### 41. What is CloudWatch used for?

Collecting and analyzing metrics/logs, creating alarms, and building
operational dashboards.

### 42. What is RPO?

The maximum acceptable amount of data loss measured in time.

### 43. What is RTO?

The target maximum time to restore a service after disruption.

### 44. How do you reduce AWS cost?

Right-size resources, remove unused resources, use lifecycle policies,
monitor data transfer, set budgets, apply suitable discounts, and review
usage regularly.

### 45. Why might a private subnet still need outbound internet access?

For tasks such as downloading updates or calling external APIs. A NAT
Gateway or other suitable connectivity design may provide that access,
while VPC endpoints can privately serve supported AWS services.

### 46. Does putting a server in a public subnet make it publicly accessible?

No. Routing, public IP addressing, security groups, NACLs, host
firewalls, and the application listener also affect reachability.

### 47. Does Multi-AZ replace backups?

No. Multi-AZ helps availability; backups help recover from data loss,
corruption, or other incidents. Both may be needed.

### 48. Does serverless mean there are no servers?

No. The provider manages the servers and much of the infrastructure
provisioning, but the application still has limits, security needs, and
operational concerns.

### 49. What is the AWS Well-Architected Framework?

A set of architecture best-practice principles organized into
Operational Excellence, Security, Reliability, Performance Efficiency,
Cost Optimization, and Sustainability.

### 50. How would you secure a file-upload feature?

Authenticate and authorize the user, use a private bucket, use
short-lived presigned URLs if appropriate, restrict permissions and
object paths, validate size/type, scan files when needed, encrypt data,
avoid public access, and log/monitor the workflow.

------------------------------------------------------------------------

# 19. Glossary and Quick Revision Sheet

## Essential abbreviations

-   **AWS:** Amazon Web Services
-   **AZ:** Availability Zone
-   **IAM:** Identity and Access Management
-   **MFA:** Multi-factor authentication
-   **VPC:** Virtual Private Cloud
-   **CIDR:** Classless Inter-Domain Routing
-   **IGW:** Internet Gateway
-   **NAT:** Network Address Translation
-   **ALB/NLB:** Application/Network Load Balancer
-   **EC2:** Elastic Compute Cloud
-   **AMI:** Amazon Machine Image
-   **EBS:** Elastic Block Store
-   **EFS:** Elastic File System
-   **S3:** Simple Storage Service
-   **RDS:** Relational Database Service
-   **HA:** High Availability
-   **DR:** Disaster Recovery
-   **RPO:** Recovery Point Objective
-   **RTO:** Recovery Time Objective
-   **IaC:** Infrastructure as Code
-   **CI/CD:** Continuous Integration / Continuous Delivery or
    Deployment
-   **ETL:** Extract, Transform, Load
-   **TLS:** Transport Layer Security
-   **ARN:** Amazon Resource Name
-   **KMS:** Key Management Service
-   **WAF:** Web Application Firewall
-   **DLQ:** Dead-Letter Queue
-   **TTL:** Time to Live

## Service-to-purpose cheat sheet

  Need                                    Service to learn first
  --------------------------------------- ---------------------------
  Virtual server                          EC2
  Event-driven code                       Lambda
  Container image registry                ECR
  AWS container orchestration             ECS
  Managed Kubernetes                      EKS
  Object storage                          S3
  Persistent block storage for EC2        EBS
  Shared file storage                     EFS
  Managed relational database             RDS
  Managed key-value/document database     DynamoDB
  In-memory cache                         ElastiCache
  Virtual private network                 VPC
  DNS                                     Route 53
  HTTP/HTTPS load balancing               ALB
  Network-level load balancing            NLB
  Metrics, logs, alarms                   CloudWatch
  API activity audit                      CloudTrail
  Resource configuration tracking         AWS Config
  Permissions and roles                   IAM
  Encryption keys                         KMS
  Secrets                                 Secrets Manager
  Message queue                           SQS
  Pub/sub notifications                   SNS
  Event routing                           EventBridge
  Workflow orchestration                  Step Functions
  API management                          API Gateway
  Infrastructure templates                CloudFormation
  Managed data integration                Glue
  SQL queries over S3 data                Athena
  Cloud data warehouse                    Redshift
  Machine-learning workflow               SageMaker AI
  Foundation-model application services   Bedrock
  Budget and spend tracking               Budgets and Cost Explorer

## Final revision checklist

You are building a strong AWS foundation when you can explain, without
memorizing a definition:

-   Why a Region contains multiple AZs and when Multi-Region is
    justified.
-   How a request travels from DNS to a load balancer, application,
    database, and storage.
-   Why a public subnet is not automatically a publicly reachable
    server.
-   How route tables, security groups, and NACLs differ.
-   Why roles and least privilege are safer than hard-coded access keys.
-   When to choose EC2, Lambda, ECS, EKS, or Fargate.
-   When to choose S3, EBS, or EFS.
-   When RDS fits better than DynamoDB, and vice versa.
-   How SNS, SQS, EventBridge, and Step Functions solve different
    integration problems.
-   How CloudWatch, CloudTrail, and AWS Config differ.
-   How to plan RPO/RTO, backups, high availability, and recovery tests.
-   How to prevent surprise costs and clean up learning resources.
-   How to justify each service in a real architecture.

**Best learning rule:** For every service, answer five questions: *What
problem does it solve? When should I use it? When should I not use it?
How is it secured? What drives its cost?* If you can answer these
clearly and demonstrate a small lab, you understand the service rather
than merely remembering its name.
