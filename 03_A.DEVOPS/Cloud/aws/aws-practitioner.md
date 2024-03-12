# AWS Cloud Practitioner Course

# 1. Introduction

You only pay for what you use.

*Key Value*: 
  Pay for what you need.
  
*Cloud Computing*

Cloud computing is the on-demand delivery of IT resources over the internet with pay-as-you-go pricing

Undifferentiated heavy lifting of IT

  Cloud Computing Models
    Infrastructure as a Service (IaaS)
    Platform as a Service (PaaS)
    Software as a Service (SaaS)
  Cloud Computing Deployment Models
    Cloud
    Hybrid
    On-premises

Cloud-Based Deployment
 
On-Premises Deployment (Rack and Stack)

Hybrid Deployment

Benefits of Cloud-Based Deployment

  Trade upfront expense for variable expense

  Stop spending money to run and maintain data centers

  Stop guessing capacity

  Benefit from massive economies of scale

  Increase speed and agility

  Go global in minutes.

# Lesson 5 Intro

AWS built datacenters and secured them.

5.1 Amazon EC2 (Elastic Compute -- CaaS)
  Hightly flexible
  Reliable
  Cost Effective
  Quick
  Virtual Machine (Sharing underlying physical infrastructure -- Multitenancy)
  Hypervisor isolates virtual machines from each other and secure & separate.
  Max out -- Vertical Scaling (Small/large)

 # Instance Types:
 
    General purpose
    Compute Optimized
    Memory Optimzed
    Accelerated Computing
    Storage Optimized

    On-Demand Instances
    Spot Instances
    Reserved Instances
    C7g Instances (Compute)
    Inf2 Instances (AI/ML)
    M7g Instances (General)
    R7g Instances (Memory)
    Tm1 Instances (Generative AI/LLM)
    Savings Plans
    Dedicated Hosts

# Server Less Resrouces
    Aws Lambda
      Trigger
        Short Running functions
        Service Oriented functions
        Event Driven applications

      Under 15 mins
        Backup
    AWS Elastic Container Services (ECS)
      a highly scalable, high-performance  container management system
      that enables to run and scale containerized applications on AWS.
      Container Orchestration Management
      Docker Instances
    AWS Elastic Kubernetes Services (EKS)
      a fully managed service to run Kubernetes on AWS
      Docker Instances
      
    AWS Fargate
      a serverless compute engine for containers.
  

# Costs
  On-Demand (uptime/OS type)
  Savings Plan 
    (Commitment for hours usage/spend 1/3 years to instance family/region)
  Reservered Instances 
    ( upto 75% of on-demand 1/3 years requires instance family/size, platform,tenancy/region  one Region)
  Spot Instances (upto 90% On-Demand, 2 minutes per reclaiming by Amazon )
  Dedicated hosts ( not shared by others)

# Scaling
    Up
    Down
  
  
  
5.2 Amazon Elastic Load Balancing 
    High Performance
    Cost Efficient
    High Available
    Automatically Scalable

    Regioncal Connect
  

5.2 Messages and Queues
    Loosely Coupled Architecture.
    Single failure won't cause cascading failures.
    
  Amazon Simple Queue Service (SQS)
      Message Queuing System.
      Send Messages
      Store Messages
      Receive Messages
      Any Volume
    Amazon Simple Notificatin Service (SNS)
      publish/subscribe service
      To Users (SMS/Mobile Push/Email)
      SNS Topic (Publisher & Subscribers)
      Subscribers can be SQS,Lambda,Webhooks
      
    
