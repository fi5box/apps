## 介绍
Tailscale makes creating software-defined networks easy: securely connecting users, services, and devices.

https://tailscale.com/kb/1185/kubernetes

## image

tailscale/tailscale:v1.72.1

## dockerfile

https://github.com/tailscale/tailscale/blob/main/Dockerfile


## 参数

需要实现通过如下命令把AUTH-kEY创建好

```
kubectl create secret generic tailscale-auth --from-literal TS_AUTHKEY=<AUTH-kEY>
```

部署后记得到tailscale官网控制台 Edit route settings of subnet-router

部署方式参见 https://github.com/tailscale/tailscale/blob/main/docs/k8s/README.md

https://chimbu.medium.com/access-kubernetes-applications-securely-without-load-balancers-via-tailscale-792584d5a59c

## 暴露端口

* 3000  -- web server

## 查询信息

```
# 查询pod网段
$ kubectl --kubeconfig ~/.kube/config -n kube-system describe pod coredns | grep 'IP:                   10'
IP:                   10.42.0.188

# 查询svc网段
$ kubectl --kubeconfig ~/.kube/config -n kube-system describe svc kube-dns | grep 'IP:                10'
IP:                10.43.0.10

# 查询 lnd pod ip
$ kubectl --kubeconfig ~/.kube/config -n default describe pod lnd-0 | grep 'IP:               10'
IP:               10.42.0.197
```
