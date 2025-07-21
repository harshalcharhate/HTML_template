# 📌LAMP stack Dynamic Web server deployment Project
### This project helps how to deploy a simple web application using a **LAMP stack** (LINUX , APACHE , MYSQL , PHP) on a Cloud based Linux server **EC2**.
### ☑️Project overview
**LAMP**  Stands for :
- **L** - Linux : Operating system 
- **A** - Apache : Web server software that is ***httpd***
- **M** - MySQL : Database server 
- **P** - PHP : Server side scripting language

This project shows how to :
1. Launch an EC2 instance on AWS
2. Install and configure Apache,MySQL,PHP
3. Deploy a httpd site
4. Deploy a test  PHP  Site
5. Create database
6. Secure the deployment with security group
## Steps to do :
### Step.1) 🛡️Create Security Group
- Go to AWS console on the search bar search ***EC2*** ,click on EC2
- In the EC2 console .on the let side panel their is `Network & Security` click on them
- In that click on `Security Groups`, 
- In that click on `create security group`
- do some basic configuration
```
 > Security group name : LAMP-SG 
 > Description : allow ssh,httpd,http
 > VPC : (default vpc )
```
- In ***inbound rules*** add the inbound rules ,click on Add rule
```
Type : SSH , Source : 0.0.0.0/0 (anywhere)
Type : HTTP , Source : 0.0.0.0/0 (anywhere)
Type : HTTPS , Source : 0.0.0.0/0 (anywhere)
```
- In Outbound rule kept as default ,no change and click on Create.
![alt text](<Screenshot 2025-07-07 002532.png>)

### Step.2) 💻Create Instance
- On Left panel of EC2 console , click on ` Instances` 
- In that instances click on `Launch instance`
- After clicking fill it
```
-> Name : LAMP-server (name the intance)
-> Application and OS Images : Amazon Linux 2023 kernel-6.1 ( just check that its is In FREE TIER ,or other mistakely click)
-> Instance type : t2.micro ( FREE TIER )
-> Key pair : .pem key ( create a key in (.pem)and add)
-> In Network setting , select existing security group : LAMP-SG (existing or create new one)
-> other setting kept default
-> Click on Launch Instance
```
![alt text](<Screenshot 2025-07-06 225545.png>)

### Step.3) 🔗Connect to EC2 with SSH
- After creating instance , select the instance which we created and then click on `Connect` ,
- In connect page click on `SSH client` and copy the last line command
 ```
ssh -i "linux-server-key.pem"ec2-user@ec2-3-95-25-136.compute-1.amazonaws.com
                       OR
ssh -i linux-server-key.pem ec2-user@3.95.25.136 
```
- go to git bash open it and paste the above command
![alt text](<Screenshot 2025-07-06 233531.png>)
### Step.4) ⚙️Install HTTPD , MySQL , PHP
#### Before that UPDATE the OS
```bash
sudo yum update
```
#### Install APACHE ( httpd)
```bash
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
```
Check that httpd is working or not , copy server public ip at hit on browser

#### Install MySQl
```bash
sudo yum search mysql           #see where the server is written ( mariadb105-server)

sudo yum install mariadb105-server -y
sudo systemctl start mariadb
sudo systemctl enable mariabd

mariadb --version               # to check the version
```
#### Install PHP
```bash
sudo yum istall php -y
sudo systemctl start php-fpm
sudo systemctl enable php-fpm


php --version                     # to check the version php
```
### Step.5) ✅Deploy httpd page 
#### Change the directory,from where application are deployed
``` bash
cd /var/www/html
```
#### For deploying httpd page , craete a file index.html to the **html/** directory
```bash
#in html/ directory

sudo vim index.html     # to create a file index.html and go inside the file,to write code inside the index.html using vim editor
```
```bash
#after going inside the vim editor press ( i ) and write given html code,

<h1>This is MY LAMP server </h1>

#and then press ( esc ) button
# and wirte ( :wq ) to save and exit
```
#### After that restart the httpd
```bash
sudo systemctl restart httpd 
```
#### and check that its is working, by hiting Public-IP of server on Browser
![alt text](<Screenshot 2025-07-07 001805.png>)
- So successfully deploy the index.html page using httpd server
### Step.6) ✅Deploy the PHP page
#### In the **html/** directory we have to create a file of index.php 
```bash
# in html/ directory

sudo vim index.php        #using vim editor we can create file index.php and add php code inside the file
```
```bash
#after going inside the vim editor press ( i ) and write given php code,

<?php
phpinfo();
?>

#and then press ( esc ) button
# and wirte ( :wq ) to save and exit
```
#### After that restart the php-fpm
```bash
sudo systemctl restart php-fpm
```
#### and check that its is working, by hiting Public-IP of server with /index.php on Browser as given below,
```
 3.95.25.136/index.php 
```
![alt text](<Screenshot 2025-07-07 001744.png>)
### Step.7) 🗄️Create database
- Go to main home directory
```bash
# in html/ directory wirte
cd

#after going to ec2-user/

sudo  mysql -u root -p  # then enter

#in that mysql we can create database 

> SHOW DATABASES;
> CREATE DATABASE lamp_db;
> USE lamp_db;
> CREATE TABLE users(#add values entity);
> EXIT;
```
Here is the DATABASE we created .<br>

You can also connected database to app ,securing database you can also create password for it, but in this project we just see that we can create three server on One server.We just deploy normal pages but in real-time it has APPLICATION which deploy securly implementing ASG , VPC ,PROXY SERVER , etc services are used to make secure environment.
## 📄Summary
In This project we  complete process of deploying a dynamic PHP-based website using a LAMP stack (Linux, Apache, MySQL, PHP) hosted on an Amazon EC2 instance.It showcases a basic, secure, and scalable method to serve dynamic content and manage a backend database on a cloud platform.<br>
The LAMP stack is one of the most popular and proven open-source stacks for hosting dynamic web applications:
- Linux: Stable, secure operating system for servers.

- Apache: Widely used, flexible web server.

- MySQL: Powerful open-source relational database.

- PHP: Popular server-side scripting language for dynamic content.

Together, these components provide a reliable, scalable, and cost-effective solution for web hosting — commonly used for WordPress, e-commerce, blogs, and custom PHP apps.