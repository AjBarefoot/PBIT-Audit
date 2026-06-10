# 📝 Audit Findings — CBI Full Inventory, Billings & Depletions

**Report:** CBI Full Inventory, Billings & Depletions
**Audit Date:** 2026-06-10
**Auditor:** GitHub Copilot Agent
**Total Measures:** 43
**Total Calculated Columns:** 10
**Total Tables:** 8
**Total Relationships:** 4

---

## Measure Inventory

### Fact_Pallet_Ending (37 measures)

| # | Measure Name | DAX Expression | Format | Used by Visual? |
|---|---|---|---|---|
| 1 | Total Billings | `SUM(Fact_Pallet_Ending[Billings])` | General Number | No (dependency only) |
| 2 | Total Depletions | `SUM(Fact_Pallet_Ending[Depletions])` | General Number | No (dependency only) |
| 3 | Total DC Inventory | `SUM(Fact_Pallet_Ending[DC Ending Inventory])` | 0 | ✅ Yes |
| 4 | Total Distributor Inventory | `SUM(Fact_Pallet_Ending[Distributor Ending Inventory])` | General Number | ✅ Yes |
| 5 | Total Full Inventory | `[Total DC Inventory]+[Total Distributor Inventory]+Sum(Fact_Pallet_Ending[Ending In-Transit])` | General Number | ✅ Yes |
| 6 | Billings YoY | `CALCULATE([Total Billings], SAMEPERIODLASTYEAR(DimDate[Date]))` | General Number | ❌ Unused |
| 7 | Billings LTM | `CALCULATE([Total Billings], DATESINPERIOD(DimDate[Date], MAX(DimDate[Date]), -12, MONTH))` | General Number | ❌ Unused (duplicate of Billings Rolling 12) |
| 8 | Billings Rolling 12 | `CALCULATE([Total Billings], DATESINPERIOD(DimDate[Date], MAX(DimDate[Date]), -12, MONTH))` | 0.00 | ✅ Yes |
| 9 | Full Inventory PY | `CALCULATE([Total Full Inventory], FILTER(ALL(DimDate), ...))` | General Number | ❌ Unused (only feeds Inventory YOY) |
| 10 | Inventory YOY | `[Total Full Inventory]-[Full Inventory PY]` | General Number | ❌ Unused |
| 11 | Depletions Rolling 12 | `CALCULATE([Total Depletions], DATESINPERIOD(DimDate[Date], MAX(DimDate[Date]), -12, MONTH))` | General Number | ✅ Yes |
| 12 | DC Inventory PY | `CALCULATE([Total DC Inventory], FILTER(ALL(DimDate), ...))` | General Number | ❌ Unused (only feeds DC Inventory YOY) |
| 13 | DC Inventory YOY | `[Total DC Inventory]-[DC Inventory PY]` | 0 | ❌ Unused (only feeds DC YoY%) |
| 14 | DC YoY% | `DIVIDE([DC Inventory YOY],[DC Inventory PY])` | 0.0%;-0.0%;0.0% | ❌ Unused |
| 15 | Inventory Coverage Months (DC) | `Divide([Total DC Inventory],[Next Month Billings])` | 0.0 | ✅ Yes |
| 16 | Inventory Coverage Months (Dist) | `Divide([Total Distributor Inventory],[Next Month Depletions])` | General Number | ✅ Yes |
| 17 | Total Billings (Plts) | `SUM(Fact_Pallet_Ending[Billings_PLT])` | General Number | No (dependency only) |
| 18 | Total Depletions (Plts) | `SUM(Fact_Pallet_Ending[Depletions_PLT])` | General Number | No (dependency only) |
| 19 | Total DC Inventory (Plts) | `SUM(Fact_Pallet_Ending[DC Ending Inventory_PLT])` | General Number | ✅ Yes |
| 20 | Total Distributor Inventory (Plts) | `SUM(Fact_Pallet_Ending[Distributor Ending Inventory_PLT])` | General Number | ✅ Yes |
| 21 | Total Full Inventory (Plts) | `[Total DC Inventory (Plts)]+[Total Distributor Inventory (Plts)]+Sum(Fact_Pallet_Ending[Ending In-Transit_PLT])` | General Number | ❌ Unused |
| 22 | DC Inventory PY (Plts) | `CALCULATE([Total DC Inventory (Plts)], FILTER(ALL(DimDate), ...))` | General Number | ❌ Unused |
| 23 | Inventory Coverage Months (DC:Plts) | `Divide([Total DC Inventory (Plts)],[Next Month Billings (Plts)])` | General Number | ✅ Yes |
| 24 | Inventory Coverage Months (Dist:Plts) | `Divide([Total Distributor Inventory (Plts)],[Next Month Depletions (Plts)])` | General Number | ✅ Yes |
| 25 | Depletions Rolling 12 (Plts) | `CALCULATE([Total Depletions (Plts)], DATESINPERIOD(DimDate[Date], MAX(DimDate[Date]), -12, MONTH))` | General Number | ✅ Yes |
| 26 | Billings Rolling 12 (Plts) | `CALCULATE([Total Billings (Plts)], DATESINPERIOD(DimDate[Date], MAX(DimDate[Date]), -12, MONTH))` | 0.00 | ✅ Yes |
| 27 | Billings Rolling 12 Prior Month (Plts) | `CALCULATE([Billings Rolling 12 (Plts)], DATEADD(DimDate[Date], -1, MONTH))` | General Number | No (dependency only) |
| 28 | Billings Rolling 12 MoM % (Plts) | `DIVIDE(([Billings Rolling 12 (Plts)]-[Billings Rolling 12 Prior Month (Plts)]),[Billings Rolling 12 Prior Month (Plts)])` | 0.0%;-0.0%;0.0% | ✅ Yes |
| 29 | Billings Rolling 12 Prior Month | `CALCULATE([Billings Rolling 12], DATEADD(DimDate[Date], -1, MONTH))` | General Number | No (dependency only) |
| 30 | Billings Rolling 12 MoM % | `DIVIDE(([Billings Rolling 12]-[Billings Rolling 12 Prior Month]),[Billings Rolling 12 Prior Month])` | 0.0%;-0.0%;0.0% | ✅ Yes |
| 31 | Depletions Rolling 12 Prior Month | `CALCULATE([Depletions Rolling 12], DATEADD(DimDate[Date], -1, MONTH))` | General Number | No (dependency only) |
| 32 | Depletions Rolling 12 MoM % | `DIVIDE(([Depletions Rolling 12]-[Depletions Rolling 12 Prior Month]),[Depletions Rolling 12 Prior Month])` | 0.0%;-0.0%;0.0% | ✅ Yes |
| 33 | Depletions Rolling 12 Prior Month (Plts) | `CALCULATE([Depletions Rolling 12 (Plts)], DATEADD(DimDate[Date], -1, MONTH))` | General Number | No (dependency only) |
| 34 | Depletions Rolling 12 MoM % (Plts) | `DIVIDE(([Depletions Rolling 12 (Plts)]-[Depletions Rolling 12 Prior Month (Plts)]),[Depletions Rolling 12 Prior Month (Plts)])` | 0.00%;-0.00%;0.00% | ✅ Yes |
| 35 | Depletions LTM | `CALCULATE([Total Depletions], DATESINPERIOD(DimDate[Date], MAX(DimDate[Date]), -12, MONTH))` | General Number | ✅ Yes |
| 36 | Inventory Coverage Months (Dist_current) | `Divide([Total Distributor Inventory],[Total Depletions])` | General Number | ✅ Yes |
| 37 | Inventory Coverage Months (DC_Current) | `Divide([Total DC Inventory],[Total Billings])` | General Number | ✅ Yes |

