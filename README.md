# Implementation-of-a-multi-tier-Cloud-network-on-AWS-VPC
This project focuses on the implementation of a multi-tier Cloud network to ensure high availability, enhanced security, and continuous compliance. By integrating advanced monitoring and security solutions, it ensures proactive protection and efficient management of Cloud resources.

Each layer has a specific role and is isolated for security and performance reasons.
A four-tier Cloud infrastructure centered on a VPC ensures that all levels can be managed independently.
The Management Layer reinforces control and infrastructure monitoring, and provides secure access through VPN configuration.
The Web Layer is responsible for direct interaction with clients and web page delivery. These first two layers are public and connected to an Internet Gateway (IGW).
The Application Layer hosts and processes requests.
The Data Layer is dedicated to storage, management, and data retrieval.
The use of three Availability Zones in our Cloud environment ensures high availability and better resilience.
We implemented EC2 instances across different subnets. At the Management layer, we set up a VPN and a monitoring tool — Uptime Kuma — to monitor the services used by the web servers.
At the Web layer, we deployed an EC2 instance hosting a web page, a database instance, and additional instances for testing purposes.

A VPC-centered Cloud infrastructure, with its configuration and monitoring components.
The infrastructure is hosted within a VPC, which allows full control over the network environment, including subnet configuration, routing tables, gateways, and more.
After configuring the VPC infrastructure and taking full control of the network environment, traffic logging is handled as follows — Flow Logs capture network traffic information within the VPC.
An IAM Role is associated with instances to provide the necessary permissions, for example to write logs or access other AWS services.
CloudTrail records API calls and tracks all actions performed on AWS resources.
CloudWatch is used to monitor system performance and events.
EventBridge enables the detection of specific events.
AWS Lambda is used to execute specific actions when events occur.
SNS Notification sends email notifications to the user.

To efficiently segment the network, we chose to divide the CIDR range 10.0.0.0/16 into 12 subnets of /22 size.
The use of CIDR (Classless Inter-Domain Routing) offers greater flexibility in IP address management (65,536 IP addresses). This makes it possible to create subnets of different sizes according to the company's needs.
A /22 subnet can contain up to 1,024 IP addresses, of which 1,022 are usable for hosts. This makes it a suitable choice for large or growing companies that require a high number of IP addresses for their hosts.

AWS uses routing tables to determine how network traffic should be directed across subnets, instances, and services within a VPC. Each subnet in a VPC is associated with a routing table, which determines the path that inbound and outbound traffic must follow. We associated a routing table for the public subnets of the Management and Web layers and attached an Internet Gateway. We associated two routing tables for the private subnets — one for the Application layer and one for the Data layer — and in each we attached a NAT Gateway.
Security Groups are virtual firewalls.

They apply at the instance level and control inbound and outbound network traffic on a network interface.
They operate in a stateful manner — meaning that if a rule allows inbound traffic, the associated outbound traffic is automatically allowed.
Network ACLs are used to control access to network resources.
They apply at the subnet level and evaluate traffic based on defined rules.
They operate in a stateless manner — meaning that separate rules must be created for both inbound and outbound traffic.
