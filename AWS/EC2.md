# Amazon Elastic Compute Cloud (EC2)

---

### 1. What is an EC2 instance type, and how do you choose the right one for your application?

An EC2 instance type determines the hardware of the host computer used for your instance. Each type offers different compute, memory, and storage capabilities. To choose the right instance type:
- **Understand your application needs**: Determine if you need more CPU, memory, storage, or network performance.
- **Evaluate instance families**: Choose from general-purpose, compute-optimized, memory-optimized, storage-optimized, and accelerated computing families.
- **Test different types**: Use AWS Free Tier or On-Demand instances to test and compare performance.

---

### 2. What is an EC2 instance family, and when would you use one family over another?

EC2 instance families group instance types based on their capabilities:
- **General Purpose**: Balanced CPU, memory, and network (e.g., t3, m5). Use for web servers, development environments.
- **Compute Optimized**: High CPU performance (e.g., c5). Use for batch processing, media transcoding.
- **Memory Optimized**: High memory capacity (e.g., r5). Use for in-memory databases, real-time big data analytics.
- **Storage Optimized**: High storage performance (e.g., i3). Use for large data sets, NoSQL databases.
- **Accelerated Computing**: Use GPUs (e.g., p3). Use for machine learning, graphics processing.

---

### 3. Describe the typical steps involved in launching an EC2 instance.

1. **Log in to AWS Management Console**: Go to the EC2 Dashboard.
2. **Choose an Amazon Machine Image (AMI)**: Select a template that includes an operating system, applications, and configurations.
3. **Choose an Instance Type**: Select the hardware configuration.
4. **Configure Instance Details**: Specify the number of instances, network settings, IAM roles, and other configurations.
5. **Add Storage**: Define the size and type of storage volumes.
6. **Add Tags**: Assign metadata to your instance for easier management.
7. **Configure Security Group**: Set up firewall rules to control inbound and outbound traffic.
8. **Review and Launch**: Review your settings and click "Launch". Select or create a key pair for SSH access.

---

### 4. What is an EC2 user data script, and how can it be used during instance launch?

An EC2 user data script is a set of commands that runs when an instance starts. It can be used to:
- Install software packages.
- Configure applications.
- Apply updates.

**Steps to use a user data script**:
1. **Create the script**: Write a shell script with the necessary commands.
2. **Add the script during instance launch**: In the "Configure Instance" step, paste the script in the "User Data" field.

---

### 5. Explain the purpose of EC2 instance metadata and how you can access it from within an instance.

EC2 instance metadata provides information about your instance that you can use to configure or manage it. This includes instance ID, security groups, and public IP address.

**Accessing instance metadata**:
- Use the following URL from within the instance: `http://169.254.169.254/latest/meta-data/`
- Use `curl` or `wget` to fetch specific metadata values.

---

### 6. How can you create custom AMIs, and why might you want to do so?

A custom AMI is an image that you create from an existing EC2 instance, capturing its configuration and installed software.

**Steps to create a custom AMI**:
1. **Set up an EC2 instance**: Configure the instance with the desired software and settings.
2. **Create an AMI**: From the EC2 dashboard, select "Actions" > "Create Image".
3. **Configure image settings**: Provide a name and description, and specify the storage settings.
4. **Create**: Click "Create Image".

**Why create custom AMIs**:
- To replicate a pre-configured environment.
- To save time when launching new instances.
- To ensure consistency across multiple instances.

---

### 7. What are security groups, and how do they control inbound and outbound traffic to EC2 instances?

Security groups act as virtual firewalls for EC2 instances. They control the inbound and outbound traffic based on specified rules.

**Key points**:
- **Inbound rules**: Define the allowed incoming traffic.
- **Outbound rules**: Define the allowed outgoing traffic.
- **Stateful**: Responses to allowed inbound traffic are automatically allowed out, and vice versa.

---

### 8. Explain the use of Network Access Control Lists (NACLs) and how they differ from security groups.

