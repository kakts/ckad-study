# 01 configmapの作成方法

```
$ k create configmap config --from-literal=foo=lala --from-literal=foo2=lolo
```
kubectl上で値を渡す場合は--from-literalを使う　1つずつ指定
--from-fileもある -hを参照

# 02 作成したconfigmapの情報確認
```
$ k describe configmap config
Name:         config
Namespace:    default
Labels:       <none>
Annotations:  <none>

Data
====
foo:
----
lala
foo2:
----
lolo
Events:  <none>
```

# 03 fileからconfigmap作成

config_03.txtを作成
```
foo3=lili
foo4=lele
```

コレを--from-file=${path}で読み込む

```
$ k create configmap config03 --from-file=config_03.txt
configmap/config03 created

```

config03の確認
```
$ k get cm config03 -o yaml
apiVersion: v1
data:
  config_03.txt: |-
    foo3=lili
    foo4=lele
kind: ConfigMap
metadata:
  creationTimestamp: "2019-11-20T15:34:00Z"
  name: config03
  namespace: default
  resourceVersion: "1039"
  selfLink: /api/v1/namespaces/default/configmaps/config03
  uid: 2c8d21cc-0bab-11ea-9453-025000000001

or

k describe cm config03
```

# 04 .envファイルからconfigmapを作成する

```
  # Create a new configmap named my-config from an env file
  kubectl create configmap my-config --from-env-file=path/to/bar.env
```
--from-env-fileで指定

```
echo -e "var1=val1\n# this is a comment\n\nvar2=val2\n#anothercomment" > config.env
``` 
config.envに吐き出してコレを読み込む

```
$ k create configmap config04 --from-env-file=config.env
configmap/config04 created
```

結果は
```
$ k describe cm config04
Name:         config04
Namespace:    default
Labels:       <none>
Annotations:  <none>

Data
====
var1:
----
val1
var2:
----
val2
```



# 05 ファイルからよみこみつつ、　specialというキーを渡してconfigmapを作る
不正解
```
echo -e "var3=val3\nvar4=val4" > config4.txt
```
ファイルを作る

```
$ k create configmap config05 --from-file=config4.txt --from-literal=special=1
configmap/config05 created
```

--from-fileと--from-literalを組み合わせる

```
$ k describe cm config05
Name:         config05
Namespace:    default
Labels:       <none>
Annotations:  <none>

Data
====
config4.txt:
----
var3=val3
var4=val4

special:
----
1
Events:  <none>
```

↑　上記は間違いだった --from-file=${keyName}=${path}で　読み込んだデータのまとまりに対してキーを付けれる

```
$ k create configmap config05 --from-file=special=config4.txt

```

```
$ k create configmap config05 --from-file=special=config4.txt
configmap/config05 created
akutsu-no-MacBook-Pro:con akutsukeita$ k describe configmap config05
Name:         config05
Namespace:    default
Labels:       <none>
Annotations:  <none>

Data
====
special:
----
var3=val3
var4=val4
```