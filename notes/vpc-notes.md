## Amazon VPC

Amazon Virtual Private Cloud (Amazon VPC) is a customizable, isolated section of the AWS cloud where users can launch and manage different AWS resources, such as databases and servers, within a virtual private network.

An AWS VPC is like a virtual house for your cloud resources, such as S3 and EC2. Just as walls in a house separate rooms, a VPC keeps different resources isolated from one another. This means databases and servers can be kept separate. You have full control over each "room" or subnet and its permissions, allowing you to keep servers in one subnet and databases in another.

![AWS VPC Diagram](assets/vpc-project//aws_vpc_diagram.png)

VPCs are region-specific, meaning each VPC exists within a specific AWS region and cannot span across regions. Within each region, there are multiple availability zones (AZs), which can be utilized to create subnets. Each subnet is confined to a single availability zone, but multiple subnets can exist within one availability zone.