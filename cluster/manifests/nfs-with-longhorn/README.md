- ##### first need install "open-iscsi", "nfs-common":
> already added in playbook/common-playbook.yml

- ##### install jq and verify cluster (prerequisite preparation):
> apt-get install jq

> curl -sSfL https://raw.githubusercontent.com/longhorn/longhorn/v1.3.2/scripts/environment_check.sh | bash

- ##### install longhorn with helm
> helm repo add longhorn https://charts.longhorn.io

> `helm repo update`

> helm install longhorn longhorn/longhorn --namespace longhorn-system --create-namespace --values longhorn-value.yaml

- ##### testing:
> kubectl apply testing-retain.yaml
> kubectl apply testing-delete.yaml