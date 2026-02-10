# MCP Configuration Guide

> Model Context Protocol configuration for NexusFlow AI tools.

## Overview

MCP (Model Context Protocol) enables structured communication between AI tools and external systems. This guide covers MCP configuration for NexusFlow's product repository.

---

## MCP Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                      Claude Code                             │
│                                                              │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │   Agents    │  │  Commands   │  │   Skills    │         │
│  └──────┬──────┘  └──────┬──────┘  └──────┬──────┘         │
│         │                │                │                  │
│         └────────────────┼────────────────┘                  │
│                          │                                   │
│                    ┌─────▼─────┐                            │
│                    │    MCP    │                            │
│                    │  Protocol │                            │
│                    └─────┬─────┘                            │
└──────────────────────────┼──────────────────────────────────┘
                           │
         ┌─────────────────┼─────────────────┐
         │                 │                 │
    ┌────▼────┐      ┌─────▼─────┐     ┌────▼────┐
    │  File   │      │    API    │     │  Data   │
    │ System  │      │  Gateway  │     │  Store  │
    └─────────┘      └───────────┘     └─────────┘
```

---

## Configuration Files

### Main Configuration

Location: `.claude/settings.json`

```json
{
  "mcp": {
    "enabled": true,
    "version": "1.0",
    "servers": [
      {
        "name": "nexusflow-api",
        "type": "http",
        "endpoint": "https://api.nexusflow.io/mcp",
        "auth": {
          "type": "bearer",
          "token_env": "NEXUSFLOW_API_TOKEN"
        }
      },
      {
        "name": "nexusflow-data",
        "type": "http",
        "endpoint": "https://data.nexusflow.io/mcp",
        "auth": {
          "type": "bearer",
          "token_env": "NEXUSFLOW_DATA_TOKEN"
        }
      }
    ],
    "tools": {
      "enabled": ["read", "write", "query", "analyze"],
      "disabled": ["delete", "admin"]
    },
    "resources": {
      "context": {
        "path": "context/",
        "writable": true
      },
      "prds": {
        "path": "context/prds/",
        "writable": true
      },
      "data": {
        "path": "context/data/",
        "writable": false
      }
    }
  }
}
```

---

## Available MCP Tools

### File Operations

| Tool | Description | Permission |
|------|-------------|------------|
| `read_file` | Read file content | Allowed |
| `write_file` | Write/create files | Allowed (context/) |
| `list_files` | List directory contents | Allowed |
| `search_files` | Search file contents | Allowed |

### Data Operations

| Tool | Description | Permission |
|------|-------------|------------|
| `query_metrics` | Query NexusFlow metrics | Allowed |
| `fetch_users` | Get user data | Allowed |
| `fetch_workflows` | Get workflow data | Allowed |
| `analyze_data` | Run analytics queries | Allowed |

### API Operations

| Tool | Description | Permission |
|------|-------------|------------|
| `api_get` | HTTP GET to NexusFlow API | Allowed |
| `api_post` | HTTP POST to NexusFlow API | Limited |

---

## Resource Configuration

### Context Resources

Resources automatically available to agents:

```yaml
resources:
  business_context:
    path: context/docs/BUSINESS_CONTEXT.md
    description: Company and product overview
    auto_load: true

  current_okrs:
    path: context/strategy/okr/2026/Q2-OKRS.md
    description: Current quarter OKRs
    auto_load: true

  service_index:
    path: context/docs/SERVICE_INDEX.md
    description: Service catalog
    auto_load: false

  templates:
    path: context/templates/
    description: Document templates
    auto_load: false
```

### Data Resources

Connection to live NexusFlow data:

```yaml
data_resources:
  metrics:
    endpoint: /mcp/metrics
    description: Product metrics
    refresh: hourly

  users:
    endpoint: /mcp/users
    description: User data
    refresh: daily

  workflows:
    endpoint: /mcp/workflows
    description: Workflow data
    refresh: realtime
