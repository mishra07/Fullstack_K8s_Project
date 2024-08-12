Monitoring a Kubernetes Cluster using Prometheus and Grafana
------------------------------------------------------------

Steps:

(1) kubectl create namespace monitoring
(2) helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
(3) helm repo update
(4) helm install prometheus prometheus-community/prometheus --namespace monitoring
(5) kubectl get pods -n monitoring
(6) kubectl expose service prometheus-server --namespace monitoring --type=NodePort --target-port=9090 --name=prometheus-server-ext
(7) helm repo add grafana https://grafana.github.io/helm-charts
(8) helm install grafana grafana/grafana --namespace monitoring
(9) kubectl get secret --namespace monitoring grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
(10) kubectl expose service grafana --namespace monitoring --type=NodePort --target-port=3000 --name=grafana-ext

Access Grafana dashboard on the NodeIP with nodePort service port.

