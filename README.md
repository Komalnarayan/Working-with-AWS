# DEPLOYMENT ON AWS

# •To Launch instance to create virtual machine

i. Sign in to AWS Management Console and open the 
EC2 Dashboard.

2.Click on "Launch Instance".
Configure Instance:Choose an Amazon Machine Image (AMI). For example, Ubuntu.

3. Choose an instance type (e.g., t2.micro for free tier).
   
4.Configure instance details like network settings, storage, and key pairs.Security Groups: Configure the security group to allow access. 

5.For a web application:Allow HTTP (port 80) or HTTPS (port 443) access.Allow SSH (port 22) to access the instance remotely (restricted to your IP for security


# • Install putty and linked it with vm by:-
1.Launch PuTTY from your desktop or start menu.

2.Enter the EC2 Instance Public IP:In the Session section, under Host Name (or IP address), enter the public IP of your EC2 instance (found in the AWS console under "Instances").

3.Set the SSH Connection:On the left-hand side of the PuTTY window, navigate to Connection > SSH > Auth.Load the .ppk file:In the Auth section, under Private key file for authentication, click Browse and select the .ppk file you saved earlier.

_Now our virtual machine is ready for further operations!!!_

_so let's get start...._

# 1. Deploying an html page using apache2 web server
# step-1 
log in to your vm by its username (eg.ubuntu) and update it by the following commamd
sudo apt update

# step-2 
Now to install apache2

```sudo apt install apache2```

(You can check if Apache2 is installed properly by entering your server’s IP address in a web browser (e.g., http://your-server-ip). 
You should see the Apache default page.)

# step-3:- 
In order to change $ into # for root user:-

```sudo su```

# Step-4:-
The default web directory for Apache2 is /var/www/html/. Navigate to this directory by:

```cd /var/www/html/```

 # step-5:- 
 Now you can create your own html page by:-

```vi index.html```

# step-6:-
This will open an editor where you can type your HTML code. Here’s an example of a basic HTML page:-

<html> 
   welcome to my first web page </html>

# step-7:-
Now inorder to save, press
**ctrl** + **C** then **shift** + **;** and **wq**

# Yupp u have done it!!!



# 2. Deploying using nginx image from docker

i. Install Docker on EC2Once logged in via PuTTY, update the package repository:
  
  ``` sudo apt update```

ii. Install Docker by:-

```sudo apt install apt-transport-https ca-certificates curl software-properties-common```

```curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -```

```sudo add-apt-repository "deb [arch=amd64]```
```https://download.docker.com/linux/ubuntu focal stable"```

```apt-cache policy docker-ce```

```sudo apt install docker-ce```

iii. Docker has installed now to enable it...

```sudo systemctl enable docker```

iv. now pull nginx to create a docker image by:-

```sudo docker pull nginx```

v. in order to run it for publically accessiblily:-

```docker run --name docker-nginx -p 80:80 nginx```

vi. now this will show this on your public ip:-

https://photos.app.goo.gl/nTvX2z4zJVL6w3rb9



vii. now to build a web page on nginx server:-

```mkdir -p ~/docker-nginx/html```
then, 

```cd ~/docker-nginx/html```

viii. now,To enter the html page directly:-

```vi index.html```

ix. now press ```i``` im order to insert and make your web page, here is an example,

https://photos.app.goo.gl/Smcb5Dw5DSowi2JS6


x. now to save it....press 
# ctrl+c 
then **shift** + **;** and type 
 **wq**


xi. now to link the Container to the Local Filesystem


```docker run --name docker-nginx -p 80:80 -d -v ~/docker-nginx/html:/usr/share/nginx/html nginx```

now copy and paste your public ip on web browser!!!









