# 🔁 Rollback Procedure

## When to Rollback

Rollback if any of the following occur after merging the audit branch:

- Measures produce incorrect values in Power BI Desktop
- Visuals break or show errors
- DAX evaluation errors appear in the formula bar
- Performance degrades significantly

---

## Rollback Steps

### Option 1 — Git Revert (preferred)

```bash
# Revert the merge commit on main
git log --oneline -5               # find the merge commit SHA
git revert -m 1 <merge-commit-sha>
git push origin main
```

### Option 2 — Restore from Baseline Branch

```bash
# Reset source files to the pre-audit baseline
git checkout main
git checkout baseline -- source/
git add source/
git commit -m "rollback: restore source to pre-audit baseline"
git push origin main
```

### Option 3 — Restore from Baseline CSV

If Git history is unavailable, re-import measures from:

```
/audit/baseline/measures_inventory.csv
```

Use Tabular Editor 3 or Power BI Desktop to manually restore each measure.

---

## Post-Rollback Verification

1. Open the `.pbip` in Power BI Desktop
2. Verify all measures evaluate without errors
3. Confirm all visuals render correctly
4. Run Best Practice Analyzer — compare against `/audit/baseline/bpa_findings.json`
5. Document the rollback reason in `/docs/governance_signoff.md`

---

## Contacts

| Role | Name | Contact |
|---|---|---|
| Report Owner | _Name_ | _Email_ |
| Audit Lead | _Name_ | _Email_ |
| IT Support | _Name_ | _Email_ |
