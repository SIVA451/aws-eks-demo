# EKS Cluster with AWS Load Balancer Controller Setup

This guide walks you through setting up an Amazon EKS cluster with a Fargate profile and deploying the AWS Load Balancer Controller. This setup allows your Kubernetes applications to utilize AWS Network and Application Load Balancers.

## Prerequisites

- AWS CLI
- `eksctl` for EKS management
- Helm for Kubernetes package management
- `kubectl` for interacting with the cluster

## Steps

### 1. Create an EKS Cluster

Run the following command to create a new EKS cluster with Fargate support:

```bash
eksctl create cluster --name my-cluster --region us-west-2 --fargate
```

### 2. Configure kubectl

Update the kubeconfig file to enable `kubectl` access to the cluster:

```bash
aws eks --region us-west-2 update-kubeconfig --name my-cluster
```

### 3. Set Up IAM Policy for AWS Load Balancer Controller

1. Download the IAM policy:

    ```bash
    curl -o iam_policy.json https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/main/docs/install/iam_policy.json
    ```

2. Create the IAM policy:

    ```bash
    aws iam create-policy --policy-name AWSLoadBalancerControllerIAMPolicy --policy-document file://iam_policy.json
    ```

### 4. Associate OIDC Provider with EKS Cluster

Run the following command to associate the OIDC provider with your cluster:

```bash
eksctl utils associate-iam-oidc-provider --region=us-west-2 --cluster=my-cluster --approve
```

### 5. Create IAM Service Account

Create a service account for the AWS Load Balancer Controller:

```bash
eksctl create iamserviceaccount --cluster=my-cluster --namespace=kube-system --name=aws-load-balancer-controller --attach-policy-arn=arn:aws:iam::767397783285:policy/AWSLoadBalancerControllerIAMPolicy --override-existing-serviceaccounts --approve
```

### 6. Add Helm Repository

Add the EKS charts repository to Helm:

```bash
helm repo add eks https://aws.github.io/eks-charts
```

### 7. Verify Helm Installation

Ensure Helm is correctly installed by checking its version:

```bash
helm version
```

### 8. Install AWS Load Balancer Controller

Install the AWS Load Balancer Controller using Helm:

```bash
helm install aws-load-balancer-controller eks/aws-load-balancer-controller -n kube-system --set clusterName=my-cluster --set serviceAccount.create=false --set serviceAccount.name=aws-load-balancer-controller --set region=us-west-2 --set vpcId=vpc-0ff6897075c1d1efa
```

## Conclusion

You have now set up an EKS cluster with Fargate and deployed the AWS Load Balancer Controller. You can now create Kubernetes resources that will automatically provision AWS Network and Application Load Balancers.

