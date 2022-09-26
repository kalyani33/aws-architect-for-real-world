# aws-architect-for-real-world
## AWS Global Infrastructure
<img width="500" alt="image" src="https://user-images.githubusercontent.com/37569003/192211068-b98668d8-65f3-4fce-98ad-3dc9ef9aa0de.png">

## EC2
### Security Groups
- A security group is a set of firewall rules that control the traffic for your instance. Add rules to allow specific traffic to reach your instance.
### User Data
- Specify user data to provide commands or a command script to run when you launch your instance.
- All these cmds run with root permissions only not by ec2-user
- Runs only once while creating instance
- https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/user-data.html?icmpid=docs_ec2_console
<img width="944" alt="image" src="https://user-images.githubusercontent.com/37569003/192141576-657391b2-d9d4-49f9-ae2d-a7e748692032.png">

### Configure an AWS Web Server
- SSH into ec2 machine
```bash
sudo yum update -y
sudo yum install httpd -y
sudo systemctl status htppd
sudo systemctl start httpd
sudo systemctl status httpd
sudo systemctl enable httpd
cd var/www/html
sudo su
echo "<h1>tag Hello welcome to AWS learning</h1>" > index.html
```
- Now in browser type the public ip address/public DNS  and voila , your server is serving now
### Stress Testing on ec2
- https://netflixtechblog.com/tagged/chaos-monkey   -- good to read one
#### Status Checks
- System check:AWS related infrastructure issues
- Instance Check:Issue related to my ec2 application
- Create an Status check alarm in Status Check tab
- Raise an alarm when  CPU Utilization is >= 50% constantly for 5 mins
- If the alarm is triggered, take Terminate action on EC2 instance
- Now connect to ec2
- sudo amazon-linux-extras install epel -y
- sudo yum install stress -y
- stress --help -- for help
- stress --cpu 7 ----> applying stress on my ec2 instance

<img width="683" alt="image" src="https://user-images.githubusercontent.com/37569003/192140342-7e09caa8-fb45-4eb9-8bc1-375ad409f9ea.png">

<img width="931" alt="image" src="https://user-images.githubusercontent.com/37569003/192140725-6dca76fa-4230-4e42-9a15-bce2c47062e7.png">

<img width="692" alt="image" src="https://user-images.githubusercontent.com/37569003/192140383-5bea9074-d3af-424f-97c7-a3a35a42b1d8.png">

<img width="921" alt="image" src="https://user-images.githubusercontent.com/37569003/192140266-7b0b454f-3036-4c68-9b2d-7580741b590f.png">

### Instance Metadata
- Just a information about your machine
- Instance metadata is data about your instance that you can use to configure or manage the running instance. 
- Instance metadata is divided into categories, for example, host name, events, and security groups.
- We can view/get the metadata only winthin the instance
<img width="617" alt="image" src="https://user-images.githubusercontent.com/37569003/192143368-305d23f1-677c-4e3e-b4a9-2e6173c9eaec.png">

- ssh into ec2
- curl http://169.254.169.254/latest/meta-data/
<img width="925" alt="image" src="https://user-images.githubusercontent.com/37569003/192143674-707ce87b-6641-4eb5-b22f-df80aceb7742.png">
- More about that at https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-metadata.html

### Elastic IP Addresses
- https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html
- An Elastic IP address is a static(it does not change over time) public IPv4 address
<img width="406" alt="image" src="https://user-images.githubusercontent.com/37569003/192144462-9cfa6ffc-3ea3-4a46-a282-2a843162c5bd.png">

<img width="426" alt="image" src="https://user-images.githubusercontent.com/37569003/192144593-95bf7bd4-b40b-4a9e-9a27-300f4f36329a.png">
- Can be associated to "Instance" or "Network Interface"

### Elastic Network Interfaces
- Flow logs can capture IP traffic flow information for the network interfaces associated with your resources. You can create multiple subscriptions to send traffic to different destinations.
### Create Custom Image
- An image (also referred to as an AMI) defines the programs and settings that are applied when you launch an EC2 instance. You can create an image from the configuration of an existing instance.
- Add you can start using your image when creating a instance
<img width="605" alt="image" src="https://user-images.githubusercontent.com/37569003/192147680-bb6aa5a5-ccf4-4a74-8b38-5fcf4153c636.png">

### Placement Groups
- Determines how the instances are placed on the underlying hardware.
- Cluster (low network latency,low availability)
- Rack crashes => All EC2 instances fail
- Partition (multiple partitions with low network latency)
- Spread (avoid simultaneous failures)
<p float="left">
<img width="330" alt="image" src="https://user-images.githubusercontent.com/37569003/192152784-b0d72e64-34b2-46d0-b248-da4f0361dc4d.png">
<img width="330" alt="image" src="https://user-images.githubusercontent.com/37569003/192152844-c342c582-3471-4568-914e-5f7ff5deb2eb.png">
<img width="330" alt="image" src="https://user-images.githubusercontent.com/37569003/192152906-6b9bad6e-d9b0-4cba-8722-047453eb6b9f.png">
</p>

### EC2 Pricing
- https://aws.amazon.com/ec2/pricing/
- On Demand
- Spot Instances
- Savings plan
- Reserved Instances
- Dedicated Hosts
## VPCs
<img width="500" alt="image" src="https://user-images.githubusercontent.com/37569003/192207077-794e0d95-8965-4a44-83a9-48c68e926faa.png">

<p float="left">
  <img width="500" alt="image" src="https://user-images.githubusercontent.com/37569003/192208926-8c077eec-581f-4f28-9154-26eae204bf58.png">
<img width="500" alt="image" src="https://user-images.githubusercontent.com/37569003/192209071-00cf1bd1-45c1-4699-9b02-1d2c6e0e52eb.png">
</p>

### Internet Gateway
- Allows communication between your insatnces in your VPC and the internet
- Your default VPC already has an IGW attached
- Internet Gateway is to be attached to VPC to enable communication with internet
- <b>Only 1 IGW can be attached to a VPC at a time</b>
- <b>An IGW cannot dettached from a VPC while there are active aws resources in the VPC(such as ec2 instance or RDS database)</b>

### Route Tables
- Route table contains a set of rules called 'Routes' that are used to determine where internet traffic is redirected
### NACLs
<img width="500" alt="image" src="https://user-images.githubusercontent.com/37569003/192219674-8caf3ae2-735e-4adc-8f17-f4c176127fa7.png">
<p float="left">
  <img width="500" alt="image" src="https://user-images.githubusercontent.com/37569003/192219947-3ccd4d60-af16-45cf-a0c9-837235d5604f.png">
  <img width="500" alt="image" src="https://user-images.githubusercontent.com/37569003/192220116-159ba398-dde4-4913-83d3-1cd60d892992.png">
 </p>
 
 ### Subnets
 <img width="500" alt="image" src="https://user-images.githubusercontent.com/37569003/192223400-4c9d6cf8-f75e-4847-b476-6d0b14c889f4.png">
 
 #### Public vs Private Subnets
 <p float="left">
<img width="500" alt="image" src="https://user-images.githubusercontent.com/37569003/192223604-e65e2adc-40e7-41d6-b4e2-6cd26a692694.png">
<img width="500" alt="image" src="https://user-images.githubusercontent.com/37569003/192223716-34af0238-49a1-419b-a0f6-27ad6bbcd089.png">
 </p>
 
 
 
 
 
 
 
 ## Useful Links
 http://examcramnotes.blogspot.com/2022/05/all-my-aws-csaa-notes-in-one-spot.html











