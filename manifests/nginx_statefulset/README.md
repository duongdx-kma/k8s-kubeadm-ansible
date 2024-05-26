kubectl apply -f web.yaml
kubectl get pods -l app=nginx
kubectl get service nginx-headless nginx-normal
kubectl get statefulset web

for i in 0 1; do kubectl exec "web-$i" -c nginx -- sh -c 'hostname'; done
kubectl run -i --tty --image busybox:1.28 dns-test --restart=Never --rm
nslookup nginx-normal
nslookup nginx-headless
nslookup web-0.nginx-headless
