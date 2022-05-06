# Karpenter #

This repository will contain the terraform templates to spin up an eks cluster and deploy karpenter on your node.
Provisoiners folder contains the yamls for provisioners that are used by karpenter to schedule your workloads. Under test folder, I have added example deployment files for you to observe how karpenter behaves when you scale your deployments. 


##### ---- What is Karpenter? ---- #####
Karpenter is an open-source node provisioning project built for Kubernetes.It is tightly integrated with Kubernetes features to make sure that the right types and amounts of compute resources are available to pods as they are needed. 
Karpenter works by:
1. Watching for pods that the Kubernetes scheduler has marked as unschedulable.  
2. Evaluating scheduling constraints (resource requests, nodeselectors, affinities, tolerations, and topology spread constraints) requested by the pods.  
3. Provisioning nodes that meet the requirements of the pods.  
5. Scheduling the pods to run on the new nodes.  
6. Removing the nodes when the nodes are no longer needed.  


##### ---- What are provisioners? ---- #####
Provisioners define how Karpenter will manage unschedulable pods and expires nodes.   
Karpenter schedule pods that have a status condition Unschedulable=True, which the kube scheduler sets when it fails to schedule the pod to existing capacity.  
Karpenter defines a Custom Resource called a Provisioner to specify provisioning configuration.  
Provisioner uses well-known Kubernetes labels to allow pods to request only certain instance types, architectures, operating systems, or other attributes when creating nodes.  
A provisioner can also include time-to-live values to indicate when nodes should be deprovisioned after a set amount of time from when they were created or after they becomes empty of deployed pods.  
Multiple provisioners can be configured on the same cluster.   

### General commands for setup ###
```bash
terraform init  
terraform plan  
terraform apply  


kubectl apply -f provisioners/default-provisioner.yaml  
kubectl apply -f provisioners/custom-provisioner.yaml  

kubectl apply -f test/deployment.yaml  
kubectl apply -f test/aws-cli.yaml  
```