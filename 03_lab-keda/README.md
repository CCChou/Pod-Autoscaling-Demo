# KEDA Demo

建立 service account 給 KEDA Trigger 使用
```
oc create serviceaccount thanos
oc describe serviceaccount thanos
```

新建 trigger 所需的身分驗證設定檔
```
apiVersion: keda.sh/v1alpha1
kind: TriggerAuthentication
metadata:
  name: keda-trigger-auth-prometheus
spec:
  secretTargetRef:
  - parameter: bearerToken
    name: thanos-token-gjprx       # update this
    key: token
  - parameter: ca
    name: thanos-token-gjprx       # update this
    key: ca.crt
```

給定權限
```
oc adm policy add-cluster-role-to-user cluster-admin -z thanos
```
- **TODO:** 理論上要給一個合適的權限就好，e.g. metrics read 
