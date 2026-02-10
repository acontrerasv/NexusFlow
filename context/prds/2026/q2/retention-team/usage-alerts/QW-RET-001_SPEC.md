# QuickWin Spec: Usage Alerts

> Quick specification for the Usage Alerts feature.

## Document Control

| Field | Value |
|-------|-------|
| **Spec ID** | QW-RET-001 |
| **Feature Name** | Usage Alerts |
| **Team** | Retention |
| **PM** | Thomas Weber |
| **Engineering Lead** | Anna Lindqvist |
| **Status** | Ready for Development |
| **Estimated Effort** | 5 days |
| **Priority** | P1 |

---

## Overview

### What
Proactive email alerts when account usage drops significantly, enabling CS team and users to take action before churn risk increases.

### Why
- Accounts with >30% usage drop have 4x higher churn risk
- Currently detected too late (at renewal or support ticket)
- Proactive outreach reduces churn by 23% (industry data)

### Success Metric
- Reduce at-risk account detection time from 45 days to 7 days
- Improve save rate for at-risk accounts from 12% to 25%

---

## User Stories

### US-1: Admin Alert
**As an** account admin
**I want to** receive an alert when my team's usage drops significantly
**So that** I can investigate and address issues early

**Acceptance Criteria**:
- [ ] Email sent when usage drops >30% week-over-week
- [ ] Alert includes usage comparison (this week vs last)
- [ ] Alert includes link to usage dashboard
- [ ] User can configure alert threshold in settings
- [ ] User can opt-out of alerts

### US-2: CS Alert
**As a** Customer Success Manager
**I want to** see accounts with dropping usage in my dashboard
**So that** I can proactively reach out

**Acceptance Criteria**:
- [ ] CS dashboard shows accounts with >30% usage drop
- [ ] Sortable by drop severity
- [ ] One-click to account details
- [ ] Mark as "acknowledged" to remove from list

### US-3: In-App Notification
**As a** user with dropping usage
**I want to** see suggestions to re-engage
**So that** I can get more value from the product

**Acceptance Criteria**:
- [ ] Banner shown on dashboard when usage drops
- [ ] Banner suggests relevant actions
- [ ] Dismissible with "remind me later" option

---

## Functional Requirements

| Req ID | Requirement | Priority |
|--------|-------------|----------|
| FR-1 | Calculate weekly usage per account | P0 |
| FR-2 | Detect >30% week-over-week drop | P0 |
| FR-3 | Send email alert to account admin | P0 |
| FR-4 | Show alert in CS dashboard | P0 |
| FR-5 | Allow threshold configuration | P1 |
| FR-6 | Allow opt-out | P0 |
| FR-7 | Show in-app banner | P1 |
| FR-8 | Track alert engagement | P1 |

---

## Technical Approach

### Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                     Usage Alerts System                      │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐     │
│  │   Daily     │    │   Alert     │    │   Email     │     │
│  │   Cron Job  │ →  │   Engine    │ →  │   Service   │     │
│  │   (5am UTC) │    │             │    │             │     │
│  └─────────────┘    └──────┬──────┘    └─────────────┘     │
│                            │                                 │
│                     ┌──────▼──────┐                         │
│                     │   Alert     │                         │
│                     │   Database  │                         │
│                     └──────┬──────┘                         │
│                            │                                 │
│         ┌──────────────────┼──────────────────┐             │
│         ▼                  ▼                  ▼             │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐     │
│  │ CS Dashboard│    │  User App   │    │  Analytics  │     │
│  │   Widget    │    │   Banner    │    │   Events    │     │
│  └─────────────┘    └─────────────┘    └─────────────┘     │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

### Data Model

```sql
-- Usage metrics (existing)
usage_metrics (
  account_id,
  date,
  workflows_run,
  active_users,
  api_calls
)

-- New: Alert records
usage_alerts (
  id,
  account_id,
  alert_type, -- 'usage_drop', 'inactive', etc.
  severity, -- 'warning', 'critical'
  current_value,
  previous_value,
  drop_percentage,
  created_at,
  acknowledged_at,
  acknowledged_by
)

-- New: Alert preferences
alert_preferences (
  account_id,
  alert_type,
  enabled,
  threshold,
  recipients
)
```

### Calculation Logic

