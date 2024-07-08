# AWS Project

## Introduction

The goal of this project is to gain proficiency in AWS through multiple projects focused on exploring various resources.

## Project One: Setting Up a VPC with WordPress

### Overview

In this project, we will establish an Amazon Virtual Private Cloud (Amazon VPC), create a subnet within it, and deploy an EC2 instance hosting WordPress into that subnet.

### Amazon VPC Overview

Amazon Virtual Private Cloud (Amazon VPC) is a customizable, isolated section of the AWS cloud where users can launch and manage different AWS resources, such as databases and servers, within a virtual private network.

An AWS VPC is like a virtual house for your cloud resources, such as S3 and EC2. Just as walls in a house separate rooms, a VPC keeps different resources isolated from one another. This means databases and servers can be kept separate. You have full control over each "room" or subnet and its permissions, allowing you to keep servers in one subnet and databases in another.

![AWS VPC Diagram](assets/vpc-project//aws_vpc_diagram.png)

VPCs are region-specific, meaning each VPC exists within a specific AWS region and cannot span across regions. Within each region, there are multiple availability zones (AZs), which can be utilized to create subnets. Each subnet is confined to a single availability zone, but multiple subnets can exist within one availability zone.

We deploy our EC2 instances into specific subnets within our VPC. Each subnet is associated with a single availability zone and cannot span across availability zones.

The VPC router handles all routing for connections that go outside of a subnet. Route tables define how traffic is routed within the VPC.

To enable internet access for resources within our VPC, we need an Internet Gateway. Each VPC can have one Internet Gateway, which facilitates outgoing (egress) and incoming (ingress) internet traffic.

Every VPC is defined by a CIDR block, which specifies the range of IP addresses available for assignment to its subnets.

### Steps

#### Step 1: Create a VPC

1. **Create a VPC with public and private subnets**
   - Go into the AWS consol and search for VPC.
   - On the left side navigation click on `Your VPC's`.
     - By deafult you get an AWS deafult VPC in every region in your AWS account, with a couple subnets for every availabity zone.
    - In the top right click the `Create VPC` button.
    - You should see a options to either to create `VPC only` or `VPC and more`. Click on `VPC and more`.
        - Using the `VPC and more` option, you can create your VPC, subnets, and route tables all at once, without needing to navigate to other sections of the AWS console.
    - Decide on the name of your project I've gone with `my-first-vpc`.


2. **Set Up a Subnets:**
    - Then we need to decide on the CIDR block. This is the network address space that is going to be used for private IP address for this VPC learn more here.
    - By default they give you `10.0.0.0/16`. You can change it to somthing else. I've changed it to `15.0.0.0/16`.
    - Keep everything else in this section the same.
    - In the next section we get to configure the availabilty zones. Leave it as `2`.
    - In the next section we can specificy the number of subnets. Also leave it as `2`.
    - In the next section it allows configuration of NAT gateways. But for this project keep it as `None`.
    - This is our public subnet, which is associated with a route table connected to an internet gateway, providing internet access.
    -  There are two private subnets, each with its own route table for intra-network traffic. They use a VPC endpoint for S3, allowing access without internet usage and keeping traffic within the AWS network.
    -  In summary, we have two public subnets and two private subnets across two availability zones. We use three route tables: one for the public subnets and one for each private subnet. Additionally, we have an internet gateway and a VPC endpoint for S3."
    -  Click on the `Create VPC` button below.



3. **Deploy an EC2 Instance:**
   - Navigate to the EC2 dashboard.
   - Click on `Launch Instance`.
   - Name the instance. For example, `wordpress-server`.
   - Choose the operating system for the virtual computer. In this case, select `Ubuntu`.
   - Keep the instance type as `t2.micro`, which has `1 vCPU` and `1 GiB` of memory.
   - Create a Key Pair to securely connect to your instance via SSH:
        - Click on the `Create new key pair` button.
        - Name the key pair. For example, `wordpress_server`.
        - Keep everything else the same and click on `Create Key Pair`.
        - This will download your private key, keep it secure.

   - Configure the network settings:
        - Ensure `HTTP & HTTPS` traffic is enabled.
        -  Click on `Edit` in the top right corner of this section.
        -   Select the VPC that we created earlier.
        -  Choose the appropriate subnet, in this case, `public1`.
        - Assign a public IP address.
   - Keep the storage setting the same.
   - Click the `Launch Instance` button on the right.

4. **Connecting to EC2 locally:**
   -  Navigate to your Instances in AWS.
   -  Click on the `Connect` button on the top right.
   -  Navigate to the `SSH client` tab.
   -  Open your terminal.
   -  Navigate to the folder containing your private key.
   -  Set appropriate permissions on your private key:
         -  ```chmod 400 private-key.pem```.
         -  Replace private-key with the name of your private key file.
         - Verify the permissions on the the file by running `ls -l private-key.pem`.
         - The output should be `-r--------`.
   - Now, you can use the ssh command to connect to your EC2 instance:
     -  Return to AWS and copy the command from the modal, which should look like: `ssh -i private-key.pem ec2-user@your-instance-public-ip`.
     - Run this command in your terminal.
   - You are now connected to your Instance.

### Conclusion

By completing this project, you will have hands-on experience in setting up and managing AWS resources within a VPC, enhancing your skills in cloud infrastructure management.

## Next Steps

Continue exploring AWS by delving into additional projects that explore different AWS services and configurations.



