-------------------------
Amazon EKS → Kubernetes
-------------------------


SSH Jump Server on your Machine

****************************************
ssh -i ~/Downloads/bastion-key.pem ubuntu@<bastion-public-ip>
****************************************

-------------------------------------
— System Update
-------------------------------------

Cmd: - sudo apt update && sudo apt upgrade -y

====================================================================================

********************************************
— AWS CLI Install
********************************************


sudo apt install unzip 

curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"

unzip awscliv2.zip

sudo ./aws/install

aws --version

=======================================================================================
************************************
— kubectl Install
************************************

curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.19.6/2021-01-05/bin/linux/amd64/kubectl

chmod +x ./kubectl

sudo mv ./kubectl /usr/local/bin

kubectl version --short --client

=============================================================================================
***********************************
— eksctl Install
***********************************


curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp

sudo mv /tmp/eksctl /usr/local/bin

eksctl version

================================================================================================
***********************************
— Helm Install
***********************************

curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash

helm version


================================================================================================
***********************************
— Terraform Install
***********************************

sudo apt install -y gnupg software-properties-common

wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg

echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] \
https://apt.releases.hashicorp.com $(lsb_release -cs) main" | \
sudo tee /etc/apt/sources.list.d/hashicorp.list

sudo apt update && sudo apt install -y terraform
terraform –version


================================================================================================
***********************************
— Docker Install
***********************************

sudo apt install -y docker.io

sudo usermod –aG docker ubuntu

newgrp docker

docker –version

================================================================================================
***********************************
— Git Install
***********************************

sudo apt install -y git

git --version

================================================================================================
