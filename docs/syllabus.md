# AWS DevOps Batch 4 - Complete Syllabus

## 🎯 Course Objectives
By the end of this course, students will be able to:
- Design and implement scalable cloud infrastructure on AWS
- Automate deployment processes using CI/CD pipelines
- Implement Infrastructure as Code using Terraform and CloudFormation
- Set up monitoring, logging, and alerting systems
- Implement security best practices in cloud environments
- Troubleshoot and optimize cloud applications
- Master containerization and orchestration with Docker and Kubernetes
- Implement comprehensive CI/CD pipelines with modern DevOps tools

## 📅 Course Duration
- **Total Duration:** 14 Weeks
- **Sessions per Week:** 3 sessions (Theory + hands-on)
- **Session Duration:** 2 hours each
- **Total Hours:** 80 hours

## 📚 Module Breakdown

### **Module 1: AWS Fundamentals & Identity Management (Weeks 1-2)**

#### Week 1: AWS Cloud Fundamentals
- **Day 1:** Introduction to Cloud Computing & AWS
  - Cloud computing concepts and benefits
  - AWS global infrastructure (Regions, AZs, Edge Locations)
  - AWS pricing models (On-demand, Reserved, Spot)
  - AWS management console and service overview
  - AWS CLI installation and configuration

- **Day 2:** AWS Account Setup & Best Practices
  - Creating AWS account with proper security
  - Multi-factor authentication (MFA) setup
  - Billing alerts and cost management
  - AWS Organizations and account structure
  - AWS Well-Architected Framework introduction

- **Day 3:** Hands-on Lab - AWS Console Navigation
  - Exploring AWS services and console
  - Setting up billing alerts and budgets
  - AWS CLI basic commands and configuration
  - Creating IAM users and groups

#### Week 2: Identity & Access Management (IAM)
- **Day 1:** IAM Fundamentals
  - IAM users, groups, and roles
  - IAM policies and permissions (JSON format)
  - Principle of least privilege
  - IAM best practices and security
  - IAM access keys and temporary credentials

- **Day 2:** Advanced IAM Concepts
  - Cross-account access and roles
  - Identity federation (SAML, OIDC)
  - IAM access analyzer and policy simulator
  - Service control policies (SCPs) in Organizations
  - AWS SSO and centralized access management

- **Day 3:** Hands-on Lab - IAM Implementation
  - Creating IAM users, groups, and roles
  - Implementing least privilege access policies
  - Setting up cross-account roles
  - Testing IAM policies and permissions

### **Module 2: Compute Services (Weeks 3-4)**

#### Week 3: Amazon EC2 & Compute Services
- **Day 1:** EC2 Fundamentals
  - EC2 instance types and families (General Purpose, Compute Optimized, Memory Optimized, etc.)
  - AMIs and instance lifecycle management
  - Security groups and key pairs
  - Instance metadata service (IMDSv2)
  - EC2 placement groups and networking

- **Day 2:** EC2 Advanced Features
  - Auto Scaling groups and policies
  - Application Load Balancer (ALB) and Network Load Balancer (NLB)
  - Spot instances and savings plans
  - Instance store vs EBS volumes
  - EC2 instance recovery and monitoring

- **Day 3:** Hands-on Lab - EC2 Deployment
  - Launching EC2 instances with different configurations
  - Configuring security groups and networking
  - Setting up auto scaling groups
  - Implementing load balancing

#### Week 4: Serverless Computing & Containers
- **Day 1:** AWS Lambda & Serverless
  - Lambda functions and runtime environments
  - Event sources and triggers (S3, DynamoDB, API Gateway, etc.)
  - Cold starts and optimization strategies
  - Lambda layers and extensions
  - Lambda monitoring and debugging

- **Day 2:** Container Services (ECS, EKS, Fargate)
  - Amazon ECS (Elastic Container Service)
  - Amazon EKS (Elastic Kubernetes Service)
  - Docker basics and containerization
  - Container orchestration concepts
  - Fargate vs EC2 launch types
  - Container security and best practices

