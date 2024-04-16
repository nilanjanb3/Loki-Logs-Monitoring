# Setting up Loki in Kubernetes

### Step 1: Add Grafana Helm Repo
```sh
$ helm repo add grafana https://grafana.github.io/helm-charts

$ helm repo update
```
### Step 2: Searching for Loki Stack
```sh
$ helm search repo loki

$ helm show values grafana/loki-stack > values.yaml
```

### Step 3: Change in values YAML File

* Enable Grafana
* Change the Grafana Image tag to Latest

### Step 4: Installing Loki Stack
```sh
$ kubectl create ns monitoring

$ helm install --values=./values.yaml loki grafana/loki-stack -n monitoring

$ kubectl get all -n monitoring
```

### Step 5: Connecting Grafana
```sh
$ kubectl port-forward service/loki-grafana 3000:80 -n monitoring

$ kubectl get secrets loki-grafana -n monitoring -o jsonpath="{.data.admin-user}" | base64 -d

$ kubectl get secrets loki-grafana -n monitoring -o jsonpath="{.data.admin-password}" | base64 -d

```