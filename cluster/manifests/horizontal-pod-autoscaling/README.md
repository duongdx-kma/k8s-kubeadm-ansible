<h3> config metric-server to horizontal scaling pod</h3>
<hr/>
<h4> follow the guidelines: </h4>
<hr/>
<h5> - https://computingforgeeks.com/deploy-metrics-server-in-kubernetes-using-helm/</h5>
<hr/>
<h5> - https://viblo.asia/p/k8s-phan-5-metrics-server-cho-k8s-va-demo-hpa-oOVlYRwz58W</h5>
<hr/>

- ##### add metric-server helm repository:
> helm repo add metrics-server https://kubernetes-sigs.github.io/metrics-server

- ##### get metrics-server values and customize your value
> helm show values metrics-server/metrics-server > metrics-server.yaml

- ##### install chart:
> helm install metrics-server metrics-server/metrics-server -n  metrics-server --create-namespace --values metrics-server.yaml

- ##### create horizontal-pod-scaler:
> kubectl apply -f horizontal-pod-scaler.yaml

- ### testing:
- ##### check horizontal-pod-scaler:
> kubectl get hpa

- ##### check resources are consuming for pods:
> check resources are consuming for pods: kubectl top pods

- ##### check resources are consuming for nodes:
> check resources are consuming for nodes: kubectl top pods

- ##### make more traffic to "backend service to test traffic spike":
> kubectl apply -f testing-traffic-spike.yaml