```

---

## Authentication

### API Token Setup

1. Generate token in NexusFlow settings
2. Set environment variable:
   ```bash
   export NEXUSFLOW_API_TOKEN="your-token-here"
   ```

3. Or add to `.env`:
   ```
   NEXUSFLOW_API_TOKEN=your-token-here
   ```

### Token Permissions

| Permission | Description | Required For |
|------------|-------------|--------------|
| `read:metrics` | Read product metrics | ai-data-analyst |
| `read:users` | Read user data | ai-user-researcher |
| `read:workflows` | Read workflow data | product-usage-analyst |
| `write:docs` | Write documentation | product-manager |

---

## Tool Definitions

### Query Metrics Tool

```typescript
interface QueryMetricsTool {
  name: "query_metrics";
  description: "Query NexusFlow product metrics";
  parameters: {
    metric: string;      // Metric name
    period: string;      // Time period (7d, 30d, 90d)
    segment?: string;    // Optional segment filter
    compare?: boolean;   // Compare to previous period
  };
  returns: {
    value: number;
    previous?: number;
    change?: number;
    trend: "up" | "down" | "stable";
  };
}
```

### Analyze Data Tool

```typescript
interface AnalyzeDataTool {
  name: "analyze_data";
  description: "Run analytics query on NexusFlow data";
  parameters: {
    query_type: "funnel" | "cohort" | "segment" | "trend";
    metric: string;
    dimensions?: string[];
    filters?: Record<string, any>;
    period: string;
  };
  returns: {
    data: any[];
    summary: string;
    insights: string[];
  };
}
```

---

## Agent MCP Permissions

### ai-data-analyst

```yaml
permissions:
  tools:
    - query_metrics
    - analyze_data
    - read_file
  resources:
    - context/data/*
    - context/docs/BUSINESS_CONTEXT.md
```

### product-manager

```yaml
permissions:
  tools:
    - read_file
    - write_file
    - search_files
  resources:
    - context/prds/*
    - context/templates/*
    - context/docs/*
```

### ai-user-researcher

```yaml
permissions:
  tools:
    - read_file
    - search_files
    - fetch_users
  resources:
    - context/data/ux/*
    - context/data/insights/*
```

---

## Error Handling

### Common Errors

| Error | Cause | Resolution |
|-------|-------|------------|
| `AUTH_FAILED` | Invalid token | Regenerate API token |
| `PERMISSION_DENIED` | Insufficient permissions | Request additional scopes |
| `RATE_LIMITED` | Too many requests | Wait and retry |
| `RESOURCE_NOT_FOUND` | Path doesn't exist | Check resource path |
| `SERVER_ERROR` | MCP server issue | Check server status |

### Error Response Format

```json
{
  "error": {
    "code": "PERMISSION_DENIED",
    "message": "Token does not have read:users permission",
    "details": {
      "required": ["read:users"],
      "granted": ["read:metrics"]
    }
  }
}
```

---

## Monitoring

### MCP Metrics

| Metric | Description |
|--------|-------------|
| `mcp_requests_total` | Total MCP requests |
| `mcp_errors_total` | Total MCP errors |
| `mcp_latency_ms` | Request latency |
| `mcp_tokens_used` | Tokens consumed |

### Logging

MCP operations logged to:
- Console (development)
- Datadog (production)

Log format:
```json
{
  "timestamp": "2026-01-15T10:30:00Z",
  "tool": "query_metrics",
  "agent": "ai-data-analyst",
  "duration_ms": 245,
  "status": "success"
}
```

---

## Best Practices

### For Tool Usage

1. **Minimize API calls** - Cache when possible
2. **Use specific queries** - Don't fetch everything
3. **Handle errors gracefully** - Always check for errors
4. **Respect rate limits** - Implement backoff

### For Resource Access

1. **Use relative paths** - Keep paths portable
2. **Check existence first** - Before reading/writing
3. **Document dependencies** - Note required resources
4. **Version sensitive data** - Track data freshness

### For Security

1. **Never commit tokens** - Use environment variables
2. **Request minimal permissions** - Principle of least privilege
3. **Rotate tokens regularly** - Every 90 days
4. **Audit access logs** - Monitor for anomalies

---

## Troubleshooting

### Token Issues

```bash
# Verify token is set
echo $NEXUSFLOW_API_TOKEN

# Test token validity
curl -H "Authorization: Bearer $NEXUSFLOW_API_TOKEN" \
  https://api.nexusflow.io/mcp/health
```

### Connection Issues

```bash
# Check MCP server status
curl https://api.nexusflow.io/mcp/status

# Test specific tool
curl -X POST \
  -H "Authorization: Bearer $NEXUSFLOW_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"metric": "dau", "period": "7d"}' \
  https://api.nexusflow.io/mcp/tools/query_metrics
```

---

*Last Updated: January 2026*
*MCP Version: 1.0*
