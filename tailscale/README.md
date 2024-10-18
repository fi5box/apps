## 介绍
Tailscale makes creating software-defined networks easy: securely connecting users, services, and devices.

## image

tailscale/tailscale:v1.72.1
tailscale/tailscale-operator:v1.72.1

## manifest

https://github.com/tailscale/tailscale/blob/v1.72.1/cmd/k8s-operator/deploy/manifests/operator.yaml

imagePullPolicy 改为 IfNotPresent

## 参数

申请oauth 并部署 secret：

```
apiVersion: v1
kind: Secret
metadata:
  name: operator-oauth
  namespace: tailscale
stringData:
  client_id: # SET CLIENT ID HERE
  client_secret: # SET CLIENT SECRET HERE
```

参见：

https://leebriggs.co.uk/blog/2024/02/26/cheap-kubernetes-loadbalancers

https://tailscale.com/kb/1236/kubernetes-operator


