# aws-solution-architect-associate
## Configure an AWS Web Server
- SSH into ec2 machine
- sudo yum update -y
- sudo yum install httpd -y
- sudo systemctl status htppd
- sudo systemctl start httpd
- sudo systemctl status httpd
- sudo systemctl enable httpd
- cd var/www/html
- sudo su
- echo "h1 tag Hello welcome to AWS learnings h1 closing tag" > index.html
- Now in browser type the public ip address/public DNS  and voila , your server is serving now
## Stress Testing
- https://netflixtechblog.com/tagged/chaos-monkey   -- good to read one
## Status Checks
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

