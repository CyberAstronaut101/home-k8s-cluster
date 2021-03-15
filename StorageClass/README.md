https://levelup.gitconnected.com/how-to-use-nfs-in-kubernetes-cluster-storage-class-ed1179a83817


1. Service Account
2. Cluster Role
3. Cluster Role Binding
4. Role
5. Role Binding


```
// Check if all Service Account roles and bindings are correct

kubectl get clusterrole,role,clusterrolebindings,rolebindings -o custom-columns='KIND:kind,NAME:metadata.name,SERVICE_ACCOUNTS:subjects[?(@.kind=="ServiceAccount")].name' | grep nfs-client

// Should get

ClusterRole          nfs-client-provisioner-runner           <none>
Role                 leader-locking-nfs-client-provisioner   <none>
ClusterRoleBinding   run-nfs-client-provisioner              nfs-client-provisioner
RoleBinding          leader-locking-nfs-client-provisioner   nfs-client-provisioner
```



```
// Create the service accounts, etc
kubectl apply -f service-account.yaml

//Create Storage Class
kubectl apply -f storage-class.yaml

// Create the provisioner
kubectl apply -f provisioner-deploy.yaml

// Test PVC 
kubectl apply -f ./Test/test-pvc.yaml
```