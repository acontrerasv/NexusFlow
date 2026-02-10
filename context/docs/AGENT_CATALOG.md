# NexusFlow Agent Catalog

> Complete documentation of all AI agents available in the NexusFlow product repository.

## Overview

| Category | Count | Primary Use |
|----------|-------|-------------|
| Product & Strategy | 3 | Product planning, PRDs |
| Research & Analysis | 4 | Data, user research |
| Engineering | 5 | Technical work |
| Design | 1 | Visual and UX design |
| **Total** | **13** | - |

---

## Product & Strategy Agents

### AI Product Manager (`ai-pm`)

**Purpose**: General product management and strategic planning.

**Capabilities**:
- Strategic product planning
- Roadmap development
- Feature prioritization (RICE, ICE)
- OKR definition and tracking
- Stakeholder communication

**When to Use**:
- Planning roadmaps
- Prioritizing features
- Strategic decisions
- Cross-functional coordination

**Example Triggers**:
- "Help me prioritize these features"
- "What should we focus on this quarter?"
- "Create a roadmap for Q3"

**Location**: `.claude/agents/ai-pm.md`

---

### Product Manager (`product-manager`)

**Purpose**: PRD writing and feature specification.

**Capabilities**:
- Write complete PRDs
- Create problem briefs and JTBD
- Define user stories with acceptance criteria
- Ensure PRD compliance

**When to Use**:
- Writing new PRDs
- Documenting features
- Creating user stories
- Reviewing existing PRDs

**Example Triggers**:
- "Write a PRD for..."
- "Create user stories for..."
- "Document the requirements for..."

**Location**: `.claude/agents/product-manager.md`

---

### AI Product Marketing (`ai-product-marketing`)

**Purpose**: Product positioning, messaging, and go-to-market.

**Capabilities**:
- Develop positioning statements
- Create messaging frameworks
- Write value propositions
- Design launch plans
- Create competitive battle cards

**When to Use**:
- Launching new features
- Competitive positioning
- Marketing copy
- Sales enablement

**Example Triggers**:
- "Position this feature against competitors"
- "Write launch messaging for..."
- "Create a battle card for..."

**Location**: `.claude/agents/ai-product-marketing.md`

---

## Research & Analysis Agents

### AI User Researcher (`ai-user-researcher`)

**Purpose**: User research, interviews, and persona development.

**Capabilities**:
- Design research studies
- Create interview guides
- Analyze transcripts
- Create personas
- Map user journeys
- Generate JTBD frameworks

**When to Use**:
- Planning user research
- Analyzing feedback
- Creating personas
- Understanding user needs

**Example Triggers**:
- "Create an interview guide for..."
- "Analyze this user feedback"
- "Build a persona for..."

**Location**: `.claude/agents/ai-user-researcher.md`

---

### AI Data Analyst (`ai-data-analyst`)

**Purpose**: Data analysis, metrics, and dashboards.

**Capabilities**:
- Analyze product metrics
- Create cohort analyses
- Build dashboards (HTML/Chart.js)
- Perform churn analysis
- Identify trends and anomalies

**When to Use**:
- Analyzing metrics
- Building reports
- Understanding trends
- Creating visualizations

**Example Triggers**:
- "Analyze our churn data"
- "Create a dashboard for..."
- "What do the metrics show?"

**Location**: `.claude/agents/ai-data-analyst.md`

---

### Product Usage Analyst (`product-usage-analyst`)

**Purpose**: Deep analysis of product usage patterns.

**Capabilities**:
- Analyze feature adoption
- Track user behavior
- Identify power users and at-risk accounts
- Build engagement scoring
- Activation analysis

**When to Use**:
- Understanding feature adoption
- Identifying at-risk users
- Analyzing engagement
- Segmentation

**Example Triggers**:
- "Which features are underused?"
- "Who are our power users?"
- "Analyze activation funnel"

**Location**: `.claude/agents/product-usage-analyst.md`

---

### Competitive Benchmarking (`competitive-benchmarking`)

**Purpose**: Competitor analysis and market research.

**Capabilities**:
- Research competitors
- Create battle cards
- Identify feature gaps
- Track competitor pricing
- Win/loss analysis

**When to Use**:
- Competitive positioning
- Feature comparison
- Market analysis
- Sales support

**Example Triggers**:
- "How do we compare to FlowForce?"
- "Create a battle card for..."
- "What features are competitors shipping?"

**Location**: `.claude/agents/competitive-benchmarking.md`

---

## Engineering Agents

### AI Architect Engineer (`ai-architect-engineer`)

**Purpose**: System architecture and technical design.

**Capabilities**:
- Design system architectures
- Create technical specifications
- Design database schemas
- Plan API structures
- Document ADRs

