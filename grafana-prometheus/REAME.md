# Grafana

Grafana was designed to be the monitoring solution of this challenge.

## Running Grafama

```
helm repo add grafana https://grafana.github.io/helm-charts
```
```
helm search repo grafana
```
```
helm install grafanaadd grafana/grafana
```
```
kubectl get secret --namespace default grafanaadd -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
```
```
export POD_NAME=$(kubectl get pods --namespace default -l "app.kubernetes.io/name=grafana,app.kubernetes.io/instance=grafanaadd" -o jsonpath="{.items[0].metadata.name}")
```
```
k get pods -A
```
```
kubectl --namespace default port-forward grafanaadd-8d7d884f5-dhfsb 3000
```

Just to check All resources Up!
```
kubectl get pods,cronjobs.batch -A
```