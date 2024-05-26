# MetalLB help expose service type LoadBalancer to end  user

- ### install metalLB with helm:

```
helm repo add metallb https://metallb.github.io/metallb
helm install metallb metallb/metallb --namespace metallb-system --create-namespace
```

- ### apply metalLB  ip-address-pool
```
kubectl apply -f metalLB/metalLB.yml
```

- ### checking metalLB
```
- kubectl get ipaddresspools -n metallb-system
- kubectl get l2advertisements -n metallb-system
```