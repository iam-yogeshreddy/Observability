# Observability

𝐈𝐧𝐭𝐫𝐨𝐝𝐮𝐜𝐭𝐢𝐨𝐧 𝐭𝐨 𝐎𝐛𝐬𝐞𝐫𝐯𝐚𝐛𝐢𝐥𝐢𝐭𝐲 :

Observability is the ability to understand the internal state of a system by analyzing the data it produces, including metrics, logs and traces.

Monitoring (Metrics) : involves tracing system metrics like, CPU usage, memory usage, networking performance. Providing alerts based on the predefined thresholds and conditions.

-> Monitoring tells us what is happening.

Logging(Logs): involves the collection of log data from various components of a system.

-> Logging explains why it is happening.

Tracing(Traces): involves tracking the flow of a request or transaction as it moves through different services and components within a system.

-> Tracing shows how it is happening.

𝑾𝒉𝒚 𝑴𝒐𝒏𝒊𝒕𝒐𝒓𝒊𝒏𝒈 ?

* Monitoring helps us keep an eye on our systems to ensure they are working properly.

* Purpose: maintaining the health, performance, and security of IT environments.

* It enables early detection of issues, ensuring that they can be addressed before causing significant downtime or data loss.

We use monitoring to:

-> Detect Problems Early

-> Measure Performance

-> Ensure Availability

𝑾𝒉𝒚 𝑶𝒃𝒔𝒆𝒓𝒗𝒂𝒃𝒊𝒍𝒊𝒕𝒚 ? 

* Observability helps us understand why our systems are behaving the way they are.

* It’s like having a detailed map and tools to explore and diagnose issues.

We use observability to:

-> Diagnose Issues

-> Understand Behavior

-> Improve Systems


𝑴𝒐𝒏𝒊𝒕𝒐𝒓𝒊𝒏𝒈 :

𝙈𝙚𝙩𝙧𝙞𝙘𝙨 𝙫𝙨 𝙈𝙤𝙣𝙞𝙩𝙤𝙧𝙞𝙣𝙜 :

Metrics are measurements or data points that tell you what is happening.

Monitoring is the process of keeping an eye on these metrics over time to understand what’s normal, identify changes, and detect problems.

𝙋𝙧𝙤𝙢𝙚𝙩𝙝𝙚𝙪𝙨 :

* Prometheus is an open-source systems monitoring and alerting toolkit originally built at SoundCloud.

* It can be configured and set up on both bare-metal servers and container environments like Kubernetes.


𝙋𝙧𝙤𝙢𝙚𝙩𝙝𝙚𝙪𝙨 𝘼𝙧𝙘𝙝𝙞𝙩𝙚𝙘𝙩𝙪𝙧𝙚 :

![image](https://github.com/user-attachments/assets/76d64498-51f1-4e0b-a47c-9da7e196494c)


𝙒𝙝𝙖𝙩 𝙞𝙨 𝙋𝙧𝙤𝙢𝙌𝙇?

* PromQL (Prometheus Query Language) is a powerful and flexible query language used to query data from Prometheus.

* It allows you to retrieve and manipulate time series data, perform mathematical operations, aggregate data, and much more.

** 𝑲𝒆𝒚 𝑭𝒆𝒂𝒕𝒖𝒓𝒆𝒔 𝒐𝒇 𝑷𝒓𝒐𝒎𝑸𝑳:

-> Selecting Time Series: You can select specific metrics with filters and retrieve their data.

-> Mathematical Operations: PromQL allows for mathematical operations on metrics.

-> Aggregation: You can aggregate data across multiple time series.

-> Functionality: PromQL includes a wide range of functions to analyze and manipulate data.


𝐈𝐧𝐬𝐭𝐚𝐥𝐥𝐚𝐭𝐢𝐨𝐧 & 𝐂𝐨𝐧𝐟𝐢𝐠𝐮𝐫𝐚𝐭𝐢𝐨𝐧𝐬 :

Step 1: Create EKS Cluster

Prerequisites

Download and Install AWS Cli - Please Refer this link.
Setup and configure AWS CLI using the aws configure command.
Install and configure eksctl using the steps mentioned here.
Install and configure kubectl as mentioned here.
eksctl create cluster --name=observability \
                      --region=us-east-1 \
                      --zones=us-east-1a,us-east-1b \
                      --without-nodegroup
eksctl utils associate-iam-oidc-provider \
    --region us-east-1 \
    --cluster observability \
    --approve
eksctl create nodegroup --cluster=observability \
                        --region=us-east-1 \
                        --name=observability-ng-private \
                        --node-type=t3.medium \
                        --nodes-min=2 \
                        --nodes-max=3 \
                        --node-volume-size=20 \
                        --managed \
                        --asg-access \
                        --external-dns-access \
                        --full-ecr-access \
                        --appmesh-access \
                        --alb-ingress-access \
                        --node-private-networking

# Update ./kube/config file
aws eks update-kubeconfig --name observability

🧰 Step 2: Install kube-prometheus-stack

helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update

🚀 Step 3: Deploy the chart into a new namespace "monitoring"

kubectl create ns monitoring

helm install monitoring prometheus-community/kube-prometheus-stack \
-n monitoring \
-f ./custom_kube_prometheus_stack.yml

✅ Step 4: Verify the Installation

kubectl get all -n monitoring

Prometheus UI:

kubectl port-forward service/prometheus-operated -n monitoring 9090:9090

NOTE: If you are using an EC2 Instance or Cloud VM, you need to pass --address 0.0.0.0 to the above command. Then you can access the UI on instance-ip:port

Grafana UI: password is prom-operator

kubectl port-forward service/monitoring-grafana -n monitoring 8080:80

Alertmanager UI:

kubectl port-forward service/alertmanager-operated -n monitoring 9093:9093

 Step 5: Clean UP
 
Uninstall helm chart:

helm uninstall monitoring --namespace monitoring

Delete namespace:

kubectl delete ns monitoring

Delete Cluster & everything else:

eksctl delete cluster --name observability