### DimDate (6 measures)

| # | Measure Name | DAX Expression | Format | Used by Visual? |
|---|---|---|---|---|
| 38 | Next Month Billings | `CALCULATE([Total Billings], DATEADD(DimDate[Date], 1, MONTH))` | General Number | No (dependency only) |
| 39 | Next Month Depletions | `CALCULATE([Total Depletions], DATEADD(DimDate[Date], 1, MONTH))` | General Number | No (dependency only) |
| 40 | Next Month Billings (Plts) | `CALCULATE([Total Billings (Plts)], DATEADD(DimDate[Date], 1, MONTH))` | General Number | No (dependency only) |
| 41 | Next Month Depletions (Plts) | `CALCULATE([Total Depletions (Plts)], DATEADD(DimDate[Date], 1, MONTH))` | General Number | No (dependency only) |
| 42 | CE per Plt (Billing) | `(SUM(Fact_Pallet_Ending[Billing Onces])/SUM(Fact_Pallet_Ending[Billings_PLT]))/288` | General Number | ✅ Yes |
| 43 | CE per Plt (Depletions) | `(SUM(Fact_Pallet_Ending[Depletion Onces])/SUM(Fact_Pallet_Ending[Depletions_PLT]))/288` | General Number | ❌ Unused |

### Calculated Columns (10 total)

