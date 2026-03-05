# Dean Kellham | Cloud Architecture Portfolio

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue)](https://www.linkedin.com/in/deankellham)
[![AWS](https://img.shields.io/badge/AWS-Solutions_Architect-FF9900)](#)

## 📌 Executive Summary
I am a **Senior Cloud Solutions Architect** specializing in AWS infrastructure design, FinOps optimization, and legacy application modernization. 

With a background that combines deep technical expertise, 14+ years of enterprise P&L management, and a BSc in Psychology, my focus is bridging the gap between complex technical risk and high-level business strategy. I design cloud environments that are not just technically sound, but financially optimized and strictly governed.

This repository contains a curated selection of **Architecture Decision Records (ADRs)** and **High-Level Designs (HLDs)** from recent real-world enterprise engagements. 

> ⚠️ **Note on Confidentiality:** All case studies and architectural documents in this repository have been fully anonymized and redacted to protect client IP and sensitive infrastructure data.

---

## 🏗️ Architectural Case Studies & ADRs

**Portfolio Context Key:**
To maintain client confidentiality, projects are prefixed by their anonymized environment:
* **`[CQ]`** - Client Q (SaaS Automotive Repair)
* **`[CN]`** - Client N (SaaS Property Tech)
* **`[IN]`** - Internal MSP Infrastructure

Some Architecture Diagrams are provided. These will vary based on intended audience, and are denoted with the following:
* **`📝`** - Mermaid.js Diagram (Code-based)
* **`🖼️`** - Visio / Draw.io Diagram (Static Image)
* **`--`** - No HLD Available

| Architecture Decision Record | Architecture Domain | Business Impact & Outcome | Architecture Diagram |
| :--- | :--- | :--- | :--- |
| **[CQ-0001: RDS Cross-Generation Right-Sizing](./adrs/CQ-0001-aws-rds-downscaling[redacted].md)** | FinOps & Cost Optimization | Architected a data-driven migration from `m5` to `m7i` instances for a mission-critical logistics platform. Delivered a **47% ($30,000+) reduction in annual AWS spend** with zero negative impact on application performance. | --
| **[CQ-0002: Decoupling Maintenance Routing from Application Logic](./adrs/CQ-0002-alb-maintenance-routing[redacted].md)** | Operational Resilience | Decoupled maintenance routing from application code, reducing emergency maintenance activation time from **30 minutes to <5 seconds** and ensuring a branded user experience even during total compute failure. | 📝
| **[CQ-0003: Implementing User-Centric Observability via CloudWatch Synthetics](./adrs/CQ-0003-synthetic-canary-observability[redacted].md)** | Observability & Reliability | Deployed "outside-in" synthetic canaries to validate actual user journeys, successfully detecting application-layer deadlocks that traditional infrastructure metrics missed and reducing **Mean Time to Detection (MTTD)**. | 📝
| **[CQ-0004: Automated FinOps Governance for Orphaned Compute Detection](./adrs/CQ-0004-automated-finops-orphaned-compute[redacted].md)** | FinOps & Automation | Engineered a serverless governance loop to detect orphaned EC2 instances post-deployment, preventing silent cost accumulation by alerting on capacity anomalies within **1 hour of CI/CD failure**. | 📝
| **[CN-0001: Monolith Decoupling & Modernization](./adrs/CN-0001-decouple-app-tiers[redacted].md)** | Migration & Security | Designed the modernization roadmap to decouple a high-risk legacy .NET/SQL monolith into a highly available, secure multi-tier architecture using **AWS Fargate (ECS), RDS, and S3**, successfully remediating critical public-facing security vulnerabilities. | 🖼️
| **[IN-0001: Serverless API Automation](./adrs/IN-0001-ninjaone-device-location-update-script[redacted].md)** | Serverless & Automation | Designed and deployed a serverless AWS footprint (**Lambda, EventBridge, S3**) to automate RMM API integrations, eliminating OS patching requirements and cutting ongoing operational compute costs to near-zero. | 🖼️
| **[IN-0002: Employing Cross-Account IAM Roles](./adrs/IN-0002-aws-iam-user-access[redacted].md)** | Security & Governance | Architected a secure, centralized Hub-and-Spoke IAM model using **AWS STS (sts:AssumeRole)** to govern cross-account access. Eliminated the security risk of decentralized, long-lived IAM user credentials across multiple client tenancies and significantly reduced administrative overhead. | 🖼️

---

## 🛠️ Core Competencies

* **Cloud Strategy:** AWS Well-Architected Framework, Monolith-to-Microservices, Serverless Architecture.
* **FinOps:** TCO Analysis, Workload Right-Sizing, Compute Migration (Graviton/Intel).
* **Security & Governance:** AWS Foundational Technical Reviews (FTR), IAM Least-Privilege, CloudTrail, AWS STS Cross-Account Access.
* **Infrastructure as Code (IaC) & Automation:** Functional scripting (PowerShell, Python, PHP, JS) for API integration, CloudFormation.

---

## 📬 Get in Touch

* **LinkedIn:** [linkedin.com/in/deankellham](https://www.linkedin.com/in/deankellham)
* **Email:** deankellham@gmail.com
