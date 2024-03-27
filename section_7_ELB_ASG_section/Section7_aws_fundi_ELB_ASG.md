# Section 7: AWS Fundamentals: ELB + ASG

## Termiology

- Elastic Load Balancer (ELB): Scalable, cloud-based service that automatically distributes incoming application traffic across multiple targets, such as EC2 instances, to ensure optimal performance, fault tolerance, and high availability.
- Amazon Security Group (ASG): Virtual firewall that controls inbound and outbound traffic for Amazon EC2 instances, providing security by allowing or denying communication based on defined rulesets.
- Scalability: application/ system can handle greater loads
  - Vertical Scalability
  - Horizontal Scalabitliy (elasticity)
- High Availability: Design and implementation of systems and architectures that ensure applications remain accessible and operational with minimal downtime by utilizing redundant infrastructure, automated failover mechanisms, and distributed data centers across multiple availability zones.

## Elastic Load Balancer

- ELB is a aws fully managed service that can load balance for services such as: EC2, EC2 Auto Scaling Groups, ECS, AWS Certificate Manager (ACM), CloudWatch, Route 53, AWS WAF, AWS Global Accelerator
- ELB have a healthcheck capability which require: port and route.
- Four kinds of load balancers
  - Application Load Balancer (ALB): HTTP, HTTPS, WebSocket
  - Network Load Balancer (NLB): TCP, TLS (secure TCP), UDP
  - Gateway Load Balancer (GWLB): Operates at Layer 3 (Network layer) - IP Protocol
- Load Balancer Security: Create a Load Balancer Security group allowing external traffic to the LB only HTTPS/HTTP from anywhere. Then set up the Application security group to allow traffic only from the LB by setting the LB security group as the source.