| Table | Column | Expression |
|---|---|---|
| Fact_Pallet_Ending | Onces per Item | `LOOKUPVALUE('Item Cross Reference'[Onces per Item],'Item Cross Reference'[Item_Code],Fact_Pallet_Ending[Item_Code])` |
| Fact_Pallet_Ending | Billing Onces | `Fact_Pallet_Ending[Billings]*Fact_Pallet_Ending[Onces per Item]` |
| Fact_Pallet_Ending | Depletion Onces | `Fact_Pallet_Ending[Depletions]*Fact_Pallet_Ending[Onces per Item]` |
| Item Cross Reference | Onces per Item | `'Item Cross Reference'[SIZE]*'Item Cross Reference'[COUNT]` |
| Item Cross Reference | Beer Weight | `'Item Cross Reference'[Onces per Item]*.066` |
| Item Cross Reference | Package Weight | `IF('Item Cross Reference'[PACKAGE]="CAN",.04*..., IF(..."BOTTLE",.4*..., 35*...))` |
| Item Cross Reference | Weight Per Item | `IF(..."KEG",...Beer Weight+Package Weight, 1+Beer Weight+Package Weight)` |
| Item Cross Reference | Brand (groups) | `SWITCH(TRUE(), ... brand categorization ...)` |
| Table | CE Shipments | `'Table'[Rpt Beer Shipments (MM)]*1000000` |
| Table (2) | 5 calculated columns | Plastic Pallet Shipments (CE), CBI Reported Shipments (CE), Total Pallets Shipments (MM), Plastic Pallet Shipments (MM), Total Shipments in Plastic, Total Shipments in MKM Supplied, MKM Fills Estimated Case Equivalent |

---

## Redundancy Analysis

### 🔴 Finding R1 — EXACT DUPLICATE: Billings LTM = Billings Rolling 12

| Property | Billings LTM | Billings Rolling 12 |
|---|---|---|
| **DAX** | `CALCULATE([Total Billings], DATESINPERIOD(DimDate[Date], MAX(DimDate[Date]), -12, MONTH))` | `CALCULATE([Total Billings], DATESINPERIOD(DimDate[Date], MAX(DimDate[Date]), -12, MONTH))` |
| **Format** | General Number | 0.00 |
| **On visual?** | ❌ No | ✅ Yes |

**Recommendation:** DELETE `Billings LTM`. It is an exact duplicate of `Billings Rolling 12` and is not used by any visual or other measure.
**Risk:** 🟢 Low — no visual or measure depends on it.

---

### 🔴 Finding R2 — EXACT DUPLICATE: Depletions LTM = Depletions Rolling 12

