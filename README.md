# ethereum-on-kubernetes
Kubernetes平台部署以太坊

1. 修改NFS服务器地址和路径
```
vim ethereum-persistent-volumes.yaml
nfs:
  path: /data/ethereum
  server: 10.250.218.55
```
2. 进行一些简单的设置
你可以通过修改```ethereum-configmap.yaml```文件```genesis.json```的配置，以设置挖矿难度等参数.

3. 创建所有资源对象
```
kubectl create -f .
```

短时间的等待后，查看所有资源状态, 它们都在一个名为```ethereum```的Namespace下
```
kubectl get all -n ethereum
```

```
NAME                           READY   STATUS    RESTARTS   AGE
pod/bootnode-996bf478d-7m8fc   1/1     Running   0          10m
pod/node1-8486864548-qkqzb     1/1     Running   0          10m
pod/node2-78f855ffd5-9dcpv     1/1     Running   0          10m
pod/node3-75954f8-dj7nn        1/1     Running   0          10m

NAME                       TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)                          AGE
service/bootnode-service   ClusterIP   10.108.248.235   <none>        30301/UDP                        10m
service/node1-service      NodePort    10.97.33.8       <none>        8545:30045/TCP,30303:30303/TCP   10m
service/node2-service      NodePort    10.101.151.234   <none>        8545:30046/TCP,30303:30304/TCP   10m
service/node3-service      NodePort    10.105.103.205   <none>        8545:30047/TCP,30303:30305/TCP   10m

NAME                       READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/bootnode   1/1     1            1           10m
deployment.apps/node1      1/1     1            1           10m
deployment.apps/node2      1/1     1            1           10m
deployment.apps/node3      1/1     1            1           10m

NAME                                 DESIRED   CURRENT   READY   AGE
replicaset.apps/bootnode-996bf478d   1         1         1       10m
replicaset.apps/node1-8486864548     1         1         1       10m
replicaset.apps/node2-78f855ffd5     1         1         1       10m
replicaset.apps/node3-75954f8        1         1         1       10m
```

默认创建账户使用的密码: ```cesgroup```