# 3 Global Infrastructure
    32 Regions
    102 AZs

    Critieria for Choosing AWS Regions
      1. Compliance (Law)
      2. Proximity to Customers (Latency--> the time it takes for the data to be sent and received)
      3. Feature availability (Amazon Braket -- Quantum Computing)
      4. Pricing
    Structure of AWS Region:
      Made of multiple of data centers. (Disaster Recovery)
      A. a single or a group of data centers... called Availability Zone.
        Regionally Scoped Services are by default highly available.
      B. Edge Locations ( CDN-- Content Delivery Network)
        Centers for storing cacheable data/contnet close to the customer base for better service experience.
        1. Amazon CloudFront (CDN Services)
          text/video/files
        2. Amazon route53 (DNS Service)
        3. Amazon Outpost (AWS Inside Customer's Datacenter)
        
    Configuring AWS Regions
      a. AWS SDK
      b. AWS Management Console
        Test Env
        View Bills
        Monitoring Resources
        Managing Non-Technical resources
      C. AWS CLI
      d. Other tools
    Interaction with AWS
      1. AWS CloudFormation
          IAC Tool (Declaractive Json/Yaml template format)
          EC2/Storage...More
      3. AWS Elastic Beanstalk
            (Code to manage EC2/ELB auto-scaling and monitoring)


# 4 Networking
    Amazon VPC (Virtual Private Cloud)
      A networking service that  can be used to establish boundaries around  AWS resources is Amazon Virtual Private Cloud (Amazon VPC). It enables to provision an isolate sections of the AWS Cloud.  A subnet is a section of a VPC that can contain resources such as Amazon EC2 instances.
      AWS Cloud:
        VPC:
          public subnet
          private subnet

      Internet Gateway
      Virtual Private Gateway :
        Create a Virtual private Network between the VPC and the internal Corporate network.
      AWs Direct Connect: 
        Create a dedicated connection between the VPC and on-premises data center.
        (Connter Router/firewall --> partner route --> aws direct connection end point --> aws virtual private gateway)

      Network hardening
        Network ACLs: (Subnet/Stateless)
          A network ACL is a virtual firewall that controls inbound and outbound traffic at the subnet level.By default, a default network ACL allows all inbound and outbound traffic.
        Security Group: (Instance/Stageful)
          A security group is a virtual firewall that controls inbound and outbound traffic for an Amazon EC2 instance.

      Application Security
      User Identity
      Authentication & Authorization
      Distributed Denial of Service Prevention
      Data Integrity
      Encryption

      Global Network
        Amazon Route 53 (DNS service)
          Latency Based Routing
          Geo-Location based DNS
            Amazon CloudFront -- CDN service  using Amazon Edge Locations
          Geoproximity routing
          Weighted round routing



# 5 Storage and Databases
      5.1 Amazon Elastic Block Storage (Amazon EBS).
          Store the data in blocks.
          Size
          Type
          Configurations
          Maximum 15TB
          Solid State
          Allows Incremental backup of the data.
          AZ level Resources
          EC2 need to be in same AZ.
          Volumes don't scale automatically.

      5.2 Amazon Simple Storage Service (Amazon S3).
          Store data as objects.(Files)
          Store objects in buckets. (Multiple/Permissions/Retention)
          Maximum 5 TB
          Version the objects
          Web Enabled
          Regionally Distributed
          Durability (11 9's)
          Offers Cost Saving
          Serverless

          Types:  
            Amazon S3 Standard (1 Year)
            Amazon S3 Standard-IA(Infrequent Access) (Backup/Disaster recovery)
            Amazon S3 Standard - One Zone IA (For low price)
            Amazon S3 Static website hosting
            Amazon S3 Glacier Instant Retrieval
            Amazon S2 Glacier Deep Archive (Retrives in 12 hours)
            Amazon S3 Glacier Flexible Retrieval (Audit files)
              WriteOnceReadMany-Locks
              Life Cycle Policy
                Standard - 90
                Standard -IA 30
                Glacier - 1 Year
            Amazon S3 Intelliegent-Tiering
            Amazon S3 Outposts
      5.3 Amazon Elastic File System (Amazon EFS).
          Multiple instances can access the data in EFS at the same time.(read/write)
          Linux File System.
          Regional Resource
          Automcaticallly scales.


      5.4 Amazon RDBMS
          MySQL
          Postgres
          Oracle
          Microsoft SQL Servers

          Automated Patching
          Backups
          Redundancy
          Failover
          Disaster Recovery

      5.4.1 Amazon Aurora (MySQL/Postgres)
            Amazon Aurora is an enterprise-class relational database.
    
            Data Replication (15 copies)
            Continuous backup to S3
            Point-in-time Recover
            Relation (Rigid Schema)
            Customer Controls
              Ownership of the data and Schema
              Network



      5.4.2 Amazon DynamoDB.
            Amazon DynamoDB is a key-value database service. It delivers single-digit millisecond performance at any scale.
            Serverless
            Create Tables
            Create Items (Attributes) in tables
            Redundantly and Across AZs
            Non-Relation NoSQL Databases
            Queries based upon Keys
            Granular API Access
      
      5.4.3 Amazon Redshift
            Amazon Redshift is a data warehousing service that you can use for big data analytics

            Buiness Intelligence
            Dataware houses
      
      5.4.4 Amazon Data Migration Service
            
            Homogeneous Databases
              Schema Structure
              Data Types
              Database Code
            Heterogeneous database
              Schema Conversion Tools
            Database Consolidations
            Continuous Database Replications
      5.4.5 Amazon Document DB (MongoDB)
      5.4.6 Amazon Neptune (Graphical DB)
      5.4.7 Amazon QLDB (Quantum Ledge Database --Immutable DB)


      5.4.8 Amazon ElasticCache (caching layers on top of your databases -- Mem CacheD/Redis)
      5.4.9 Amazon DynamoDB Accelerator  (In-Memory Cache for Amazon DynamoDB)

# 6 Security

    Amazon controls the security of the Cloud
      Physical
      Network
      Hypervisor

    Customer controls the secuirty in the Cloud.
      Operating System
      Application
      Data
    6.1 User Permission and Access

      6.1.1 AWS Account root user
        MFA
        
      6.1.2 AWS IAM
        6.1.2.1 AWS User  (no permissions by default)
        6.1.2.2 Least Privileged Principle
        6.1.2.3 IAM Policies (Statement json)
            Effect (Allow/Deny)
            Action (AWS API call)
            Resource (AWS Resource)
        6.1.2.4: IAM groups
            An IAM group is a collection of IAM users.
            Policy associate to IAM Group
        6.1.2.5 IAM Roles
          TimeBound
          Associate Permissions
          Grant to Users/External Identities/Applications/Other AWS Services
        6.1.2.6 Identity Federation to Corp IAM

      6.2.0 AWS Organizations

        A Central location to manage multiple AWS Accounts
        Consolidated Billing
        Hierachical groupings of accounts
        Access Control for Accounts on AWS Service/API
        Service Control Policies (SCPs)

      6.3.0 Compliance
        GDPR (General Data Protection Regulation)
        HIPAa (Health Insurance Portability & Accountability Act)

        AWS Artifact (Agreements/Reports)
        AWS Compliance Centre
          Answers to key compliance questions
          An overview of AWS risk & compliance
          An auditing security checklist
      
      6.4.0 DDoS (Distributed denial of Service)

          UDP Flood
            Security Groups
          HTTP Level Attack
          SLOWLORIS Attack
            ELB
          
          AWS Shield:
            AWS Shield is a service that protects applications against DDoS attacks. AWS Shield provides two levels of protection: Standard and Advanced.
              Advanced is a paid service that provides detailed attack diagnostics and the ability to detect and mitigate sophisticated DDoS attacks. 

          AWS WAF(Web Application Firewall)
            WAF is a web application firewall that lets you monitor network requests that come into your web applications. 
            Web Access Control List (ACL) (CloufFront and ELB)

      6.5.0 
        Encryption:
          At Rest
          In transist
            TLS
        AWS KMS (Key Management Service)
        Amazon Inspector 
          AWS Inspector  is a service that provides intelligent threat detection for your AWS infrastructure and resources.
          To perform automated security assessments
          Network Configuration Reliability
          Amazon Agent
          Security Assessment Service
        Amazon Guard Duty (Threat Detection Service)
          Network and Account Activity
          Intelligently detects threats.
        Amazon Advance Shield


# 7 Monitoring
      Observing systems and collectings metrics

      7.1 Amazon Cloud Watch
        Cloud Watch web service that enables you to monitor and manage various metrics and configure alarm actions based on data from those metrics.
        Create an alaram
        Trigger an event
        Integrated with SNS
        Dashboard UI
        Access all metrics at central location
        Visibilty into applications/infrastructure and services.
        Reduce MTTR (Mean time to respond) and increase TCO (Total cost of ownership)
        Drive insights to optimize applications and operational resources.

     7.2 Amazon CloudTrail
        CloudTrail records every API calls.
        CloudTrail Insights
          CloudTrail to automatically detect unusual API activities
     7.3 Amazon Trust Advisor
        Inspects  AWS environment and provides real-time recommendations 

        Cost Optimization
        Performance
        Security
        Fault Tolerance
        Service Limits


# 8 Pricing

    # 8.1 AWS Free Tier
      8.2 Model
          Pay for what use
          Pay less when you reserve
          Pay less volume based discounts when used more.
      8.2 Pricing Calculator
      8.3 AWS Budgets
      8.4 AWS Cost Explorer
      8.5 AWS support plan
          Base Support
          Developer Support
            24 hours
          Business Support
            Direct Phone Access
            4 Hours
            1 hour (if resource is down)
          Enterprise On-Ramp Support
            30 mins response
          Enterprise Support
            15 mins
            dedicated TAM 
      8.6 AWS Market place
          Infrastructure Software
          DevOps
          Data Products
          Professional Services
          Business Applications
          Machine Learning
          Industries
          Internets of Things
          



# 9 Migration
    9.1 Cloud Adoption Framework
      Business
      People
      Governance
      Platform
      Security
      Operations
    9.2 Six R's
      Time
      Cost
      Criticality

      Lift and Shift
      Replatforming (few Cloud Optimization)
      Retire
      Retain
      Repurchasing
      Refactoring
    9.3 
      AWS SNOW Cone (14 TB)
      AWS SnowBall Edge (Compute/Storage Optimzed 80TB)
      AWs SnowMobile(100 PB)
    9.4 
      VMWare Cloud on AWS
      Amzaon SageMaker
      Amazon Augmented AI (A2I)
      Amazon Lex
      Amazon Textract
      Amazon DeepRacer
      AWS Ground Station

# 10 
    AWS Well Architected Framework

      Operational Excellence
        Operational excellence is the ability to run and monitor systems to deliver business value and to continually improve supporting processes and procedures.  
      Security
        Is the ability to protect information, systems, and assets while delivering business value through risk assessments and mitigation strategies. 
      Reliability
        Reliability is the ability of a system to do the following:

          Recover from infrastructure or service disruptions
          Dynamically acquire computing resources to meet demand
          Mitigate disruptions such as misconfigurations or transient network issues
      Performance Efficiency
        Performance efficiency is the ability to use computing resources efficiently to meet system requirements and to maintain that efficiency as demand changes and technologies evolve. 
      Cost Optimization
        Cost optimization is the ability to run systems to deliver business value at the lowest price point. 
      Sustainability
        Improve sustainability impacts by reducing energy consumption and increasing efficiency across all components of a workload by maximizing the benefits from the provisioned resources and minimizing the total resources required
      
    10.2 Benefits
      Scale,Flexible,Reliable,Secure

      Trade fixed expense for variable expense
      Benefits from massive economies of scale.
      Stop guessing capacity - Scaling on AWS
      Increased spead and agility
      Stop spending money running and maintaining data centers.
      Go Global in minutes


    





    
    
# AWS Compute Services
    Instances
      EC2 
      EC2 Spot
      EC2 AutoScaling
      Amazon Lightsail -- Easy-to-use cloud platform that offers you everything you need to build an application or website 
      AWS Batch -- Fully managed batch processing at any scale
    Containers
      ECS 
      ECS Anywhere -- Run containers on customer-managed infrastructure
      ECS Fargate - Serverless compute for containers
      ECR (Container Registry)
      EKS
      EKS Anywhere  - Create and operate Kubernetes clusters on your own infrastructure
      Amazon App Runner - Build and run containerized applications on a fully managed service
    Serverless
      AWS Lambda - Run code without thinking about servers.
    Edge and hybrid
      AWS Outposts - Run AWS infrastructure and services on premises 
      AWS Snow Family - Collect and process data in rugged or disconnected edge environments
      AWS Wavelength - Deliver ultra-low latency application for 5G devices
      VMware Cloud on AWS -  Preferred service for all vSphere workloads to rapidly extend and migrate to the cloud
      AWS Local Zones -- Run latency sensitive applications closer to end-users
    Cost and capacity management
      AWS Savings Plan - Flexible pricing model that provides savings of up to 72% on AWS compute usage
      AWS Compute Optimizer - Recommends optimal AWS compute resources for your workloads to reduce costs and improve performance
      AWS Elastic Beanstalk - Easy-to-use service for deploying and scaling web applications and services
      EC2 Image Builder - Build and maintain secure Linux or Windows Server images
      ELB - Automatically distribute incoming application traffic across multiple targets
    
    The AWS Nitro System
       With the Nitro System, offload virtualization functions(protect the physical hardware and BIOS, virtualize the CPU, storage, and networking, and provide a rich set of management capabilities) to dedicated hardware and software, and reduce our costs by delivering all of the resources of a server to customers.
          The Nitro System is comprised of three main parts: The Nitro Cards are a family of cards that offloads and accelerates I/O for functions including 
            Amazon Virtual Private Cloud (VPC), 
            Amazon Elastic Block Store (EBS), and 
            Amazon EC2 instance storage, 
          ultimately increasing overall system performance

    Amazon Lightsail offers a simple cloud platform at a low, predictable price. AWS Amplify is a set of tools and services to help front-end web and mobile developers build scalable full stack applications. The AWS Marketplace is a digital catalog with thousands of software listings from independent software vendors that make it easy to find, test, buy, and deploy software that runs on AWS






