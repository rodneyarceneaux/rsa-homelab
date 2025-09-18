# Phase 0 – Ground Rules & Initial Setup

📅 Duration: ~1–2 hours  
🎯 Objective: Prepare secure identities, cost guardrails, conventions, and documentation scaffolding before building the AWS landing zone.

---

## 🔐 0.1 Secure the Root & Account Hygiene
- Created a **dedicated email** for the AWS Management Account (`aws-root@domain.com`) stored in password manager.
- Configured a **30+ character passphrase** and enabled **MFA** (Authenticator + Security Key).
- Verified **no root access keys** exist.
- Enabled **IAM access to billing** in the root account.

---

## 🏷️ 0.2 Naming & Tagging Conventions
- **Region strategy**:  
  - Primary: `us-east-1`  
  - Secondary: `us-west-2` (for DR/lab variety)
- **Naming format**:  
rsa-<env>-<service>
e.g., rsa-sec-guardduty, rsa-dev-eks
- **Mandatory tags** applied to all resources:  
- `Owner=Rodney`  
- `Env`  
- `CostCenter=Homelab`  
- `DataClass`  
- `Compliance=CIS`
- Enabled **Cost Allocation Tags** in Billing.

---

## 💰 0.3 Cost Guardrails
- Configured **AWS Budgets**:
- Daily alerts at **$2**, **$5**, **$10**
- Monthly alert at **$100–150**
- Enabled **Cost Anomaly Detection** with default monitor.

---

## 🖥️ 0.4 Workstation & Tooling
Installed and configured:
- **AWS CLI v2**
- **Terraform**
- **kubectl, eksctl, Helm**
- **Docker Desktop**
- **Node.js LTS + Python 3.11+**
- Terminal profile with base environment setup (using SSO later, no static creds).

---

## 📁 0.5 Portfolio & Evidence Scaffolding
- Created **GitHub repo** [`rsa-homelab`](https://github.com/rodneyarceneaux/rsa-homelab)
- Repo structure initialized:
- /README.md
/docs
00-phase-0.md
01-landing-zone.md
/evidence
screenshots/
exports/
cli/
/infra
accounts/
modules/
/grc
risk-register.csv
evidence-exports/
runbooks/

- Added `.gitignore` to exclude Terraform state files.
- Created `evidence/redaction-guide.md` to define redaction standards (blur account IDs, emails, sensitive ARNs).

---

## 📝 0.6 Diagramming
- Prepared initial **architecture diagram** (Control Tower + accounts + logging flow).  
- Saved to `/docs/img/landing-zone.png` (placeholder until updated in Phase 1).

---

## 🗄️ 0.7 Terraform State Plan
- Decision: **per-account state buckets** with DynamoDB lock table.  
- Example: `rsa-tf-state-security`, `rsa-tf-state-dev`
- To be provisioned in Phase 1.

---

## 📸 Evidence Captured
- Screenshot of repo created on GitHub  
- Screenshot of local repo structure (`tree` output)  
- Budget setup confirmation  
- MFA enforcement screen from Management Account

(All stored in `/evidence/screenshots/` with sensitive info redacted)

---

## ✅ Deliverables
- GitHub repo skeleton with structured folders
- README.md (portfolio-facing)
- Phase 0 documented here (`00-phase-0.md`)
- Evidence folder initialized with redaction guide

---

## 📌 Lessons Learned
- Starting with cost controls and naming/tagging conventions ensures long-term discipline.
- A clear repo/evidence strategy makes it easy to showcase skills while protecting sensitive information.
- Early investment in structure reduces rework when adding SIEM, GRC, and AI experiments later.

---

