## Question 01
Create a namespace called 'mynamespace' and a pod with image nginx called nginx on this namespace

### Solve
1: Add a Namespace resource called 'mynamespace'
2: Add a Pod belong to 'mynamespace' Namespace.


### Answer with kubectl
```
kubectl create namespace mynamespace
kubectl run nginx --image=nginx --restart=Never -n mynamespace
```

## Question 02
Create the pod that was just described using YAML

### Solve
See pod.yaml.

or

```
kubectl run nginx --image=nginx --restart=Never --dry-run -o yaml > pod.yaml
```
kubectl run -o yaml returns the manifest of the Pod in YAML.
 