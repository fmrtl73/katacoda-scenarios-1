Before installing Portworx, let's ensure Kubernetes is setup.

### Step: Wait till nodes are ready

Click the below section which waits for all Kubernetes nodes to be ready.
```
./k8s-wait-ready.sh
```{{execute T1}}

### Step: List Kubernetes nodes

To list nodes, click: `kubectl get nodes`{{execute T1}}

### Step: Wait till Portworx pods are ready
```
kubectl get pods -n kube-system -l name=portworx -o wide

while true; do
    NUM_READY=`kubectl get pods -n kube-system -l name=portworx -o wide | grep Running | grep 1/1 | wc -l`
    if [ "${NUM_READY}" == "3" ]; then
        echo "All portworx nodes are ready !"
        kubectl get pods -n kube-system -l name=portworx -o wide
        break
    else
        echo "Waiting for portworx nodes to be ready. Current ready nodes: ${NUM_READY}"
    fi
    sleep 5
done
```{{execute T1}}

Now that we have the Portworx cluster up, let's proceed to the next step !