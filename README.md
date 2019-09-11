# ethereum-on-kubernetes
Kubernetes平台部署以太坊

1. 修改NFS服务器地址和路径
```
    vim ethereum-persistent-volumes.yaml
    nfs:
      path: /data/ethereum
      server: 10.250.218.55
```

2. 
