## Deployment Strategy Type
    RollingUpdate
        maxSurge: 25%
        maxUnavailable: 25%
    Recreate

Different type of implementation of service discovery :
    User Space Proxy Mode ?
    IPVS Mode (Hashing)
        IPVS (IP Virtual Server) implements transport-layer load balancing (also known as L4 switch) inside the linux kernel. IPVC running on a host acts as a load balancer before a cluster of real servers, it can direct requests for TCP/UDP based services to the real servers, and make services of the real servers to appear as a virtual service on a single IP Address. The machine that is configured as the load balancer is also known as "Director".
        For routing, NAT, Direct and IPinIP is supported
        Connection Scheduling Algorithms supported :
            Round Robin
            Least Connection
            Destination Hashing
            Source Hashing
            Shorted expected delay
            Never queue

        Configure the Director :
            #apt install ipvsadm -y
            #ipvsadm -L
            #ipvsadm -lcn

        ---
        apiVersion: kubeproxy.config.k8s.io/v1alpha1
        kind: KubeProxyConfiguration
        mod: ipvs


    IPTABLES Mode (Chains)
        Round Robin Method for Load Balancing
        The Basic firewall software most commonly used in Linux is called IPTABLES. the iptables firewall works by interacting with the packet filtering hooks in the linux kernels networking stack. These kernel hooks are known ass the netfilter framework.
        The iptables firewall used tables to organize its rules. These tables classify rules according to the type of decisions they are used to make. For instance if a rule deals with network address translation, it will be put into the NAT Table. If the rule is used to decide whether to allow the packet to continue to its destination, it will be added to the filter table.
        Within each iptable table, rules are further organized within separate "chains", While tables are defined by the general aim of the rules they hold, the built-in chains represent the netfilter hooks which trigger them. Chains basically determine when rules will be evaluated.
        Type of IPTABLES 
            filter
            nat
            mangle
            raw

        Kube-Proxy iptables mode perf Issues (For Large Installation)
        -> For each service add, multitude of iptables rules must be added
        -> Tables are not indexed. Sequential search is done to find which chains and rules applied to a packet
        -> Incremental changes ae not supported (Copy all rules, make changes, save all rules back)
        -> It was never designed to be an efficient load balancer in extermely demanding situations.

Taint Effect :
    NoSchedule
    PreferNoSchedule
    NoExecute

Type of NodeAffinity :
requiredDuringSchedulingIgnoredDuringExecution
preferredDuringSchedulingIgnoredDuringExecution
requiredDuringSchedulingRequiredDuringExecution

Static Pods:
    By Default Path of Configuration file - /etc/kubernetes/manifests/*.yaml
    Else check in kubelet configuration:
        --pod-manifest-path=/etc/kubernetes/manifests
        OR
        --config=kubeconfig.yaml

        kubeconfig.yaml
            staticPodPath: /etc/kubernetes/manifests
    
    Check Container status using :
        #docker ps

Scheduler :
    Default Scheduler Name : default-scheduler
    Customer Scheduler Name : my-custom-scheduler

Metrics Server - In Memory monitoring solution, it runs a subcomponent under kubelet with named c-advisor.

Different STATUS in Kubernetes get command
    Running
    Completed
    ImagePullBackOff
    CrashLoopBackOff
    Pending
    Init
    Failed
    terminated
    Waiting

Multi-Container Pod :
    Ambassador - Backend connection is written in this container and main container will connect on localhost to ambassador container
    Adaptor - Convert the logs into required format
    SideCar - Send multiple application logs to Destination

Cluster Maintenance :
    OS Upgrade :
        #kubectl drain node01 --ignore-daemonsets
        UPGRADE + RESTART THE OS PATCHES
        #kubectl uncordon node01

    Cluster Upgrade :
        Release version - 1.11.3
        1 = Major
        11 = Minor
        3 = Patch
        
        Kubernetes support last 3 minor version support.

        Kubernetes Version :
        kube-apiserver      x
        controller manager  x, x-1
        kube-scheduler      x, x-1
        kubelet             x, x-1, x-2
        kube-proxy          x, x-1, x-2
        kubectl             x-1, x, x+1