NACLs provide an additional layer of security at the subnet level. They control inbound and outbound traffic to and from subnet level.

**Differences**:
- **NACLs**: Operate at the subnet level, are stateless (each request needs a rule), and support both allow and deny rules.
- **Security Groups**: Operate at the instance level, are stateful, and support only allow rules.

---

### 9. How do you enable and configure AWS Web Application Firewall (WAF) in front of an EC2-based web application?

1. **Create a Web ACL**: Define the rules to filter traffic (e.g., IP match, SQL injection match).
2. **Add rules to the Web ACL**: Specify the conditions for the rules.
3. **Associate the Web ACL with resources**: Link it to your CloudFront distribution or Application Load Balancer (ALB) that routes traffic to your EC2 instances.

---

### 10. What is Auto Scaling, and how can it be used to ensure high availability and scalability of EC2 instances?

Auto Scaling automatically adjusts the number of EC2 instances in your application based on demand.

**Benefits**:
- **High Availability**: Replaces unhealthy instances.
- **Scalability**: Adds or removes instances based on traffic.

**Steps to set up Auto Scaling**:
1. **Create a launch configuration**: Define the AMI, instance type, and other settings.
2. **Create an Auto Scaling group**: Specify the launch configuration, VPC, and scaling policies.
3. **Define scaling policies**: Set rules for adding or removing instances.

---

### 11. Explain the purpose of Amazon Elastic Load Balancing (ELB) and its integration with EC2 instances.

ELB distributes incoming traffic across multiple EC2 instances, ensuring no single instance is overwhelmed.

**Benefits**:
- **Improves fault tolerance**: Distributes traffic to healthy instances.
- **Enhances scalability**: Adjusts traffic based on load.

**Integration**:
- **Attach EC2 instances**: Register instances with the load balancer.
- **Configure health checks**: ELB checks the health of instances and routes traffic only to healthy ones.

---

### 12. What is Amazon EC2 Container Service (ECS), and how does it help with containerized applications on EC2 instances?

Amazon ECS is a fully managed container orchestration service that simplifies running containerized applications on EC2 instances.

**Benefits**:
- **Scalability**: Easily scales containerized applications.
- **Management**: Automates deployment and management of containers.
- **Integration**: Works with Docker containers and integrates with other AWS services.

---

### 13. How can you configure Amazon Route 53 for DNS-based load balancing of EC2 instances?

1. **Create a hosted zone**: Set up a domain name.
2. **Create record sets**: Define DNS records pointing to your EC2 instances or ELB.
3. **Set routing policies**: Choose policies like weighted, latency-based, or failover for traffic distribution.

---

### 14. What is a status check in EC2 instance?

Status checks monitor the health of your EC2 instances.

**Types of status checks**:
- **System status check**: Verifies the AWS infrastructure's functionality.
- **Instance status check**: Verifies the instance's network and operating system.

**View status checks**:
- Use the EC2 console or AWS CLI to monitor the status checks.

---

### 15. How to change instance types for running applications without downtime of application?

1. **Stop the instance**: Temporarily halt the instance.
2. **Change instance type**: Modify the instance type in the EC2 console or using AWS CLI.
3. **Start the instance**: Restart the instance with the new type.

**Note**: Ensure that your application can handle a short downtime during the change.

---

### 16. What is the difference between AMI and Snapshot?

- **AMI (Amazon Machine Image)**: A template that includes an operating system, applications, and configurations. Used to launch new instances.
- **Snapshot**: A backup of an EBS volume at a specific point in time. Used to restore volumes or create new AMIs.

---

### 17. How to handle boot-related issues like kernel panic in EC2 instances?

1. **Stop the instance**: Halt the instance showing kernel panic.
2. **Detach the root volume**: Disconnect the EBS root volume.
3. **Attach the volume to another instance**: Attach the volume to a healthy instance.
4. **Fix the issue**: Access the volume and correct configuration or file issues.
5. **Reattach the volume**: Attach the volume back to the original instance.
6. **Start the instance**: Restart the instance and check if the issue is resolved.



