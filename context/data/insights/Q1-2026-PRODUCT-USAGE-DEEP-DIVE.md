# Q1 2026 Product Usage Deep Dive

> Detailed analysis of NexusFlow product usage patterns.

## Workflow Analysis

### Workflow Creation Patterns

#### By Template Usage

| Creation Method | % | Avg Success Rate |
|-----------------|---|------------------|
| From Template | 58% | 96.2% |
| Blank Canvas | 32% | 91.5% |
| Duplicate Existing | 10% | 95.8% |

**Insight**: Template-based workflows succeed 5% more often. Promote templates.

#### Most Used Templates

| Template | Usage | Success Rate |
|----------|-------|--------------|
| Lead Follow-up Sequence | 2,340 | 97.1% |
| Deal Stage Automation | 1,890 | 95.8% |
| Meeting Scheduler | 1,650 | 94.2% |
| Contact Enrichment | 1,420 | 93.5% |
| Win/Loss Notification | 1,280 | 96.8% |

#### Workflow Complexity

| Complexity | % | Definition |
|------------|---|------------|
| Simple | 45% | 1-3 steps |
| Medium | 38% | 4-7 steps |
| Complex | 17% | 8+ steps |

**Insight**: Most users stick to simple workflows. Complex workflow adoption correlates with retention.

### Workflow Step Analysis

#### Most Used Steps

| Step Type | Usage | % of All Steps |
|-----------|-------|----------------|
| Send Email | 45,230 | 28% |
| Wait/Delay | 32,450 | 20% |
| Update CRM | 28,900 | 18% |
| If/Else Condition | 21,340 | 13% |
| Webhook | 12,560 | 8% |
| AI Generate | 8,920 | 6% |
| Other | 11,400 | 7% |

#### Step Success Rates

| Step Type | Success Rate | Failure Cause |
|-----------|--------------|---------------|
| Send Email | 98.2% | Invalid email |
| Wait/Delay | 99.9% | N/A |
| Update CRM | 89.5% | Auth expired |
| If/Else | 99.8% | N/A |
| Webhook | 85.2% | Timeout/error |
| AI Generate | 92.1% | Rate limit |

**Insight**: CRM and Webhook steps have lowest success. Focus on reliability.

---

## CRM Integration Deep Dive

### Integration Status

| Status | Users | % |
|--------|-------|---|
| Connected & Active | 4,114 | 34% |
| Connected, Inactive | 1,452 | 12% |
| Setup Started, Not Completed | 1,815 | 15% |
| Never Started | 4,719 | 39% |

### CRM Provider Distribution

| CRM | Connected Users | % of Integrations |
|-----|-----------------|-------------------|
| Salesforce | 1,850 | 45% |
| HubSpot | 1,480 | 36% |
| Pipedrive | 620 | 15% |
| Zoho | 164 | 4% |

### Sync Metrics

| Metric | Value | Target |
|--------|-------|--------|
| Sync Success Rate | 87.5% | 95% |
| Avg Sync Time | 2.3 min | 1 min |
| Failed Syncs/Day | 342 | <100 |
| Sync Conflicts/Day | 89 | <30 |

### CRM Setup Funnel

| Step | Completion | Drop-off |
|------|------------|----------|
| Start Setup | 100% | - |
| Select CRM | 92% | 8% |
| OAuth Connect | 68% | 24% |
| Field Mapping | 52% | 16% |
| Initial Sync | 45% | 7% |
| Complete | 34% | 11% |

**Key Insight**: OAuth connection is the biggest barrier (24% drop-off).

---

## AI Feature Analysis

### AI Assist Usage

| Feature | Users | Usage/User/Week |
|---------|-------|-----------------|
| Workflow Suggestions | 890 | 3.2 |
| Email Composer | 650 | 4.8 |
| Smart Search | 420 | 2.1 |
| Lead Insights | 180 | 1.5 |

### AI Feature Impact

