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
