# Overview

This is a demo for using env0 for both Terraform and Ansible to build a Jenkins container in an EC2 instance in AWS.

## SSH into the EC2 Instance

First, save the private key locally by running these commands:

```bash
terraform output -raw private_key > myKey.pem
sudo chmod 400 myKey.pem
ssh -i myKey.pem ubuntu@$(terraform output -raw public_ip)
```

## Update the Ansible Inventory File

```bash
sed -i "s/<placeholder_app>/$(terraform output -raw public_ip)/g" Ansible/inventory
```

## Run Ansible

```bash
cd Ansible
ansible-playbook --private-key ../myKey.pem -i inventory jenkinsPlaybook.yaml
````