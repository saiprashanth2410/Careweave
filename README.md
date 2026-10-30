# CareWeave 🏥 — Agentic AI Clinical Operations Platform

> **Submission for Product Verse Hackathon 2026**  
> *Organized by Product Space on Unstop*  
> **Theme:** Building Agentic AI Solutions That Reason, Interact with Tools, and Execute Independently

[![Agentic AI: Gemma 4](https://img.shields.io/badge/Agentic_AI-Google_Gemma_4-blue.svg)](https://ai.google.dev/)
[![Analytics: Exasol Personal](https://img.shields.io/badge/Analytics-Exasol_Personal_In--Memory-blueviolet.svg)](EXASOL_SETUP.md)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Hackathon: Product Verse](https://img.shields.io/badge/Hackathon-Product_Verse_2026-teal.svg)](https://unstop.com)

CareWeave is an **Agentic Healthcare Platform** unifying reception, diagnostic laboratories, and physician consultation onto a single source of truth. It integrates multimodal vision agents, autonomous molecular safety interceptors, and high-performance in-memory analytics to eliminate clinical transcription errors and preventable drug harms.

Everything runs on **synthetic demonstration data** with strict human-in-the-loop (Maker-Checker) clinical review authority.

---

## 1. Product Thinking: The Core Problem

In community hospitals and diagnostic networks worldwide, clinical departments operate in disconnected operational silos:

1. **The Paper-Slip Trap:** Patients carry crumpled paper lab reports from outside clinics. Receptionists and lab technicians re-enter numerical values manually, where a single misplaced decimal can quietly corrupt a patient's legal medical chart.
2. **Blind Prescribing & Molecular Doubling:** Physicians prescribe without real-time visibility into external clinic histories. Patients taking branded formulations like *Augmentin 625* are frequently prescribed *Moxikind-CV 625* at a different clinic, causing accidental 200% drug overdoses because legacy EHRs only match identical brand strings.
3. **Operational Analytics Blindspots:** Hospital leadership waits days or weeks for batch reporting. Diagnostic SLA bottlenecks (routine vs. urgent turnaround times) and pharmacy stock runout risks remain invisible until crises occur.

---

## 2. The Solution: CareWeave Agentic Architecture

CareWeave solves this through an autonomous agentic system where multiple specialized AI agents collaborate with hospital staff while enforcing safety guardrails:

```
                                  ┌──────────────────────────────────────────────┐
                                  │           CareWeave Agentic Core             │
                                  └──────────────────────────────────────────────┘
                                                          │
          ┌───────────────────────────────────────────────┼───────────────────────────────────────────────┐
          ▼                                               ▼                                               ▼
┌───────────────────────────┐               ┌───────────────────────────┐               ┌───────────────────────────┐
│ Multimodal Clinical Agent │               │ Molecular Safety Intercept│               │ In-Memory Analytics Agent │
│   (Google Gemma 4 / Vision)│               │  (94K-Drug Formulation)   │               │ (Exasol Personal Columnar)│
├───────────────────────────┤               ├───────────────────────────┤               ├───────────────────────────┤
│ • Reads messy paper scans │               │ • Canonical salt breakdown│               │ • Sub-second window SQL   │
│ • Physiological sanity    │               │ • Cross-brand collision   │               │ • SLA turnaround tracking │
│ • Draft-only maker-checker│               │ • Enforced audit overrides│               │ • Pharmacy demand curves  │
└───────────────────────────┘               └───────────────────────────┘               └───────────────────────────┘
          │                                               │                                               │
          └───────────────────────────────────────┬───────────────────────────────────────────────────────┘
                                                  ▼
                                    ┌───────────────────────────┐
                                    │    Unified Care Record    │
                                    │  (Front Desk · Lab · Dr)  │
                                    └───────────────────────────┘
```

### Key AI Agents & Capabilities:

#### 1. Multimodal Clinical Perception Agent (Google Gemma 4)
- **Document Ingestion:** Technicians upload photos or PDFs of physical diagnostic slips. The vision agent extracts unstructured numeric and unit values into structured fields.
- **Autonomous Physiological Guardrails:** Built-in biological validation automatically rejects impossible measurements (e.g., negative fasting glucose, hemoglobin > 25 g/dL, potassium > 12 mmol/L).
- **Maker-Checker Protocol:** AI extraction is restricted to a **draft state**. The agent cannot publish to a patient's chart without explicit human verification by an authorized pathologist.

#### 2. Cross-Brand Molecular Doubling & Allergy Interceptor Agent
- **Chemical Salt Decomposition:** Analyzes a **94,000-drug formulary** (`BrandMaster.tsv`) and normalizes commercial brand names into canonical active molecules (e.g., resolving *Augmentin* and *Moxikind-CV* both to `amoxicillin + clavulanic acid`).
- **Autonomous Collision Detection:** Evaluates active medications across multi-facility records. If a clinician orders a drug sharing an active molecule with an active outside prescription, the agent halts submission with a `HIGH_COLLISION` modal.
- **Allergy Family Guard:** Automatically detects class-level allergens (e.g., stopping Amoxicillin for patients with documented Penicillin allergies).
- **Maker-Checker Override:** Overriding a safety block requires a documented clinical justification (minimum 15 characters) and explicit risk acknowledgment, permanently written to the audit log.

#### 3. Operational Analytics Agent (Exasol Personal HTAP Engine)
- **In-Memory Columnar Speed:** Executes real-time SQL window functions (`PERCENTILE_CONT`, moving averages) over hospital patient flow, diagnostic turnaround times (TAT), and pharmacy consumption velocity.
- **Dual-Database Resiliency:** High-throughput transactional data (OLTP) is maintained in MongoDB Atlas and synchronized into Exasol Personal (OLAP) via idempotent SQL `MERGE` pipelines.
- **SQL Inspector:** Complete transparency — hospital administrators can view the exact SQL queries executed in-memory with row counts and query execution times in milliseconds.

#### 4. Deterministic Multi-Facility Reconciliation Agent
- Cross-references external clinic records against existing charts using a weighted 70-point heuristic (UHID, date of birth, phone, normalized name), preventing duplicate patient profiles while flagging conflicting test values.

---

## 3. Project Deliverables & Demo

| Deliverable | Location | Details |
|---|---|---|
| **3-Minute Demo Video** | [`demo_video.mp4`](demo_video.mp4) | High-definition walkthrough demonstrating Receptionist check-in, Gemma 4 lab intake, Doctor safety interception, and Exasol in-memory analytics |
| **Walkthrough Script** | [`DEMO.md`](DEMO.md) | Timed click-by-click presenter script and judge evaluation checklist |
| **Exasol Setup Guide** | [`EXASOL_SETUP.md`](EXASOL_SETUP.md) | Local installation and schema architecture for Apple Silicon and Linux |
| **Source Code** | Full Repository | Monorepo containing React 19 frontend (`careweave/client`) and Express backend (`careweave/server`) |

> **Tip for evaluators:** Sign in as Front Desk or Doctor and click **"Load sample scenario (synthetic)"** in the top navigation. This generates the synthetic patient *Priya Raman* with active allergies, conflicting outside reports, and pending laboratory orders to test the agentic workflows instantly.

---

## 4. System Architecture & Tech Stack

```
   [ Front Desk ]       [ Laboratory Portal ]       [ Physician Workspace ]
          │                      │                            │
          └──────────────────────┼────────────────────────────┘
                                 ▼
                     ┌───────────────────────┐
                     │   Express Node API    │
                     │ (Roles, Zod, Audits)  │
                     └───────────┬───────────┘
                                 │
           ┌─────────────────────┴─────────────────────┐
           ▼ (OLTP - Atomic CRUD)                      ▼ (OLAP - In-Memory Analytics)
  ┌─────────────────┐                        ┌───────────────────┐
  │  MongoDB Atlas  │───[Idempotent Pipeline]───►│  Exasol Personal  │
  │ (Encounters, Rx)│      (SQL MERGE)       │(Columnar Analytics│
  └─────────────────┘                        └───────────────────┘
           ▲                                           │
           │                                           ▼
 ┌──────────────────┐                        ┌───────────────────┐
 │  Gemma 4 Vision  │                        │ CareWeave Insights│
 │ (Report Scanner) │                        │ (Operational Hub) │
 └──────────────────┘                        └───────────────────┘
```

| Layer | Technologies |
|---|---|
| **Frontend** | React 19, TypeScript, Vite, Tailwind CSS, Lucide icons, Recharts |
| **Backend** | Node.js, Express, TypeScript, Zod validation |
| **Agentic AI & Vision** | Google Gemma 4 (`gemma-4-26b-a4b-it` / `gemma-4-31b-it`) via Gemini API |
| **Transactional Database** | MongoDB Atlas (Cloud Cluster) |
| **Analytical Database** | Exasol Personal In-Memory Engine via `@exasol/exasol-driver-ts` |
| **Drug Formulary** | 94,000-drug generic master dataset (`BrandMaster.tsv`) |

---

## 5. Local Setup & Running Instructions

### Prerequisites
- Node.js 20+ (developed and verified on macOS Apple Silicon M1 / Linux)
- MongoDB instance (Atlas connection string or local MongoDB)

### Step 1: Clone Repository & Install Dependencies
```bash
git clone <repository-url>
cd CareWeave
npm install
```

### Step 2: Configure Environment Variables
Create `.env` inside `careweave/server/.env`:
```env
PORT=4000
MONGODB_URI="mongodb+srv://<user>:<password>@<cluster>.mongodb.net/careweave"
MONGODB_DB="careweave"
ALLOW_LOCAL_LOGIN="true"
ALLOW_SAMPLE_DATA="true"
GEMINI_API_KEY="your-gemini-api-key"

# Optional Exasol connection (falls back cleanly if offline)
EXASOL_HOST="localhost"
EXASOL_PORT=8563
EXASOL_USER="sys"
EXASOL_PASSWORD="your-exasol-password"
EXASOL_SCHEMA="CAREWEAVE_ANALYTICS"
```

### Step 3: Run Development Servers
```bash
# Terminal 1: Backend API (port 4000)
npm run server

# Terminal 2: React Frontend (port 5173)
npm run dev
```

### Step 4: Run Test Suites
```bash
# Run backend safety, duplicate-therapy and agent unit tests (23 tests)
cd careweave/server
npm test

# Run frontend build check
cd ../client
npm run build
```

---

## 6. Known Scope & Responsible AI Disclosure

- **Synthetic Data Only:** All clinical records, patient profiles, and laboratory values are synthetic.
- **Clinical Decision Support:** CareWeave is designed as review-support software to assist medical practitioners; it does not replace certified clinical judgment.
- **Maker-Checker Mandate:** AI perception and extraction are permanently restricted to unverified draft states until authenticated human operators sign off.

---

## 7. License

Distributed under the [MIT License](LICENSE). Copyright © 2026 Saiprashanth T, Suriya Sudhakar, Dhivya Dharshini C S.
