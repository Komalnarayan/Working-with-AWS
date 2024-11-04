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

![hqdefault](https://github.com/user-attachments/assets/b62fcbb5-7c3c-4eeb-b2d0-8657951a3c19)


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

![default_page](https://github.com/user-attachments/assets/3b10e3b0-94a2-4ae4-8abf-7f60f0b92079)



vii. now to build a web page on nginx server:-

```mkdir -p ~/docker-nginx/html```
then, 

```cd ~/docker-nginx/html```

viii. now,To enter the html page directly:-

```nano index.html```

ix. Now make your web page, here is an example,

![hqdefault](https://github.com/user-attachments/assets/fd3d8858-9837-473a-a7ba-c7646c386ce1)



x. now to save it....press 
**ctrl+x** 
then **y** and **enter**


xi. now to link the Container to the Local Filesystem


```docker run --name docker-nginx -p 80:80 -d -v ~/docker-nginx/html:/usr/share/nginx/html nginx```

now copy and paste your public ip on web browser!!!


# STEPS TO INSTALL MINIKUBE:-

In order to install minikube, thete are some prerequisites given below:-

• Pre-Install Ubuntu 22.04 system

• 2 GB RAM or more

• 2 CPU or more

• 20 GB free disk space

**STEP-1**To download and install minikube binary, run following commands,


```$ curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64```

```$ sudo install minikube-linux-amd64 /usr/local/bin/minikube```

**STEP-2** To verify the minikube version, run

```$ minikube version```


![image](https://github.com/user-attachments/assets/56d5e70f-1a73-466b-a8df-f4d542896565)


**STEP-3** Install Kubectl tool:-
Kubectl is a command line tool, used to interact with your Kubernetes cluster. 
So, to install kubectl run beneath curl command->

```$ curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl```

**STEP-4** set the executable permission on it and move to /usr/local/bin:-

```$ chmod +x kubectl```

```$ sudo mv kubectl``` 

```/usr/local/bin/``` 

**STEP-5** Verify the kubectl version, run

```$  kubectl version -o yaml```


![image](https://github.com/user-attachments/assets/8709c13c-e23a-487b-846f-2939aae5680f)


# Start Minikube Cluster
**STEP-6** Now that Minikube is installed, start a Kubernetes cluster using the following command:

```$ minikube start--driver=docker```


![image](https://github.com/user-attachments/assets/acaebd0c-cc9f-4dbf-bb27-ebece02e1b30)



This command initializes a single-node Kubernetes cluster, and it might take a few minutes to download the necessary components.

**STEP-7** Once the minikube has started, verify the status of your cluster, run

```$minikube status```

**STEP-8** Use kubectl to interact with your Minikube Kubernetes cluster. For example, you can check the nodes in your cluster:


```$ kubectl get nodes```
```$ kubectl cluster-info```

**STEP-9** To deploy a sample nginx deployment, run following set of commands.

```$ kubectl create deployment nginx-web --image=nginx```

```$ kubectl expose deployment nginx-web --type NodePort --port=80```

```$ kubectl get deployment,pod,svc```

**STEP-10** To enable the more funtionality with addons or to view all the available addons, run:-


```$ minikube addons list```


![image](https://github.com/user-attachments/assets/f079dc03-6684-4b99-94d6-56dde3c824ff)



```$ minikube addons enable dashboard```

```$ minikube addons enable ingress```

**STEP-11** To start the Kubernetes dashboard run below command, it will automatically launch the dashboard in the web browser as shown below:-

```$ minikube dashboard```



![image](https://github.com/user-attachments/assets/9edecd03-b7fe-4c2b-804a-4e0f9e059596)


![image](https://github.com/user-attachments/assets/8b348cfa-12ce-451f-a9fe-3ed933a2aaa8)


# To Install openstack on VM and create a VM on it

*STEP 1*. Create an instance  in  AWS  , using operating system *UBUNTU* then make some changes 

• Take Amozon Machine Image (AMI)

•Instance type-> t3.xlarge

•Storage-> 50GB

In Network setting 
i). SSH

ii). HTTP

iii). HTTPS

iv). ALL TRAFFIC



*STEP 2.* Launch instance

*STEP 3.* Then copy the IP address and paste it on *Putty* , now browse the Key as usual then click on OPEN , to create your *Virtual Machine*.

*STEP 4.* Install the openstack snap:-

```sudo snap install openstack --channel 2024.1/beta```


*STEP 5.* To Prepare the machine

_Sunbeam can generate a script to ensure that the machine has all of the required dependencies installed and is configured correctly for use in OpenStack - you can review this script using:_

```sunbeam prepare-node-script```


```sunbeam prepare-node-script | bash -x && newgrp snap_daemon```

_This will directly execute it_

*STEP 6.* Now, deploy the OpenStack cloud using the cluster bootstrap command and accept software defaults:-


```sunbeam cluster bootstrap --accept-defaults```

_It will take around 30 minutes._

*STEP 7.* To configure the deployed cloud:-

```sunbeam configure --accept-defaults --openrc demo-openrc```

 *STEP 8.* To open the VM which ead created on OpenStack

```sunbeam launch ubuntu --name test```












