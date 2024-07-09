resources:
    limits:
        cpu:
        memory:
    requests:
        


cpu: "1" = cpu:"1000" = cpu:"1000m"

memory için byte cinsinden de kullan denebilir.


***
Kubernetes node'lar üstünde cpu ve memory kullanımının kontrol edilmesi.

```
$ kubectl top node 
# kubectl top node "node_ismi" ile tekil bakılabilir #
```
***
Kubernetes pod'lar üstünde cpu ve memory kullanımının kontrol edilmesi.

```
$ kubectl top pod 
# kubectl top pod "pod_ismi" ile tekil bakılabilir #
```