- **Day 3:** Hands-on Lab - Serverless & Container Applications
  - Creating Lambda functions with different triggers
  - Deploying containers on ECS with Fargate
  - API Gateway integration with Lambda
  - Setting up EKS cluster and deploying applications

### **Module 3: Storage & Database Services (Weeks 5-6)**

#### Week 5: Storage Services
- **Day 1:** Amazon S3 & Object Storage
  - S3 buckets and objects management
  - Storage classes (Standard, IA, Glacier, etc.) and lifecycle policies
  - S3 security and encryption (SSE-S3, SSE-KMS, SSE-C)
  - S3 versioning and cross-region replication
  - S3 access points and bucket policies

- **Day 2:** Block & File Storage (EBS, EFS, Storage Gateway)
  - Amazon EBS volumes and snapshots
  - EFS file systems and access points
  - Storage Gateway for hybrid storage
  - Storage optimization and performance tuning
  - Backup and disaster recovery strategies

- **Day 3:** Hands-on Lab - Storage Implementation
  - Creating S3 buckets with proper security and encryption
  - Implementing lifecycle policies and versioning
  - Setting up EBS snapshots and AMI creation
  - Configuring EFS file systems

#### Week 6: Database Services
- **Day 1:** Relational Databases (RDS, Aurora)
  - Amazon RDS and supported database engines
  - Aurora database engine and architecture
  - Multi-AZ deployments and failover
  - Read replicas and read scaling
  - RDS backup and recovery strategies

- **Day 2:** NoSQL Databases (DynamoDB, ElastiCache, Redshift)
  - Amazon DynamoDB tables and data modeling
  - DynamoDB streams and change data capture
  - Global tables and multi-region replication
  - DAX (DynamoDB Accelerator) caching
  - ElastiCache (Redis/Memcached) for caching
  - Amazon Redshift for data warehousing

- **Day 3:** Hands-on Lab - Database Deployment
  - Setting up RDS instances with proper security
  - Creating DynamoDB tables with optimal design
  - Implementing backup and recovery strategies
  - Configuring ElastiCache clusters

### **Module 4: Networking & Security (Weeks 7-8)**

#### Week 7: Networking Fundamentals
- **Day 1:** Amazon VPC & Networking
  - VPC components and architecture (CIDR blocks, subnets)
  - Subnets (public, private, database) and route tables
  - Internet Gateway and NAT Gateway
  - VPC peering and Transit Gateway
  - VPC endpoints for AWS services

- **Day 2:** Advanced Networking Services
  - Route 53 DNS service and routing policies
  - CloudFront CDN and edge locations
  - API Gateway for REST and WebSocket APIs
  - VPC endpoints and private connectivity
  - AWS Global Accelerator

- **Day 3:** Hands-on Lab - Network Setup
  - Creating custom VPC with proper subnet design
  - Setting up public and private subnets with route tables
  - Configuring NAT Gateway and security groups
  - Setting up VPC endpoints

#### Week 8: Security & Compliance
- **Day 1:** Security Services & Monitoring
  - AWS Shield (Standard & Advanced) and WAF
  - AWS Config and GuardDuty threat detection
  - CloudTrail and CloudWatch monitoring
  - AWS Secrets Manager and KMS
  - AWS Security Hub and compliance

- **Day 2:** Compliance & Governance
  - AWS Organizations and account management
  - Control Tower for multi-account governance
  - Well-Architected Framework security pillar
  - Security best practices and compliance standards
  - AWS Artifact and compliance reports

- **Day 3:** Hands-on Lab - Security Implementation
  - Setting up CloudTrail and CloudWatch monitoring
  - Implementing WAF rules and security policies
  - Configuring AWS Config and GuardDuty
  - Setting up Secrets Manager and KMS

### **Module 5: DevOps Tools & CI/CD (Weeks 9-10)**

#### Week 9: Version Control & Collaboration
- **Day 1:** Git & GitHub/GitLab
  - Git fundamentals and version control concepts
  - Branching strategies (GitFlow, GitHub Flow)
  - Code review processes and pull requests
  - GitHub Actions and GitLab CI/CD basics
  - Repository management and collaboration

