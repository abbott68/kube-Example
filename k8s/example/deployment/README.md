1. 创建deployment对象的pod

```shell
kubectl apply  -f nginx-deployment.yaml
```
2. 检查是否创建成功

```
kubectl get deployment  -n webnginx
```

3. 滚动更新

```

```