# EKS Cluster with AWS Load Balancer Controller Setup

This guide walks you through setting up an Amazon EKS cluster with a Fargate profile and deploying the AWS Load Balancer Controller. This setup allows your Kubernetes applications to utilize AWS Network and Application Load Balancers.

## Prerequisites

- AWS CLI
- `eksctl` for EKS management
- Helm for Kubernetes package management
- `kubectl` for interacting with the cluster
- IAM user with programmatic access configured

### 1. Install AWS CLI

Download and install the AWS CLI by following the instructions [here](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html). For Windows, you can download the installer and run it.

After installation, configure the AWS CLI using your IAM user credentials:

```bash
aws configure
```

You will be prompted to enter:
- AWS Access Key ID
- AWS Secret Access Key
- Default region name (e.g., `us-west-2`)
- Default output format (e.g., `json`)

### 2. Create an IAM User and Configure Access Keys

1. Go to the [IAM Console](https://console.aws.amazon.com/iam/).
2. Create a new IAM user with **Programmatic access**.
3. Attach necessary policies, such as **AmazonEKSFullAccess**, **IAMFullAccess**, and **AmazonEC2FullAccess**.
4. Download the access key ID and secret access key.
5. Configure the AWS CLI with the keys using the following command:

    ```bash
    aws configure
    ```

    Enter your access key ID, secret access key, default region, and output format.

### 3. Install eksctl

Download the `eksctl` zip file from the [eksctl GitHub releases page](https://github.com/weaveworks/eksctl/releases). Extract the zip file and add the extracted directory to your system's PATH.

1. Download the zip file and extract it:
    ```bash
    curl -LO "https://github.com/weaveworks/eksctl/releases/download/latest_release/eksctl_Windows_amd64.zip"
    unzip eksctl_Windows_amd64.zip -d C:\eksctl
    ```

2. Add `C:\eksctl` to your system environment PATH.

### 4. Install kubectl

Download the `kubectl` binary from the [Kubernetes release page](https://kubernetes.io/docs/tasks/tools/install-kubectl/). Extract the zip file and add the extracted directory to your system's PATH.

1. Download the zip file and extract it:
    ```bash
    curl -LO "https://dl.k8s.io/release/v1.23.0/bin/windows/amd64/kubectl.exe"
    move kubectl.exe C:\kubectl
    ```

2. Add `C:\kubectl` to your system environment PATH.

### 5. Install Helm

Download the Helm binary from the [Helm GitHub releases page](https://helm.sh/docs/intro/install/). Extract the zip file and add the extracted directory to your system's PATH.

1. Download the zip file and extract it:
    ```bash
    curl -LO "https://get.helm.sh/helm-v3.7.0-windows-amd64.zip"
    unzip helm-v3.7.0-windows-amd64.zip -d C:\helm
    ```

2. Add `C:\helm` to your system environment PATH.
