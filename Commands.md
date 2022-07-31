# COMMANDS


## POD COMMANDS
#kubectl run nginx --image=nginx
#kubectl create -f pod.yaml
#kubectl get pods -o wide --show-labels
#kubectl describe pod nginx
#kubect logs -f --tail 20 nginx
#kubectl delete pod nginx
#kubectl delete -f pod.yaml
#kubectl delete pod --all
#kubectl run nginx --image=nginx --dry-run=client -o yaml


## DEPLOYMENT COMMANDS
#kubectl get all
#kubectl create deployment nginx --image=nginx --replicas=2 --dry-run=client -o yaml
#kubectl scale --replicas=3 deployment nginx
#kubectl rollout history deployment nginx
#kubectl rollout status deployment nginx
#kubectl rollout undo deployment nginx
#kubectl rollout undo deployment nginx --to-revision=1
#kubectl rollout pause deployment nginx
#kubectl rollout resume deployment nginx
#kubectl logs -f --selector app=nginx
#kubectl set image deployment nginx nginx=nginx:1.16.1
#kubectl autoscale deployment nginx --min=10 --max=15 --cpu-percent=80


## SERVICE COMMANDS
#kubectl get svc,endpoints
#sudo iptables -n -t nat -L KUBE-SERVICES   **To check the Iptables rules for k8s services
#sudo iptables -n -t nat -L KUBE-SVC-NPX46M4PTMTKRN6Y
#sudo iptables -n -t nat -L KUBE-SEP-V3G4RSCMTSLYTA5C
#kubectl edit configmap kube-proxy -n kube-system
    mode: ipvs
    scheduler: "rr"


## NAMESPACE COMMANDS
#kubectl create ns dev
#kubectl config set-context $(kubectl config current-context) --namespace=dev
#kubectl get all -A
#kubectl get all --all-namespaces


## IMPERATIVE COMMANDS
#kubectl run nginx --image=nginx --dry-run=client -o yaml
#kubectl create deployment nginx --image=nginx --dry-run=client --replicas=2 -o yaml
#kubectl scale --replicas=2 deployment nginx
#kubectl create service nodeport -h
#kubectl expose pod nginx --port=80 --protocol=TCP --target-port=80 --name=clusterip-nginx

## SCHEDULING COMMANDS
#kubectl taint node gke-cluster-1-default-pool-bfa03019-p5mj color=blue:NoSchedule
#kubectl get pods --selector app=nginx
#kubectl label node gke-cluster-1-default-pool-bfa03019-p5mj size=large

## DOCKER REGISTRY SECRET OBJECT CREATION
#kubectl create secret docker-registry regcred --docker-server=docker.io --docker-username=achordia --docker-password=Hello@123 --docker-email=email.abhishekchordia@gmail.com