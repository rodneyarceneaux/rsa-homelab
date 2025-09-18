# Phase 1 – Multi-Account Landing Zone

📅 Duration: ~1–2 days  
🎯 Objective: Build a secure AWS Organization with OUs, accounts, SSO, centralized logging, and baseline security services.

---

## 🏗️ 1.1 Accounts & Organizational Units
**Planned structure:**
- Management (root / payer only)
- Security OU → `security`, `log-archive`
- Workloads OU → `shared-services`, `dev`
- Sandbox OU (optional for experiments)

**Actions Taken:**
- [ ] Enabled AWS Control Tower (or DIY Organizations setup)
- [ ] Created OUs: Security, Workloads, Sandbox
- [ ] Provisioned accounts via Account Factory:
  - `security` (security tooling, audit)
  - `log-archive` (immutable logging)
  - `shared-services` (CI/CD, bastion, central services)
  - `dev` (application workloads)

📸 **Evidence:**  
- Screenshot of Organizations → Accounts tab  
- Screenshot of Control Tower landing zone dashboard  
- CLI:  
  ```bash
  aws organizations list-accounts > evidence/cli/org-accounts.json

  👥 1.2 Identity & Access

Actions Taken:

 Enabled IAM Identity Center (SSO)

 Created groups:

Administrators

SecurityAuditors

BillingViewers

 Created permission sets:

ViewOnly

SecurityAudit

PowerUser (lab only)

Billing

 Assigned users to accounts with least privilege

📸 Evidence:

Screenshot of SSO → Permission Sets

Screenshot of Assignments

CLI:
aws sso-admin list-instances > evidence/cli/sso-instances.json

📜 1.3 Logging & Encryption

Actions Taken:

 Enabled org-wide CloudTrail (multi-region, global services, log validation enabled)

 Destination: S3 bucket in log-archive with SSE-KMS

 Enabled Object Lock (governance) + versioning

 Created CMK rsa-log-kms in log-archive

📸 Evidence:

Screenshot of CloudTrail settings

Screenshot of S3 bucket with versioning + Object Lock

Screenshot of KMS key policy

CLI:
aws cloudtrail list-trails > evidence/cli/trails.json
aws s3api get-bucket-versioning --bucket <log-bucket> > evidence/cli/s3-bucket-versioning.json

📊 1.4 Posture & Security Services

Actions Taken:

 Enabled AWS Config (org) + aggregator in security

 Enabled GuardDuty (org) with security as delegated admin

 Enabled Security Hub (org) with CIS 1.5 + Foundational Best Practices

 Created Access Analyzer (org-level in security)

📸 Evidence:

Screenshot of Config aggregator status

Screenshot of GuardDuty → Admin + Members

Screenshot of Security Hub → Standards enabled

CLI:
aws configservice describe-configuration-aggregators > evidence/cli/config-aggregators.json
aws guardduty list-detectors > evidence/cli/gd-detectors.json
aws securityhub get-enabled-standards > evidence/cli/sh-standards.json

🔒 1.5 Service Control Policies (SCPs)

Policies implemented:

DenyUnsupportedRegions (allow only us-east-1, us-west-2)

DenyCloudTrailTamper

RequireS3EncryptionOnPut

DenyPublicS3ACLs

DenyIAMPolicyWildcards

DenyUntaggedResourceCreation

📸 Evidence:

Screenshot of SCP list in Organizations

JSON files saved in /infra/org/scp/

CLI:
aws organizations list-policies --filter SERVICE_CONTROL_POLICY > evidence/cli/scp-list.json

💰 1.6 Cost & Governance

Actions Taken:

 Enabled cost allocation tags org-wide

 Created budgets per account with daily + monthly alerts

 Configured Tag Policies for consistency

📸 Evidence:

Screenshot of Budgets

Screenshot of Tag Policies

🗄️ 1.7 Terraform State Buckets

Actions Taken:

 Created rsa-tf-state-<account> S3 buckets (per account)

 Created rsa-tf-lock DynamoDB tables for state locking

 Restricted access via bucket policies + KMS

📸 Evidence:

Screenshot of S3 bucket (state)

Screenshot of DynamoDB lock table

📸 1.8 Evidence Index

Evidence captured during Phase 1 has been stored in:

/evidence/screenshots/ (screenshots with redactions)

/evidence/cli/ (JSON exports from CLI)

/infra/org/scp/ (policy JSONs)

✅ Deliverables

AWS Organization with OUs + accounts

IAM Identity Center (SSO) with least privilege

Org-wide CloudTrail, Config, GuardDuty, Security Hub

Centralized logging with KMS + Object Lock

SCPs enforcing encryption, region allow-list, tagging

Budgets + anomaly detection

Terraform backends (per-account state buckets + locks)

📌 Lessons Learned

SCPs are powerful but can easily block needed services → test in Sandbox OU first.

Evidence must be captured at the moment of implementation (screenshots + CLI exports) for GRC value.

Automating account setup with Control Tower is cleaner than DIY, but DIY gives deeper understanding of AWS Organizations.


---

👉 This gives you a **Phase 1 documentation shell**. As you go through the landing zone build, you’ll just **drop screenshots + CLI exports into `/evidence/` and link them here**.  

Do you want me to also generate the **starter SCP JSON files** (like `DenyUnsupportedRegions.json`, `RequireS3EncryptionOnPut.json`) so you can commit them under `/infra/org/scp/` right away?
