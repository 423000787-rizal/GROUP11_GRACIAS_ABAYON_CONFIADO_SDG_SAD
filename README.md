# NTCentinel: Automated Student Violation Management System

[![SDG Goal 4: Quality Education](https://img.shields.io/badge/SDG-Goal%204-gold)](https://sdgs.un.org/goals/goal4)
[![SDG Goal 11: Sustainable Cities and Communities](https://img.shields.io/badge/SDG-Goal%2011-orange)](https://sdgs.un.org/goals/goal11)
[![VB.NET](https://img.shields.io/badge/Language-VB.NET%20Forms-blue)](https://learn.microsoft.com/en-us/dotnet/visual-basic/)
[![SQL Server](https://img.shields.io/badge/Database-SQL%20Server-red)](https://www.microsoft.com/en-us/sql-server)
[![Course](https://img.shields.io/badge/Course-ITELEC1-lightgrey)](https://github.com/424004322/GROUP11_GRACIAS_SDG_SAD)

---

## 📋 Table of Contents

- [Project Overview](#project-overview)
- [SDG Alignment](#sdg-alignment)
- [Key Features](#key-features)
- [Technical Requirements](#technical-requirements)
- [System Architecture](#system-architecture)
- [Repository Structure](#repository-structure)
- [Installation & Setup](#installation--setup)
- [Database Setup](#database-setup)
- [Usage Guide](#usage-guide)
- [Contributors](#contributors)
- [Academic Information](#academic-information)

---

## Project Overview

**Project Title:** NTCentinel — Automated Student Violation Management System
**Course:** ITELEC1 — IT Elective 1 (.NET/C#)
**Program:** BSIT, 2nd Year | 2nd Semester, Cycle 2
**Institution:** National Teachers College (NTC)

NTCentinel is a professional-grade **VB.NET Windows Forms Application** that digitizes the student violation tracking process at the National Teachers College. The system replaces error-prone physical logbooks with a centralized, role-secured digital platform, enabling real-time violation logging, automated sanction calculation via the 3-Strike Rule, and analytical reporting for the Office of Student Affairs (OSA).

### The Problem

The traditional manual logging system at NTC relies on physical logbooks, which leads to:

- **Manual Bottlenecks** — Processing each student takes significant time, causing long queues that extend onto public streets and pose safety risks.
- **Data Integrity Issues** — Illegible handwriting makes it difficult for OSA staff to decode and accurately encode violation records.
- **Security Risks** — Physical logbooks containing sensitive student data are accessible to unauthorized individuals, raising Data Privacy Act concerns.

### The Solution

NTCentinel provides a kiosk-based digital solution that integrates QR code scanning for rapid identity verification and a touchscreen-optimized interface for security guards to log violations in seconds. All records are persisted to a centralized SQL Server database accessible by authorized OSA staff in real time.

---

## SDG Alignment

| SDG Goal | Target | How NTCentinel Contributes |
|---|---|---|
| **Goal 4 — Quality Education** | 4.a: Build inclusive, safe learning environments | Digitizes the discipline process, ensuring fair, consistent, and transparent enforcement of school policies, promoting a safer and more accountable academic environment. |
| **Goal 11 — Sustainable Cities & Communities** | 11.2: Safe and accessible public spaces | Reduces student congestion at campus gates — a documented public safety hazard — by cutting per-student processing time to under 3 seconds. |

---

## Key Features

- **QR-Based Rapid Verification** — Student identity is confirmed via QR scan in under 3 seconds, minimizing gate congestion.
- **Automated Sanction Calculation** — The system enforces the 3-Strike Rule, automatically flagging repeat offenders and escalating sanctions.
- **Full CRUD Violation Management** — Security guards and OSA staff can Create, Read, Update, and Delete violation records through a role-appropriate interface.
- **Role-Based Access Control (RBAC)** — Separate Admin (OSA) and Standard User (Security Guard) roles, justified by the Data Privacy Act of 2012.
- **Report Viewer Integration** — Generates printable violation summary reports, including monthly trend analytics for OSA administration.
- **Digital Audit Trail** — Eliminates manual encoding errors and provides OSA with a reliable, searchable violation history.
- **Offline Resilience** — Capable of local temporary storage during network interruptions, syncing when connectivity is restored.

---

## Technical Requirements

This application satisfies all mandatory technical requirements of the ITELEC1 Final Project:

| Category | Requirement | Implementation |
|---|---|---|
| **Logic & Structure** | OOP — Classes, Properties, Sub/Function procedures | `StudentClass`, `ViolationClass`, `UserClass` modules encapsulate all business logic |
| **Architecture** | Forms-Centric with modularized code-behind | Each form has dedicated code-behind; business rules are isolated in Class modules |
| **Persistence** | ADO.NET (SqlClient) with MS SQL Server; ≥2 related tables | `Students` and `Violations` tables linked by FK; all queries use `SqlCommand` with parameters |
| **Reporting** | Microsoft Report Viewer for summary documents | Monthly Violation Summary Report generated via ReportViewer control |
| **Robustness** | Try-Catch-Finally blocks; structured error messaging | All DB operations wrapped in Try-Catch-Finally; user-facing errors shown via `MessageBox` |
| **Validation** | Numeric-only fields, required fields, Regex where applicable | Student ID validated as numeric; all required fields enforced before DB write |
| **Security** | Login System with Admin vs. Standard User role awareness | Login form gates access; `CurrentUser.Role` checked on each privileged action |

### Functional Requirements

- **FR1 — Data Persistence:** Full CRUD operations on SQL Server using parameterized queries to prevent SQL injection.
- **FR2 — Business Logic:** The 3-Strike Rule sanction engine and violation severity calculation are implemented within dedicated Class modules.
- **FR3 — Reporting:** Monthly Violation Summary Report generated via Report Viewer, showing trends by violation type and student.
- **FR4 — Security:** Login system with role awareness; Admin role unlocks record modification and student management; Standard User role is limited to violation logging.

### Non-Functional Requirements

- **NFR1 — UI Consistency:** All controls follow standard naming conventions (e.g., `btnSubmit`, `lblStatus`, `txtStudentID`, `dgvViolations`).
- **NFR2 — Maintainability:** All complex logic is documented with inline comments explaining business rules and DB operations.
- **NFR3 — Reliability:** Database connection strings are managed through a dedicated `DatabaseConnection` class, centralizing configuration.

---

## System Architecture

NTCentinel follows a **Client-Server Architecture** optimized for Local Area Network (LAN) deployment within the NTC campus.

```
┌─────────────────────────────────────────────────────────┐
│                  PRESENTATION LAYER                     │
│   frmLogin  │  frmDashboard  │  frmViolation  │  frmReport  │
└─────────────────────┬───────────────────────────────────┘
                      │ (ADO.NET / SqlClient)
┌─────────────────────▼───────────────────────────────────┐
│                  BUSINESS LOGIC LAYER                   │
│    StudentClass  │  ViolationClass  │  SanctionEngine   │
└─────────────────────┬───────────────────────────────────┘
                      │
┌─────────────────────▼───────────────────────────────────┐
│                   DATA LAYER                            │
│        DatabaseConnection Class → SQL Server            │
│        Tables: Students, Violations, Users              │
└─────────────────────────────────────────────────────────┘
```

**Architecture Decisions:**
- **QR Integration:** Chosen for high-speed data retrieval (decoding under 1 second), crucial for gate throughput.
- **Centralized SQL Server:** Enables real-time synchronization between the kiosk and OSA backend.
- **RBAC:** Implemented per the Data Privacy Act of 2012, ensuring only authorized OSA staff can modify student records.

---

## Repository Structure

```
GROUP11_GRACIAS_SDG_SAD/          ← Root (matches required naming convention)
│   .gitignore
│   README.md                     ← This file (Project Overview & Installation)
│
├── CODE/
│   ├── NTCentinel.sln            ← Visual Studio Solution File
│   └── NTCentinel/               ← Project Files
│       ├── Forms/
│       │   ├── frmLogin.vb
│       │   ├── frmDashboard.vb
│       │   ├── frmViolation.vb
│       │   └── frmReport.vb
│       ├── Classes/
│       │   ├── StudentClass.vb
│       │   ├── ViolationClass.vb
│       │   ├── UserClass.vb
│       │   └── DatabaseConnection.vb
│       └── Reports/
│           └── ViolationSummary.rdlc
│
├── DATABASE/
│   └── Database_Script.sql       ← Full schema export with seed data
│
├── DOCUMENTATION/
│   ├── SDAD_GROUP11_GRACIAS.pdf  ← Software Design & Analysis Document
│   └── ERD_Diagram.png           ← Entity Relationship Diagram
│
├── MODELS/                       ← UI/UX Prototypes & Mockups
│
├── PROTOTYPE/
│   └── Finals Prototype/         ← Latest working prototype build
│
└── REPORTS/
    └── Sample_Report_Export.pdf  ← Sample Report Viewer output
```

---

## Installation & Setup

### Prerequisites

Before running NTCentinel, ensure the following are installed:

| Requirement | Version | Download |
|---|---|---|
| Windows OS | Windows 10 / 11 | — |
| Visual Studio | 2019 or later | [visualstudio.microsoft.com](https://visualstudio.microsoft.com/) |
| .NET Framework | 4.7.2 or later | Included with Visual Studio |
| Microsoft SQL Server | 2019 Express or later | [microsoft.com/sql-server](https://www.microsoft.com/en-us/sql-server/sql-server-downloads) |
| SQL Server Management Studio (SSMS) | Latest | [aka.ms/ssmsfullsetup](https://aka.ms/ssmsfullsetup) |
| Microsoft Report Viewer | 2015 Runtime | Included in project references |

### Step-by-Step Setup

**1. Clone the Repository**
```bash
git clone https://github.com/424004322/GROUP11_GRACIAS_SDG_SAD.git
cd GROUP11_GRACIAS_SDG_SAD
```

**2. Set Up the Database**

See [Database Setup](#database-setup) below.

**3. Configure the Connection String**

Open `CODE/NTCentinel/Classes/DatabaseConnection.vb` and update the connection string to match your SQL Server instance:

```vb
Public Shared ReadOnly ConnectionString As String =
    "Server=YOUR_SERVER_NAME;Database=NTCentinelDB;Integrated Security=True;"
```

Replace `YOUR_SERVER_NAME` with your local SQL Server instance name (e.g., `.\SQLEXPRESS`).

**4. Open the Solution**

Open `CODE/NTCentinel.sln` in Visual Studio.

**5. Restore NuGet Packages**

In Visual Studio: `Tools → NuGet Package Manager → Restore Packages`

**6. Build and Run**

Press `F5` or click **Start** in Visual Studio. The Login form will appear.

---

## Database Setup

**1. Open SSMS** and connect to your SQL Server instance.

**2. Execute the Database Script**

Open and run `DATABASE/Database_Script.sql`. This script will:
- Create the `NTCentinelDB` database
- Create all required tables (`Students`, `Violations`, `Users`)
- Insert seed/test data for immediate testing

**3. Default Login Credentials (from seed data)**

| Role | Username | Password |
|---|---|---|
| Admin (OSA) | `admin` | `admin123` |
| Standard User (Guard) | `guard01` | `guard123` |

> ⚠️ Change default credentials before any production or live demonstration use.

### Database Schema Overview

**Students Table** — Stores student profile and QR identifier data.
**Violations Table** — Stores individual violation events, linked to a student via `StudentID` (FK).
**Users Table** — Stores system user accounts with hashed passwords and role assignments.

See `DOCUMENTATION/ERD_Diagram.png` for the full Entity Relationship Diagram, and `DOCUMENTATION/SDAD_GROUP11_GRACIAS.pdf` for the complete Data Dictionary.

---

## Usage Guide

### Login

Launch the application. Enter your credentials on `frmLogin`. Access level is determined by your assigned role (Admin or Standard User).

### Logging a Violation (Standard User / Guard)

1. Navigate to the **Log Violation** form (`frmViolation`).
2. Scan or enter the student's QR/ID number.
3. The student's profile populates automatically.
4. Select the violation type from the dropdown.
5. Click **Submit** (`btnSubmit`). The system records the violation and checks the 3-Strike Rule.
6. If the student has reached 3 violations, a flag alert is automatically displayed.

### Managing Records (Admin / OSA Only)

1. Navigate to **Dashboard** (`frmDashboard`).
2. Search, view, update, or delete student and violation records.
3. All changes are logged with a timestamp and the acting user.

### Generating Reports

1. Navigate to the **Reports** module.
2. Select report type (e.g., Monthly Violation Summary) and date range.
3. Click **Generate**. The Report Viewer will render a printable summary.
4. Print or export as PDF via the Report Viewer toolbar.

---

## Contributors

| # | Team Member | Primary Contribution / Assigned Module |
|---|---|---|
| 1 | **Gracias, Kevin Jay C.** | Project Lead · System Analysis · SRS Documentation · Database Schema Design · `DatabaseConnection` Class · UI/UX Design · `frmLogin` · `frmDashboard` · Frontend Dashboard Development |

> This is a Group 11 submission. Additional members and their assigned modules are detailed in `DOCUMENTATION/SDAD_GROUP11_GRACIAS.pdf` under the **Individual Contributions** section.

---

## Academic Information

| Field | Details |
|---|---|
| **Course Code** | ITELEC1 |
| **Course Name** | IT Elective 1 (.NET/C#) |
| **Program** | BSIT, 2nd Year |
| **Term** | 2nd Semester, Cycle 2 |
| **Group** | Group 11 |
| **Primary SDG** | Goal 4 — Quality Education |
| **Secondary SDG** | Goal 11 — Sustainable Cities and Communities |
| **Digital Submission Deadline** | May 22, 2026 |
| **Oral Defense / Presentation** | May 25, 2026 |
| **Institution** | National Teachers College |

### Academic Integrity Statement

All source code, documentation, and diagrams in this repository are original work produced by the contributors listed above. Any third-party libraries or references are properly cited within the code comments and the SDAD document, in compliance with the course's Academic Integrity Policy.

---

*Developed as the ITELEC1 Final Project / Terminal Requirement — National Teachers College, 2026.*
