In this step, we will deploy the mysql application using the `PersistentVolumeClaim` created before.

### Step: Deploy mysql

```
echo mysql123 > password.txt
tr --delete '\n' <password.txt >.strippedpassword.txt && mv .strippedpassword.txt password.txt
kubectl create secret generic mysql-pass --from-file=password.txt

kubectl create -f mysql-app.yaml
```{{execute HOST1}}


### Step: Verify mysql pod starts running

```
kubectl get pods -l app=mysql -o wide
```{{execute HOST1}}

### Step: Initialize a sample db

```
POD=`kubectl get pods -l app=mysql | grep  Running | awk '{print $1}'`
sleep 10
kubectl exec -it $POD -- 'mysql --user=root --password=mysql123;\
 create database pxdemo;\
  use pxdemo;\
   create table grapevine (counter int unsigned);\
    show tables;\
     quit;'
```{{execute HOST1}}