---

### 18. How many maximum number of IPs can be attached to an instance?

An EC2 instance can have:
- **One primary private IP address**.
- **Multiple secondary private IP addresses** (up to the limit of the instance type).
- **One public IP address or Elastic IP address** per private IP address.

The exact number of secondary private IP addresses depends on the instance type.

---

### 19. Describe different types of purchasing options available in AWS?

1. **On-Demand Instances**: Pay by the hour or second without long-term commitments. Best for short-term, irregular workloads.
2. **Reserved Instances**: Commit to using an instance for a one- or three-year term and receive a discount. Best for steady-state usage.
3. **Spot Instances**: Bid for unused EC2 capacity and pay lower prices. Best for flexible, interruption-tolerant applications.
4. **Dedicated Hosts**: Physical servers dedicated to your use. Best for regulatory requirements and licensing constraints.
5. **Dedicated Instances**: Instances run on dedicated hardware. Best for workloads that require physical isolation.

---

### 20. What are the different types of AWS Placement Groups, and how do they differ?

1. **Cluster Placement Group**: Instances are placed close together in a single Availability Zone. Provides low-latency network performance.
2. **Spread Placement Group**: Instances are placed on distinct hardware to reduce the risk of simultaneous failures. Used for critical applications.
3. **Partition Placement Group**: Instances are divided into logical partitions, each with its own set of racks. Used for large distributed and replicated workloads.

---

### 21. Can you change the placement group of a running EC2 instance?

No, you cannot change the placement group of a running instance. To move an instance to a different placement group, you must:
1. Stop the instance.
2. Create an AMI from the instance.
3. Launch a new instance from the AMI in the desired placement group.

---

### 22. What is the difference between an Availability Zone and a Placement Group?

- **Availability Zone (AZ)**: A distinct location within a region, designed to be isolated from failures in other AZs. Provides high availability.
- **Placement Group**: A logical grouping of instances within a single AZ to optimize network performance or reduce the risk of simultaneous failures.

---

### 23. What are some best practices for using Placement Groups in AWS?

- Use **Cluster Placement Groups** for low-latency, high-throughput applications.
- Use **Spread Placement Groups** for critical applications that need to minimize failure risk.
- Use **Partition Placement Groups** for large distributed workloads.
- Ensure all instances in a Cluster Placement Group are of the same instance type to maximize performance.
- Plan your capacity needs in advance to avoid insufficient capacity errors.

---

### 24. Explain the limitations or constraints of AWS Placement Groups?

- **Cluster Placement Groups**: Limited to a single AZ, instances must be of the same instance type.
- **Spread Placement Groups**: Limited to seven running instances per AZ per group.
- **Partition Placement Groups**: Limited to seven partitions per AZ, recommended for large-scale distributed applications.

---

### 25. Give examples of scenarios or applications where each type of EBS volume (gp2, io1, st1, sc1, gp3) is the most appropriate choice.

- **gp2 (General Purpose SSD)**: Boot volumes, low-latency applications, development and test environments.
- **io1 (Provisioned IOPS SSD)**: Databases, I/O-intensive applications requiring consistent IOPS.
- **st1 (Throughput Optimized HDD)**: Big data, data warehouses, log processing requiring high throughput.
- **sc1 (Cold HDD)**: Infrequently accessed data, archival storage.
- **gp3 (General Purpose SSD)**: Boot volumes, medium to high-performance applications with a lower cost than io1/io2.

---

### 26. What is Amazon Elastic Block Store (EBS), and how does it differ from Amazon S3?

- **Amazon EBS**: Block storage for EC2 instances, designed for high-performance access to data. Ideal for databases, file systems, or applications requiring frequent read/write operations.
- **Amazon S3**: Object storage for unstructured data, designed for scalability, durability, and cost-effectiveness. Ideal for backups, media hosting, and big data storage.

