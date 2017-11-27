# SysOps01

## VPC

Is made of IGW, Route Tables, NACLs, SGs, Subnets

- Max subnet is a /16 network

- AWS reserves 5 ips from the subnet’s pool

    - network address

    - first usable address for VPC router

    - second usable for dns

    - third reserved for aws’ future use

    - broadcast

- Subnets are locked to AZ, can not spread across AZ’s

    - eg 1 Subnet = 1 AZ

- Only 1 IGW per VPC

- Security Groups / resource

- NACLs / only one allowed per subnet

- VPC Peering with No Transitive Peering

### VPC Access

#### Gateway (IGW)

  1. IGW

  2. VPG

  3. CG

#### VPN

  1. Direct Connect (Connection in certain AZs where they have a partner)

    - Higher Bandwidth than VPN

    - VLAN like setup

    - Dedicated and Isolated

    - No Internet

    - HA supported

 2. Hardware-based VPN via VPG

### Creating a VPC (per region)

0. ipcalc tool for sub-netting

1. Tag, CIDR block (no larger than /16), Tenancy (set to Default $$$$)

2. Automatically creates a default SG, Route Table and NACL

3. Subnet and IGW needs to be manually created

### Creating a subnet

1. Tag, VPC, AZ, CIDR block

2. If public set Auto-Assign Public IP to yes

### Create a IGW

1. Create IGW and attach it to VPC (just 1 IGW per VPC)

### Add default route

1. Create a new route table and add the 0.0.0.0/0 to that route table using IGW

2. For security do not add 0.0.0.0/0 to Main route table 1.1 Everytime you create a new subnet it is going to use the Main route table

3. Associate the route table to the subnet

### What is NAT?

#### Add NAT instance

1. Create an EC2 instance and place it in the public subnet, marketplace NAT

2. Enable Source/Destination Check and disable in the EC2 instance

3. Add default route table 0.0.0.0/0 to NAT instance

#### Add NAT Gateway

1. Choose Subnet, Elastic IP

2. Add default route table 0.0.0.0/0 to NAT Gateway

3. It doesn’t sit behind a SG

|| NAT Gateway | NAT Instance | 
|---|---|---|
| Availability | yes | user managed |
| Bandwidth | up to 10Gbps | depends in instance type |
| Mantenaince | aws | user | 
| Performance | optimized | generic ami configured to nat |
| Cost | | |
| SG | not available | user managed sg |
| NACL | yes | yes |
| Flow logs | yes | yes |
| Port forwarding | no | user managed | 
| Can be used as bastion server | not supported | yes |
| Traffic meters | not supported | can see cloudwatch |
| Timeout behaviour | sends a RST | sends a FIN | 
| IP fragmentation | udp only | yes |
| Public IP | auto | user managed EIP |

### VPC Security

Stateless / Stateful Ephemeral ports / User ports (1025 - 49152 - 65535) Root Ports bastion hosts or jump boxes

- SGs (first line of defense)

    - Operates at instance/resource level (first level of defense)

    - allow-rules only

    - Stateful

    - Ingress Policy is set to DENY / does not create a default rule

    - Egress Policy is set to DENY / by default creates 1 rule to allow everything

    - All rules are evaluated

    - Has to be explicitly/manually attached to a resource

    - filters only destination ports

    - 5 per resource, 50 rules per sg, soft limit, 100 sgs per VPC

    - Instances can’t communicate unless allowed (by default sg allows communication within the same sg)

- NACLs (second line of defense)

    - Operates in subnet level (second layer of defense)

    - Supports allow and deny rules

    - Stateless

    - Rules processed in order by prio number match and out (cascade)

    - Auto applies to all resources within the subnet (backup layer of defense not to rely on sgs)

    - Policy is set to allowed until first allow rule

    - Policy is set to DENY

    - It is recommended to add rules numbered in increases of a 100

    - Has inbound/outbound rules

    - Filters both src and destination ports / IP’s

    - Soft limit 20, can be increased to 40 with performance downgrade

    - Use to block single IPs

### VPC Flow Logs

Enables to capture ip traffic flow information for the network interfaces in your resources

1. Filter

2. Role

    - create a role with
        * logs:CreateLogGroup
        * logs:CreateLogStream
        * logs:DescribeLogGroups
        * logs:DescribeLogStreams
        * logs:PutLogEvents

9. Destination Log Group
    0. create a log group
    1. log streams are created by eni

### Other resources

- [docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_Introduction.html](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_Introduction.html)

## return to Index
