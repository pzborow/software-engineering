# Kubernetes MicroK8s

 Świerzy artykuł, jest w nim alias
https://www.endpointdev.com/blog/2022/01/kubernetes-101/

https://adamtheautomator.com/microk8s/

http://thinkmicroservices.com/blog/2020/kubernetes/docker-compose-to-kubernetes-part-1.html
http://thinkmicroservices.com/blog/2020/kubernetes/docker-compose-to-kubernetes-part-2.html
http://thinkmicroservices.com/blog/2020/kubernetes/docker-compose-to-kubernetes-part-3.html

`kubectl describe service kubernetes-dashboard -n kube-system`  IP address of dashboard
`kubectl get service`  IP adrees of nginx
`kubectl port-forward -n kube-system service/kubernetes-dashboard 10443:443 --address 0.0.0.0` aby dostać się do dashboard z zewnątrz
