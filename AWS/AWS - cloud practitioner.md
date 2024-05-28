## Terminology

- **Data Center**: A group of servers. AWS has many data centers across the globe.
- **Virtualization**: Separating one single physical server into multiple small units called virtual machines (VM).

### AWS Payment Models

1. **On-Demand**: No upfront payment or long-term commitment.
2. **Pay-As-You-Go**: Pay by hour/second based on usage.

## Cloud Computing

**Cloud Computing**: Delivery of computing services over the internet, using AWS servers/data centers to store and compute data instead of local machines. One of the key benefits of cloud computing is the opportunity to **replace upfront capital infrastructure expenses with low variable costs that scale** with your business.

### Advantages

- Trade fixed expense for variable expense.
- Benefit from massive economies of scale.
- Stop guessing.
- Increase speed and agility.
- Stop spending money running and maintaining data centers.
- Go global in minutes.

### Types of Computing Services

1. **Compute**: EC2
2. **Storage**: S3
3. **Networking**: VPS
4. **Database**: RDS
5. **Development, Messaging and Deployment**: AWS Code Family
6. **Migration**: Migration hub
7. **AI and ML**: Rekognition
8. **Auditing and Logging**: Trust Advisor
9. **Security, Compliance and Governance**: IAM
10. **Pricing, Billing and Support**: Pricing Calculator

### Benefits

1. **High Availability**: Servers will not go down easily.
2. **Elasticity**: You don’t need to plan the capacity.
3. **Agility**.
4. **Durability**: Data will not corrupt.

## CapEx and OpEx

- **CapEx**: Capital expenditures, upfront purchases toward fixed assets.
- **OpEx**: Operating expenses, funds used to run day-to-day operations.

## Latency

The time passes between user request and the resulting response.

## AWS Regions

AWS has below Geographic locations:

| US WEST | South America | Africa | Australia |
| --- | --- | --- | --- |
| US EAST | Europe | Asia Pacific |     |

Each Geographic location can have multiple AWS Regions. For example US East has Ohio(**us-east-2**) and N. Virginia(**us-east-1**). Regions are fully independent and isolated. If one region is impacted by an earthquake, the rest will not be affected. Their resources and data are not replicated across them.

AWS Regions consist of multiple availability zones, consisting of one or more datacenters in different physical places. For example, **us-east-1a**, **us-east-1b** etc.

Each availability zone (AZ) is connected using low latency links. AZs are fault tolerant. If one AZ goes out of servers, rest will not be affected. They also have high availability. For example, if an application is running on us-east-1a only, it is not fault tolerant. To be fault tolerant, it should be spanned across multiple AZs.

If your application is across multiple AZs and it still went down, this might mean the whole region is down.

In summary, A region is global and made up of two or more AZs, an AZ is made up of multiple data centers, and Multi-AZ deployments provide high availability.

## Cloud Deployment Models

1. **Private Cloud**: On-premises internal data center, no cloud advantages.
2. **Public Cloud**: Offered by AWS, cloud advantages, no hardware responsibility.
3. **Hybrid Cloud**: Combines Private cloud and Public cloud. Sensitive data is stored locally, app runs on AWS, connected via VPN and **Direct Connect**.

## AWS Service Categories

| Category                      | Services                                       |
|-------------------------------|------------------------------------------------|
| Analytics                     | - Application integration                      |
|                               | - Blockchain                                   |
|                               | - Business applications                       |
|                               | - Cloud Financial Management                  |
|                               | - Robotics                                     |
|                               | - Cloud Transformation Domains                |
|                               | - Cloud Transformation Phases                 |
| Compute services              | - Customer enablement                          |
|                               | - Containers                                   |
|                               | - Databases                                    |
|                               | - Developer tools                              |
|                               | - Satellite                                    |
| End user computing            | - Front-end web and mobile services            |
|                               | - Game tech                                    |
|                               | - Internet of Things (IoT)                     |
|                               | - Machine Learning (ML) and Artificial Intelligence (AI) |
|                               | - Security, identity, and compliance           |
| Management and governance    | - Media                                        |
|                               | - Migration and transfer                       |
|                               | - Networking and content delivery              |
|                               | - Quantum technologies                         |
|                               | - Security, identity, and compliance           |
|                               | - Storage                                      |

## AWS Management Tools

- **AWS Management Console**: The web platform of AWS cloud.
- **AWS CLI**: AWS Command line interface has similar capabilities as the Management Console but mainly used by technical people with commands. Sometimes new features are available on CLI before the management console. Access is done through a **terminal** session. You can also access the resources using **Application code** or with **SDK**s.

## Root User

The most powerful user in the account, the only user who can delete every resource and the account. It should not be used for day-to-day tasks and not logged in often. Instead, it should have MFA enabled and create a new user group for regular usage.

## Cloud Computing Models

1. **Infrastructure as a Service (IaaS)**
2. **Software as a Service (SaaS)**
3. **Platform as a Service (PaaS)**: Developing using online tools.

## AWS Frameworks

1. **Cloud Adaptation Framework**
    - Perspectives and foundational capabilities
2. **Cloud Transformation Domains**  
        ![alt text](https://github.com/kcakar/StudyNotes/blob/master/AWS/aws1.png?raw=true)
3. **Cloud Transformation Phases**  
        ![alt text](https://github.com/kcakar/StudyNotes/blob/master/AWS/aws2.png?raw=true)
4. **Summary (What You Need to Know)**  
        ![alt text](https://github.com/kcakar/StudyNotes/blob/master/AWS/aws3.png?raw=true)

### Well-Architected Framework

**Overview**:

- Security: Using CloudTrail to log all actions.
- Cost Optimization: Using S3 Intelligent Tiering to automatically move data.
- Performance Efficiency: Using Lambda to run code with zero administration.
- Operational Excellence: Using CodeCommit for code and template version control.
- Reliability: Using Multi-AZ deployments of RDS databases.
- Sustainability: Using EC2 auto-scaling to ensure maximum utilization.

**General Design Principles**:

- Stop guessing your capacity needs.
- Test systems at production scale.
- Consider evolutionary architectures.
- Automate with architectural experimentation in mind.
- Drive architectures using data.
- Improve through game days.
