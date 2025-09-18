# AWS Cloud Security Homelab

🚀 **Hands-on cloud security portfolio project** — a multi-account AWS landing zone with centralized logging, SIEM integration, GRC evidence collection, and AI security experiments.  

This homelab is designed to **fill cloud security knowledge gaps** and serve as a **portfolio case study** for demonstrating practical skills in cloud architecture, detection engineering, auditing, and compliance.

---

## 🎯 Goals
- Build a **secure AWS landing zone** with Control Tower/Organizations, SCPs, and IAM Identity Center.
- Centralize **logging & monitoring** across accounts (CloudTrail, Config, GuardDuty, Security Hub).
- Deploy **workloads** (serverless API, EKS cluster with Juice Shop, EC2 instances) to generate real telemetry.
- Implement a **SIEM pipeline** using AWS Security Lake + Athena/OpenSearch and optionally Wazuh.
- Maintain a **Risk Register** and **Evidence Store** for GRC/audit readiness.
- Explore **AI in security** — Amazon Bedrock and self-hosted LLMs with security guardrails.
- Keep costs under **$100–150/month** with budgets, anomaly detection, and scheduling.

---

## 🏗️ Architecture (Phase 1 Landing Zone)
> _Placeholder — replace with your diagram when ready_  

![Architecture Diagram](docs/img/landing-zone.png)

- **Accounts:** root (payer), security, log-archive, shared-services, dev
- **Guardrails:** Service Control Policies (SCPs), tagging enforcement, region allow-list
- **Identity:** IAM Identity Center (SSO) with least-privilege permission sets
- **Logging:** Org-wide CloudTrail, Config aggregator, GuardDuty, Security Hub, Access Analyzer
- **Evidence:** S3 with versioning + Object Lock, KMS encryption

---

## 📂 Repo Structure
rsa-homelab/
├── README.md # This file
├── docs/ # Case study writeups
│ ├── 00-phase-0.md # Ground rules & setup
│ ├── 01-landing-zone.md # Multi-account landing zone
│ └── img/ # Diagrams & screenshots
├── evidence/ # Screenshots, CLI outputs, exports (redacted in main branch)
│ ├── screenshots/
│ ├── exports/
│ └── cli/
├── infra/ # Terraform/IaC modules & account configs
│ ├── accounts/
│ └── modules/
├── grc/ # Governance, Risk, and Compliance
│ ├── risk-register.csv
│ ├── evidence-exports/
│ └── runbooks/
└── .gitignore


---

## 📜 Case Studies
Each phase has its own documentation & evidence:

- [Phase 0 – Ground Rules](docs/00-phase-0.md)  
- [Phase 1 – Landing Zone](docs/01-landing-zone.md)  
- Phase 2+ (Networking, Workloads, SIEM, GRC, AI) coming soon

---

## 🔒 Governance & Risk
- **Risk Register:** [grc/risk-register.csv](grc/risk-register.csv)  
- **Evidence Store:** structured S3 bucket (Object Lock + KMS), mirrored in `/evidence/` folder with redactions for public repo  
- **Runbooks:** incident response & audit processes in `/grc/runbooks/`

---

## 🛡️ Security Tooling
- AWS Security Hub (CIS 1.5, Foundational Best Practices)
- AWS GuardDuty, Macie, Access Analyzer
- AWS Security Lake (OCSF schema, Athena queries, optional OpenSearch)
- Wazuh (optional) for host/endpoint SIEM & compliance checks

---

## 🤖 AI Experiments
- **Amazon Bedrock:** retrieval-augmented generation (RAG) over S3 policies/evidence  
- **Self-hosted LLMs:** Ollama + Open WebUI on GPU EC2 inside private VPC  
- **Security Exercises:** prompt injection tests, guardrails, logging & redaction pipelines

---

## 📊 Evidence for Employers
This repo doubles as a **portfolio case study**:
- **Screenshots** (Control Tower setup, CloudTrail configs, GuardDuty findings)
- **CLI exports** (`aws organizations list-accounts`, `aws configservice describe-configuration-aggregators`, etc.)
- **Policy files** (SCP JSONs, KMS key policies, Config rules)
- **One-pager** (executive summary in `/docs/one-pager-landing-zone.md`)

---

## ✅ Current Progress
- [x] Repo skeleton created  
- [x] Phase 0 documented  
- [ ] Phase 1 landing zone (in progress)  
- [ ] Networking & workloads  
- [ ] SIEM integration  
- [ ] GRC evidence store  
- [ ] AI lab  

---

## 📌 Notes
- This repo shows **portfolio-ready, redacted outputs** on `main`.  
- The **`lab` branch** contains raw configs and unredacted evidence (not public).  

---

### Author
**Rodney Arceneaux** — Cybersecurity Professional (CISSP, CISM, CCSK)  
_Focusing on cloud security, GRC, and AI-driven security engineering._

---
