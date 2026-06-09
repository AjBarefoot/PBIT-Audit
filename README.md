# 📘 Power BI Structural DAX Audit via `.pbip` + GitHub Copilot Agent Mode

**Workflow ID:** `PBI-AUDIT-002`
**Owner:** Alex Barefoot
**Last Updated:** 2026-06-05
**Status:** ✅ Production-ready
**Repo Type:** BI / Semantic Model Audit

---

## 🎯 Purpose

Convert a Power BI report into a **Git-trackable, text-based project** (`.pbip`) so that **GitHub Copilot Agent Mode** can read every DAX measure, visual definition, and semantic model object as source code — enabling **batch audit, refactoring, and optimization** of measures that would otherwise require manual review one-by-one inside Power BI Desktop.

**Use this workflow when you need to:**
- Audit dozens-to-hundreds of DAX measures for redundancy, naming inconsistency, or inefficiency.
- Standardize measure formatting, display folders, and format strings across a model.
- Version-control your semantic model changes.
- Generate before/after diff reports for governance/audit trails.

---

## 🧰 Prerequisites

| Requirement | Version / Notes |
|---|---|
| Power BI Desktop | March 2024 or later (`.pbip` GA) |
| VS Code | Latest stable |
| GitHub Copilot subscription | **Business or Enterprise** (Agent Mode required) |
| GitHub Copilot Chat extension | VS Code marketplace |
| Git | 2.40+ |
| GitHub repo | Private, with branch protection on `main` |
| Optional | Tabular Editor 3 (for cross-validation of Copilot's recommendations) |

---

## 📁 Repository Structure

```
PBI-Audit/
│
├── README.md                          ← this file
├── .gitignore                         ← excludes /Cache and binary artifacts
├── /source/
│   └── <ReportName>.pbip              ← entry point (open this in Desktop)
│   └── <ReportName>.Report/
│   │   ├── report.json
│   │   ├── reportExtensions.json      ← 🎯 AUDIT TARGET (measures live here)
│   │   ├── /visuals/
│   │   └── /staticResources/
│   └── <ReportName>.SemanticModel/
│       ├── definition.pbism
│       ├── model.bim
│       └── /definition/
│           ├── tables/
│           ├── relationships.tmdl
│           └── cultures/
│
├── /audit/
│   ├── /baseline/
│   │   ├── measures_inventory.csv
│   │   └── bpa_findings.json
│   ├── /copilot_prompts/
│   │   ├── 01_inventory.md
│   │   ├── 02_redundancy_check.md
│   │   ├── 03_performance_refactor.md
│   │   └── 04_naming_standardization.md
│   ├── /reports/
│   │   ├── audit_findings.md
│   │   ├── diff_summary.md
│   │   └── optimization_log.csv
│   └── /post_refactor/
│
└── /docs/
    ├── governance_signoff.md
    └── rollback_procedure.md
```

---

## 🚦 Step-by-Step Workflow

### **STEP 1 — Export `.pbix` to `.pbip`**

1. Open the report in **Power BI Desktop**.
2. **File → Save As → Browse → Save as type: `Power BI project files (*.pbip)`**.
3. Save into `/source/` of your repo folder.

### **STEP 2 — Initialize Git Repo**

```bash
cd PBI-Audit
git init
git add .
git commit -m "baseline: import .pbip pre-audit"
git checkout -b audit/copilot-pass-1
```

### **STEP 3 — Baseline Snapshot**

```powershell
$json = Get-Content reportExtensions.json -Raw | ConvertFrom-Json
$json.entities.measures | Select-Object name, expression, formatString, displayFolder |
    Export-Csv ../../audit/baseline/measures_inventory.csv -NoTypeInformation
```

### **STEP 4 — Open in VS Code + Enable Copilot Agent Mode**

1. `code .` from the repo root.
2. Open the Copilot Chat panel (Ctrl+Alt+I).
3. Select **Agent** mode.

### **STEP 5 — Run the Audit Prompts**

Run prompts 01 → 04 in sequence from `/audit/copilot_prompts/`.
Commit after each pass.

### **STEP 6 — Validate**

Reopen `.pbip` in Power BI Desktop, refresh, confirm no measure errors, verify visuals render, run BPA again.

### **STEP 7 — Generate Diff Summary**

Have Copilot compare baseline vs current `reportExtensions.json` and output `/audit/reports/diff_summary.md`.

### **STEP 8 — Commit, PR, Sign-off**

```bash
git add .
git commit -m "audit: Copilot pass 1 — refactor + standardize measures"
git push origin audit/copilot-pass-1
gh pr create --title "DAX Audit – Copilot Pass 1" --body-file audit/reports/diff_summary.md
```

---

## 🔁 Rollback Procedure

See `/docs/rollback_procedure.md`.

---

## 📊 Success Metrics

| Metric | Target |
|---|---|
| Measures audited | 100% of `reportExtensions.json` |
| Redundant measures eliminated | ≥ 10% of total |
| Avg. Storage Engine time reduction | ≥ 15% on flagged measures |
| Naming convention compliance | 100% |
| Visual breakage post-refactor | 0 |

---

## 🔗 Related Workflows

- `PBI-AUDIT-001` — DAX Query View + Copilot (in-Desktop quick wins)
- `PBI-AUDIT-003` — Tabular Editor 3 + DAX Optimizer (performance deep-dive)
- `WF-REPO-001` — Workflow Starter Kit (parent template)

---

**End of README — `PBI-AUDIT-002`**