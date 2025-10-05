# 🚀 Salesforce DevOps with Gearset (Standard Project)

## 📌 Overview  
This repository demonstrates a **Salesforce DevOps pipeline** using **Gearset** and **GitHub** for a standard Salesforce app — the **Event Registration App**.  
The app automates event management and registration capacity tracking with a real-world DevOps workflow that mirrors enterprise deployment processes.

It simulates a standard multi-org setup using **Developer Edition Orgs**:  
- **Dev Org** → Active development & metadata commits  
- **UAT/Prod Org** → Validation and production deployment through Gearset  

The goal: **showcase end-to-end source-driven DevOps**, CI/CD automation, and release governance for a Salesforce ISV-style project.

---

## 🧰 Tools & Technologies  
- **Salesforce Developer Edition Orgs** (Dev & UAT environments)  
- **Gearset** – for CI/CD, deployment pipelines, monitoring, and backups  
- **GitHub** – for source control and collaboration  
- **Flows & Permission Sets** – for declarative logic and access management  
- **Apex Tests (optional)** – for validation on promotion  

---

## 🔄 Workflow  

### **Release Flow Diagram**  
```
Dev Org → GitHub (Feature Branch)
           ↓
GitHub (Main Branch) → Gearset Pipeline
           ↓
      UAT / Prod Org
```

### **Branching Strategy**
| Branch | Purpose | Deployment Target |
|---------|----------|-------------------|
| `feature/*` | Developer builds new metadata | Local validation only |
| `main` | Approved & reviewed metadata | Deployed via Gearset |
| `uat` | Pre-production validation | UAT Sandbox / Prod org |

---

## 📂 Project Structure
```
/salesforce-devops-standard
│
├── README.md                     # Documentation
├── force-app/main/default/        # Salesforce metadata
│   ├── objects/
│   │   ├── Event__c/
│   │   └── Registration__c/
│   ├── flows/
│   │   └── Event_Registration.flow-meta.xml
│   ├── permissionsets/
│   │   ├── Event_Manager.permissionset-meta.xml
│   │   └── Attendee_Support.permissionset-meta.xml
│   └── applications/
│       └── Event_Registration.app-meta.xml
│
├── .gearset/                     # Gearset configuration files
└── feature/                      # Example feature branches
```

---

## ⚙️ Example Customizations  

**Core Custom Objects:**  
- **Event__c** – Represents an event with fields:  
  - `Event_Date__c` (Date)  
  - `Max_Tickets__c` (Number)  
  - `Total_Tickets_Sold__c` (Rollup or manual update)  
- **Registration__c** – Tracks attendee info with fields:  
  - `Attendee_Name__c`  
  - `Attendee_Email__c`  
  - `Ticket_Count__c`  
  - `Event__c` (Lookup)

**Key Features Implemented:**  
✅ **Screen Flow** for creating registrations  
✅ **Capacity validation** using flow logic and event data  
✅ **Permission sets** for profile segregation  
✅ **Custom Lightning App** for simplified access  

---

## 🚀 Deployment Process  
1. **Develop & test** new configurations in the Dev Org  
2. **Retrieve metadata** using Gearset or SFDX  
3. **Commit & push** changes to a feature branch in GitHub  
4. **Create Pull Request** → Review & merge into `main`  
5. **Gearset Pipeline** automatically validates against UAT  
6. **Promote** from `main` → `UAT` → `Prod` through Gearset  

---

## ✅ Release Governance  
| Stage | Validation | Description |
|--------|-------------|-------------|
| **Pre-Merge** | PR Review | Manual review of XML diffs |
| **Gearset Validation** | Auto-validation job | Detects config drift |
| **Deployment** | Automated pipeline | Validated + tested deployments |
| **Audit Trail** | GitHub history | Complete metadata versioning |

---

## 🧩 Security & Access Configuration  
| Permission Set | Object Access | Description |
|----------------|----------------|--------------|
| **Event_Manager** | `Event__c` (CRED), `Registration__c` (Read) | Manage event data and registrations |
| **Attendee_Support** | `Event__c` (Read), `Registration__c` (Read) | Read-only visibility for support users |

Field-Level Security (FLS) included for:  
- `Event__c`: `Event_Date__c`, `Max_Tickets__c`, `Total_Tickets_Sold__c`  
- `Registration__c`: `Attendee_Name__c`, `Attendee_Email__c`, `Ticket_Count__c`, `Event__c`

---

## 🧪 Testing Workflow  
**Manual Testing:**  
- Run the “Registration Creation” flow from an Event record page  
- Validate that capacity logic prevents overbooking  

**Automated Testing (optional):**  
- Create Apex tests for Event and Registration validation rules  
- Run tests automatically during Gearset validations  

---

## 🛠️ Gearset Configuration  
**Pipeline Setup:**  
- **Connected Orgs:** Dev → UAT → Prod  
- **Source Control:** GitHub repo connected to Gearset  
- **Deployment Filters:**  
  - Include: Custom Objects, Flows, Permission Sets, App Metadata  
  - Exclude: Profiles, standard picklist value sets  

**Monitoring:**  
- Daily change monitoring between UAT and Prod  
- Automatic backup schedule enabled  

---

## 🌱 Future Roadmap  
- [ ] Add Experience Cloud site for public event registration  
- [ ] Integrate email notifications on registration  
- [ ] Add dashboard for event metrics (tickets sold, remaining)  
- [ ] Include Apex test coverage and linting in CI pipeline  

---

## 💡 Key Takeaways  
- Demonstrates **end-to-end DevOps** using Gearset and GitHub  
- Fully source-driven workflow — metadata lives in Git  
- Clear separation between Dev, UAT, and Prod  
- Applies real-world release governance practices  
- Perfect for **Gearset Academy** or **DevOps Launchpad certification** demonstration  

---

## 👩‍💻 Author  
**Isamar Francisco** – Salesforce QA → DevOps Engineer  
🎯 Building OEM/ISV DevOps projects with Gearset pipelines & CI/CD automation.  
🔗 Connect on [LinkedIn](https://linkedin.com/in/isamarfrancisco)