| Property | Depletions LTM | Depletions Rolling 12 |
|---|---|---|
| **DAX** | `CALCULATE([Total Depletions], DATESINPERIOD(DimDate[Date], MAX(DimDate[Date]), -12, MONTH))` | `CALCULATE([Total Depletions], DATESINPERIOD(DimDate[Date], MAX(DimDate[Date]), -12, MONTH))` |
| **Format** | General Number | General Number |
| **On visual?** | ✅ Yes (pie chart) | ✅ Yes (combo charts) |

**Recommendation:** MERGE — keep `Depletions Rolling 12`, update the pie chart visual on pages "CBI-Units/Kegs" and "Current Coverage CBI-Units/Kegs" to reference `Depletions Rolling 12` instead of `Depletions LTM`, then delete `Depletions LTM`.
**Risk:** 🟡 Medium — requires visual update but DAX is identical.

---

### 🟡 Finding R3 — UNUSED MEASURE CHAIN: YoY Inventory Analysis

These 7 measures form a dependency chain that is **not connected to any visual**:

| Measure | Used By |
|---|---|
| Full Inventory PY | → Inventory YOY |
| Inventory YOY | → *(nothing)* |
| DC Inventory PY | → DC Inventory YOY |
| DC Inventory YOY | → DC YoY% |
| DC YoY% | → *(nothing)* |
| DC Inventory PY (Plts) | → *(nothing)* |
| Billings YoY | → *(nothing)* |

**Recommendation:** Review whether these measures are needed for future development. If not, DELETE all 7 to reduce model complexity.
**Risk:** 🟢 Low — none are used by any visual. However, they may be intentionally kept for ad-hoc analysis or future dashboard pages.

---

### 🟡 Finding R4 — UNUSED: Total Full Inventory (Plts)

- **DAX:** `[Total DC Inventory (Plts)]+[Total Distributor Inventory (Plts)]+Sum(Fact_Pallet_Ending[Ending In-Transit_PLT])`
- **Used by visual?:** ❌ No
- **Used by other measure?:** ❌ No

**Recommendation:** DELETE or flag for future use. The non-pallet version `Total Full Inventory` IS used on the "SKU Inventory Levels" page.
**Risk:** 🟢 Low

---

### 🟡 Finding R5 — UNUSED: CE per Plt (Depletions)

- **DAX:** `(SUM(Fact_Pallet_Ending[Depletion Onces])/SUM(Fact_Pallet_Ending[Depletions_PLT]))/288`
- **Used by visual?:** ❌ No
- **Used by other measure?:** ❌ No
- **Note:** The companion measure `CE per Plt (Billing)` IS used on the "CBI-Pallet" page.

**Recommendation:** DELETE or add to a visual for completeness.
**Risk:** 🟢 Low

---

### 📊 Redundancy Summary

| Category | Count | Measures |
|---|---|---|
| Exact duplicates | 2 | Billings LTM, Depletions LTM |
| Unused (no visual, no dependency) | 10 | Billings YoY, Full Inventory PY, Inventory YOY, DC Inventory PY, DC Inventory YOY, DC YoY%, DC Inventory PY (Plts), Total Full Inventory (Plts), CE per Plt (Depletions), Billings LTM |
| Potentially eliminable | 10 of 43 | **23.3% of total measures** |

---

## Performance Refactoring

### ⚡ Finding P1 — FILTER(ALL()) Anti-Pattern (3 measures)

The following measures use `FILTER(ALL(DimDate), ...)` to get prior-year values. This is a known performance anti-pattern because it iterates the entire date table row-by-row.

**Affected measures:**

