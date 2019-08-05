# k8s

k8s架构：  最少三节点Master(ApiServer, Scheduler, Controller Manager, etcd, docker, kubelet, kube-proxy, fluted, pod) + node(docker, kubelet, kube-proxy, fluted, pod) * 2; 

pod: k8s调度的最小单元