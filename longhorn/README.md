# Longhorn configuration

- ### install prerequisite

```
sudo apt-get update


apt-get install open-iscsi
apt-get install nfs-common

sudo systemctl enable iscsid
sudo systemctl start iscsid

sudo systemctl enable rpcbind
sudo systemctl start rpcbind
```

- ### verify prerequisite for longhorn (only master node)

```
apt-get install jq
curl -sSfL https://raw.githubusercontent.com/longhorn/longhorn/v1.3.2/scripts/environment_check.sh | bash
```

- ### add longhorn helm repository
```
helm repo add longhorn https://charts.longhorn.io
helm repo update
```

- ### get longhorn values and override some config
```
helm show values longhorn/longhorn > longhorn.values.yml
```

- ### install longhorn:
```
helm install longhorn longhorn/longhorn --namespace longhorn-system --create-namespace --values longhorn.values.yml
```
