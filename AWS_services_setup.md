DOcumentation:

Setting Up VPC:
1.) Launch VPC WIzzard to create VPC with public and private subnets. This will automatically make 2 subnets, 2 route tables, and 1 internet gateway.
2.) Instead of NAT Gateway, use dedicated ec2 instance (t2.micro is free tier)
3.) Create additional 2 public (mask /21 for 2039 ips) and 2 private (mask /19 for 8187 ips) subnets.
4.) Attach 2 public subnets to the Route Table with the original public subnet.
5.) Attach 2 private subnets to the Route Table with the original private subnet.
6.) If does not already exist, add an Internet Gateway to the Public Route Table's routes. This will allow internet access.

Launching Ec2 Instance:
1.) Launch an ec2 server with Ubuntu Server as OS.
2.) Pick a proper ec2 type (t2.micro is free tier)
3.) Configure it to use the VPC and Public Subnet created previously, make sure to auto-assign Public IP.
4.) Configure storage (default 8gb) and key as needed.
5.) Configure security groups to allow SSH - port 22 for remote access, HTTP - port 80 for hosting unecnrypted web pages, and HTTPS - port 443 for hosting encrypted web pages.

Purchasing Domain:
1.) Go to Domain Webiste Vendor.
2.) Create account through that Vendor.
3.) Purchase a domain name for sale.
4.) Then go to the account setting and the go to  domain list.
5.) Select the domain that you purchased and click manage.
6.) Then you scroll to the DNS setting and add the namesevers that you want to point your domain name too.


Creating an SSH User:
1.) You must ssh as root user then run these commands.
2.) sudo adduser new_user
3.) sudo adduser new_user --disabled-password
4.) sudo su - new_user
5.) mkdir .ssh
6.) chmod 700 .ssh
7.) touch .ssh/authorized_keys
8.) chmod 600 .ssh/authorized_keys
9.) Then you are going to make generate a public key and private key with putty generator.
10.) Then nano the authorized_keys file and copy the public key in there.
11.) Then open up your putty application and input the IP address of the ec2 and select the private key as your authorized key.
12.) Then  make sure you login as you username in the Data setting.

Connecting Domain Name with ec2 Instance:
1.)

Creating an SSL Certificate
1.) 

Create Load Balancer.
1.) Create a load balancer, use previous generation option.
2.) Use the VPC created previously, add 2 public subnets for availability.
3.) Add HTTP and HTTPS protocols to Load Balancer.
4.) Use the same security group used for ec2 (should include SSH, HTTP, HTTPS)
5.) For Security Settings, use the TLS key from previous step.
6.) Confugure Health Check, and select the ec2 instance created previously.

Creating the Ansible playbook
The ansible playbook for installing lamp:
file list:
index.html
apache2.conf
/_css
1.Apache version: apache2
2.Start the apache2 server after finish installing
3.Install mySQL
4.PHP version: php 7.1
5.The HTML file, apache2.conf file, and the _css folder are created separately to be used by ansible playbook.
6.The ansible playbook creates the /var/www/html/index.html and copy the index.html and _css folder file into it.
7.The ansible playbook also copies the apache2.conf into etc/apache2 folder.
