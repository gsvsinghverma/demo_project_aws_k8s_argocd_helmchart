------------------------------------------
— Configure the AWS CLI using an IAM role.
------------------------------------------


Note: - The 'Bastions-EC2-Role' is attached to the Bastion EC2 instance; therefore, no credentials need to be entered.

****************************************
aws configure set region ap-south-1

aws configure set output json

aws sts get-caller-identity   

****************************************

-------------------------------------
— Output:
-------------------------------------

json{

"UserId": "AROA...",

"Account": "123456789012",

"Arn": "arn:aws:iam::123456789012:assumed-role/bastion-ec2-role/..."

}


====================================================================================