- **Day 2:** Code Quality & Testing
  - Static code analysis tools (SonarQube, ESLint, Pylint)
  - Unit and integration testing frameworks
  - Code coverage and quality gates
  - SonarQube integration and quality metrics
  - Automated testing strategies

- **Day 3:** Hands-on Lab - Git Workflow
  - Setting up Git repository with proper structure
  - Implementing branching strategy and workflows
  - Code review process and collaboration
  - Setting up GitHub Actions workflows

#### Week 10: CI/CD Pipelines
- **Day 1:** AWS CodePipeline & CodeBuild
  - Pipeline components and stages
  - Source, build, and deploy stages
  - Pipeline triggers and webhooks
  - Pipeline monitoring and notifications
  - CodeBuild and build specifications

- **Day 2:** Jenkins & Other CI/CD Tools
  - Jenkins installation and configuration
  - Pipeline as Code (Jenkinsfile) and declarative pipelines
  - Integration with AWS services (ECR, S3, etc.)
  - Blue-green deployments and rollback strategies
  - CircleCI, GitLab CI/CD, and other tools

- **Day 3:** Hands-on Lab - CI/CD Implementation
  - Creating CodePipeline with multiple stages
  - Setting up Jenkins pipeline with AWS integration
  - Implementing automated testing and deployment
  - Blue-green deployment implementation

### **Module 6: Infrastructure as Code (Weeks 11-12)**

#### Week 11: Terraform Fundamentals
- **Day 1:** Terraform Basics & HCL
  - Terraform installation and setup
  - HCL (HashiCorp Configuration Language) syntax
  - Providers and resources
  - State management and backend configuration
  - Terraform workflow (init, plan, apply, destroy)

- **Day 2:** Advanced Terraform Concepts
  - Modules and reusability
  - Variables, outputs, and locals
  - Remote state storage (S3, Azure, GCS)
  - Workspaces and environment management
  - Terraform Cloud and enterprise features

- **Day 3:** Hands-on Lab - Terraform Infrastructure
  - Creating VPC and networking with Terraform
  - Deploying EC2 instances and auto scaling groups
  - Managing state files and backend configuration
  - Creating reusable modules

#### Week 12: CloudFormation & Other IaC Tools
- **Day 1:** AWS CloudFormation
  - CloudFormation templates (JSON/YAML)
  - Stacks and stack sets
  - Change sets and drift detection
  - Nested stacks and cross-stack references
  - CloudFormation macros and custom resources

- **Day 2:** CDK and Configuration Management
  - AWS CDK (TypeScript/Python) and CDK constructs
  - Ansible for configuration management and automation
  - Packer for AMI creation and image management
  - Terraform vs CloudFormation comparison and use cases
  - Chef and Puppet for configuration management

- **Day 3:** Hands-on Lab - Multi-Tool IaC
  - CloudFormation template creation and deployment
  - CDK application development with TypeScript
  - Ansible playbook creation for server configuration
  - Multi-tool infrastructure deployment

### **Module 7: Monitoring & Logging (Weeks 13-14)**

#### Week 13: Monitoring & Observability
- **Day 1:** CloudWatch Fundamentals
  - CloudWatch metrics and alarms
  - Custom metrics and dashboards
  - CloudWatch logs and log groups
  - CloudWatch insights and log queries
  - CloudWatch events and event rules

- **Day 2:** Advanced Monitoring & APM
  - Application performance monitoring (APM)
  - Distributed tracing with AWS X-Ray
  - Synthetic monitoring and canaries
  - Real-time monitoring and alerting
  - Third-party monitoring tools (Prometheus, Grafana)

- **Day 3:** Hands-on Lab - Monitoring Setup
  - Creating CloudWatch dashboards and widgets
  - Setting up alarms and SNS notifications
  - Implementing custom metrics and logging
  - Setting up X-Ray tracing

