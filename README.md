<h1>Phase 1</h1>

<h2>Backend</h2>
(1) Created deployment for backend in Node.js.<br>
(2) Configured clusterip service for backend for interpod communication.<br>
(3) Created HPA for backend depployment for autoscaling based on memory and cpu.<br>
(4) Created liveness and readiness probe for pod health check.<br>
(5) Created secret for registry to authenticate the iamge pull.<br>
(6) Cofigured secret for mongodb username and password.<br>
(7) Created network policy for backend deployment for pod security.<br>
(8) Created config map for environment variables.<br>
(9) Configured rolling update in deployment.<br>
(10) Configured resource and limits for resource management.<br>

<h2>Frontend</h2>
(1) Created deployment for frontend for angular.<br>
(2) Configured clusterip service for frontend deployment for interpod communication.<br>
(3) Created HPA for backend depployment for autoscaling based on memory and cpu.<br>
(4) Configured resource and limits for resource management.<br>
(5) Created secret for registry to authenticate the iamge pull.<br>
(6) Created liveness and readiness probe for pod port check.<br>
(7) Configured image pull policy only ifNotPresent.<br>
(8) Created ingress for exposing application to external world.<br>
(9) Creted tls secret for ssl cert of the domain.<br>
(10) Configured rolling update in deployment.<br>

<h2>MongoDB</h2>
(1) Created statefulset for mongodb database.<br>
(2) Configured headless-service for service discovery.<br>
(3) Configured side car container which is designed to manage and monitor the MongoDB replica set.<br>
(4) Configured volumeClaimTemplate for data persistant.<br>
(5) Created secret for mongodb username and password.<br>
(6) Configured terminationGracePeriodSeconds for smooth creation of pod after termination.<br>

<h2>RabbitMQ</h2>







Monitoring a Kubernetes Cluster using Prometheus and Grafana

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

