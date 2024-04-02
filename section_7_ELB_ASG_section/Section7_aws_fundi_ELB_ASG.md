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
- Cross-Zone Load Balancing
  - ALB: enabled by default can be disabled at the Target Group level, no charge for inter AZ data.
  - NLB & GLB: disabled by default and you are charged for inter AZ data if enabled
- SSL/TLS:
  - Server Name Indication (SNI): Solves the problem of loading multiple TLS certificates onto one web server(to serve multiple websites)
  - SNI supports the new protocol that requires the client to indicate the hostname of the target server in the inital TLS handshake.
  - SNI only works with ALB & NLB, CLoudFront.
  - Connecton Draining: Also known as Deregistration Delay for ALB & NLB. You can set a time for exisiting user to finish a session on the Ec2 instance and the LB will not allow new connections.
- Sticky Session feature ensures traffic for the same client is always redireted tot he same target. Helps slients not lose their session data. (duration cookies and application cookies.)

### Application Load Balancer (ALB)

- ALB can route traffic to different Target Groups based on URL Path, Hostname, HTTP Headers and Query Strings.
- Some registered targets in a Target Group for an ALB are: Lambda Functions, Private IP Addresses, and EC2 Instances.
- Use for Docker/ containers.
- Can be infront of Lambda functions
- Query Strings/ Parameters Routing: ?Platform = Moblie and ?Platform = Desktop
- ALB provides a static DNS name but it does NOT provide a static IP.
- ALB can be configured to add X-Forwarded-For header which will add the client IP address to track where the request originated from.
- X-Forwarded-For header modes: append(add client's IP), preserve(leave as is), remove(have the ALB remove the header from the request before forwarding.)

### Network Load Balancer (NLB)

- Works on the layer 4 of the osi model (transport layer) focused on TCP and UDP.
- NLB provides both static DNS name and static IP address.

### Gateway Load Balancer (GLB)

- Used mostly as a Firewall and does packet analysis.

## Auto Scaling Group (ASG)

- Allow to set a minimum, desired, and maximum capacities. (number of ec2 instances for example.)
- ASG work with load balancers: requires Launch Template.
- ASG also can work with CloudWatch Alarms & Scaling. (set a policy to change the behavior of the ASG: CPU% for example.)
- Scaling Policies:
  - Dynamic Scaling: Set a target tracking scaling on a metric.
  - Simple/ Step Scaling: Set for when a Cloud Watch alarm is triggered.
  - Scheduled Scaling: Known usage pattern.
  - Predictive Scaling: Create forecast based on known past usage.
- Good metrics to scale on: CPU Utilization, Request Count Per Target, Average Network In/Out, or set up your own in cloudwatch.
- ASG Scaling Cooldown (Cooldown Period): 5 min window to allow the metrics to stability. (possilbe to reduce the cooldown time.)
- Instance Refresh: Allows you to update a whole ASG by providing a new Launch template.
