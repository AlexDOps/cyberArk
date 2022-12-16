Role Name
=========
Role name: ec2-instance

Requirements
------------

Instance that will be used to run this playbook requires;

- Ansible
- awscli
- python 
- pip
- boto, boto3

Role Variables
--------------

Variable values referenced in the main tasks can be found in /etc/ansible/roles/ec2-instance/vars/main.yml


How the Playbook works
-----------------------

The ec2-instance ansible role created in this project will create a keypair, create an hidden folder in the /etc/ansible directory and save the created keypair in this format keypair.pem, create a security group with HTTP and SSH ports open to Johnson's public IP address on the ingress while HTTP and HTTPS ports are open to all traffic on the egress.

The other tasks that will be executed include obtaining default VPC info, assigning a random public subnet to the ec2-instance, spinning up an instance on the configured AWS account and attached the already created security group to the instance and install/start apache web server on the instance using a bash script created in this project.

Note: Follow the following guide to run the playbook


- Before you run this playbook, kindly create a directory named "files" in home directory: sudo mkdir ~/files, then create a file named apache.sh inside the "files" directory that was previously created

- Edit the host inventory file and add a group named "[apachebox]" to the last line of the file; sudo vi /etc/ansible/hosts

- Create a run-setup.yml file in /etc/ansible directory and paste the following bash script: sudo vi /etc/ansible/run-setup.yml

- run this command: sudo ansible-galaxy init roles/ec2-instance from the /etc/ansible directory to be able to generate a  template using ansible-galaxy. Override the files in tasks/, var/, meta/ directory as it apppears in this project

#!/bin/bash
sudo su
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd



Best practices 
---------------

- private key was saved in an hidden folder
- used variables within the files to provide code reuse
- values were stored in var files so it could be easily referenced and not exposed in any part when running the code
- AWS configure was used to configure the profile used to run the project to protect the access key and the secret key





