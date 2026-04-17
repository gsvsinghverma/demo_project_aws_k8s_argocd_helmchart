-------------------------
Amazon EC2 → Jump Server 
-------------------------

****************************************
AWS Console → EC2 → Launch instance (Ubuntu 22)

****************************************


======================================================================================
Name:  bastion-tools-server
AMI:  Ubuntu Server 22.04 LTS (Free tier eligible)
Instance type: t3.small
Key pair: bastion-key
Network: Default VPC
Subnet: ap-south-1a
Auto-assign IP: Enable

Security Group — Create new:
Name: bastion-sg
Inbound rules:
SSH | TCP | 22 | My IP
Storage: 20 GB gp3

Launch Instance

====================================================================================
