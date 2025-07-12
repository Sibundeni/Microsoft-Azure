Lab1.json: Basic Network Infrastructure
This ARM template defines a foundational network setup suitable for a simple multi-tier application.

Key Features
Virtual Network (vnet1)

Address space: 10.0.0.0/16

Subnets

webTierSubnet: 10.0.1.0/24

ApplicationTierSubnet: 10.0.2.0/24

DatabaeTierSubnet: 10.0.3.0/24

Network Security Group (nsg1)

Allows:

HTTP (port 80) & HTTPS (port 443) for WebASG

HTTPS (port 443) for ApplicationASG

SQL Server (port 1433) for DatabaseASG

Includes a "Deny All" inbound rule

Azure Load Balancer (loadbalancer1)

Frontend IP configuration

Backend address pool

Load balancing rules for ports 80 and 443

Health probes for HTTP and HTTPS

 Lab2.json: Parameterized Network with ASGs
This template introduces parameterization and Application Security Groups (ASGs) for flexible deployment.

 Key Features
Virtual Network

Configurable address space (default: 10.0.0.0/16)

Subnets

webSubnet: 10.0.1.0/24

appSubnet: 10.0.2.0/24

dbSubnet: 10.0.3.0/24

Network Security Group

Rules to allow:

HTTP (80) and HTTPS (443) inbound

Web-to-App (TCP 443)

App-to-DB (TCP 1433)

Final "Deny All" rule

Application Security Groups (ASGs)

WEB-ASG, APP-ASG, and DB-ASG for fine-grained control

Azure Load Balancer (webLoadBalancer)

Frontend IP linked to a public IP

Backend pool and load balancing rules

Health probes for ports 80 and 443

Public IP Address

Static IP for the load balancer

 Lab3.json: Advanced Multi-VNet Deployment
A full-featured deployment template integrating multiple VNets, NSGs, ASGs, DNS Zones, and a virtual machine.

 Key Features
Virtual Networks

CoreServiceVnet (10.20.0.0/16)

SharedServiceSubnet: 10.20.10.0/24

DatabaseSubnet: 10.20.20.0/24

ManufactoringVnet (10.30.0.0/16)

SensorSubnet1: 10.30.20.0/24

SensorSubnet2: 10.30.21.0/24

Network Security Groups

myNSGSecure

Allows ASG on ports 80 and 444

Denies outbound traffic on port 8080

Additional NSGs:

One with ssh_rule (TCP 22)

Another with default-allow-22

Application Security Group

ASG deployed for resource grouping

DNS Zones

Public DNS Zone: contoso.com

A record for www → 10.1.1.4

Private DNS Zone: private.contoso.com

Link for manufactoring-link

Record for sensorvm → 10.1.1.4

Virtual Machine

Ubuntu Server 22.04 LTS (Gen2)

SSH public key authentication

Connected to a subnet via NIC and public IP

