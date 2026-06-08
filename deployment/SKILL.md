---
name: deployment
description: Manage deployment workflows, configurations, and procedures. Use this skill when the user asks to deploy an application, set up deployment pipelines, configure environments, manage releases, handle rollbacks, or document deployment procedures. Covers multi-environment strategies, containerization, CI/CD, and production readiness.
---

# Deployment

Manage deployment workflows with a focus on safety, repeatability, and clear documentation. Never guess deployment details - always confirm with the user or check existing documentation.

## When to use this skill

- User asks to deploy an application or service
- User asks to set up or modify deployment pipelines
- User asks about environments, releases, or rollbacks
- User asks to document deployment procedures
- User asks to troubleshoot deployment issues
- User asks about containerization, CI/CD, or infrastructure

## Core Principles

1. **Never guess**: If deployment details are unknown, document them as "Unknown" and ask the user
2. **Document everything**: Every deployment step, command, and configuration must be recorded
3. **Safety first**: Always have a rollback plan before deploying
4. **Repeatability**: Deployments should be automated and reproducible
5. **Environment parity**: Dev, staging, and production should be as similar as possible

## Deployment Workflow

### 1. Pre-Deployment Checklist

Before any deployment, verify:

- [ ] All tests pass
- [ ] CHANGELOG.md is updated
- [ ] HANDOVER.md reflects current state
- [ ] Database migrations are tested and reversible
- [ ] Environment variables are configured for target environment
- [ ] Secrets are managed securely (not hardcoded)
- [ ] Rollback plan is documented
- [ ] Monitoring and alerting are configured
- [ ] Health check endpoints are working
- [ ] Dependencies are up to date and secure

### 2. Environment Strategy

Maintain separate configurations for each environment:

```
environments/
├── development/
│   ├── .env
│   ├── docker-compose.yml
│   └── config.yml
├── staging/
│   ├── .env
│   ├── docker-compose.yml
│   └── config.yml
└── production/
    ├── .env
    ├── docker-compose.yml
    ── config.yml
```

Rules:
- Never commit production secrets to version control
- Use environment-specific config files
- Document all environment differences in DEPLOYMENT.md
- Staging should mirror production as closely as possible

### 3. Deployment Methods

#### Container-Based (Docker)

```dockerfile
# Multi-stage build example
FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY . .
RUN npm run build

FROM node:18-alpine
WORKDIR /app
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/node_modules ./node_modules
USER node
EXPOSE 3000
HEALTHCHECK --interval=30s CMD wget -qO- http://localhost:3000/health || exit 1
CMD ["node", "dist/main.js"]
```

Best practices:
- Use multi-stage builds to minimize image size
- Run as non-root user
- Include health checks
- Pin base image versions
- Use `.dockerignore` to exclude unnecessary files

#### CI/CD Pipeline

Example GitHub Actions structure:

```yaml
name: Deploy
on:
  push:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: npm ci && npm test

  deploy-staging:
    needs: test
    runs-on: ubuntu-latest
    environment: staging
    steps:
      - uses: actions/checkout@v4
      - run: ./scripts/deploy.sh staging

  deploy-production:
    needs: deploy-staging
    runs-on: ubuntu-latest
    environment: production
    steps:
      - uses: actions/checkout@v4
      - run: ./scripts/deploy.sh production
```

#### Manual Deployment

When automation is not available, document every step:

```markdown
## Manual Deployment Steps

1. SSH into server: `ssh user@host`
2. Pull latest code: `cd /app && git pull origin main`
3. Install dependencies: `npm ci --production`
4. Run migrations: `npm run migrate`
5. Build application: `npm run build`
6. Restart service: `sudo systemctl restart app`
7. Verify health: `curl http://localhost:3000/health`
```

### 4. Rollback Procedures

Every deployment must have a documented rollback:

```markdown
## Rollback Plan

### Quick Rollback (last known good)
1. `git checkout <previous-tag>`
2. `npm run build`
3. `sudo systemctl restart app`

### Database Rollback
1. Run reverse migration: `npm run migrate:down`
2. Verify data integrity
3. Restart application

### Full Rollback
1. Restore from backup: `./scripts/restore.sh <backup-date>`
2. Verify database state
3. Deploy previous version
4. Run smoke tests
```

### 5. Monitoring & Health Checks

Configure:

- **Health endpoint**: `/health` returning 200 when healthy
- **Readiness probe**: Checks dependencies (DB, cache, external APIs)
- **Metrics**: Request rate, error rate, latency, resource usage
- **Alerts**: Error rate threshold, high latency, resource exhaustion
- **Logs**: Structured logging with correlation IDs

### 6. Security Considerations

- Store secrets in environment variables or secret managers (not in code)
- Use TLS for all external communication
- Implement rate limiting on public endpoints
- Run containers as non-root
- Keep base images updated
- Scan dependencies for vulnerabilities before deployment
- Use network policies to restrict traffic
- Implement proper CORS headers

## Documentation Requirements

Update DEPLOYMENT.md with:

- Server/device names and roles
- IP addresses or hostnames
- File paths for application code, configs, logs
- Service names and management commands (start/stop/restart)
- Port mappings
- Domain names and DNS configuration
- Environment variable locations
- Backup procedures and schedules
- Rollback procedures
- Troubleshooting guide with common issues and fixes

## Troubleshooting Common Issues

| Issue | Check | Fix |
|-------|-------|-----|
| Service won't start | Logs, port conflicts, permissions | Check `journalctl -u service`, verify port availability |
| High memory usage | Process list, memory leaks | Restart service, profile application |
| Database connection failed | Credentials, network, DB status | Verify env vars, check DB is running |
| Slow response times | Resource usage, query performance | Check CPU/memory, optimize queries, add caching |
| Deployment failed | CI/CD logs, permissions | Check pipeline logs, verify deploy credentials |
