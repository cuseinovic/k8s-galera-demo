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
## Environment Variables

You can adjust the configuration of your container by passing one or more environment variable in statefullset.yaml file

#### MYSQL_ROOT_PASSWORD
This variable is mandatory and specifies the password that will be set for the root superuser account.

#### MYSQL_DATABASE
Specify the name of a database to be created on container. If a user/password was supplied (see below) then that user will be granted superuser access (corresponding to GRANT ALL) to this database.

#### MYSQL_USER, MYSQL_PASSWORD
Create a new user and set the user's password. This user will be granted superuser permissions for the database specified by the MYSQL_DATABASE variable.

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

