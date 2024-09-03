# Highly-Available-Kubernetes-Cluster-on-Minikube
How to Create Highly Available (HA) Kubernetes Cluster on Minikube

##Prerequisites
1. Driver - Docker
2. Container Runtime - Containerd
3. Minikube > 1.32.0
4. Kubectl
   

1. Start an HA cluster with the driver (docker) and container runtime (containerd) using the command below:
  ```
  minikube start --ha --driver=docker --container-runtime=containerd --profile iquant-k8s-ha
  ```

2. Verify your HA cluster and nodes using the commands:
  ```
  kubectl get nodes -o wide
  minikube profile list
  minikube status -p iquant-k8s-ha
  ```

3. Remove one of the Control plane nodes using the command:
   ```
   minikube node delete m03 -p iquant-k8s-ha
   ```

4. Verify removed control plane node:
   ```
   kubectl get nodes -o wide
   minikube profile list
   minikube status -p iquant-k8s-ha
   ```

5. Replace the deleted Control plane node with a Worker node using the command:
   ```
   minikube node add -p iquant-k8s-ha
   ```

6. Label the new Worker node as "worker"
   ```
   kubectl label node iquant-k8s-ha-m03 node-role.kubernetes.io/worker=worker
   ```

CLEAN UP
1. Delete cluster nodes:
  ```
  kubectl delete nodes iquant-k8s-ha iquant-k8s-ha-m02 iquant-k8s-ha-m03
  ```

2. Stop the minikube cluster:
   ```
   minikube delete --all
   ```
 

