Amazon IAM → Create Role
Create four IAM Roles

Role 1: bastion-ec2-role (Tools server)
Console → IAM → Roles → Create role
→Trusted entity type:  AWS Service → (Use case)EC2
→Policies attach (search): AdministratorAccess
→Create role → Name: bastion-ec2-role

Role 2: eks-cluster-role (EKS Control Plane)
Console → IAM → Roles → Create role
→Trusted entity:  AWS Service → EKS → EKS - Cluster
→Policies attach (search): Policy: AmazonEKSClusterPolicy
→Create role → Name: eks-cluster-role


Role 3: eks-node-role (Worker Nodes)
Console → IAM → Roles → Create role
→Trusted entity:  AWS Service → EC2
→Policies: AmazonEKSWorkerNodePolicy, AmazonEKS_CNI_Policy →AmazonEC2ContainerRegistryReadOnly
     Name: eks-node-role

Role 4: github-actions-role (CI/CD)
Console → IAM → Roles → Create role
→Trusted entity:  AWS Service → EC2
→Policies: AmazonEC2ContainerRegistryFullAccess, AmazonEKSClusterPolicy
    Name: github-actions-role

