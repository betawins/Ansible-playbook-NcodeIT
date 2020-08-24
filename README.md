# README file for ncd-ansible repository
---
## Use Cases 

### UseCase1:
Your Manager asks you to write a playbook which can setup the aws environment,same playbook will be used
for provisioning in different environments.

Your playbook should create the below services:
1) Create a Security group.
2) Create Ec2 Insance.
3) Create target group and attach it to Ec2 instace.
4) Create a loadbalancer and attach target group to loadbalancer.
5) create mysql service.
6) create a RDS service.
7) Update the records in Route53.
#### Description
Small teams of developers (about  3 to 5 members per team) work on temporary aws mini environments
that are built and destroyed on regular basis.
They need it for 2 to 3 days and done. 

We get multiple requests per day to create such environments with minor customizations.
We have designed playbooks to create the environment as per the requirements.
Before running the playbook, we adjust the variables file with required parameters and run it to create the environment.
This playbook creates the environment with ec2 instances, randomly generated vpc names/security groups and necessary routing rules.
We are also specifying different target group to loadbalancer and ip of instance is updated in Route53 records.
### Prerequisites:
1) Ansible server.
2) Aws Account Access key and secret key.
3) Domain name.
4) Publc hosted zone in Route53.
5) keypair to provision the Ec2 Instances.
### How to run the Ansible-playbook:
1) Please store the Aws_access_key and aws_secret_key in secrets.yml.
2) Encrypt the secret.yml by using ansible vault.
--> ansible-vault encrypt secrets.yml
3) Change the hosted zone name from your playbook.
4) Run the playbook.
--> ansble-playbook playbook.yml

### Usecase2:
Your Manager asks you for a playbook to pull a docker image from
docker registry and create a container out of the image with a persistent storage.

Your playbook should create the below services:
1) Install prerequisites for docker.
2) Install docker.
3) Log into DockerHub.
4) Create a container.
5) Create a volume.
#### Description
Team of developers,deployment engineer will be working on different docker container where the container are created and tested.
This work is done on a regular basis by different teams and these containers are upgraded if required and pushed back to docker
registry and then are destroyed from the local machines.
This playbook will help developers and deployment engineers to connect to docker regisrty and pull the required image into 
docker engine and up the container with a persistent volume.
### Prerequisites:
1) Ansible server.
2) Docker hub account.
3) Docker Image which needs to pe pulled from Docker hub.
### How to run the Ansible-playbook:
1) Cutomize the default.yml parameters as per requirement.
2) Pass DockerHub username and password in default.yml.
3) Run the playbook.
--> ansible-playbook playbook.yml

### Usecase3:
Team requires a playbook to check the list of services running in instances,
if the service is not running then start the service and if the service is already running
then restart the service.

Your playbook should create the below services:
1) Connect to all the servers.
2) Check for the required services.
3) Check the status of service.
4) Start/Restart the service.

#### Description
Lot of issues are caused when a service is stop in any environment,it will Downgrade the complete application.
In this situation we can login to server and check for the related services but what if there are 100 servers? It is not possible
to check login and check the services manually,this issues was reported by many teams like Devops,Middleware,Linux Admins etc..
To overcome this issue we have developed a asible playbook which will check the status of service in all 100 servers and
start the server if it is stopped or restart the service.
### Prerequisites:
1) Ansible server.
2) Some running services in servers.
### How to run the Ansible-playbook:
1) Customize the playbook to check the running services.
2) Run the playbook.
--> ansible-playbook playbook .yml

### Usecase4:
Client requires a playbook which can provision the Apcahe tomcat server,
create a specific Apache tomcat user with Read-Write-Edit Permissions for Deployment.
Your playbook should create the below services:

