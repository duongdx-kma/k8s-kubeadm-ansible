- ##### install nfs-subdir-external-provisioner:
> follow: https://github.com/kubernetes-sigs/nfs-subdir-external-provisioner/blob/master/charts/nfs-subdir-external-provisioner/README.md

- ##### add helm repo
> helm repo add nfs-subdir-external-provisioner https://kubernetes-sigs.github.io/nfs-subdir-external-provisioner

- ##### create new namespace
> kubectl create ns storage

> helm install delete-nfs-subdir-external-provisioner --namespace storage nfs-subdir-external-provisioner/nfs-subdir-external-provisioner \
--set nfs.server=192.168.56.198 \
--set nfs.path=/mnt/delete \
--set storageClass.reclaimPolicy=Delete \
--set storageClass.name=nfs-delete

> helm install retain-nfs-subdir-external-provisioner --namespace storage nfs-subdir-external-provisioner/nfs-subdir-external-provisioner \
--set nfs.server=192.168.56.198 \
--set nfs.path=/mnt/retain \
--set storageClass.reclaimPolicy=Retain \
--set storageClass.name=nfs-retain

- ##### making content:
> ssh to nfs_server => create index.html inside the mounting directory