| Measure | Current DAX |
|---|---|
| Full Inventory PY | `CALCULATE([Total Full Inventory], FILTER(ALL(DimDate), DimDate[Year] = MAX(DimDate[Year]) - 1 && DimDate[MonthNum] = MAX(DimDate[MonthNum])))` |
| DC Inventory PY | `CALCULATE([Total DC Inventory], FILTER(ALL(DimDate), DimDate[Year] = MAX(DimDate[Year]) - 1 && DimDate[MonthNum] = MAX(DimDate[MonthNum])))` |
| DC Inventory PY (Plts) | `CALCULATE([Total DC Inventory (Plts)], FILTER(ALL(DimDate), DimDate[Year] = MAX(DimDate[Year]) - 1 && DimDate[MonthNum] = MAX(DimDate[MonthNum])))` |

**Proposed refactored DAX (using PARALLELPERIOD):**

```dax
// Full Inventory PY — refactored
CALCULATE(
    [Total Full Inventory],
    PARALLELPERIOD(DimDate[Date], -12, MONTH)
)

// DC Inventory PY — refactored
CALCULATE(
    [Total DC Inventory],
    PARALLELPERIOD(DimDate[Date], -12, MONTH)
)

// DC Inventory PY (Plts) — refactored
CALCULATE(
    [Total DC Inventory (Plts)],
    PARALLELPERIOD(DimDate[Date], -12, MONTH)
)
```

**Impact:** 🟡 Medium — eliminates row-by-row iteration. However, note that `PARALLELPERIOD` returns a full month range vs the point-in-time FILTER approach. If the intent is truly "same month last year ending inventory" and data is monthly, both approaches yield the same result. If data is daily, the behavior differs.

**⚠️ IMPORTANT:** These 3 measures are currently unused by any visual (see Finding R3). If they are deleted as recommended in the redundancy analysis, this refactoring is moot.

---

### ⚡ Finding P2 — Inconsistent SUM Casing (2 measures)

| Measure | Current | Issue |
|---|---|---|
| Total Full Inventory | `...+Sum(Fact_Pallet_Ending[Ending In-Transit])` | `Sum` should be `SUM` |
| Total Full Inventory (Plts) | `...+Sum(Fact_Pallet_Ending[Ending In-Transit_PLT])` | `Sum` should be `SUM` |

**Impact:** 🟢 Low — DAX is case-insensitive, so this is cosmetic only, but inconsistency suggests copy-paste errors and reduces readability.

---

### ⚡ Finding P3 — CE per Plt Division Without DIVIDE (2 measures)

| Measure | Current DAX |
|---|---|
| CE per Plt (Billing) | `(SUM(Fact_Pallet_Ending[Billing Onces])/SUM(Fact_Pallet_Ending[Billings_PLT]))/288` |
| CE per Plt (Depletions) | `(SUM(Fact_Pallet_Ending[Depletion Onces])/SUM(Fact_Pallet_Ending[Depletions_PLT]))/288` |

**Proposed refactored DAX:**

```dax
// CE per Plt (Billing) — safe division
DIVIDE(
    SUM(Fact_Pallet_Ending[Billing Onces]),
    SUM(Fact_Pallet_Ending[Billings_PLT]) * 288
)

// CE per Plt (Depletions) — safe division
DIVIDE(
    SUM(Fact_Pallet_Ending[Depletion Onces]),
    SUM(Fact_Pallet_Ending[Depletions_PLT]) * 288
)
```

**Impact:** 🟡 Medium — The `/` operator returns an error on divide-by-zero; `DIVIDE()` returns BLANK by default. This is a best practice for robustness.

---

### ⚡ Finding P4 — LOOKUPVALUE Calculated Column

| Column | Table | DAX |
|---|---|---|
| Onces per Item | Fact_Pallet_Ending | `LOOKUPVALUE('Item Cross Reference'[Onces per Item],'Item Cross Reference'[Item_Code],Fact_Pallet_Ending[Item_Code])` |

**Issue:** `LOOKUPVALUE` in a calculated column on the fact table performs a row-by-row lookup. Since there is already a relationship between `Fact_Pallet_Ending[Item_Code]` and `Item Cross Reference[Item_Code]`, this could use `RELATED()` instead.

**Proposed refactored DAX:**

```dax
RELATED('Item Cross Reference'[Onces per Item])
```

