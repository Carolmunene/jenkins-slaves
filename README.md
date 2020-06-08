yum install java-1.8*
#yum -y install java-1.8.0-openjdk

Setup Jenkins Slave
# Create user and add the user to wheel group
useradd jenkins-slave-01
# Create SSH Keys
sudo su - jenkins-slave-01
ssh-keygen -t rsa -N "" -f /home/jenkins-slave-01/.ssh/id_rsa
# The private and public keys will be created at these locations `/home/jenkins-slave-01/.ssh/id_rsa` and `/home/jenkins-slave-01/.ssh/id_rsa.pub`
cd .ssh
cat id_rsa.pub > authorized_keys
chmod 700 authorized_keys

Configuration on Master
mkdir -p /var/lib/jenkins/.ssh
cd /var/lib/jenkins/.ssh
ssh-keyscan -H SLAVE-NODE-IP-OR-HOSTNAME >>/var/lib/jenkins/.ssh/known_hosts
# ssh-keyscan -H 172.31.38.42 >>/var/lib/jenkins/.ssh/known_hosts
chown jenkins:jenkins known_hosts
chmod 700 known_hosts

Configure the Slave using Manage Jenkins
Configure the node as shown here Manage Jenkins > Manage Nodes > New Node
Test Jenkins Jobs
Create “new item”
Enter an item name – My-First-Project
Chose Freestyle project
Under General Section
Choose Restrict where this project can be run
Update your jenkins slave label Java
Under Build section Execute shell
#!/bin/bash

Save your job
Build job
Check "console output"
Other Videos
