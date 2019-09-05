Create 3 pods with names nginx1, nginx2, nginx3. All of them should have the label app=v1

# YAML版
nginx{1..3}.yamlをapplyする。

# kubectl版
```
kubectl run nginx1 --image=nginx --restart=Never --labels=app=v1
kubectl run nginx2 --image=nginx --restart=Never --labels=app=v1
kubectl run nginx3 --image=nginx --restart=Never --labels=app=v1
```