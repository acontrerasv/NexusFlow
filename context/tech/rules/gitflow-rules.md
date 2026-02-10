# Git Flow Rules

> Git workflow and branching strategy for NexusFlow development.

## Overview

NexusFlow uses a modified Git Flow with feature branches, release branches, and hotfixes. All changes go through pull requests with code review.

---

## Branch Strategy

### Branch Types

| Branch | Purpose | Base | Merges To |
|--------|---------|------|-----------|
| `main` | Production code | - | - |
| `develop` | Integration branch | main | main (via release) |
| `feature/*` | New features | develop | develop |
| `bugfix/*` | Bug fixes | develop | develop |
| `release/*` | Release preparation | develop | main + develop |
| `hotfix/*` | Production fixes | main | main + develop |

### Branch Naming

```
# Features
feature/ACT-123-smart-onboarding
feature/INT-456-crm-sync-v2

# Bugfixes
bugfix/ACT-789-oauth-redirect-loop

# Releases
release/v2.4.0

# Hotfixes
hotfix/v2.3.1-sync-timeout
```

---

## Workflow

### Feature Development

```bash
# 1. Create feature branch from develop
git checkout develop
git pull origin develop
git checkout -b feature/ACT-123-smart-onboarding

# 2. Make commits (see commit guidelines)
git add .
git commit -m "feat(onboarding): add role selection step"

# 3. Push and create PR
git push origin feature/ACT-123-smart-onboarding
# Create PR via GitHub

# 4. After approval, squash merge to develop
```

### Release Process

```bash
# 1. Create release branch
git checkout develop
git checkout -b release/v2.4.0

# 2. Version bump and changelog
npm version minor
# Update CHANGELOG.md

# 3. Final testing and fixes
git commit -m "chore: bump version to 2.4.0"

# 4. Merge to main
git checkout main
git merge --no-ff release/v2.4.0
git tag -a v2.4.0 -m "Release v2.4.0"
git push origin main --tags

# 5. Back-merge to develop
git checkout develop
git merge --no-ff release/v2.4.0
git push origin develop

# 6. Delete release branch
git branch -d release/v2.4.0
```

### Hotfix Process

```bash
# 1. Create hotfix from main
git checkout main
git checkout -b hotfix/v2.3.1-sync-timeout

# 2. Fix and commit
git commit -m "fix(sync): increase timeout for large datasets"

# 3. Merge to main
git checkout main
git merge --no-ff hotfix/v2.3.1-sync-timeout
git tag -a v2.3.1 -m "Hotfix v2.3.1"
git push origin main --tags

# 4. Back-merge to develop
git checkout develop
git merge --no-ff hotfix/v2.3.1-sync-timeout
git push origin develop
```

---

## Commit Guidelines

### Commit Message Format

```
<type>(<scope>): <subject>

[optional body]

[optional footer]
```

### Types

| Type | Description |
|------|-------------|
| `feat` | New feature |
| `fix` | Bug fix |
| `docs` | Documentation only |
| `style` | Formatting, no code change |
| `refactor` | Code change, no new feature or fix |
| `perf` | Performance improvement |
| `test` | Adding tests |
| `chore` | Build process, tooling |

### Scopes

| Scope | Area |
|-------|------|
| `onboarding` | Activation/onboarding |
| `workflow` | Workflow engine |
| `sync` | CRM sync |
| `ai` | AI features |
| `api` | API changes |
| `ui` | Frontend UI |
| `auth` | Authentication |
| `admin` | Admin features |

### Examples

```
feat(onboarding): add role selection during signup

- Added 4 role options: Sales Rep, Manager, Ops, Executive
- Roles are stored in user profile
- Dashboard customizes based on role

Closes ACT-123
```

```
fix(sync): handle null values in contact fields

Previously, null values from Salesforce caused sync failures.
Now we properly coalesce null to empty string.

Fixes INT-456
```

```
perf(workflow): reduce execution time by 40%

- Parallelized independent workflow steps
- Added caching for repeated lookups
- Optimized database queries

Before: 2.3s average
After: 1.4s average
```

---

## Pull Request Guidelines

### PR Title Format

```
[TEAM-XXX] Brief description of changes
```

Examples:
- `[ACT-123] Add role selection to onboarding`
- `[INT-456] Fix CRM sync timeout for large datasets`

### PR Description Template

```markdown
## Summary
Brief description of what this PR does.

## Changes
- Change 1
- Change 2
- Change 3

## Testing
- [ ] Unit tests added/updated
- [ ] Integration tests pass
- [ ] Manual testing completed

## Screenshots
If applicable, add screenshots.

## Related Issues
Closes #123
```

### PR Requirements

- [ ] Code review by 1+ team member
- [ ] All CI checks pass
- [ ] No merge conflicts
- [ ] Branch is up to date with base
- [ ] Tests pass locally

---

## Code Review Guidelines

### For Authors

1. Keep PRs small (< 400 lines when possible)
2. Self-review before requesting review
3. Respond to feedback promptly
4. Don't merge without approval

### For Reviewers

1. Review within 24 hours
2. Be constructive and specific
3. Distinguish between blocking and non-blocking feedback
4. Approve when ready (don't nitpick)

### Review Checklist

- [ ] Code is readable and maintainable
- [ ] Logic is correct
- [ ] Edge cases are handled
- [ ] Tests cover the changes
- [ ] No security vulnerabilities
- [ ] Performance is acceptable
- [ ] Documentation is updated

---

## CI/CD Pipeline

### On Pull Request

```yaml
# .github/workflows/pr.yml
jobs:
  lint:
    - ESLint
    - Prettier check
  test:
    - Unit tests
    - Integration tests
  build:
    - Type check
    - Build check
  preview:
    - Deploy preview environment
```

### On Merge to Develop

```yaml
jobs:
  deploy-staging:
    - Build Docker image
    - Push to registry
    - Deploy to staging
    - Run smoke tests
```

### On Merge to Main

```yaml
jobs:
  deploy-production:
    - Build Docker image
    - Push to registry
    - Deploy to production (canary)
    - Run smoke tests
    - Full rollout
    - Notify team
```

---

## Branch Protection

### Main Branch

- Require PR with 2 approvals
- Require status checks to pass
- Require linear history
- Do not allow force push
- Do not allow deletion

### Develop Branch

- Require PR with 1 approval
- Require status checks to pass
- Allow squash merge only

---

## Release Versioning

### Semantic Versioning

```
MAJOR.MINOR.PATCH

MAJOR - Breaking changes
MINOR - New features (backwards compatible)
PATCH - Bug fixes (backwards compatible)
```

### Version Examples

| Version | Reason |
|---------|--------|
| 2.0.0 | Breaking API changes |
| 2.1.0 | New AI Workflow Builder feature |
| 2.1.1 | Fix sync timeout bug |
| 2.2.0 | New Dashboard redesign |

---

## Emergency Procedures

### Rollback

```bash
# Revert to previous release
git checkout main
git revert --no-commit HEAD~1  # Or specific commit
git commit -m "revert: rollback v2.4.0 due to sync issues"
git push origin main

# Redeploy previous version
kubectl rollout undo deployment/nexusflow-api
```

### Hotfix Without Review

In critical production incidents:

1. Create hotfix branch
2. Make minimal fix
3. Get verbal approval from team lead
4. Merge with `[EMERGENCY]` tag
5. Create post-incident PR for review

---

*Document Owner: Engineering Team*
*Last Updated: January 2026*
