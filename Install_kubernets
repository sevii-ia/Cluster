install:
  virtualbox
  kubectl
  minikube
dism.exe /Online /Disable-Feature:Microsoft-Hyper-V
========================

minikube start --cpus=2 --memory=2gb --disk-size=10gb -p STEP
minikube start --cpus=2 --memory=2gb --disk-size=10gb -p STEP --driver=virtualbox
minikube stop -p STEP
minikube delete -p STEP

kubectl get componentstatuses
kubectl get services

kubectl cluster-info

kubectl get nodes
kubectl get pods
kubectl delete pods hello
kubectl describe pods hello
kubectl exec hello date
kubectl exec -it hello (-- /bin/bash)(sh)

kubectl run pode-1 --image=ubuntu/apache2 --port=80
kubectl describe pod pode-1
kubectl exec -it pode-1 --container pode-1 -- /bin/bash

kubectl port-forward pode-1 8000:80
