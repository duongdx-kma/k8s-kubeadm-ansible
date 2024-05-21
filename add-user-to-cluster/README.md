- ##### 1. generate user key:
> openssl genrsa -out argocd.key 2048

- ##### 2. create new user csr (certificate signing request) key:
> openssl req -new -key argocd.key -out argocd.csr -subj "/CN=argocd/O=devops/O=maintainer"

- ##### 2.1 explore certificate signing request:
> openssl req -in argocd.csr -noout -text

- ##### 3. get user csr (certificate signing request) have just created:
> cat argocd.csr | base64 | tr -d "\n"

- ##### 4. apply certificate signing request:
> kubectl apply -f certificate-signing-request.yaml

- ##### 5. checking csr:
> kubectl get csr

- ##### 6. approve csr:
> kubectl certificate approve argocd-csr

- ##### 7. get argocd.crt
> kubectl get csr argocd-csr -o jsonpath='{.status.certificate}'| base64 -d > argocd.crt

- ##### 8. assign role for group and user:
> kubectl apply -f role.yaml

> kubectl apply -f role-binding.yaml

> kubectl apply -f cluster-role.yaml

> kubectl apply -f cluster-role-binding.yaml


- ##### 9. check user and group:
> kubectl auth can-i create deployments --namespace=default --as=argocd

> kubectl auth can-i create deployments \
--server=https://192.168.49.2:8443 \
--certificate-authority=/home/duongdx/.minikube/ca.crt \
--client-certificate=argocd.crt \
--client-key=argocd.key

> kubectl auth can-i create secrets --namespace=default --as=john

> kubectl auth can-i get pods --namespace=default --as=john

- ##### 10.a add cluster to kube.config file:

> kubectl config set-cluster kubeadm-cluster --certificate-authority=/home/duongdx/.kube/kubeadm-cluster/kubeadm-cluster-ca.crt --server=https://192.168.56.167:6443


- ##### 10.b adding user to kube.config file:
> kubectl config set-credentials argocd --client-key=argocd.key --client-certificate=argocd.crt --embed-certs=true

- ##### 10.c set-context by cluster and user have just added to config file
> kubectl config set-context argocd --cluster=kubeadm-cluster --user=argocd
<!-- --cluster=kubernetes or --cluster=minikube depend on your purpose -->


- ##### 11. set user to argocd
> kubectl config use-context argocd

- ##### 12. if don't add user to 
> kubectl get pods \
--server=https://192.168.49.2:8443 \
--certificate-authority=/home/duongdx/.minikube/ca.crt \
--client-certificate=argocd.crt \
--client-key=argocd.key