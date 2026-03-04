# Data Engineering Introduction: Datahub Setup and Usage
This introduction explains how to deploy DataHub using Kubernetes Helm charts and provides basic usage instructions

---

## DataHub Architecture Overview
<img src="image\DataHub Architecture Overview.png" width=100% height=40%>

---

## Components
Datahub consists of 4 main components: [GMS](https://datahubproject.io/docs/metadata-service/), 
[MAE Consumer](https://datahubproject.io/docs/metadata-jobs/mae-consumer-job) (optional), 
[MCE Consumer](https://datahubproject.io/docs/metadata-jobs/mce-consumer-job) (optional), and 
[Frontend](https://datahubproject.io/docs/datahub-frontend). Kubernetes deployment 
for each of the components are defined as subcharts under the main 
[Datahub](https://github.com/acryldata/datahub-helm/tree/master/charts/datahub) 
helm chart.

The main components are powered by 4 external dependencies:
- Kafka
- Local DB (MySQL, Postgres, MariaDB)
- Search Index (Elasticsearch)
- Graph Index (Supports either Elasticsearch or Neo4j)

The dependencies must be deployed before deploying Datahub. We created a separate 
[chart](https://github.com/acryldata/datahub-helm/tree/master/charts/prerequisites) 
for deploying the dependencies with example configuration. They could also be deployed 
separately on-prem or leveraged as managed services.

---

## Getting Start
### 1. Setup
### 2. Usage

---

## Contributing

We welcome contributions from the community. Please refer to our [Contributing Guidelines](CONTRIBUTING.md) for more details. 

---

## Community

Join our [slack workspace](https://slack.datahubproject.io) for discussions and important announcements. 

---
