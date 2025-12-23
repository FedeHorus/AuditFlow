# AuditFlow: Automated Quality Assurance

AuditFlow is a high-performance, **single-tenant** automated Quality Assurance (QA) pipeline designed for the call industries. It automates the ingestion, and analysis of 100% of phone calls from several platforms.

---

## 🚀 Value Proposition
Traditional QA relies on human auditors who can only monitor 2-5% of total call volume. **AuditFlow** eliminates these blind spots by auditing **100% of calls** at a fraction of the cost, ensuring compliance, identifying sales opportunities, and providing instant feedback.



---

## 🛠️ System Architecture

1.  **Ingestion (AWS Lambda):** Triggered by **Amazon EventBridge**. It fetches call logs and recording from your platform of choice(single or multiple platforms), storing them in **DynamoDB** with a `PENDING` status.
2.  **Intepreting (AWS Fargate + GPU):** A containerized worker. It downloads the audio, analyzes it locally, and updates the record ready to get the outcome of the call.
3.  **AI Analysis (AWS Lambda + AI API):** A specialized worker with integrated LLM. It applies a custom business rubric to categorize the call (e.g., *Appointment Set*, *Not Interested*, *Wrong Number*) and generates a detailed summary.
4.  **Reporting (AWS Lambda):** Finalized data is exported to a **Google Sheets** dashboard for real-time stakeholder review.

---

## 💰 Cost Comparison: Human vs. AuditFlow

The following table compares the cost of auditing **1,000 calls** (average 5 minutes each).

| Feature | Human Auditor | AuditFlow | Savings |
| :--- | :--- | :--- | :--- |
| **Audit Coverage** | 2% - 5% | **100%** | +95% Coverage |
| **Cost per minute**| $0.40 | $0.0036 |99.1%|
| **Time per Call** | ~8 Minutes | **~1.5 Minutes (Parallel)** | 81% Faster |
| **Cost per Call** | $2.00 | **$0.018** | 99.1% Cheaper |
| **Cost per 1,000 Calls**| $2,000.00 | **$18.10** | **$1,981.90** |

### Detailed AI Cost Breakdown (per 5-min call)
* **AWS Fargate (GPU Compute):** ~$0.017 (Based on `g4ad.xlarge` spot pricing).
* **Outcome notator API:** ~$0.0001 (Processing ~1,500 tokens).
* **AWS Lambda & DynamoDB:** ~$0.001 (Orchestration and storage).

---

## 🔐 Security & Privacy
* **Single-Tenant Deployment:** Each client receives their own isolated AWS stack. No data is shared between different customers.
* **Direct API Integration:** Secure communication with your platforms using encrypted environment variables

---

## 🛠️ Configuration & Setup

### Requirements
* **AWS Account:** With permissions for Lambda, Fargate (ECS), and DynamoDB.
* **Text-to-speech** 
* **Access to API Keys:** For your platforms of choice. 



---

## 📈 Future Roadmap
* **PII Masking** 
* **Custom Rubrics:** Dynamic prompt management via S3 or DynamoDB.
* **Advanced Analytics:** Integration with Amazon QuickSight, Looker, or Power BI for deep-dive sales funnels.
