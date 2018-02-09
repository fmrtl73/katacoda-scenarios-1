In this step, we will create a Portworx volume (PVC) for postgres.

### Step: Create StorageClass and PersistentVolumeClaim

Take a look at the StorageClass definition for Portworx
```
cat px-repl3-sc.yaml
```{{execute T1}}

The parameters here are declarative policies for your storage volume. See here for a full list of supported parameters.
  
Create the storage class using:
```
kubectl create -f px-repl3-sc.yaml
```{{execute T1}}

Take a look at the Persistent Volume Claim
```
cat px-postgres-pvc.yaml
```{{execute T1}}

This defines the maximum volume size. Portworx will thing provision the volume and let it grow to 10GB size.
 
Create the PersistentVolumeClaim using:
```
kubectl create -f px-postgres-pvc.yaml
```{{execute T1}}

Now that we have the volumes created, let's deploy postgres !