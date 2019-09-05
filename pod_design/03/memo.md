Change the labels of pod 'nginx2' to be app=v2

hint
```
kubectl label pods ${podName} app=v2
```
で、Podに対してラベルを追加できる。
すでに存在しているPodのラベルキーを変更する場合は、エラーになってしまう。

```
$ kubectl label pods nginx2 app=v2
error: 'app' already has a value (v1), and --overwrite is false
```


kubectl labelのhelpを確認して、オプションに--overwriteがあるので、それを使うと変更できる。
```
      --overwrite=false: If true, allow labels to be overwritten, otherwise reject label updates that overwrite existing
labels.
```


answer
```
$ kubectl label pods nginx2 app=v2 --overwrite
```