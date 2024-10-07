# Steps to Deploy the Application and Verify Resources

This guide provides step-by-step instructions for deploying an application using Kubernetes Deployment and Ingress YAML files, along with verifying the deployment and checking logs for different Kubernetes resources.

## Step 1: Deploy Deployment and Service YAML Files
1. **Apply Deployment and Service YAML Files**
   - Use the following command to apply the Deployment and Service YAML files:
     ```bash
     kubectl apply -f deployment.yaml
     ```
   - This will create the pods and expose the service internally.

## Step 2: Deploy Ingress YAML File
1. **Apply Ingress YAML File**
   - Apply the Ingress YAML file using the following command:
     ```bash
     kubectl apply -f ingress.yaml
     ```
   - This will expose your service externally via an Application Load Balancer (ALB).

## Step 3: Verify Deployment Status
1. **Check Status of Pods**
   - Use the following command to check the status of all the pods:
     ```bash
     kubectl get pods -n default
     ```
   - This will show the state of the pods, which should ideally be in a `Running` state.

2. **Check Status of Services**
   - To check the status of the services, run:
     ```bash
     kubectl get svc -n default
     ```
   - This will display the service details, including the internal/external IP and port information.

3. **Check Ingress Status**
   - Use the following command to verify the status of the Ingress resource:
     ```bash
     kubectl get ingress -n default
     ```
   - This will provide the URL through which the application can be accessed.

## Step 4: Describe and Troubleshoot Resources
1. **Describe Pods**
   - For more detailed information about a specific pod, including events and potential issues:
     ```bash
     kubectl describe pod <pod-name> -n default
     ```
   - Replace `<pod-name>` with the actual name of the pod.

2. **Check Pod Logs**
   - To view the logs for a specific pod, use:
     ```bash
     kubectl logs <pod-name> -n default
     ```
   - This will show the output of the container running inside the pod, which is useful for debugging.

## Step 5: Verify Load Balancer Controller and System Logs
1. **Check Status of Load Balancer Controller**
   - To verify that the AWS Load Balancer Controller is running properly:
     ```bash
     kubectl get pods -n kube-system | grep aws-load-balancer-controller
     ```
   - Ensure that the controller pod is in a `Running` state.

2. **Check Logs of Load Balancer Controller**
   - To troubleshoot the AWS Load Balancer Controller, view the logs using:
     ```bash
     kubectl logs <load-balancer-controller-pod-name> -n kube-system
     ```
   - Replace `<load-balancer-controller-pod-name>` with the actual name of the load balancer controller pod.

3. **Check Status of Core System Pods**
   - To verify the status of important system pods, such as `coredns` or other components:
     ```bash
     kubectl get pods -n kube-system
     ```
   - This command will list all the core system pods and their statuses, which are essential for cluster health.

## Summary
These steps guide students through deploying an application, verifying the deployment status, and troubleshooting Kubernetes resources. Always ensure that all necessary resources are in a `Running` state and logs are reviewed in case of any issues during the deployment. This helps ensure the application is deployed successfully and is accessible as expected.