---

### 27. What are the different types of EBS volumes available, and when would you use each type (e.g., gp2, io1, st1, sc1, gp3)?

- **gp2 (General Purpose SSD)**: Use for a wide range of workloads, including boot volumes and general-purpose applications.
- **io1 (Provisioned IOPS SSD)**: Use for applications requiring high IOPS and consistent performance, like databases.
- **st1 (Throughput Optimized HDD)**: Use for frequently accessed, throughput-intensive workloads.
- **sc1 (Cold HDD)**: Use for less frequently accessed data with lower cost requirements.
- **gp3 (General Purpose SSD)**: Use for applications needing high performance at a lower cost than io1/io2.

---

### 28. Explain the concept of Provisioned IOPS (PIOPS) and when it's necessary for achieving consistent performance.

Provisioned IOPS (PIOPS) allows you to specify a consistent IOPS performance level for your EBS volumes, essential for:
- Databases and other I/O-intensive applications.
- Workloads requiring predictable performance.
- Applications where performance consistency is critical.

---

### 29. How do you resize an EBS volume, and what precautions should be taken when doing so?

1. **Modify the volume**: Use the EC2 console or AWS CLI to increase the size of the volume.
2. **Extend the file system**: Log in to the instance and extend the file system to use the new space.

**Precautions**:
- Ensure you have backups or snapshots before resizing.
- Check compatibility with your operating system.
- Plan for potential downtime if your application does not support resizing without a restart.

---

### 30. What is the difference between EBS volume types and EBS volume size, and how do they impact performance?

- **EBS Volume Types**: Determines the performance characteristics (IOPS, throughput). For example, gp2 provides balanced performance, while io1 offers high IOPS.
- **EBS Volume Size**: Larger volumes can achieve higher throughput and IOPS. However, the volume type primarily dictates performance characteristics.

---

### 31. What is an EBS snapshot, and why is it important for data durability and disaster recovery?

An EBS snapshot is a point-in-time backup of an EBS volume stored in Amazon S3. It is important for:
- Data durability: Provides backups to restore in case of data loss.
- Disaster recovery: Enables recovery of instances and volumes in different regions.

---

### 32. How often should you create EBS snapshots, and what strategies can be employed for efficient backup and retention policies?

- **Frequency**: Regular intervals based on data change rate, application needs, and business requirements (e.g., daily, weekly).
- **Strategies**:
  - **Automate snapshots** using AWS Backup or Lambda.
  - **Incremental snapshots** to save storage space.
  - **Lifecycle policies** to manage retention and deletion of old snapshots.

---

### 33. What are the best practices for encrypting EBS volumes at rest, and how do you implement encryption?

- **Best Practices**:
  - Encrypt sensitive data at rest.
  - Use AWS Key Management Service (KMS) to manage encryption keys.
  - Enable encryption by default for new EBS volumes.

- **Implementation**:
  - When creating a new EBS volume, select the encryption option.
  - For existing volumes, create an encrypted snapshot and restore it to a new encrypted volume.

---

### 34. Describe the difference between EBS-backed and instance-store-backed EC2 instances and their respective advantages and limitations.

- **EBS-backed Instances**:
  - Persistent storage.
  - Data persists after instance stop/terminate.
  - Supports snapshot and volume resizing.

- **Instance-store-backed Instances**:
  - Temporary storage.
  - Data is lost when the instance stops/terminates.
  - Higher I/O performance for temporary data.

---

### 35. How can you monitor the performance and health of EBS volumes, and what AWS services or tools can assist in this process?

- **CloudWatch**: Monitor metrics like IOPS, throughput, and latency.
- **CloudWatch Alarms**: Set alarms for thresholds on performance metrics.
- **AWS Trusted Advisor**: Provides recommendations for improving performance and cost.
- **EBS Volume Metrics**: Use to analyze and optimize performance.

---
