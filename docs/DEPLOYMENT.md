# 🚀 ParlaChore Deployment

This document outlines the **deployment strategy, environment configuration, and infrastructure readiness** for ParlaChore.  
It complements the architectural and security documentation.

---

## 🌐 Hosting & Infrastructure

- **Amazon Web Services (AWS)**
    - Domain hosted via AWS Route 53.
    - Application deployed on AWS EC2 or ECS (containerized services).
    - Static assets (CSS, JS, images) served via AWS S3 + CloudFront CDN for caching and global distribution.
    - Logs and metrics integrated with AWS CloudWatch.

- **Containerization**
    - Docker images built for backend services.
    - Stateless design ensures portability across environments.
    - Health endpoints exposed for orchestration.

- **Orchestration**
    - Kubernetes (EKS) readiness:
        - Externalized configuration via `ConfigMap` and `Secrets`.
        - Horizontal Pod Autoscaling (HPA) planned for traffic spikes.
        - Rolling updates supported for zero‑downtime deployments.

---

## ⚙️ Environment Configuration

- **application.yml**
    - Environment‑specific settings (dev, staging, production).
    - Database connection strings externalized.
    - Security keys and secrets injected via environment variables.

- **logback.xml**
    - Centralized logging configuration.
    - Debug flags toggle lifecycle visibility.
    - Planned integration with ELK stack (Elasticsearch, Logstash, Kibana).

---

## 🔄 Deployment Flow

1. **Build**
    - Maven builds backend services.
    - Surefire plugin runs unit/integration tests.
    - Docker image created for each service.

2. **Push**
    - Images pushed to AWS Elastic Container Registry (ECR).
    - Static assets uploaded to S3 with cache‑busting.

3. **Deploy**
    - ECS tasks or EKS pods pull latest images.
    - CloudFront invalidates caches for updated assets.
    - Health checks verify service readiness.

4. **Monitor**
    - CloudWatch dashboards track CPU, memory, and request latency.
    - Alerts configured for error rates and downtime.

---

## 🧪 DevOps Practices

- **CI/CD Pipeline**
    - GitHub Actions or Jenkins for automated builds and deployments.
    - Branch‑based environments (feature → staging → production).
- **Testing**
    - Spring Boot Test for unit/integration.
    - Planned load testing with JMeter or Gatling.
- **Scalability**
    - Stateless services allow horizontal scaling.
    - CDN ensures global asset delivery.

---

## 📌 Notes

- Deployment strategy emphasizes **scalability, resilience, and transparency**.
- Current setup is AWS‑based, but portable to other cloud providers.
- Documentation released publicly to demonstrate **DevOps readiness and infrastructure design**.

---
## 👥 Author & Links
Created by [Sam Parlatore](https://linkedin.com/in/projectswithsam)  
GitHub: [github.com/samparlatore](https://github.com/samparlatore)
---