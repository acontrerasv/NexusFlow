# API Gateway Service Documentation

> Central entry point for all NexusFlow API traffic.

## Overview

| Field | Value |
|-------|-------|
| **Service Name** | API Gateway |
| **Technology** | Kong + Custom Plugins |
| **Port** | 8000 (HTTP), 8443 (HTTPS) |
| **Owner** | Platform Team |
| **Repository** | nexusflow/gateway |

---

## Responsibilities

1. **Authentication** - Validate JWT tokens, API keys
2. **Rate Limiting** - Enforce usage limits by plan
3. **Routing** - Direct traffic to appropriate services
4. **Load Balancing** - Distribute load across instances
5. **Request/Response Transformation** - Header manipulation, CORS
6. **Logging** - Access logs, request tracing

---

## Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                        API GATEWAY                          │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────────────┐ │
│  │    Auth     │  │    Rate     │  │      Routing        │ │
│  │   Plugin    │  │   Limiter   │  │      Service        │ │
│  └──────┬──────┘  └──────┬──────┘  └──────────┬──────────┘ │
│         │                │                     │            │
│         └────────────────┼─────────────────────┘            │
│                          │                                  │
│                          ▼                                  │
│  ┌───────────────────────────────────────────────────────┐ │
│  │                    Kong Core                          │ │
│  │  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐  │ │
│  │  │ Plugins │  │ Routing │  │ Upstream│  │ Logging │  │ │
│  │  └─────────┘  └─────────┘  └─────────┘  └─────────┘  │ │
│  └───────────────────────────────────────────────────────┘ │
│                                                             │
└─────────────────────────────────────────────────────────────┘
                          │
         ┌────────────────┼────────────────┐
         ▼                ▼                ▼
   ┌──────────┐    ┌──────────┐    ┌──────────┐
   │   Core   │    │ Workflow │    │   Sync   │
   │ Service  │    │ Service  │    │ Service  │
   └──────────┘    └──────────┘    └──────────┘
```

---

## Authentication

### JWT Authentication

```yaml
# Kong JWT Plugin Configuration
plugins:
  - name: jwt
    config:
      claims_to_verify:
        - exp
        - iat
      key_claim_name: kid
      secret_is_base64: false
```

**JWT Structure**:
```json
{
  "header": {
    "alg": "RS256",
    "typ": "JWT",
    "kid": "key-001"
  },
  "payload": {
    "sub": "user-uuid",
    "org": "org-uuid",
    "role": "admin",
    "iat": 1704067200,
    "exp": 1704068100
  }
}
```

### API Key Authentication

```yaml
# For external API access
plugins:
  - name: key-auth
    config:
      key_names:
        - X-API-Key
        - apikey
      hide_credentials: true
```

---

## Rate Limiting

### Limits by Plan

| Plan | Requests/Min | Requests/Day | Burst |
|------|--------------|--------------|-------|
| Starter | 60 | 10,000 | 100 |
| Professional | 300 | 100,000 | 500 |
| Enterprise | 1,000 | Unlimited | 2,000 |

### Configuration

```yaml
plugins:
  - name: rate-limiting
    config:
      minute: 60
      day: 10000
      policy: redis
      fault_tolerant: true
      redis_host: redis.nexusflow.internal
      redis_port: 6379
```

### Rate Limit Headers

```
X-RateLimit-Limit: 60
X-RateLimit-Remaining: 45
X-RateLimit-Reset: 1704067260
```

---

## Routing

### Route Configuration

```yaml
services:
  - name: core-service
    url: http://core.nexusflow.internal:3001
    routes:
      - name: organizations
        paths: ["/api/v1/organizations"]
      - name: users
        paths: ["/api/v1/users"]
      - name: contacts
        paths: ["/api/v1/contacts"]

  - name: workflow-service
    url: http://workflow.nexusflow.internal:3002
    routes:
      - name: workflows
        paths: ["/api/v1/workflows"]

  - name: sync-service
    url: http://sync.nexusflow.internal:3003
    routes:
      - name: integrations
        paths: ["/api/v1/integrations"]
```

### Path Rewriting

```yaml
plugins:
  - name: request-transformer
    config:
      remove:
        headers:
          - X-Internal-Header
      add:
        headers:
          - "X-Request-ID:$(uuid)"
