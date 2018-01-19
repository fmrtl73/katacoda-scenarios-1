In this step, we will deploy the mysql application using the `PersistentVolumeClaim` created before.

### Step: Create secret for mysql

Below we are creating a Secret to store the mysql password.
```
echo mysql123 > password.txt
tr --delete '\n' <password.txt >.strippedpassword.txt && mv .strippedpassword.txt password.txt
kubectl create secret generic mysql-pass --from-file=password.txt
```{{execute T1}}

### Step: Create secret for mysql
Below we will create a mysql [Deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) that uses a Portworx PVC.
```
kubectl create -f mysql-app.yaml
```{{execute T1}}

Feel free to ```cat mysql-app.yaml```{{execute T1}} and observe the `volumeMounts` and `volumes` sections where we mount the PVC.

### Step: Verify mysql pod is ready

Below commands wait till the mysql pods are in ready state.
```
while true; do
    NUM_READY=`kubectl get pods -l app=mysql -o wide | grep Running | grep 1/1 | wc -l`
    if [ "${NUM_READY}" == "1" ]; then
        echo "mysql is ready !"
        break
    else
        echo "Waiting for mysql to be ready..."
        kubectl get pods -l app=mysql -o wide
    fi
    sleep 5
done
```{{execute T1}}
