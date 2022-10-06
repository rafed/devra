---
title: Deploy Wordpress on AWS with Autoscaling (Super Fast Config!)
date: 2022-09-24
tags: [cloud, AWS]
image: "s3.jpg"
draft: true
---

There are hundreds of hosting providers that you can use to host wordpress easily. But shared hosting is not good for sites receiving heavy traffic. If you want a wordpresss website can scale to any amount of traffic, this tutorial is for you. We will use AWS to set up our servers.

Here's the steps we'll go through for our deployment
1. Create a VPC
1. Create a database
1. Create a redis instance
1. Create an efs
1. Create an ec2 and mount the efs on /var/www/html
1. Download and install wordpress on efs
1. Configure Wordpress (wp-config)
1. Create a load balancer (ALB)
1. Create autoscaling group
1. Point DNS to Loadbalancer

#### 1. Create a VPC


#### 2. Create a database

create database wordpress;
CREATE USER 'wp_user'@'%' IDENTIFIED BY 'PASSWORD';
GRANT ALL PRIVILEGES ON `wordpress`.* TO "wp_user"@"%";
FLUSH PRIVILEGES;


#### 3. Create a redis instance


#### 4. Create an efs


#### 5. Create an ec2 and mount the efs on /var/www/html
make sure sg is ok


#### 6. Download and install wordpress

install apache2
sudo chown -R www-data:www-data /var/www/html
download & install wordpress

sudo apt install nfs-common 
install nginx
sudo apt install mysql-client

sudo apt install php7.2-cli php7.2-fpm php7.2-mysql php7.2-json php7.2-opcache php7.2-mbstring php7.2-xml php7.2-gd php7.2-curl

sudo apt-get install redis-server php-redis
sudo apt-get install php-xml
sudo apt-get install php-curl



#### 7. Configure Wordpress (wp-config)


#### 8. Create a load balancer (ALB)


#### 9. Create autoscaling group

no-reboot enable in ami creation

#### 10. Point DNS to Loadbalancer


The actual OG https://www.cloudbooklet.com/setup-a-load-balanced-wordpress-website-on-aws-ec2-part-2/