**When to Use**:
- System design decisions
- API design
- Database modeling
- Technical specifications

**Example Triggers**:
- "Design the architecture for..."
- "How should we structure this API?"
- "Review this technical approach"

**Location**: `.claude/agents/ai-architect-engineer.md`

---

### AI Frontend Engineer (`ai-frontend-engineer`)

**Purpose**: Frontend development and UI implementation.

**Capabilities**:
- Build React/Next.js components
- Implement TailwindCSS designs
- Create interactive UIs
- Write frontend tests
- Performance optimization

**When to Use**:
- Building UI components
- Frontend implementation
- UI/UX coding
- Component library work

**Example Triggers**:
- "Create a component for..."
- "Implement this design in React"
- "Optimize this frontend code"

**Location**: `.claude/agents/ai-frontend-engineer.md`

---

### AI Data/ML Engineer (`ai-data-ml-engineer`)

**Purpose**: AI/ML feature development.

**Capabilities**:
- Design AI architectures
- Integrate LLM APIs
- Build RAG systems
- Develop prompt strategies
- Create evaluation frameworks

**When to Use**:
- AI feature development
- LLM integration
- ML pipeline work
- Prompt engineering

**Example Triggers**:
- "Implement AI suggestions for..."
- "Design the RAG pipeline"
- "Optimize this prompt"

**Location**: `.claude/agents/ai-data-ml-engineer.md`

---

### Architecture Guardian (`nexusflow-architecture-guardian`)

**Purpose**: Code review and architecture compliance.

**Capabilities**:
- Review architectural compliance
- Check coding standards
- Identify anti-patterns
- Security review
- Test coverage verification

**When to Use**:
- Code reviews
- Architecture validation
- Standards compliance
- PR reviews

**Example Triggers**:
- "Review this code"
- "Check architecture compliance"
- "Validate against standards"

**Location**: `.claude/agents/nexusflow-architecture-guardian.md`

---

### QA Expert (`qa-expert`)

**Purpose**: Quality assurance and testing.

**Capabilities**:
- Design test strategies
- Write test cases
- Create automation scripts
- Regression analysis
- Bug triage

**When to Use**:
- Test planning
- Writing test cases
- QA strategy
- Bug analysis

**Example Triggers**:
- "Create test cases for..."
- "Design the QA strategy"
- "What should we test?"

**Location**: `.claude/agents/qa-expert.md`

---

## Design Agents

### AI Product Designer (`ai-product-designer`)

**Purpose**: Product design, UX, and visual design.

**Capabilities**:
- Create user flows
- Design wireframes
- Define interaction patterns
- Create design specs
- Write UX copy

**When to Use**:
- UX design
- Wireframing
- Design specifications
- User flow design

**Example Triggers**:
- "Design the flow for..."
- "Create wireframes for..."
- "What's the best UX pattern?"

**Location**: `.claude/agents/ai-product-designer.md`

---

## Agent Selection Guide

### By Task Type

| Task | Primary Agent | Secondary |
|------|--------------|-----------|
| Write PRD | product-manager | ai-pm |
| Analyze data | ai-data-analyst | product-usage-analyst |
| User research | ai-user-researcher | - |
| Technical design | ai-architect-engineer | ai-frontend-engineer |
| Competitive analysis | competitive-benchmarking | ai-product-marketing |
| Code review | nexusflow-architecture-guardian | - |
| UI design | ai-product-designer | ai-frontend-engineer |
| AI features | ai-data-ml-engineer | - |
| Testing | qa-expert | - |
| Marketing | ai-product-marketing | - |

### By Question Type

| Question | Agent |
|----------|-------|
| "How should we prioritize?" | ai-pm |
| "What do users need?" | ai-user-researcher |
| "What do the metrics show?" | ai-data-analyst |
| "How do competitors do it?" | competitive-benchmarking |
| "How should we architect?" | ai-architect-engineer |
| "How should we design this UI?" | ai-product-designer |
| "What should we test?" | qa-expert |

---

## Agent Interactions

### Common Workflows

**Discovery → PRD**:
1. `ai-user-researcher` - Gather insights
2. `ai-data-analyst` - Validate with data
3. `competitive-benchmarking` - Market context
4. `product-manager` - Write PRD

**Feature Development**:
1. `product-manager` - Requirements
2. `ai-architect-engineer` - Technical design
3. `ai-frontend-engineer` - UI implementation
4. `qa-expert` - Test strategy

**Strategic Planning**:
1. `ai-data-analyst` - Metrics review
2. `competitive-benchmarking` - Market analysis
3. `ai-pm` - Strategy and priorities

---

*Last Updated: January 2026*
*See `.claude/SELECTION_RULES.md` for automatic selection logic*
