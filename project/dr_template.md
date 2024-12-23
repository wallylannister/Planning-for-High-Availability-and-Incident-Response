# Infrastructure

## AWS Zones
- **us-east-2** (Ohio)
- **us-west-1** (N. California)

## Servers and Clusters

### Table 1.1 Summary
| Asset              | Purpose                               | Size               | Qty | DR                                                                                                           |
|--------------------|---------------------------------------|--------------------|-----|--------------------------------------------------------------------------------------------------------------|
| Ubuntu-Web         | Web server for hosting applications    | t3.micro           | 3   | Deployed in multiple availability zones for redundancy.                                                      |
| Udacity-cluster    | EKS cluster for container orchestration | n/a                | 2   | Set up in both regions with 2 nodes each for high availability and failover capability.                    |
| udacity_cluster-p   | Primary database cluster               | db.t3.medium       | 2   | Replicated in the other region for disaster recovery.                                                        |
| udacity-lb-tf      | Application Load Balancer              | n/a                | 2 | Deployed each in both regions to ensure high availability and traffic distribution.                              |

### Descriptions
1. **Ubuntu-Web**: This asset serves as the primary web server hosting the application. It is configured to handle incoming traffic and serve web pages to users.
2. **Udacity-cluster**: This is an Amazon EKS (Elastic Kubernetes Service) cluster that manages the deployment of containerized applications. Each cluster consists of 2 nodes to ensure scalability and reliability.
3. **udacity_cluster-p**: The primary database cluster that stores application data. It is set up for high availability and is replicated to another region for disaster recovery.
4. **udacity-lb-tf**: This is an Application Load Balancer (ALB) deployed in each region to distribute incoming application traffic across multiple targets, ensuring fault tolerance and scalability.

## DR Plan
### Pre-Steps:
1. Deploy the Terraform code to both the primary and secondary regions.
2. Ensure that all necessary resources (EC2 instances, EKS clusters with 2 nodes each, RDS instances) are provisioned in the secondary region.
3. Configure the VPC with IPs in multiple availability zones to allow communication between resources in both regions.

### Steps:
1. **Failover the database (RDS) instance**: Promote the read replica in the secondary region to a primary instance.
2. **Point the load balancer DNS**: Update the DNS settings to point to the application load balancer in the secondary region.
3. **Redirect traffic**: Ensure that all incoming traffic is routed to the secondary region's resources.
4. **Verify application functionality**: Conduct tests to ensure that the application is fully operational in the new region.
