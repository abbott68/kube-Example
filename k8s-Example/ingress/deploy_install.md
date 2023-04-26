#部署ingress应用
```
kubectl apply -f deploy.yaml
```
> <font color="red"> 需注意：在什么情景下应用</font>
1. 类型为NodePort
- 修改类型
```yaml
  selector:
    app.kubernetes.io/component: controller
    app.kubernetes.io/instance: ingress-nginx
    app.kubernetes.io/name: ingress-nginx
    #type: LoadBalancer
    type: NodePort  //修改为NodePort 类型
```
- 配置IP地址
```yaml
spec:
  #externalTrafficPolicy: Local
  externalIPs:
    - 192.168.0.112
    - 192.168.0.111
```
2. 类型为LoadBalancer
3. 类型为裸金属设备


#获取Ingres的service的状态
```
kubectl get po,svc -n ingress-nginx
```
#输出状态
```
NAME                                            READY   STATUS    RESTARTS        AGE
pod/ingress-nginx-controller-85dff79875-tqdmg   1/1     Running   1 (6h27m ago)   26h

NAME                                         TYPE        CLUSTER-IP      EXTERNAL-IP                   PORT(S)                      AGE
service/ingress-nginx-controller             NodePort    10.108.231.15   192.168.0.112,192.168.0.111   80:30319/TCP,443:32352/TCP   35h
service/ingress-nginx-controller-admission   ClusterIP   10.104.96.91    <none>                        443/TCP   
```



#创建应用
```
kubectl apply -f aks-helloworld-one.yaml --namespace ingress-basic
kubectl apply -f aks-helloworld-two.yaml --namespace ingress-basic
```
#创建ingress route
```
kubectl apply -f hello-world-ingress.yaml --namespace ingress-basic
```