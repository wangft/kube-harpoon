# docker registry & kubernetes

## registry use kubernetes pv & pvc (nfs)

### Docker Engine 1.9 or Docker Engine 1.11

* pv use openstack cinder volume from ceph RBD
pv.yaml:

  apiVersion: v1
    kind: PersistentVolume
  metadata:
    name: registry-nfs
    namespace: kube-system
  spec:
    capacity:
      storage: 900Gi
    accessModes:
      - ReadWriteMany
    nfs:
      # FIXME: use the right IP
      server: 192.168.1.34
      path: "/mnt/data"  
## registry use openstack swift storage

### Docker Engine 1.9 or Docker Engine 1.11

* confiy.yml
