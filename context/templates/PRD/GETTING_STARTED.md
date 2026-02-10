# Getting Started with PRDs

> Quick start guide for writing product requirements documents at NexusFlow.

## Your First PRD in 5 Steps

### Step 1: Determine Document Type

| Situation | Document Type |
|-----------|---------------|
| New feature, >2 weeks dev | Full PRD (with discovery) |
| Small feature, 1-2 weeks | OnePage PRD |
| Bug fix or quick improvement | QuickWin Spec |

### Step 2: Create Your Folder

```bash
# For full PRDs
context/prds/2026/q1/your-team/feature-name/

# For OnePage PRDs
context/prds/2026/q1/your-team/PRD-TEAM-001.md

# For QuickWins
context/prds/2026/q1/your-team/QW-TEAM-001_SPEC.md
```

### Step 3: Copy the Template

Copy the appropriate template from:
```
context/templates/PRD/
├── PRD_Template.md          # Full PRD
├── PRD_Template_OnePage.md  # OnePage
└── QuickWin_Spec.md         # QuickWin
```

### Step 4: Fill In the Sections

Start with:
1. **Overview** - What is this feature?
2. **Problem** - Why are we building it?
3. **Goals** - What does success look like?
4. **Requirements** - What must it do?

### Step 5: Submit for Review

1. Create PR with your PRD
2. Request review from PM Lead
3. Address feedback
4. Get approval

---

## Quick Reference

### Required Sections (All PRDs)

| Section | Purpose |
|---------|---------|
| Overview | Quick summary of the feature |
| Problem Statement | Why we're building this |
| Goals | What success looks like |
| Requirements | What it must do |
| Success Metrics | How we'll measure |

### Optional Sections

| Section | When to Include |
|---------|-----------------|
| JTBD Analysis | Complex user problems |
| Technical Architecture | System changes |
| Migration Plan | Breaking changes |
| Rollback Plan | High-risk features |

---

## Template Quick Links

- [Full PRD Template](./PRD_Template.md)
- [OnePage PRD Template](./PRD_Template_OnePage.md)
- [QuickWin Spec Template](./QuickWin_Spec.md)
- [Problem Brief Template](./01_Problem_Brief_Template.md)
- [JTBD Template](./02_JTBD_Template.md)
- [Solution Hypothesis Template](./03_Solution_Hypothesis_Template.md)
- [Validation Checklist](./PRD_Validation_Checklist.md)

---

## Need Help?

- **Questions**: Ask in #product-team Slack
- **Examples**: See `context/prds/2025/` for completed PRDs
- **Reviews**: Tag @pm-lead in your PR

---

*Last Updated: January 2026*
