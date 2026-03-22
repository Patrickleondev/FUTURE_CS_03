# FUTURE_CS_03 — API Security Risk Analysis

![API Security](images/api_security_header.png) *(Note: Placeholder for user image)*

## 🔍 About This Task
This repository is the submission for **Task 3** of the **Future Interns Cyber Security Track (2026)**.

**Task:** Analyze a vulnerable API to identify common API security risks (OWASP API Top 10), assess authorization controls, and explain risks in simple business language with clear remediation steps.

---

## 🎯 Target API
| Field | Details |
|---|---|
| **API** | VAmPI (Vulnerable API made with Flask) |
| **Reason for selection** | Explicitly designed to simulate the **OWASP API Security Top 10** vulnerabilities found in modern enterprise SaaS applications. |
| **Hosting** | Local Docker Environment (Isolated) |

---

## 🛠️ Tools Used
| Tool | Purpose |
|---|---|
| Postman | Manual API interaction, endpoint inspection, and JWT token management |
| Python 3 (Requests) | Development of a custom automated exploitation script |
| Docker | Secure, isolated hosting of the vulnerable API |
| Markdown | Professional security reporting |

---

## 📁 Repository Structure
```
FUTURE_CS_03/
├── API_Security_Risk_Analysis_Report.md  # ✅ Professional vulnerability report
├── vampi_exploit.py                      # ✅ Custom Python script automating the BOLA attack
├── Postman_Instructions.md               # ✅ Step-by-step Postman testing guide
├── Task3_Strategy.md                     # Assessment strategy & deployment guide
├── README.md                             # This file
└── images/                               # Directory containing Postman screenshots
```

---

## 📄 Key Deliverables
- [📊 **API Security Risk Analysis Report**](API_Security_Risk_Analysis_Report.md) — The comprehensive final report documenting BOLA (Broken Object Level Authorization), Excessive Data Exposure, and remediation strategies in business language.
- [🐍 **vampi_exploit.py Script**](vampi_exploit.py) — A practical, custom Python script that automatically registers, authenticates, and exploits the API to demonstrate data theft.

---

*Submitted by: Patrick Leon | Future Interns Cyber Security Program 2026*