**Impact:** 🟢 Low — `RELATED()` leverages the existing relationship and is generally more efficient than `LOOKUPVALUE` when a relationship exists. Both produce the same result.

---

### Performance Summary

| Finding | Severity | Measures Affected | Can Auto-Fix? |
|---|---|---|---|
| P1: FILTER(ALL()) anti-pattern | Medium | 3 (all unused) | Yes (but recommend delete) |
| P2: Inconsistent SUM casing | Low | 2 | Yes |
| P3: Division without DIVIDE | Medium | 2 | Yes |
| P4: LOOKUPVALUE vs RELATED | Low | 1 calculated column | Yes |

---

## Naming Standardization

### 🏷️ Finding N1 — No Display Folders

**None of the 43 measures have a display folder assigned.** All measures appear in a flat, unsorted list in the field pane.

**Recommendation:** Organize measures into display folders:

| Proposed Folder | Measures |
|---|---|
| **Billings** | Total Billings, Billings Rolling 12, Billings Rolling 12 Prior Month, Billings Rolling 12 MoM %, Billings YoY, Billings LTM, Total Billings (Plts), Billings Rolling 12 (Plts), Billings Rolling 12 Prior Month (Plts), Billings Rolling 12 MoM % (Plts), Next Month Billings, Next Month Billings (Plts) |
| **Depletions** | Total Depletions, Depletions Rolling 12, Depletions Rolling 12 Prior Month, Depletions Rolling 12 MoM %, Depletions LTM, Total Depletions (Plts), Depletions Rolling 12 (Plts), Depletions Rolling 12 Prior Month (Plts), Depletions Rolling 12 MoM % (Plts), Next Month Depletions, Next Month Depletions (Plts) |
| **Inventory** | Total DC Inventory, Total Distributor Inventory, Total Full Inventory, Full Inventory PY, Inventory YOY, DC Inventory PY, DC Inventory YOY, DC YoY%, Total DC Inventory (Plts), Total Distributor Inventory (Plts), Total Full Inventory (Plts), DC Inventory PY (Plts) |
| **Coverage** | Inventory Coverage Months (DC), Inventory Coverage Months (Dist), Inventory Coverage Months (DC:Plts), Inventory Coverage Months (Dist:Plts), Inventory Coverage Months (DC_Current), Inventory Coverage Months (Dist_current) |
| **Conversion** | CE per Plt (Billing), CE per Plt (Depletions) |

---

### 🏷️ Finding N2 — Inconsistent Format Strings

| Issue | Measures | Current Format | Recommended Format |
|---|---|---|---|
| Most percentage measures | Billings Rolling 12 MoM %, DC YoY%, etc. | `0.0%;-0.0%;0.0%` | `0.0%;-0.0%;0.0%` ✅ OK |
| Depletions Rolling 12 MoM % (Plts) | 1 measure | `0.00%;-0.00%;0.00%` | `0.0%;-0.0%;0.0%` (match others) |
| Billings Rolling 12, Billings Rolling 12 (Plts) | 2 measures | `0.00` | Should be `#,##0` (whole numbers for rolling totals) |
| Total DC Inventory | 1 measure | `0` (decimal hint) | `#,##0` (thousands-formatted integer) |
| Inventory Coverage Months (DC) | 1 measure | `0.0` | OK ✅ |
| Inventory Coverage Months (Dist) | 1 measure | General Number | Should be `0.0` (match DC version) |
| Most measures | 36 measures | General Number | Should specify explicit format |

---

### 🏷️ Finding N3 — Generic Table Names

| Current Name | Recommended Name | Reason |
|---|---|---|
| Table | CBI_Quarterly_Shipments | Contains CBI quarterly beer shipment data |
| Table (2) | Pallet_Shipment_Analysis | Contains pallet shipment metrics by quarter |
| Table (3) | Brand_Group_Rank | Contains brand grouping with rank values |

