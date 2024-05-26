- ##### install ingress-controller, service account, roles, role binding by helm

> helm upgrade --install ingress-nginx ingress-nginx \
--repo https://kubernetes.github.io/ingress-nginx \
--namespace ingress-nginx --create-namespace

- ##### config ingress:
> kubectl create ingress socket-ingress \
 --class=nginx \
 --rule=/*=frontend:80 \
 --annotation nginx.ingress.kubernetes.io/ssl-redirect="false" \
 --dry-run=client -o yaml

> kubectl create ingress socket-ingress-api \
--class=nginx \
--rule="/api(/|$)(.*)"=backend:8088 \
--annotation nginx.ingress.kubernetes.io/rewrite-target="/\$2" \
--annotation nginx.ingress.kubernetes.io/ssl-redirect="false" \
--annotation nginx.ingress.kubernetes.io/use-regex="true" \
--dry-run=client -o yaml
