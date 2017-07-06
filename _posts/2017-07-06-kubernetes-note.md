## 1.常用命令
```

kubectl get all --all-namespaces

kubectl get all --all-namespaces --show-all -o wide

kubectl get ns

kubectl get pods/pod/ing/rc/rs/svc/ns -n core

kubectl get pods -n=<namespace>

kubectl exec -it <pod_id> -n=<namespace> /bin/bash

kubectl exec -it <pod_id> -n=<namespace> bash

kubectl create -f *.yaml

kubectl delete -f *.json

kubectl describe pod <pod_name> -n <namespace>

kubectl get pod <pod_name> -n <namespace> -o yaml/json

kubectl get pod <pod_name> -n <namespace> -o yaml/json > /tmp/pod.yaml/json

kubectl logs -f idm-2958378241-nsqq3 -n core -c idm



```