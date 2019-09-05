## Question 05
Get the YAML for a new namespace called 'myns' without creating it

### Solve
There is a way to get the yaml without creating it.
You can easily add --dry-run flag when you use kubectl 






## Question 06
Get the YAML for a new ResourceQuota called 'myrq' without creating it

### Solve
You can use create.
But, if you don't know about this type of Resource, first you can check the Resource via kubectl api-resources

```
$ kubectl api-resources | grep Resource
resourcequotas                    quota                                       true         ResourceQuota
customresourcedefinitions         crd,crds     apiextensions.k8s.io           false        CustomResourceDefinition
```

You can know the short name of ResourceQuota resource.

So you just only type the name when you use kubectl create ${resource name} ${name} --dry-run -o yaml
```
$ kubectl create quota myns --dry-run -o yaml
apiVersion: v1
kind: ResourceQuota
metadata:
  creationTimestamp: null
  name: myns
spec: {}
status: {}
```

## Question 07
Get pods on all namespaces

### Solve
First, we should check the options for kubectl get.

In the help, you can find a option about namespaces.
```
  -A, --all-namespaces=false: If present, list the requested object(s) across all namespaces. Namespace in current
context is ignored even if specified with --namespace.
```
If you use -A(or --all-namespaces), you can find the resources from all of namespaces in the cluster.

So answer is below.
```
kubectl get pods -A
```