| Metric | AI Users | Non-AI Users | Lift |
|--------|----------|--------------|------|
| Workflows Created | 12.4 | 6.2 | +100% |
| Session Duration | 12.3 min | 7.1 min | +73% |
| 30-day Retention | 92% | 78% | +14pp |
| NPS | 52 | 34 | +18 |

**Key Insight**: AI users are 2x more engaged and retain 14% better.

### AI Generation Quality

| Metric | Value |
|--------|-------|
| Suggestions Accepted | 68% |
| Emails Sent (unedited) | 42% |
| Avg Edits per Email | 2.3 |
| User Satisfaction | 4.2/5 |

---

## Dashboard & Reporting

### Dashboard Usage

| Behavior | Users | % |
|----------|-------|---|
| View Default Dashboard | 5,445 | 45% |
| Customized Dashboard | 1,815 | 15% |
| Created Custom Reports | 847 | 7% |
| Never Viewed | 4,840 | 40% |

### Most Viewed Widgets

| Widget | Views | Engagement |
|--------|-------|------------|
| Pipeline Overview | 45,230 | High |
| Workflow Performance | 38,920 | High |
| Recent Activity | 32,450 | Medium |
| Team Leaderboard | 18,340 | Medium |
| Revenue Forecast | 12,560 | Low |

### Report Exports

| Format | Exports/Month | Trend |
|--------|---------------|-------|
| CSV | 3,240 | ↑ 15% |
| PDF | 1,890 | ↑ 8% |
| Excel | 1,450 | → |

---

## Mobile/PWA Usage

### Mobile Metrics

| Metric | Value | vs Desktop |
|--------|-------|------------|
| Mobile Users | 968 | 8% of total |
| Sessions/Week | 1.8 | vs 4.2 |
| Session Duration | 3.2 min | vs 8.5 min |
| Features Used | 2.1 | vs 4.8 |

### Mobile Feature Usage

| Feature | Mobile | Desktop |
|---------|--------|---------|
| View Dashboards | 65% | 45% |
| Check Notifications | 78% | 32% |
| Create Workflow | 8% | 67% |
| Edit Workflow | 5% | 58% |
| CRM Sync | 2% | 34% |

**Insight**: Mobile is used for monitoring, not creation. Optimize for mobile viewing.

---

## User Journey Analysis

### First Week Behavior (Activated Users)

| Day | Primary Action | Completion |
|-----|----------------|------------|
| Day 1 | Sign up, explore | 100% |
| Day 2 | Connect CRM | 68% |
| Day 3 | Create first workflow | 82% |
| Day 4 | Run workflow | 75% |
| Day 5 | Review results | 70% |
| Day 6 | Create second workflow | 55% |
| Day 7 | Invite team member | 32% |

### Power User Behavior

Power users (top 10%) exhibit these patterns:

| Behavior | Power Users | Average |
|----------|-------------|---------|
| Workflows | 24+ | 8 |
| Daily logins | 5+ days/week | 2.3 days |
| Features used | 8+ | 3.8 |
| Team invites | 4+ | 0.8 |
| Templates created | 3+ | 0.2 |

### Churned User Patterns (30 days before)

| Signal | Churned | Retained |
|--------|---------|----------|
| Logins/week | 0.8 | 3.2 |
| Workflows run | 12 | 89 |
| Support tickets | 2.4 | 0.6 |
| Failed syncs | 8.2 | 1.1 |

---

## Recommendations

### Product Priorities

1. **Simplify CRM OAuth** - Biggest activation barrier
2. **Promote AI features** - Strongest retention signal
3. **Mobile optimization** - For dashboard viewing
4. **Template library expansion** - Drives activation

### UX Improvements

1. **Workflow success feedback** - Users unsure if working
2. **CRM sync status** - Unclear current state
3. **AI feature discovery** - Low awareness
4. **Mobile notifications** - Enable monitoring use case

### Experiments to Run

1. **AI-first onboarding** - Start with AI workflow suggestions
2. **CRM connect skip option** - Allow value before CRM
3. **Template recommendations** - Based on industry/role
4. **Gamification** - Progress tracking, achievements

---

*Report Date: January 2026*
*Owner: Product Analytics Team*
