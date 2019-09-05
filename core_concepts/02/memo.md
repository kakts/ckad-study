## Question02
Create a busybox pod (using kubectl command) that runs the command "env". Run it and see the output

### Solve
Use kubectl run --command --it -- ${command}
or
Use kubectl run --command -- ${command}

If you don't use --it. After doing kubectl run, you can see logs via `kubectl logs ${pod}`


## Question 03
Create a busybox pod (using YAML) that runs the command "env". Run it and see the output

### Solve
Apply busybox-pod.yaml and kubectl logs ${pod}

https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.14/#container-v1-core
In container spec, there is `command` parameter.
So you set command in yaml
```
containers:
    - name: busybox
      image: busybox
      command:
        - env
...
```