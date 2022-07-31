# Queries

1.) How to check logs for all pods within same deployment type object?
kubectl logs --selector component=kube-proxy -n kube-system
       
2.) Different STATUS in Kubernetes get command
    Running
    Completed
    ImagePullBackOff
    CrashLoopBackOff
    Pending
    Init
    Failed
    terminated
    Waiting

3.) Where is the ipvsadm deployed in NCS and Non_NCS Cluster