```

---

## API Versioning

### URL Versioning

```
/api/v1/workflows
/api/v2/workflows
```

### Version Support Policy

| Version | Status | EOL |
|---------|--------|-----|
| v1 | Current | - |
| v2 | Beta | - |

### Deprecation Headers

```
Deprecation: true
Sunset: Sat, 01 Jul 2026 00:00:00 GMT
Link: </api/v2/workflows>; rel="successor-version"
```

---

## Error Handling

### Error Response Format

```json
{
  "error": {
    "code": "RATE_LIMIT_EXCEEDED",
    "message": "Rate limit exceeded. Try again in 45 seconds.",
    "details": {
      "limit": 60,
      "reset_at": "2026-01-15T10:30:00Z"
    }
  },
  "request_id": "req-abc123"
}
```

### Error Codes

| HTTP | Code | Description |
|------|------|-------------|
| 400 | BAD_REQUEST | Invalid request format |
| 401 | UNAUTHORIZED | Missing or invalid auth |
| 403 | FORBIDDEN | Insufficient permissions |
| 404 | NOT_FOUND | Resource not found |
| 429 | RATE_LIMIT_EXCEEDED | Too many requests |
| 500 | INTERNAL_ERROR | Server error |
| 502 | BAD_GATEWAY | Upstream service error |
| 503 | SERVICE_UNAVAILABLE | Service temporarily unavailable |

---

## CORS Configuration

```yaml
plugins:
  - name: cors
    config:
      origins:
        - "https://app.nexusflow.io"
        - "https://*.nexusflow.io"
      methods:
        - GET
        - POST
        - PUT
        - PATCH
        - DELETE
        - OPTIONS
      headers:
        - Authorization
        - Content-Type
        - X-Request-ID
      exposed_headers:
        - X-RateLimit-Limit
        - X-RateLimit-Remaining
      credentials: true
      max_age: 3600
```

---

## Health Checks

### Gateway Health

```
GET /health
```

Response:
```json
{
  "status": "healthy",
  "version": "2.4.0",
  "uptime": 86400,
  "checks": {
    "redis": "healthy",
    "upstream_core": "healthy",
    "upstream_workflow": "healthy"
  }
}
```

### Upstream Health

```yaml
upstreams:
  - name: core-service
    healthchecks:
      active:
        healthy:
          interval: 5
          successes: 2
        unhealthy:
          interval: 5
          http_failures: 3
```

---

## Logging

### Access Log Format

```
{
  "timestamp": "2026-01-15T10:30:00.123Z",
  "request_id": "req-abc123",
  "client_ip": "192.168.1.1",
  "method": "GET",
  "path": "/api/v1/workflows",
  "status": 200,
  "latency_ms": 45,
  "user_id": "user-uuid",
  "org_id": "org-uuid",
  "upstream": "workflow-service",
  "upstream_latency_ms": 32
}
```

### Log Levels

| Level | Use Case |
|-------|----------|
| DEBUG | Development only |
| INFO | Normal operations |
| WARN | Recoverable issues |
| ERROR | Failures requiring attention |

---

## Metrics

### Key Metrics

| Metric | Description |
|--------|-------------|
| `gateway_requests_total` | Total request count |
| `gateway_request_duration_ms` | Request latency histogram |
| `gateway_upstream_latency_ms` | Upstream latency |
| `gateway_rate_limit_exceeded_total` | Rate limit hits |
| `gateway_auth_failures_total` | Auth failures |

### Prometheus Endpoint

```
GET /metrics
```

---

## Configuration

### Environment Variables

```bash
# Kong
KONG_DATABASE=postgres
KONG_PG_HOST=postgres.nexusflow.internal
KONG_PG_PORT=5432
KONG_PG_DATABASE=kong

# Redis (for rate limiting)
REDIS_HOST=redis.nexusflow.internal
REDIS_PORT=6379

# Logging
LOG_LEVEL=info
LOG_FORMAT=json

# Feature flags
ENABLE_API_V2=true
ENABLE_WEBSOCKETS=false
```

---

## Deployment

### Kubernetes Resources

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: api-gateway
  namespace: nexusflow
spec:
  replicas: 3
  selector:
    matchLabels:
      app: api-gateway
  template:
    spec:
      containers:
        - name: kong
          image: nexusflow/gateway:2.4.0
          ports:
            - containerPort: 8000
            - containerPort: 8443
          resources:
            requests:
              cpu: 500m
              memory: 512Mi
            limits:
              cpu: 2000m
              memory: 2Gi
```

---

## Troubleshooting

### Common Issues

| Issue | Cause | Solution |
|-------|-------|----------|
| 502 errors | Upstream down | Check service health |
| High latency | Rate limiting | Check Redis |
| Auth failures | Token expired | Refresh token |
| CORS errors | Missing origin | Update CORS config |

### Debug Mode

```bash
# Enable debug logging
kubectl set env deployment/api-gateway LOG_LEVEL=debug

# View logs
kubectl logs -f deployment/api-gateway
```

---

*Document Owner: Platform Team*
*Last Updated: January 2026*