```python
# Weekly usage calculation (pseudocode)
def calculate_usage_drop(account_id):
    this_week = sum(workflows_run for last 7 days)
    last_week = sum(workflows_run for previous 7 days)

    if last_week == 0:
        return 0  # No comparison possible

    drop = (last_week - this_week) / last_week * 100
    return drop

# Alert triggering
def check_alerts():
    for account in active_accounts:
        drop = calculate_usage_drop(account.id)
        threshold = account.alert_threshold or 30

        if drop >= threshold:
            create_alert(account, drop)
            send_email_alert(account, drop)
```

---

## Email Template

**Subject**: ⚠️ Your NexusFlow usage dropped {{drop_percentage}}% this week

**Body**:
```
Hi {{admin_name}},

We noticed that {{company_name}}'s NexusFlow usage dropped
{{drop_percentage}}% compared to last week.

This Week: {{this_week_workflows}} workflows run
Last Week: {{last_week_workflows}} workflows run

This could indicate:
• Team members need help getting started
• Workflows need updating
• Integration issues

Here's what you can do:
1. Check your workflow performance [Link]
2. Review team activity [Link]
3. Contact support if you need help [Link]

We're here to help you get the most out of NexusFlow.

Best,
The NexusFlow Team

---
To adjust these alerts, visit Settings > Notifications
```

---

## UI Designs

### CS Dashboard Widget

```
┌─────────────────────────────────────────────────────────┐
│  ⚠️ Accounts with Dropping Usage                   [↻] │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  Account          Drop    This Week  Last Week  Action  │
│  ─────────────────────────────────────────────────────  │
│  Acme Corp        -45%    120        218        [View]  │
│  TechStart GmbH   -38%    45         73         [View]  │
│  SalesForward     -32%    89         131        [View]  │
│                                                         │
│  Showing 3 accounts with >30% drop                      │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

### User Banner

```
┌─────────────────────────────────────────────────────────┐
│  💡 Your team's activity dropped 35% this week.         │
│     Need help getting back on track?                    │
│     [View Suggestions]  [Dismiss]                       │
└─────────────────────────────────────────────────────────┘
```

---

## Test Cases

| ID | Scenario | Expected Result |
|----|----------|-----------------|
| TC-1 | Usage drops 35% | Alert created, email sent |
| TC-2 | Usage drops 25% (below threshold) | No alert |
| TC-3 | User opts out | No email sent |
| TC-4 | CS acknowledges alert | Removed from active list |
| TC-5 | New account (no history) | No alert |
| TC-6 | Account inactive >30 days | Different alert type |

---

## Analytics Events

| Event | Properties |
|-------|------------|
| `usage_alert_created` | account_id, drop_percentage, severity |
| `usage_alert_email_sent` | account_id, recipient |
| `usage_alert_email_opened` | account_id, recipient |
| `usage_alert_cta_clicked` | account_id, cta_type |
| `usage_alert_dismissed` | account_id, dismiss_type |
| `usage_alert_acknowledged` | account_id, csm_id |

---

## Rollout Plan

### Phase 1: Internal (Day 1-2)
- Enable for internal test accounts
- Verify calculations and emails

### Phase 2: Beta (Day 3-4)
- Enable for 10% of accounts
- Monitor false positive rate

### Phase 3: GA (Day 5)
- Enable for all accounts
- CS team briefing

---

## Success Criteria

| Metric | Target | Measurement |
|--------|--------|-------------|
| Alert accuracy | >90% | Manual review of flagged accounts |
| Email open rate | >40% | Email analytics |
| CS response rate | >60% | Acknowledged within 48h |
| Save rate improvement | +13pp | At-risk to saved conversion |

---

## Dependencies

| Dependency | Owner | Status |
|------------|-------|--------|
| Usage metrics data | Data Team | ✅ Available |
| Email service | Platform | ✅ Available |
| CS dashboard | Frontend | ✅ Exists |

---

## Open Questions

| Question | Owner | Status |
|----------|-------|--------|
| Should we alert for inactive accounts differently? | PM | Decided: Yes, separate alert |
| What's the right threshold? | PM | Decided: 30% default, configurable |
| Who receives the email? | PM | Decided: Account admin(s) |

---

*Document Owner: Thomas Weber*
*Last Updated: January 2026*
*Status: Ready for Development*