#### Week 14: Logging & Analytics
- **Day 1:** Centralized Logging & ELK Stack
  - CloudWatch Logs and log streams
  - Log aggregation strategies and patterns
  - Log retention and archival policies
  - Log analysis and insights
  - ELK Stack (Elasticsearch, Logstash, Kibana) integration

- **Day 2:** Advanced Analytics & Big Data
  - AWS X-Ray for distributed tracing
  - CloudWatch Insights and log queries
  - Log-based metrics and custom dashboards
  - Real-time log processing and streaming
  - AWS Glue and data analytics services

- **Day 3:** Hands-on Lab - Logging Implementation
  - Setting up centralized logging with CloudWatch
  - Creating log-based dashboards and metrics
  - Implementing log retention policies and archival
  - Setting up ELK Stack for log analysis

### **Module 8: Advanced Topics & Projects (Weeks 15-16)**

#### Week 15: Advanced DevOps Practices
- **Day 1:** Microservices & Container Orchestration
  - Microservices architecture and design patterns
  - Container orchestration with Kubernetes (EKS)
  - Service mesh (Istio, Linkerd) implementation
  - Serverless microservices with Lambda and API Gateway
  - Container security and best practices

- **Day 2:** Performance & Optimization
  - Performance testing and load testing tools
  - Load balancing strategies and algorithms
  - Caching mechanisms (Redis, ElastiCache, CloudFront)
  - Cost optimization and resource management
  - Auto-scaling and performance tuning

- **Day 3:** Hands-on Lab - Advanced Deployment
  - Deploying microservices on EKS
  - Implementing blue-green and canary deployments
  - Performance testing with tools like JMeter
  - Setting up service mesh with Istio

#### Week 16: Final Projects & Certification Prep
- **Day 1:** Project Planning & Architecture
  - Project requirements analysis and scope definition
  - Architecture design and system planning
  - Implementation planning and timeline
  - Team collaboration and project management
  - Risk assessment and mitigation strategies

- **Day 2:** Project Implementation & Deployment
  - Building complete DevOps pipeline with CI/CD
  - Infrastructure deployment using Terraform/CloudFormation
  - Application deployment and configuration
  - Testing and validation (unit, integration, performance)
  - Monitoring and alerting setup

- **Day 3:** Project Presentation & Certification Prep
  - Project demonstrations and presentations
  - AWS certification overview and exam paths
  - Exam preparation strategies and study plans
  - Course wrap-up and next steps
  - Industry best practices and career guidance

## 📊 Assessment Criteria

### **Continuous Assessment (60%)**
- **Weekly Quizzes:** 20%
- **Hands-on Labs:** 30%
- **Assignments:** 10%

### **Final Project (40%)**
- **Project Implementation:** 25%
- **Documentation:** 10%
- **Presentation:** 5%

### **Grading Scale**
- **A (90-100%):** Excellent understanding and implementation
- **B (80-89%):** Good understanding with minor issues
- **C (70-79%):** Satisfactory understanding with some gaps
- **D (60-69%):** Basic understanding with significant gaps
- **F (Below 60%):** Insufficient understanding

## 🎓 Certification Path

### **Recommended AWS Certifications**
1. **AWS Certified Cloud Practitioner** (Entry-level)
2. **AWS Certified Solutions Architect - Associate**
3. **AWS Certified Developer - Associate**
4. **AWS Certified DevOps Engineer - Professional**

### **Additional Certifications**
- **Terraform Associate**
- **Docker Certified Associate**
- **Kubernetes Administrator (CKA)**

## 📚 Additional Resources

### **Books**
- "AWS Certified Solutions Architect Study Guide" by Ben Piper
- "Terraform: Up & Running" by Yevgeniy Brikman
- "The Phoenix Project" by Gene Kim

### **Online Resources**
- AWS Documentation and Whitepapers
- AWS Well-Architected Framework
- HashiCorp Learn
- Kubernetes Documentation

### **Practice Platforms**
- AWS Free Tier
- Terraform Cloud (Free tier)
- GitHub Student Developer Pack
- AWS Skill Builder

---

**Note:** This syllabus is subject to updates based on AWS service changes and industry best practices.