1) Install basic packages.
2) Install Java.
3) Create Tomcat user
4) Create Tomcat group.
5) Download Tomcat.
6) Create Tomcat directory.
7) Extract Tomcat archive.
8) Create user.
9) Start Tomcat service.
#### Description
A common requirement for any client will be either of webserver or app server to deploy the application.
Problem with the requirement is we can manually provision the webserver in 100 servers with specific user permissions,
but this can lead to human errors and take a lot of time to do the same task in all 100 servers.
So why not use Ansible?
With a single playbook we can do the same set of task in all 100 servers and without any error!!
This playbook will help to provision ApacheTomcat in 100 servers and create a user with required permissions 
and add the user to "WHEEL" group for permissions.
### Prerequisites:
1) Ansible server.
2) Ubuntu/linux node machines.
### How to run the Ansible-playbook:
1) Change the username and password in  "templates/tomcat-users.xml" file.
2) Run the playbook.
--> ansible-playbook tomcat-setup.yml

### Usecase5:
Your Manager requires a playbook to provision jenkins server,this same playbook will be used to
setup jenkins server for different teams.

Your playbook should create the below services:
1) Install packages.
2) Install wget.
3) Install java 1.8.
4) Install Jenkins.
5) Enable Jenkins.
6) Display the Jenkins initialAdminPassword.
#### Description
Developers,Testers,Devops Team requires jenkins server more ofently,in most of the organization a single server will be used for
different cients or different jenkins server will be used for each client to maintain different pipelines for building artifacts and deployment.
For developers it important to test if there code passes all the test cases and to check the quality of code which can be easily processed by
using jenkins for Continous integration.
For Devops jenkins ease there work to build artifacts and pushed the artifacts to any of the artifactory repository or to deploy in Servers.
so to provision these server we a playbook to whcih can setup the server without any manual intervention in a single click.
Jenkins reqires JDK 1.8 version to be installed to run the server and is run at default port number8080.
Playbook will include the steps to install JDK1.8 and export the JAVA_HOME path to enviromental varaibles and it will install
jenkins server and it will display the InitialAdminPassword to the user,which is used to configure the jenkins server at webbrowser.
### Prerequisites:
1) Ansible server.
2) ubuntu node machines.
### How to run the Ansible-playbook:
1) Execute the playbook.
--> ansible-playbook jekins.yml

### Usecase6:
Your team requires a playbook to deploy a war file into multiple tomcat server
for Dev,Test and production.

Your playbook should create the below services:
1) Install basic packages.
2) Install Java.
3) Create Tomcat user
4) Create Tomcat group.
5) Download Tomcat.
6) Create Tomcat directory.
7) Extract Tomcat archive.
8) Create user.
9) Start Tomcat service.
10) Install git.
11) Download .war file github to ansible-master
12) Copy the file from ansbile master to tomcat path in ansbile node mahines.
#### Description
For every new release/test deployments we need a new build artifact to deploy in all servers.
Devops engineer Will be working on this on a regular sprint along with developers to deploy the new update 
in Development/UAT/PROD Environments.
For every new update there will be a new artifact with different versions,these artifacts are either stored in artifactory repository
or any other tool to store as per the client requirements.
In our case we have stored a artifact in github repository which needs to be deployed in all servers.
This work can be manually deployed in one or two servers and again high chances of human error's if working manyally.
To avoid these errors and to make the same task reusable we require a playbook which can deploy in "N" number of servers and then
restart the tomcat servers to reflect the changes.
### Prerequisites:
1) Ansible server.
2) ubuntu node machines.
3) .war file in github account.
### How to run the Ansible-playbook:
1) Change the username and password in  "templates/tomcat-users.xml" file.
2) Modify the github account url.
3) Run the playbook.
--> ansible-playbook tomcat-setup.yml

### Usecase7:
Aws architect requires a playbook which can spinup aws instances
With SSD volumes for three Dev,Test and Prod Environments.

