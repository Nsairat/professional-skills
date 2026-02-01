# DevOps & Operational Excellence

## CI/CD Pipeline Design

### Pipeline Stages

```
Code → Build → Test → Security → Artifact → Deploy (Dev) → Deploy (Staging) → Deploy (Prod)
```

**Stage Details**:

| Stage | Duration Target | Actions |
|-------|-----------------|---------|
| Build | <5 min | Compile, dependency resolution, Docker build |
| Unit Tests | <10 min | Fast, isolated tests |
| Integration Tests | <15 min | Service integration, database tests |
| Security Scan | <10 min | SAST, dependency scan, secrets detection |
| Artifact | <5 min | Push to registry, tag with version |
| Deploy Dev | <10 min | Auto-deploy on merge to main |
| Deploy Staging | <10 min | Auto-deploy, smoke tests |
| Deploy Prod | <30 min | Manual approval, canary, full rollout |

### Deployment Strategies

**Rolling Deployment**:
- Gradual replacement of instances
- Zero downtime if health checks pass
- Slower rollback (must re-deploy)
- Simple to implement

**Blue-Green Deployment**:
- Two identical environments
- Switch traffic instantly
- Fast rollback (switch back)
- Higher infrastructure cost

**Canary Deployment**:
- Route small % to new version
- Monitor error rates and latency
- Gradual traffic increase
- Fast rollback (route to stable)

**Feature Flags**:
- Deploy code, enable later
- Per-user or percentage rollout
- Instant kill switch
- A/B testing capability
- Tools: LaunchDarkly, Split, Flagsmith

---

### Testing Strategy

**Test Pyramid**:
```
           /\
          /  \  E2E Tests (few, slow)
         /----\
        /      \ Integration Tests (moderate)
       /--------\
      /          \ Unit Tests (many, fast)
     --------------
```

**Unit Tests**:
- Target: 80%+ code coverage
- Fast: <1ms per test
- Isolated: No external dependencies
- Run: Every commit

**Integration Tests**:
- Test service boundaries
- Use test containers or mocks
- Run: Every PR, pre-deploy

**End-to-End Tests**:
- Critical user journeys only
- Flaky-test management strategy
- Run: Pre-production deploy

**Contract Tests**:
- API compatibility between services
- Consumer-driven contracts (Pact)
- Run: On API changes

**Load Tests**:
- Baseline performance metrics
- Stress and soak testing
- Run: Weekly or pre-major release

---

## Observability Stack

### Three Pillars

**Logs**:
- Structured logging (JSON format)
- Correlation IDs across services
- Log levels: DEBUG, INFO, WARN, ERROR
- Centralized aggregation (ELK, Datadog, Splunk)
- Retention policy by environment

**Metrics**:
- USE method: Utilization, Saturation, Errors
- RED method: Rate, Errors, Duration
- Custom business metrics
- Tools: Prometheus + Grafana, Datadog, CloudWatch

**Traces**:
- Distributed tracing across services
- Span context propagation
- Latency breakdown analysis
- Tools: Jaeger, Zipkin, Datadog APM, X-Ray

### Key Metrics to Monitor

**Infrastructure**:
- CPU utilization (target: <70% sustained)
- Memory usage
- Disk I/O and space
- Network throughput and errors

**Application**:
- Request rate (RPS)
- Error rate (target: <0.1%)
- Latency percentiles (p50, p95, p99)
- Queue depths

**Business**:
- Conversion rates
- Revenue per minute
- User signups
- Feature adoption

### Alerting Philosophy

**Alert Fatigue Prevention**:
- Alert on symptoms, not causes
- Page only for customer impact
- Use warning thresholds for early detection
- Aggregate related alerts
- Regular alert review and pruning

**Runbooks**:
- Every alert has a runbook
- Document: What triggered, why it matters, how to fix
- Keep runbooks updated after incidents
- Link from alert to runbook

---

## SRE Practices

### Service Level Objectives (SLOs)

**SLI Examples**:
- Availability: % of successful requests
- Latency: % of requests under threshold
- Throughput: Requests per second capacity
- Correctness: % of correct results

