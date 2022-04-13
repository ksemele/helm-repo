# helm-repo [WIP]
Test repo for Helm charts experiments.

Follow this instructions to local run if you are download this repo.

# Subcharts
Use this commands to see what it happened:

```
$ helm install service service-subchart
$ helm list
$ kubectl get po
```
You may see 2 Running Pods:
```
$ helm install service service-subchart

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

$ helm list
NAME    NAMESPACE       REVISION        UPDATED                                 STATUS          CHART                   APP VERSION
service default         1               2022-04-13 10:17:16.344290362 +0400 +04 deployed        service-subchart-0.1.0  1.16.0

$ kubectl get po
NAME                                        READY   STATUS    RESTARTS   AGE
service-service-subchart-776b9b785c-sgj9w   1/1     Running   0          5s
service-subchart-6cf4994db9-nnchs           1/1     Running   0          5s
```

# Environment related chart
Use this commands to see what it happened:
```
$ helm template ./service-chart -f service-source-code/values.yaml --namespace d007  --debug
$ helm template ./service-chart -f service-source-code/values.yaml --namespace s007  --debug
$ helm template ./service-chart -f service-source-code/values.yaml --namespace p007  --debug
```

# Uninstall all charts
```
$ for each in $(helm list -q); do helm uninstall $each; done
```

# Using this repo as Helm repo

## Add repo
```
$ helm repo add ksemele-helm https://github.com/ksemele/helm-repo/raw/master/ 
"ksemele-helm" has been added to your repositories

$ helm repo update
Hang tight while we grab the latest from your chart repositories...
...Successfully got an update from the "ksemele-helm" chart repository
Update Complete. ⎈Happy Helming!⎈

$ helm repo list
NAME                	URL                                               
ksemele-helm        	https://github.com/ksemele/helm-repo/raw/master/

$ helm search repo ksemele-helm
NAME                         	CHART VERSION	APP VERSION	DESCRIPTION                
ksemele-helm/service-chart   	0.1.0        	1.16.0     	A Helm chart for Kubernetes
ksemele-helm/service-subchart	0.1.0        	1.16.0     	A Helm chart for Kubernetes
ksemele-helm/subchart        	0.1.0        	1.16.0     	A Helm chart for Kubernetes
ksemele-helm/test-chart      	0.1.0        	1.16.0     	A Helm chart for Kubernetes
```
Then you can install charts from this repo like that:
```
$ helm template ksemele-helm/service-chart --namespace d007  --debug
```