Your playbook should create the below services:
1) Install Pip in ansible master.
2) Install 'boto', 'boto3', 'botocore'.
3) Create a security group.
4) Create Ec2 Instances.
5) Create volume and attach it to Ec2 Instances.
#### Description
A small team of developers works on aws instances which are provisioned and destroyed after there work is done.
Access to these aws cloud will be restricted to many developers and testers where they can't spinup instances and create a HDD for instance.
These requests are raised by developers to cloud engineers.Spinup of aws instances on a regular basis is a rework to the team.
To overcome these requests a generic playbook is developed which helps to spin up aws instances with HDD attached to instances for
any dev/test/prod environments.
Playbook can be executed by cloud engineers when a request is raised.
Once the instances are spinned up the Public ip is shared with the respective team to access the instance.
### Prerequisites:
1) Ansible server.
2) Aws Account Access key and secret key.
3) keypair to provision the Ec2 Instances.
### How to run the Ansible-playbook:
1) Please store the Aws_access_key and aws_secret_key in secrets.yml.
2) Encrypt the secret.yml by using ansible vault.
--> ansible-vault encrypt secrets.yml
3) Change the Keypair name in playbook. 
4) Run the playbook.
--> ansble-playbook provision.yml
### Usecase8:
A nodejs code is in your github private account and you need to write a playbook
to clone the source code from github and install all prerequisites and Launch the Simple NodeJS Application.

Your playbook should create the below services:
1) Install Node and NPM.
2) Download the NodeJS code from the GitRepo.
3) Install Dependencies with NPM install command.
4) Start the App.
5) Validating the port is open.
#### Description
A team of developers working on a node js application from different locations,these developers requires to deploy the applciation
in aws environment and check the functionality of there application.
Every time a aws instance is spinned up is Terminated after the work is done to avoid the billing.
The new modules and new changes to code is stored in github repository,all the developers need a instance with all nodejs prerequisites
to test the functionality of application.
Each time a developer needs to test should spin instance and install node and npm,download soruce code,install all dependencies and
start the app,this work will be done on a regular basis till the final release is ready and doing the same work manually will be boring.
To avoid doing the same work again and again we will be developing a playbook which will help install npm,download source code,
install all dependencies and then to start the application.
The only thing developers needs to do is access to the webbrowser and test the functionality.
With Ansible things are easy!!
### Prerequisiites:
1) Ansible server.
2) Ubuntu node machines.
3) Github account.
4) NodeJs Applciation source code in github.
### How to run the Ansible-playbook:
1) Store the Github username and password in secrets.yml.
2) Change the gthub url in nodejs.yml playbook.
3) Run the playbook.
--> ansible-playbook nodejs.yml

### Usecase9:
Let us suppose that you work for the DevOps team of a Big Organization where you manage 100+ ec2 instances. 
You have a new hire in your team and you ought to give him access to all these boxes and you should be ideally 
adding his SSH Key to each EC2 instances so that he can log in without having to use the Root PEM file.

Your playbook should create the below services:
1) Generate a ssh key.
2) Copy the private key to the host machines.
#### Description
A new Devops Engineer joined the team and organization maintains more than 100+ aws instances.New hire should be given access to all these 100+
instances to work and to deploy the application.
We can't provide the root access to new hire as well we can't share the other resource credentials as it will go against policy of organization.
We need to create a new ssh key for New hire and add the key in all 100+ instances,this can be done manually but what if the next day/week/month
a new joinee joined?Again we need to do the same work for New Joinee,we need a permanent solution for this problem.
The problem has been raised to Ansible team and team will develop a playbook which will create a ssh key and copy the key to all 100+ instances.
This will resolve the problem permanently.
### Prerequisites:
1) Ansible Server.
2) Ec2 instances in running state.
3) ssh-key in Ansible master server.
3) key pair associated with instances - private key.(Ansible Master server)
### How to run the Ansible-playbook:
1) All the variables defined in playbook are passed at
executing playbook.
--> ansible-playbook add-key.yml --user ubuntu --key-file kubernetes.pem
---
###TODO  


#
