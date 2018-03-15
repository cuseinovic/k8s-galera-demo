It's a fork of the project k8s-galera-demo from ObjectifLibre

## Prerequisite

- K8S cluster
- Rook
- kube config 

## Storageclass

I used the project rook to create a ceph cluster inside my nodes k8s
You can find this project [here](https://github.com/rook/rook)

```
volumeClaimTemplates:
- metadata:
    name: percona
    annotations:
      volume.beta.kubernetes.io/storage-class: rook-block
```

## Usage

Create Namespace
```
./create-namespace.sh
```
Deploy the service
```
kubectl create -f svc.yaml
```
Add configmap
```
kubectl create -f configmap.yaml
```
Deploy your statefulset
```
kubectl create -f statefulset.yaml
```

