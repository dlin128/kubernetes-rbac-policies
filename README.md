Cluster RBAC Policies
========================
These RBAC files have been modified from the original (by uruddarraju) to work on Kubernetes 1.4. Certain configuration checks were tightened from 1.3 -> 1.4 and thus will not work.

You'll need to add the following options to your api-server:

The super user noted below comes from the CN in the cert that is used for authentication with the default kubeadm installation.

```
--authorization-mode=RBAC --authorization-rbac-super-user=kubernetes-admin --runtime-config=api/v1,rbac.authorization.k8s.io/v1alpha1
```
As soon as the api server comes up with these new options everything will break, don't panic. Now we just need to use the "super user" we specified above to set the rbac policies detailed in the folders in this repo.

To do that copy /etc/kubernetes/kubelet.conf to your own ~/.kube/config and do kubectl use-context admin@kubernetes if it isn't already

```
EX:
kubectl apply -f roles/
kubectl apply -f rolebindings/
```

