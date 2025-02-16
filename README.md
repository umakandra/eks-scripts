Connect to cluster

aws eks --region <your-region> update-kubeconfig --name <your-cluster-name>


The error message indicates that your EKS worker nodes lack the necessary IAM permissions to attach EBS volumes to the instances. Specifically, this error:


aws eks describe-nodegroup --cluster-name <your-cluster-name> --nodegroup-name <your-nodegroup-name> --query "nodegroup.nodeRole" --output text

2. Attach Required Policies to the IAM Role
Now, attach the required IAM policies to allow EBS volume attachment.

Attach IAM Policies via CLI
Run these commands:

aws iam attach-role-policy --role-name <your-worker-node-role> --policy-arn arn:aws:iam::aws:policy/AmazonEKSWorkerNodePolicy

aws iam attach-role-policy --role-name <your-worker-node-role> --policy-arn arn:aws:iam::aws:policy/AmazonEC2ContainerRegistryReadOnly

aws iam attach-role-policy --role-name <your-worker-node-role> --policy-arn arn:aws:iam::aws:policy/service-role/AmazonEBSCSIDriverPolicy
