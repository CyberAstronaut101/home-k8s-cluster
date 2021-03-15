# Configure NFS Based Persistent Volume

https://www.linuxtechi.com/configure-nfs-persistent-volume-kubernetes/

A PersistentVolume (PV) is a piece of storage in the cluster that has been provisioned by an administrator or dynamically provisioned using Storage Classes. It is a resource in the cluster just like a node is a cluster resource. PVs are volume plugins like Volumes, but have a lifecycle independent of any individual Pod that uses the PV. This API object captures the details of the implementation of the storage, be that NFS, iSCSI, or a cloud-provider-specific storage system.

A PersistentVolumeClaim (PVC) is a request for storage by a user. It is similar to a Pod. Pods consume node resources and PVCs consume PV resources. Pods can request specific levels of resources (CPU and Memory). Claims can request specific size and access modes (e.g., they can be mounted ReadWriteOnce, ReadOnlyMany or ReadWriteMany, see AccessModes).

--- 

NFS: `10.21.180.4:/mnt/share`

--- 

`nfs-pv.yaml` is used to configure the NFS PV mount on the K8s cluster

```bash
// Create the Persistent Volume
kubectl create -f nfs-pv.yaml

// Verify status of Persistent Volume
kubectl get pv

//Create PVC
kubectl create -f nfs-pvc.yaml

// DELETING REQUIRES DELETE PVC THEN PV

// Delete PV
kubectl delete pvc PVC_NAME
kubectl delete pv PV_NAME
```



# Creating Persistent Volume Claim

A persistent volume claim (PVC) specifies the desired access mode and storage capacity. Currently, based on only these two attributes, a `PVC is bound to a single PV`. Once a PV is bound to a PVC, that PV is essentially tied to the PVC’s project and cannot be bound to by another PVC. There is a one-to-one mapping of PVs and PVCs. However, multiple pods in the same project can use the same PVC. This is the use case we are highlighting in this example.


# Deleting PVC and PV

`kubectl patch pv PV_NAME -p '{"spec":{"persistentVolumeReclaimPolicy":"Delete"}}'`

Running busybox

`kubectl run -i --tty --rm debug --image=busybox --restart=Never --`