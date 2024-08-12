Monitoring a Kubernetes Cluster using Prometheus and Grafana
------------------------------------------------------------

Steps:

(1) kubectl create namespace monitoring<br>
(2) helm repo add prometheus-community https://prometheus-community.github.io/helm-charts<br>
(3) helm repo update<br>
(4) helm install prometheus prometheus-community/prometheus --namespace monitoring<br>
(5) kubectl get pods -n monitoring<br>
(6) kubectl expose service prometheus-server --namespace monitoring --type=NodePort --target-port=9090 --name=prometheus-server-ext<br>
(7) helm repo add grafana https://grafana.github.io/helm-charts<br>
(8) helm install grafana grafana/grafana --namespace monitoring<br>
(9) kubectl get secret --namespace monitoring grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo<br>
(10) kubectl expose service grafana --namespace monitoring --type=NodePort --target-port=3000 --name=grafana-ext<br>

Access Grafana dashboard on the NodeIP with nodePort service port.

