# End-to-End-Observability-Stack-with-Metrics-Logs-and-Tracing-in-Kubernetes
This project implements an end-to-end observability stack on Kubernetes to provide complete visibility into application performance and system health. It integrates metrics, centralized logging, and distributed tracing to help developers and SREs monitor, debug, and optimize microservices efficiently.

# 🧭 Architecture Diagram

<img width="1279" height="720" alt="Image" src="https://github.com/user-attachments/assets/9175554c-efdf-4c04-aaa3-6a88a5f14223" />

# 📌 GitHub Repository Structure
```

k8s-observability-stack/
│
├── manifests/
│   ├── prometheus.yaml
│   ├── grafana.yaml
│   ├── efk/
│   │   ├── elasticsearch.yaml
│   │   ├── fluentd.yaml
│   │   └── kibana.yaml
│   ├── jaeger.yaml
│
├── screenshots/
│   ├── 01-prometheus-metrics.png
│   ├── 02-grafana-dashboard.png
│   ├── 03-kibana-logs.png
│   ├── 04-jaeger-trace.png
│
├── docs/
│   └── architecture.md
│
└── README.md

```


# 📖 README.md 

🚀 Project Overview

This project implements a complete observability stack in Kubernetes covering:
-  Metrics (Prometheus + Grafana)
- Logs (EFK Stack)
- Distributed Tracing (Jaeger)

# 🎯 Objectives

- Centralized monitoring and logging
- End-to-end request tracing
- Real-time dashboards for performance insights

# 🛠️ Technologies Used

1.Kubernetes
2.Prometheus
3.Grafana
4.Elasticsearch
5.Fluentd
6.Kibana
7.Jaeger

# ⚙️ Implementation Steps

1️⃣ Metrics Setup

🔹 Install Prometheus

``` 
//  apiVersion: v1
kind: Namespace
metadata:
  name: monitoring

apiVersion: apps/v1
kind: Deployment
metadata:
  name: prometheus
  namespace: monitoring
spec:
  replicas: 1
  selector:
    matchLabels:
      app: prometheus
  template:
    metadata:
      labels:
        app: prometheus
    spec:
      containers:
      - name: prometheus
        image: prom/prometheus
        ports:
        - containerPort: 9090

```

🔹 Install Grafana

```

//  apiVersion: apps/v1
kind: Deployment
metadata:
  name: grafana
  namespace: monitoring
spec:
  replicas: 1
  selector:
    matchLabels:
      app: grafana
  template:
    metadata:
      labels:
        app: grafana
    spec:
      containers:
      - name: grafana
        image: grafana/grafana
        ports:
        - containerPort: 3000

```

2️⃣ Logging Setup

🔹 Elasticsearch

```

//  apiVersion: apps/v1
kind: Deployment
metadata:
  name: elasticsearch
spec:
  replicas: 1
  selector:
    matchLabels:
      app: elasticsearch
  template:
    metadata:
      labels:
        app: elasticsearch
    spec:
      containers:
      - name: elasticsearch
        image: docker.elastic.co/elasticsearch/elasticsearch:7.10.1

```

🔹 Fluentd

```

//  apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: fluentd
spec:
  selector:
    matchLabels:
      app: fluentd
  template:
    metadata:
      labels:
        app: fluentd
    spec:
      containers:
      - name: fluentd
        image: fluent/fluentd

```

🔹 Kibana

```

//  apiVersion: apps/v1
kind: Deployment
metadata:
  name: kibana
spec:
  replicas: 1
  selector:
    matchLabels:
      app: kibana
  template:
    metadata:
      labels:
        app: kibana
    spec:
      containers:
      - name: kibana
        image: docker.elastic.co/kibana/kibana:7.10.1

```

3️⃣ Distributed Tracing 

```

//  apiVersion: apps/v1
kind: Deployment
metadata:
  name: jaeger
spec:
  replicas: 1
  selector:
    matchLabels:
      app: jaeger
  template:
    metadata:
      labels:
        app: jaeger
    spec:
      containers:
      - name: jaeger
        image: jaegertracing/all-in-one:latest
        ports:
        - containerPort: 16686

```

 4️⃣ Apply All Manifests

//  kubectl apply -f manifests/

 # 📊 Visualization
 
1.Metrics Dashboard

- CPU Usage
- Memory Usage
- Pod Health

2.Logs Dashboard

- Centralized logs in Kibana
- Search by pod/service

3.Tracing

- Request flow between services
- Latency breakdown

# 🧠 Observability Architecture

- Prometheus scrapes metrics from Kubernetes
- Grafana visualizes metrics
- Fluentd collects logs → sends to Elasticsearch
- Kibana visualizes logs
- Jaeger traces requests across services

# 📸 Important screenshots

<img width="1280" height="687" alt="Image" src="https://github.com/user-attachments/assets/38382bdb-43b5-472b-8497-9190e8c11d1f" />

<img width="1280" height="687" alt="Image" src="https://github.com/user-attachments/assets/4746bc6f-b46b-4128-8660-4e09cf14d3b3" />

<img width="1280" height="687" alt="Image" src="https://github.com/user-attachments/assets/b3753b48-ba7a-4f0e-9894-176f039bf135" />

<img width="1280" height="687" alt="Image" src="https://github.com/user-attachments/assets/3074ad97-1652-407d-b68e-7e94732d8933" />

<img width="1280" height="687" alt="Image" src="https://github.com/user-attachments/assets/ea0084cc-c289-42a0-bfa8-8ed106971562" />

<img width="1280" height="687" alt="Image" src="https://github.com/user-attachments/assets/57fffa41-9717-40e1-8ce9-8cc96c90c7b8" />

<img width="1280" height="687" alt="Image" src="https://github.com/user-attachments/assets/74b3f770-a6c9-48e2-ba15-2d05054506ab" />

































