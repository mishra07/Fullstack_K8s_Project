<h1>Phase 1</h1>
Architectural Diagram -> ![K8s_Project](https://github.com/user-attachments/assets/36a8ac24-8380-4a86-9d24-3df3006b58ce)
<br>
-> Created backend, frontend, DB and RabbitMQ.<br>
-> Backend will communicate with MongoDB and RabbitMQ.<br>
-> DB will used for storing user details, order details etc.<br>
-> RabbitMQ will be used for storing order status with asynchronous communication.<br>
-> Users will access frontend using domain name and path.<br>

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
(1) Created statefulset for rabbitmq.<br>
(2) Configured headless-service for service discovery.<br>
(3) Configured volumeClaimTemplate for data persistant.<br>
(4) Configured init container to mount configmap to give container the read-write access of configmap.<br>
(5) Created liveness and readiness probe for pod port check.<br>
(6) Created service account and rbac for role based access and to have limited permission.<br>
(7) Configured security context for non-root user access.<br>

<h2>OPA/Gatekeeper</h2>
(1) Implimented policies to prevent using :latest as the image tag for ensuring that only stable images are used.<br>
(2) Implimented policies to enforce resource quota, limitng cpu, memory and otehr resources.<br>
(3) Impliment policies to enforce liveness and readiness probe to enusre health, port check etc.<br>

<h1>Phase 2</h1>

<h2>Monitoring a Kubernetes Cluster using Prometheus and Grafana</h2>

-> Used helm package manager to deploy prometheus and grafana.
-> Deployed prometheus as daemonset to ensure running on all the nodes.<br>
-> Deployed prometheus-alertmanager as statefulset.<br>
-> Deployed grafana as deployment and exposed as nodeport service.<br>

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

<h2>Logging using EFK Stack</h2>
(1) Created statefulset for ElasticSearch.<br>
(2) Created headless service for elasticsearch for service discovery.<br>
(3) Created deployment for kibana.<br>
(4) Configured service as nodeport of access using clusterip.<br>
(5) Created fluntd as daemonset to run on all the nodes.<br>
(6) Configured service account and rbac for limited communication with api-server.<br>

<h1>Phase 3</h1>

<h2>Troubleshooting Frontend</h2>
(1) Check logs and events.<br>
(2) Verify service configuration of frontend service.<br>
(3) Check ingress configuration for frontend.<br>
(4) Check network policies of frontend. If it is blocking any call to or from the pod.<br>
(5) Use nslookup to resolve domain name. Check it is correct or not.<br>

<h2>Troubleshooting DB/Backend</h2>
(1) Check logs and events.<br>
(2) Verify service configuration of backend and db service.<br>
(3) Check the network policy for backend and db. If it is blocking any call to or from the pod.<br>
(4) Check if rbac is configured to communicate with db via api-server.<br>
(5) Use ping to check latency and packet-loss.<br>

<h2>Troubleshooting RabbitMQ</h2>
(1) Check logs and events.<br>
(2) Check metics of rabbitmq pod.<br>
(3) Exec into the node and check rabbitmq service level configuration.<br>
(4) Use ping to check latency and packet-loss.<br>





