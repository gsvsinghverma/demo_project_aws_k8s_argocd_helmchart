-------------------------
Deploy Steps
-------------------------

RUN ALL COMMAND ON JUMP SERVER

****************************************
Step 1 — LBC Policy File Download
****************************************

curl -o lbc-policy.json \
  https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/main/docs/install/iam_policy.json

====================================================================================

********************************************
Step 2 — Terraform Deploy
********************************************


cd /home/gsv-project

terraform init

terraform plan

terraform apply

=======================================================================================
************************************
Step 3 — .env Auto-Generate (generate-env.sh)
************************************

#!/bin/bash
# generate-env.sh
echo "Generating .env..."

S3_BUCKET=$(terraform output -raw s3_bucket_name)
RDS_HOST=$(terraform output -raw rds_endpoint)
ECR_URL=$(terraform output -raw ecr_repo_url)
APP_ROLE=$(terraform output -raw app_s3_role_arn)
LBC_ROLE=$(terraform output -raw lbc_role_arn)
EKS_NAME=$(terraform output -raw eks_cluster_name)

cat > .env << EOF
AWS_REGION=ap-south-1
S3_BUCKET_NAME=${S3_BUCKET}
RDS_HOST=${RDS_HOST}
RDS_DB=gsvdb
RDS_USER=dbadmin
RDS_PASSWORD=GsvSecure@2024!
ECR_URL=${ECR_URL}
EKS_CLUSTER_NAME=${EKS_NAME}
APP_S3_ROLE_ARN=${APP_ROLE}
LBC_ROLE_ARN=${LBC_ROLE}
EOF

echo ".env ready!"
cat .env
chmod +x generate-env.sh
./generate-env.sh

=============================================================================================
***********************************
Step 4 — EKS Connect
***********************************


aws eks update-kubeconfig --region ap-south-1 --name gsv-eks-cluster
kubectl get nodes
kubectl get pods -A

================================================================================================
*********************************************
Step 5 — AWS Load Balancer Controller Install
*********************************************


helm repo add eks https://aws.github.io/eks-charts
helm repo update

helm install aws-load-balancer-controller eks/aws-load-balancer-controller \
  -n kube-system \
  --set clusterName=gsv-eks-cluster \
  --set serviceAccount.create=true \
  --set serviceAccount.annotations."eks\.amazonaws\.com/role-arn"=$(terraform output -raw lbc_role_arn)

# Verify
kubectl get pods -n kube-system | grep aws-load-balancer


================================================================================================
