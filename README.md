# 🛡️ Multi-Line Insurance Policy & Claims Management System

A Salesforce-based insurance management platform designed to streamline **policy quoting, policy issuance, claim processing, approval workflows, and claims management** for **Vehicle, Property, and Life Insurance**.

The system combines **Salesforce Flows, Apex, Lightning Web Components (LWC), Record Types, Field Sets, Approval Processes, Validation Rules, Permission Sets, and automated claim routing** to provide a centralized insurance management solution.

---

## 📌 Table of Contents

* [Overview](#-overview)
* [Problem Statement](#-problem-statement)
* [Objectives](#-objectives)
* [Key Features](#-key-features)
* [System Architecture](#-system-architecture)
* [Technology Stack](#-technology-stack)
* [Salesforce Data Model](#-salesforce-data-model)
* [Insurance Products](#-insurance-products)
* [Policy Management](#-policy-management)
* [Claims Management](#-claims-management)
* [Automation](#-automation)
* [Apex Components](#-apex-components)
* [Lightning Web Components](#-lightning-web-components)
* [Approval Workflow](#-approval-workflow)
* [Security & Access Control](#-security--access-control)
* [Validation](#-validation)
* [Testing](#-testing)
* [Project Milestones](#-project-milestones)
* [Benefits](#-benefits)
* [Future Enhancements](#-future-enhancements)
* [Project Structure](#-project-structure)
* [Installation & Setup](#-installation--setup)
* [Author](#-author)

---

# 🚀 Overview

The **Multi-Line Insurance Policy & Claims Management System** is a Salesforce solution developed to replace slow and inconsistent manual insurance processes with a centralized and automated platform.

The system supports multiple insurance products:

* 🚗 Vehicle Insurance
* 🏠 Property Insurance
* ❤️ Life Insurance

It provides a unified view of **Customer, Policy, and Claim information** while automating quoting, premium calculation, claim routing, approval, and adjuster workflows.

---

# ❗ Problem Statement

Traditional insurance systems can suffer from:

* Manual policy quoting
* Slow policy issuance
* Inconsistent data entry
* Manual claim review
* Long claim resolution times
* High operational costs
* Limited visibility across customer, policy, and claim information
* Difficulty supporting multiple insurance product types

This project addresses these challenges through a **single Salesforce platform** that standardizes policy operations and automates claim management.

---

# 🎯 Objectives

The primary objectives are:

1. Standardize and accelerate policy quoting and issuance.
2. Support Vehicle, Property, and Life insurance within a unified data model.
3. Automate claim initiation and routing.
4. Route claims based on policy type.
5. Automate high-value claim approvals.
6. Provide adjusters with a dedicated claims dashboard.
7. Provide a 360-degree view of customer, policy, and claim information.
8. Enforce data validation and access control.
9. Provide automated premium calculation.
10. Improve operational efficiency through Salesforce automation.

---

# ✨ Key Features

### 📋 Policy Management

* Centralized Policy object
* Vehicle, Property, and Life Record Types
* Customer lookup
* Policy start date
* Policy term
* Premium information
* Product-specific fields
* Automated policy number generation

### 💰 Automated Quoting

* Screen Flow-based quoting
* Vehicle-specific information collection
* Customer information capture
* Policy state selection
* Automated premium calculation using Apex

### 📝 Claims Management

* Centralized Claim object
* Accident, Property, and Life Record Types
* Claim amount tracking
* Date of loss
* Claim description
* Assigned adjuster
* Approval status
* Policy relationship

### 🔀 Automated Claim Routing

Claims are automatically routed according to the associated policy type:

```text
Claim
  │
  ├── Auto Policy ───────> Auto Queue
  │
  ├── Property Policy ───> Property Queue
  │
  └── Life Policy ───────> Life Queue
```

### 📊 Claims Adjuster Dashboard

The Lightning Web Component dashboard provides:

* Assigned claims
* Claim number
* Claim amount
* Policy type
* Policy holder
* Claim status
* Days open
* Policy-type filtering

### ✅ High-Value Claim Approval

Claims above **$50,000** enter an approval process:

```text
Claim Amount > $50,000
          │
          ▼
   Senior Adjuster
          │
          ▼
   Department Manager
          │
     ┌────┴────┐
     ▼         ▼
 Approved    Rejected
```

---

# 🏗️ System Architecture

```text
                    ┌─────────────────────┐
                    │      Salesforce     │
                    │        Platform     │
                    └──────────┬──────────┘
                               │
              ┌────────────────┼────────────────┐
              │                │                │
              ▼                ▼                ▼
       ┌─────────────┐  ┌─────────────┐  ┌─────────────┐
       │   Policy    │  │    Claim    │  │   Contact   │
       │    Object   │  │    Object   │  │    Object   │
       └──────┬──────┘  └──────┬──────┘  └─────────────┘
              │                │
              ▼                ▼
       ┌─────────────┐  ┌─────────────┐
       │ Screen Flow │  │ Record Flow │
       └──────┬──────┘  └──────┬──────┘
              │                │
              ▼                ▼
       ┌─────────────┐  ┌─────────────┐
       │    Apex     │  │  Approval   │
       │ Controllers │  │   Process   │
       └──────┬──────┘  └──────┬──────┘
              │                │
              └───────┬────────┘
                      ▼
             ┌─────────────────┐
             │      LWC        │
             │ Claims Dashboard│
             └─────────────────┘
```

---

# 🧰 Technology Stack

| Technology               | Purpose                                 |
| ------------------------ | --------------------------------------- |
| Salesforce               | CRM & application platform              |
| Apex                     | Business logic & server-side processing |
| SOQL                     | Salesforce data querying                |
| Lightning Web Components | User interface                          |
| Salesforce Flow          | Process automation                      |
| Screen Flow              | Interactive quoting & claim review      |
| Record-Triggered Flow    | Automated claim routing                 |
| Approval Process         | High-value claim approval               |
| Record Types             | Product-specific configuration          |
| Field Sets               | Dynamic product-specific fields         |
| Validation Rules         | Data validation                         |
| Permission Sets          | Role-based access control               |
| Salesforce Objects       | Data storage                            |

---

# 🗂️ Salesforce Data Model

## Policy Object

The `Policy__c` custom object stores insurance policy information.

Important fields include:

| Field              | Type            |
| ------------------ | --------------- |
| Policy Number      | Auto Number     |
| Customer           | Lookup(Contact) |
| Beneficiary Name   | Text            |
| Model Year         | Text            |
| Policy Start Date  | Date            |
| Policy Term Months | Number          |
| Premium            | Currency        |
| Square Footage     | Number          |
| VIN                | Text            |
| Year Built         | Text            |

The Policy object uses Record Types for:

* Auto
* Property
* Life

---

## Claim Object

The `Claim__c` custom object stores insurance claim information.

Important fields include:

| Field           | Type           |
| --------------- | -------------- |
| Claim Number    | Auto Number    |
| Adjuster        | Lookup(User)   |
| Approval Status | Picklist       |
| Claim Amount    | Currency       |
| Date of Loss    | Date/Time      |
| Description     | Long Text Area |
| Policy          | Lookup(Policy) |

Claim Record Types include:

* Accident
* Property
* Life

---

# 🚗 Insurance Products

## 1. Auto Insurance

Vehicle-specific information includes:

* VIN
* Model Year
* Policy State
* Customer
* Policy Start Date

The system validates that an Auto policy VIN contains exactly **17 characters**.

---

## 2. Property Insurance

Property-specific information includes:

* Square Footage
* Year Built

---

## 3. Life Insurance

Life-specific information includes:

* Beneficiary Name
* Policy Term Months

---

# 📋 Policy Management

The system uses Salesforce Record Types and Field Sets to handle product-specific policy information.

### Record Types

```text
                 Policy
                    │
        ┌───────────┼───────────┐
        ▼           ▼           ▼
       Auto      Property       Life
```

### Field Sets

Product-specific Field Sets dynamically organize the relevant fields.

**Vehicle Field Set**

* VIN
* Model Year

**Property Field Set**

* Square Footage
* Year Built

**Life Field Set**

* Beneficiary Name
* Policy Term Months

---

# 💻 Auto Quoting Flow

The Auto Quoting Flow is implemented using Salesforce Screen Flow.

### Process

```text
Start
  │
  ▼
Get Vehicle Record Type
  │
  ▼
Basic Policy Information
  │
  ├── Customer
  ├── Policy Start Date
  └── Policy State
  │
  ▼
Vehicle Details
  │
  ├── VIN
  └── Model Year
  │
  ▼
Create Draft Policy
  │
  ▼
Calculate Premium
  │
  ▼
Update Policy
  │
  ▼
Finish
```

---

# 💰 Premium Calculation

The `PremiumCalculator` Apex class calculates the policy premium based on policy information.

The current implementation considers:

* Policy state
* Vehicle model year

Example logic:

```text
Base Premium = $1000

California:
Base Premium × 1.15

Texas:
Base Premium × 1.05

Model Year < 2018:
Additional $100
```

The Apex action is invoked from the Auto Quoting Flow and the calculated premium is written back to the Policy record.

---

# 📝 Claims Management

Claims are represented using the custom `Claim__c` object.

A claim contains:

* Claim Number
* Policy
* Adjuster
* Claim Amount
* Date of Loss
* Description
* Approval Status

The system automatically identifies the associated policy type and routes the claim accordingly.

---

# 🔀 Automated Claim Routing

A Record-Triggered Flow processes newly created claims.

### Routing Logic

```text
                    New Claim
                       │
                       ▼
                Get Policy Type
                       │
             ┌─────────┼─────────┐
             ▼         ▼         ▼
           Auto     Property     Life
             │         │         │
             ▼         ▼         ▼
        Auto Queue  Property   Life Queue
                    Queue
```

This reduces manual assignment work for claims teams.

---

# 📊 Claims Adjuster Dashboard

The project includes an LWC named:

```text
claimsDashboardLwc
```

The dashboard retrieves assigned claims through:

```text
ClaimsAdjusterController
```

The component supports client-side filtering by:

* All Policy Types
* Auto
* Property
* Life

Each claim is displayed using the reusable:

```text
claimTileLwc
```

---

# 🧩 Apex Components

## ClaimsAdjusterController

The `ClaimsAdjusterController` Apex class:

* Retrieves claims owned by the logged-in user
* Uses SOQL to retrieve related policy information
* Retrieves customer information
* Creates a wrapper object for LWC consumption
* Calculates days open
* Exposes data through an Aura-enabled method

### Wrapper Information

```text
Claim ID
Claim Number
Claim Amount
Status
Policy Type
Policy Holder Name
Days Open
```

---

## PremiumCalculator

The `PremiumCalculator` Apex class:

* Accepts a Policy ID
* Queries policy information
* Calculates the premium
* Returns the calculated premium
* Is invoked from Salesforce Flow

---

# ⚡ Lightning Web Components

## claimsDashboardLwc

Main claims dashboard component.

### Responsibilities

* Retrieve assigned claims
* Display claims
* Filter claims
* Display total assigned claims
* Pass claim data to claim tiles

---

## claimTileLwc

Reusable component used to display individual claim information.

It displays:

```text
Claim Number
Policy Type
Policy Holder
Claim Amount
Status
Days Open
```

The component dynamically selects an icon based on policy type.

---

# ✅ Approval Workflow

High-value claims are automatically submitted for approval when:

```text
Claim Amount > $50,000
```

### Approval Process

**Step 1 — Senior Adjuster**

The claim is first reviewed by the Senior Adjuster.

**Step 2 — Department Manager**

After the first approval, the claim moves to the Department Manager.

### Possible Results

```text
                Claim > $50,000
                       │
                       ▼
              Senior Adjuster
                       │
              ┌────────┴────────┐
              ▼                 ▼
           Approve            Reject
              │
              ▼
       Department Manager
              │
        ┌─────┴─────┐
        ▼           ▼
     Approve       Reject
```

Approval Status values:

```text
New
Submitted for Approval
Approved
Rejected
```

---

# 🖥️ Claim Approver Screen Flow

A dedicated Screen Flow allows approvers to review claim information.

The flow displays:

* Claim ID
* Claim Amount
* Policy Type
* Approval Decision
* Approver Comments

The approver can select:

```text
Approve
Reject
```

The flow is exposed through a Salesforce Quick Action named:

```text
Approve/Reject Claim
```

---

# 🔐 Security & Access Control

The project implements Salesforce security using:

* Permission Sets
* Sharing Rules
* Record-level access
* Object permissions
* Apex class permissions
* Flow permissions

## Permission Sets

### Insurance Agent Access

Provides:

* Create/Read Policy
* Read/Edit Contact
* Read Claim
* Flow User access
* PremiumCalculator Apex access

### Claims Manager Access

Provides:

* Read Policy
* Read/Edit Contact
* Read/Edit/Delete Claim
* Run Reports
* Manage Approvals

### Claims Adjuster Access

Provides:

* Read Policy
* Read/Edit Claim
* ClaimsAdjusterController Apex access

---

# 🌎 Territory-Based Sharing

Claim records can be shared based on the policyholder's state.

Configured sharing criteria include:

```text
Policy Account Holder State = CA
Policy Account Holder State = TX
```

The configured access level is:

```text
Read / Write
```

This helps control claim visibility based on territory/state requirements.

---

# 🛡️ Validation

The system contains validation rules to ensure data accuracy.

### VIN Validation

For Auto policies:

```text
VIN length must equal 17 characters
```

Validation formula:

```apex
AND(
    RecordType.DeveloperName = "Auto",
    LEN(VIN__c) <> 17
)
```

Error message:

```text
The Vehicle Identification Number (VIN)
must be exactly 17 characters long for Auto Policies.
```

---

# 🧪 Testing

The project includes an Apex test class:

```text
ClaimsAdjusterControllerTest
```

The test class creates test data for:

* User
* Contact
* Policy
* Claim

It then validates the behavior of:

```text
ClaimsAdjusterController.getAssignedClaims()
```

The test verifies:

* Claim ID
* Claim Number
* Status
* Claim Amount
* Policy Holder
* Policy Type

The project specification targets **95%+ Apex code coverage** for the controller.

---

# 📅 Project Milestones

## Milestone 1 — Core Data Model & Policy Configuration

* Policy custom object
* Claim custom object
* Policy Record Types
* Claim Record Types
* Field Sets
* Policy fields
* Claim fields
* Auto Quoting Screen Flow
* VIN validation

## Milestone 2 — Policy Issuance & Claim Routing

* PremiumCalculator Apex
* Premium calculation Flow integration
* Policy update automation
* Claim Record-Triggered Flow
* Auto Queue routing
* Property Queue routing
* Life Queue routing

## Milestone 3 — Claims Adjuster Dashboard

* ClaimsAdjusterController
* Apex/SOQL integration
* claimsDashboardLwc
* claimTileLwc
* Client-side filtering

## Milestone 4 — Advanced Claim Processing & Security

* High-value claim approval
* Senior Adjuster approval
* Department Manager approval
* Claim Approver Screen Flow
* Quick Action
* Apex test class
* Sharing Rules
* Permission Sets

---

# 📈 Benefits

The solution is designed to provide:

* Centralized insurance data
* Standardized policy processing
* Automated claim routing
* Automated premium calculation
* Faster claim review
* Reduced manual processing
* Better adjuster visibility
* Product-specific data management
* Structured approval workflows
* Role-based access control
* Improved data validation

---

# 🔮 Future Enhancements

Potential future enhancements include:

* AI-based claim fraud detection
* Predictive claim severity analysis
* Automated document processing
* OCR-based insurance document extraction
* Customer self-service portal
* Email/SMS claim notifications
* External vehicle/property database integration
* AI-powered premium recommendations
* Advanced analytics dashboards
* Predictive claim resolution time
* Mobile application for adjusters
* Automated customer communication

---

# 📁 Project Structure

A recommended GitHub repository structure:

```text
Multi-Line-Insurance-Management/
│
├── README.md
│
├── force-app/
│   └── main/
│       └── default/
│           │
│           ├── classes/
│           │   ├── PremiumCalculator.cls
│           │   ├── PremiumCalculator.cls-meta.xml
│           │   ├── ClaimsAdjusterController.cls
│           │   ├── ClaimsAdjusterController.cls-meta.xml
│           │   ├── ClaimsAdjusterControllerTest.cls
│           │   └── ClaimsAdjusterControllerTest.cls-meta.xml
│           │
│           ├── lwc/
│           │   ├── claimsDashboardLwc/
│           │   │   ├── claimsDashboardLwc.html
│           │   │   ├── claimsDashboardLwc.js
│           │   │   └── claimsDashboardLwc.js-meta.xml
│           │   │
│           │   └── claimTileLwc/
│           │       ├── claimTileLwc.html
│           │       ├── claimTileLwc.js
│           │       └── claimTileLwc.js-meta.xml
│           │
│           ├── objects/
│           │   ├── Policy__c/
│           │   └── Claim__c/
│           │
│           ├── flows/
│           │   ├── AutoQuotingFlow.flow-meta.xml
│           │   ├── SubmissionAutomationFlow.flow-meta.xml
│           │   ├── ClaimApproverScreenFlow.flow-meta.xml
│           │   └── ClaimPolicyHolderStateUpdate.flow-meta.xml
│           │
│           └── permissionsets/
│               ├── InsuranceAgentAccess.permissionset-meta.xml
│               ├── ClaimsManagerAccess.permissionset-meta.xml
│               └── ClaimsAdjusterAccess.permissionset-meta.xml
│
├── docs/
│   ├── architecture/
│   ├── screenshots/
│   └── project-documentation/
│
└── sfdx-project.json
```

---

# ⚙️ Installation & Setup

## Prerequisites

Before deploying the project, you need:

* Salesforce Developer Edition / Salesforce Org
* Salesforce CLI
* Visual Studio Code
* Salesforce Extension Pack
* Lightning Web Components support

---

## Clone Repository

```bash
git clone https://github.com/<your-username>/Multi-Line-Insurance-Management.git
```

Navigate into the project:

```bash
cd Multi-Line-Insurance-Management
```

---

## Authenticate Salesforce Org

```bash
sf org login web
```

Authenticate with your Salesforce Developer Org.

---

## Deploy Metadata

```bash
sf project deploy start
```

After deployment, configure:

* Record Types
* Field Sets
* Flows
* Permission Sets
* Approval Process
* Sharing Rules
* Lightning Pages

---

# 📸 Screenshots

Add project screenshots here after deploying the Salesforce application.

Example:

```markdown
## Claims Dashboard

![Claims Dashboard](docs/screenshots/claims-dashboard.png)

## Auto Quoting Flow

![Auto Quoting Flow](docs/screenshots/auto-quoting-flow.png)

## Claim Approval Process

![Claim Approval](docs/screenshots/claim-approval.png)
```

---

# 🎓 Project Type

**Domain:** Insurance Technology / CRM / Cloud Computing

**Platform:** Salesforce

**Project Type:** Enterprise CRM & Workflow Automation

**Core Areas:**

```text
Salesforce CRM
Apex
SOQL
LWC
Salesforce Flow
Process Automation
Approval Workflow
Data Modeling
Security
Role-Based Access Control
```

---

# 👨‍💻 Author

**Mohamed Anwar**

Computer Science and Engineering Student

### Areas of Interest

* Salesforce Development
* Software Development
* Cloud Computing
* Data Analytics
* Artificial Intelligence
* Full-Stack Development

---

# ⭐ Project Highlights

```text
✓ Multi-line insurance support
✓ Automated policy quoting
✓ Apex-based premium calculation
✓ Automated claim routing
✓ LWC Claims Dashboard
✓ High-value claim approval workflow
✓ Role-based security
✓ Territory-based sharing
✓ Data validation
✓ Apex unit testing
✓ Salesforce Flow automation
```

---

## 📜 License

This project was developed for educational, academic, and portfolio purposes.

---

⭐ If you find this project useful, consider giving the repository a star!
