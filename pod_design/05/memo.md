Remove the 'app' label from the pods we created before

hint
これもkubectl labelコマンドでいける
kubectl label --helpで、コマンドの使用例のところに、削除する方法が書いてあるのでそれを参考にする
```
  # Update pod 'foo' by removing a label named 'bar' if it exists.
  # Does not require the --overwrite flag.
  kubectl label pods foo bar-
```

answer

```
キー名の後ろにハイフンをつけると削除扱いになる。

kubectl label pods nginx1 app-
kubectl label pods nginx2 app-
kubectl label pods nginx3 app-

Pod名に規則があれば、まとめて削除できる。
$ kubectl label pods nginx{1..3} app-
pod/nginx1 labeled
pod/nginx2 labeled
pod/nginx3 labeled
$ kubectl get po --show-labels
NAME     READY   STATUS    RESTARTS   AGE   LABELS
nginx1   1/1     Running   0          33m   <none>
nginx2   1/1     Running   0          33m   <none>
nginx3   1/1     Running   0          33m   <none>
```