**Risk:** 🟡 Medium — Renaming tables requires updating all calculated column references and any visual bindings. This is a breaking change that must be validated in Power BI Desktop.

---

### 🏷️ Finding N4 — Inconsistent Naming Patterns

| Issue | Examples | Recommendation |
|---|---|---|
| Inconsistent YoY vs YOY casing | `Billings YoY` vs `Inventory YOY` vs `DC Inventory YOY` | Standardize to `YoY` |
| Inconsistent coverage naming | `(DC)` vs `(DC_Current)` vs `(DC:Plts)` | Use consistent delimiter: `(DC)`, `(DC - Current)`, `(DC - Plts)` |
| "LTM" vs "Rolling 12" for same concept | `Billings LTM` = `Billings Rolling 12` | Standardize to one term |
| Pallet suffix inconsistency | `(Plts)` used throughout | OK — consistent ✅ |
| Column naming: "Onces" | `Billing Onces`, `Depletion Onces` | Should be "Ounces" (typo) |

---

### 🏷️ Finding N5 — Measures on Wrong Table

| Measure | Current Table | Recommended Table | Reason |
|---|---|---|---|
| Next Month Billings | DimDate | Fact_Pallet_Ending | Billings measure should be with other billing measures |
| Next Month Depletions | DimDate | Fact_Pallet_Ending | Depletions measure should be with other depletion measures |
| Next Month Billings (Plts) | DimDate | Fact_Pallet_Ending | Same as above |
| Next Month Depletions (Plts) | DimDate | Fact_Pallet_Ending | Same as above |
| CE per Plt (Billing) | DimDate | Fact_Pallet_Ending | Conversion metric, not a date measure |
| CE per Plt (Depletions) | DimDate | Fact_Pallet_Ending | Same as above |

**Note:** All 6 measures on `DimDate` are not date-related — they reference `Fact_Pallet_Ending` columns. They should be moved to `Fact_Pallet_Ending` for logical organization.

---

### Naming Summary

| Finding | Items Affected | Severity |
|---|---|---|
| N1: No display folders | 43 measures | 🟡 Medium |
| N2: Inconsistent format strings | ~38 measures | 🟡 Medium |
| N3: Generic table names | 3 tables | 🟡 Medium (breaking) |
| N4: Inconsistent naming | 5+ measures | 🟢 Low |
| N5: Measures on wrong table | 6 measures | 🟡 Medium |

---

## Overall Audit Summary

| Metric | Value |
|---|---|
| **Total measures audited** | 43 of 43 (100%) |
| **Exact duplicate measures** | 2 (Billings LTM, Depletions LTM) |
| **Unused measures (no visual, no dependency)** | 10 (23.3%) |
| **Performance anti-patterns** | 4 findings (8 measures/columns) |
| **Naming issues** | 5 findings |
| **Measures without display folders** | 43 (100%) |
| **Measures without explicit format strings** | 36 (~84%) |
| **Visual breakage risk** | 🟢 Low for redundancy cleanup, 🟡 Medium for table renames |

### Recommended Priority Actions

1. **🟢 Quick Win — Delete `Billings LTM`** (exact duplicate, unused)
2. **🟢 Quick Win — Fix "Onces" → "Ounces" typo** in calculated column names
3. **🟢 Quick Win — Standardize `Sum` → `SUM` casing**
4. **🟡 Medium — Add display folders** to all 43 measures
5. **🟡 Medium — Merge `Depletions LTM` into `Depletions Rolling 12`** (update visual reference)
6. **🟡 Medium — Replace `/` with `DIVIDE()`** in CE per Plt measures
7. **🟡 Medium — Replace `LOOKUPVALUE` with `RELATED()`** in calculated column
8. **🔴 Decide — Keep or delete 10 unused measures** (YoY chain, Total Full Inventory (Plts), CE per Plt (Depletions))
9. **🔴 Breaking — Rename generic tables** (Table, Table (2), Table (3)) — requires full validation
