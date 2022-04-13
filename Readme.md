# helm-repo
Test repo for Helm chart.

Follow this instructions to local run if you are download this repo.

## subcharts
Use this commands to see what it happened:

```
helm install service service-subchart

helm list

kubectl get po
```
You may see 2 Running Pods:
```
➜  helm-repo git:(master) ✗ helm install service service-subchart

NAME: service
LAST DEPLOYED: Wed Apr 13 10:17:16 2022
NAMESPACE: default
STATUS: deployed
REVISION: 1
NOTES:
1. Get the application URL by running these commands:
  export POD_NAME=$(kubectl get pods --namespace default -l "app.kubernetes.io/name=service-subchart,app.kubernetes.io/instance=service" -o jsonpath="{.items[0].metadata.name}")
  export CONTAINER_PORT=$(kubectl get pod --namespace default $POD_NAME -o jsonpath="{.spec.containers[0].ports[0].containerPort}")
  echo "Visit http://127.0.0.1:8080 to use your application"
  kubectl --namespace default port-forward $POD_NAME 8080:$CONTAINER_PORT
➜  helm-repo git:(master) ✗ helm list
NAME    NAMESPACE       REVISION        UPDATED                                 STATUS          CHART                   APP VERSION
service default         1               2022-04-13 10:17:16.344290362 +0400 +04 deployed        service-subchart-0.1.0  1.16.0     
➜  helm-repo git:(master) ✗ kubectl get po
NAME                                        READY   STATUS    RESTARTS   AGE
service-service-subchart-776b9b785c-sgj9w   1/1     Running   0          5s
service-subchart-6cf4994db9-nnchs           1/1     Running   0          5s
```

## environment related chart


Use this commands to see what it happened:
```
helm template ./service-chart -f service-source-code/values.yaml --namespace d007  --debug

helm template ./service-chart -f service-source-code/values.yaml --namespace s007  --debug

helm template ./service-chart -f service-source-code/values.yaml --namespace p007  --debug
```

## uninstall all charts
```
for each in $(helm list -q); do helm uninstall $each; done
```

# Using this repo as Helm repo [WIP]

## Add repo
```
helm repo add 
```