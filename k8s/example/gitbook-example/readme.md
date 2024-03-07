1. 创建 Deployment 文件（deployment.yaml）
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: gitbook-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: gitbook
  template:
    metadata:
      labels:
        app: gitbook
    spec:
      containers:
      - name: gitbook
        image: your-gitbook-image:latest  # 替换成你的 Docker 镜像名称和版本
        ports:
        - containerPort: 4000
        volumeMounts:
        - name: gitbook-data
          mountPath: /app  # 挂载到容器的数据目录
  volumes:
  - name: gitbook-data
    hostPath:
      path: /data/gitbook/y37  # 挂载到宿主机的目录
      type: Directory
    
  #  emptyDir: {}  # 使用空目录，也可以使用 PersistentVolumeClaim 进行持久化存储
```

2. 创建 Service 文件（service.yaml）
```yaml

apiVersion: v1
kind: Service
metadata:
  name: gitbook-service
spec:
  selector:
    app: gitbook
  ports:
    - protocol: TCP
      port: 4000
      targetPort: 4000
  type: LoadBalancer  # 根据需要选择 Service 类型
```

3. 应用 Kubernetes 资源清单
使用 kubectl 命令应用上述创建的 YAML 文件：

```bash

kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

4. 访问服务
一旦部署完成，你可以通过 Service 暴露的 IP 或域名访问 GitBook 服务。你可以使用 kubectl get services 命令查看 Service 的外部 IP 地址。

```bash
kubectl get services
```

注意事项：
这个示例使用了 Deployment 来运行 GitBook 容器，并使用了 LoadBalancer 类型的 Service 来暴露服务。你可以根据需要调整 Replicas、容器镜像、存储等配置。

数据目录 /app/data 使用了一个 emptyDir 卷，这是一个在 Pod 生命周期内存在的临时卷。如果需要持久化存储，你可能需要考虑使用 PersistentVolumeClaim 和 PersistentVolume。

请确保你的 GitBook 服务能够正确运行，并且容器镜像包含了正确的配置。

5. 创建ingress

```shell
kubectl  apply  -f ingress.yaml
```