**SLO Template**:
```
99.9% of requests will complete successfully within 200ms,
measured over a 30-day rolling window.
```

**Error Budget**:
- Budget = 100% - SLO (e.g., 0.1% for 99.9% SLO)
- Track consumption over time
- Freeze features when budget exhausted
- Prioritize reliability work

### On-Call Practices

**Rotation Design**:
- Primary and secondary on-call
- Follow-the-sun for global teams
- 1 week rotations (avoid burnout)
- Handoff documentation required

**On-Call Expectations**:
- Response time: <15 min for pages
- Laptop and connectivity always available
- Escalation after 30 min if stuck
- Compensatory time off after incidents

**Reducing On-Call Burden**:
- Fix causes, not just symptoms
- Automate remediation where possible
- Improve alerting signal-to-noise
- Regular postmortem review

### Postmortem Process

**Timeline**:
- Incident closed: Document preliminary timeline
- +24 hours: Draft postmortem
- +48 hours: Review meeting
- +1 week: Action items assigned and prioritized

**Template Sections**:
1. Summary (1-2 sentences)
2. Impact (customers affected, duration)
3. Timeline (what happened when)
4. Root cause analysis
5. Contributing factors
6. What went well
7. What could be improved
8. Action items (owner, due date)

**Blameless Culture**:
- Focus on systems, not individuals
- "What" failed, not "who" failed
- Safe to admit mistakes
- Celebrate thorough analysis

---

## Cloud Cost Optimization

### Cost Visibility

**Tagging Strategy**:
- Required tags: team, service, environment, cost-center
- Enforce via policy (deny untagged resources)
- Regular tag compliance audits

**Cost Allocation**:
- Chargeback to teams/products
- Monthly cost reviews
- Anomaly detection and alerts
- Forecast vs actual tracking

### Optimization Levers

**Compute**:
- Right-sizing (most instances oversized)
- Reserved instances for stable workloads (30-60% savings)
- Spot instances for fault-tolerant workloads (70-90% savings)
- Auto-scaling tuned to actual demand
- Shutdown non-production nights/weekends

**Storage**:
- Lifecycle policies (move to cold storage)
- Delete unused snapshots and volumes
- Compression where applicable
- Right-size provisioned IOPS

**Data Transfer**:
- Keep traffic within AZ/region
- Use VPC endpoints
- CDN for static assets
- Compress API responses

**Database**:
- Right-size instance types
- Reserved capacity for production
- Read replicas only if needed
- Archive old data

### Cost Governance

**Budget Controls**:
- Set budget alerts by team/service
- Approval workflow for expensive resources
- Regular spend reviews with engineering leaders

**FinOps Practice**:
- Dedicated cost optimization owner
- Engineering awareness training
- Gamification (leaderboards, savings goals)
- Cost as architecture decision factor

---

## Disaster Recovery

### Recovery Objectives

**RTO (Recovery Time Objective)**:
- Time to restore service after disaster
- Drives backup/failover architecture
- Business criticality determines target

**RPO (Recovery Point Objective)**:
- Maximum acceptable data loss
- Drives backup frequency
- Near-zero RPO requires real-time replication

### DR Strategies

| Strategy | RTO | RPO | Cost |
|----------|-----|-----|------|
| Backup/Restore | Hours | Hours | $ |
| Pilot Light | 10-30 min | Minutes | $$ |
| Warm Standby | Minutes | Seconds | $$$ |
| Active-Active | Near-zero | Near-zero | $$$$ |

### DR Testing

**Tabletop Exercise**:
- Walk through scenarios verbally
- Identify gaps in documentation
- Quarterly for critical systems

**Functional Test**:
- Actually failover non-critical systems
- Validate runbooks work
- Semi-annually

**Full DR Test**:
- Failover production to DR site
- Complete customer traffic handling
- Annually for regulated industries

### Backup Practices

- 3-2-1 rule: 3 copies, 2 media types, 1 offsite
- Automated backup verification
- Regular restore testing
- Encryption at rest
- Immutable backups (ransomware protection)
- Cross-region replication for critical data
