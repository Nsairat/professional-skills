# Cloud Architecture Patterns

## Compute Patterns

### Container Orchestration (Kubernetes)

**When to Use**
- Multiple microservices
- Need for auto-scaling
- Complex deployment requirements
- Multi-cloud portability desired

**Architecture Components**
```
                    ┌─────────────────────────────────────────┐
                    │              Ingress Controller         │
                    └─────────────────┬───────────────────────┘
                                      │
        ┌─────────────────────────────┼─────────────────────────────┐
        │                             │                             │
   ┌────▼────┐                  ┌─────▼────┐                  ┌─────▼────┐
   │ Service │                  │ Service  │                  │ Service  │
   │    A    │                  │    B     │                  │    C     │
   └────┬────┘                  └────┬─────┘                  └────┬─────┘
        │                            │                             │
   ┌────▼────┐                  ┌────▼─────┐                  ┌────▼─────┐
   │  Pods   │                  │   Pods   │                  │   Pods   │
   └─────────┘                  └──────────┘                  └──────────┘
```

**Best Practices**
- Use namespaces for isolation
- Implement resource limits and requests
- Use liveness and readiness probes
- Implement pod disruption budgets
- Use horizontal pod autoscaler
- Externalize configuration (ConfigMaps, Secrets)

---

### Serverless Architectures

**Event-Driven Pattern**
```
Event Source → Function → Output
     │              │
     ▼              ▼
[API Gateway]  [Transform/Process]  → [Database]
[S3 Upload]                         → [Queue]
[Database]                          → [Notification]
[Schedule]                          → [Another Function]
```

**Fan-Out Pattern**
```
                    ┌─────────────┐
                    │   SNS/      │
Event ────────────► │  EventBridge├──────┬──────┬──────┐
                    └─────────────┘      │      │      │
                                         ▼      ▼      ▼
                                     [Lambda][Lambda][Lambda]
                                         │      │      │
                                         ▼      ▼      ▼
                                     [DynamoDB][S3][SQS]
```

**Saga Pattern for Distributed Transactions**
```
Step Functions / Temporal Workflow:

┌─────────┐    ┌─────────┐    ┌─────────┐    ┌─────────┐
│ Create  │───►│ Reserve │───►│ Process │───►│ Complete│
│ Order   │    │ Inventory│   │ Payment │    │ Order   │
└────┬────┘    └────┬────┘    └────┬────┘    └─────────┘
     │              │              │
     ▼              ▼              ▼
[Compensate]   [Compensate]   [Compensate]
(Cancel Order) (Release Inv)  (Refund)
```

---

### Hybrid Cloud Patterns

**Cloud Bursting**
- On-premises handles baseline load
- Cloud handles peak demand
- Requires consistent networking
- Data sync considerations

**Tiered Deployment**
- Development/Test in cloud
- Production on-premises
- Or vice versa based on requirements

**Edge + Cloud**
```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│  Edge       │     │  Regional   │     │  Central    │
│  Location   │────►│  Cloud      │────►│  Cloud      │
│             │     │             │     │             │
│ - Latency   │     │ - Process   │     │ - Analytics │
│ - Filtering │     │ - Aggregate │     │ - ML Train  │
│ - Cache     │     │ - Store     │     │ - Archive   │
└─────────────┘     └─────────────┘     └─────────────┘
```

---

## Networking Patterns

### Hub-and-Spoke Network

```
                    ┌─────────────────┐
                    │    Hub VPC      │
                    │                 │
                    │  - Firewall     │
                    │  - DNS          │
                    │  - VPN Gateway  │
                    │  - Transit      │
                    └────────┬────────┘
                             │
        ┌────────────────────┼────────────────────┐
        │                    │                    │
   ┌────▼────┐         ┌─────▼────┐         ┌────▼────┐
   │ Spoke 1 │         │ Spoke 2  │         │ Spoke 3 │
   │ (Prod)  │         │ (Dev)    │         │ (Data)  │
   └─────────┘         └──────────┘         └─────────┘
```

**Benefits**
- Centralized security and monitoring
- Simplified connectivity management
- Cost-efficient shared services
- Clear network segmentation

---

### Service Mesh

```
┌─────────────────────────────────────────────────────────┐
│                    Control Plane                        │
│  (Config, Discovery, Certificates, Policies)            │
└─────────────────────────────────────────────────────────┘
                            │
        ┌───────────────────┼───────────────────┐
        │                   │                   │
   ┌────▼────┐         ┌────▼────┐         ┌────▼────┐
   │ Service │         │ Service │         │ Service │
   │┌───────┐│         │┌───────┐│         │┌───────┐│
   ││ Proxy ││◄───────►││ Proxy ││◄───────►││ Proxy ││
   │└───────┘│         │└───────┘│         │└───────┘│
   └─────────┘         └─────────┘         └─────────┘
```

**When to Use**
- Many microservices (>10-15)
- Need mTLS between services
- Complex traffic management
- Distributed tracing required
- Team has operational expertise

**When to Avoid**
- Few services
- Simple communication patterns
- Limited operational capacity
- Latency-critical applications

---

## Data Patterns

### CQRS (Command Query Responsibility Segregation)

```
                    ┌─────────────┐
                    │   Client    │
                    └──────┬──────┘
                           │
              ┌────────────┴────────────┐
              │                         │
         ┌────▼────┐              ┌─────▼────┐
         │ Command │              │  Query   │
         │ Service │              │ Service  │
         └────┬────┘              └─────┬────┘
              │                         │
         ┌────▼────┐              ┌─────▼────┐
         │ Write   │──────────────│  Read    │
         │ Database│   Sync/CDC   │ Database │
         └─────────┘              └──────────┘
```

**When to Use**
- Different read/write scaling needs
- Complex read queries
- Event sourcing systems
- High-performance read requirements

---

### Event Sourcing

```
┌─────────┐     ┌─────────────────┐     ┌─────────────┐
│ Command │────►│  Event Store    │────►│ Projections │
└─────────┘     │                 │     │             │
                │ [OrderCreated]  │     │ [Order View]│
                │ [ItemAdded]     │     │ [Analytics] │
                │ [OrderShipped]  │     │ [Search]    │
                └─────────────────┘     └─────────────┘
```

**Benefits**
- Complete audit trail
- Temporal queries (state at any point)
- Event replay for debugging
- Natural fit for event-driven systems

**Challenges**
- Schema evolution complexity
- Event store scaling
- Learning curve
- Eventual consistency

---

### Data Lake Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                        Data Sources                              │
│  [Databases] [APIs] [Files] [Streams] [IoT] [SaaS]              │
└─────────────────────────────┬───────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                      Ingestion Layer                             │
│  [Batch: Airflow, Glue] [Stream: Kafka, Kinesis] [CDC: Debezium]│
└─────────────────────────────┬───────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                      Storage Layer (S3/ADLS/GCS)                 │
│  ┌─────────┐    ┌──────────┐    ┌───────────┐                   │
│  │  Raw    │───►│ Curated  │───►│ Enriched  │                   │
│  │ (Bronze)│    │ (Silver) │    │  (Gold)   │                   │
│  └─────────┘    └──────────┘    └───────────┘                   │
└─────────────────────────────┬───────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Consumption Layer                             │
│  [SQL: Athena, Presto] [BI: Tableau, Looker] [ML: SageMaker]    │
└─────────────────────────────────────────────────────────────────┘
```

---

## Resilience Patterns

### Circuit Breaker States

```
        ┌──────────────────────────────────────┐
        │                                      │
        ▼                                      │
   ┌─────────┐    Failures > Threshold    ┌───┴────┐
   │ CLOSED  │ ─────────────────────────► │  OPEN  │
   │(Normal) │                            │(Reject)│
   └─────────┘                            └───┬────┘
        ▲                                     │
        │                                     │ Timeout
        │         Success                     ▼
        │    ◄──────────────────────── ┌───────────┐
        │                              │HALF-OPEN  │
        └─────────────────────────────│(Test)     │
              Failure                  └───────────┘
```

### Bulkhead Pattern

```
┌─────────────────────────────────────────────────────┐
│                    Application                       │
│                                                      │
│  ┌──────────────┐  ┌──────────────┐  ┌────────────┐│
│  │ Connection   │  │ Connection   │  │ Connection ││
│  │ Pool A       │  │ Pool B       │  │ Pool C     ││
│  │ (Critical)   │  │ (Standard)   │  │ (Batch)    ││
│  │ [10 conn]    │  │ [5 conn]     │  │ [3 conn]   ││
│  └──────┬───────┘  └──────┬───────┘  └──────┬─────┘│
│         │                 │                 │       │
└─────────┼─────────────────┼─────────────────┼───────┘
          │                 │                 │
          ▼                 ▼                 ▼
    [Critical DB]     [Standard DB]     [Batch DB]
```

### Retry with Exponential Backoff

```
Attempt 1: Immediate
     │
     ▼ Fail
Attempt 2: Wait 1s + jitter
     │
     ▼ Fail
Attempt 3: Wait 2s + jitter
     │
     ▼ Fail
Attempt 4: Wait 4s + jitter
     │
     ▼ Fail
Attempt 5: Wait 8s + jitter
     │
     ▼ Fail
Give Up: Return error to caller
```

**Jitter Formula**: `delay = base_delay * 2^attempt + random(0, 1000ms)`

---

## Security Patterns

### API Security Layers

```
┌─────────────────────────────────────────────────────────┐
│                     Internet                             │
└────────────────────────┬────────────────────────────────┘
                         │
┌────────────────────────▼────────────────────────────────┐
│ Layer 1: Edge Protection                                 │
│ [DDoS Protection] [WAF] [Bot Detection] [Rate Limiting] │
└────────────────────────┬────────────────────────────────┘
                         │
┌────────────────────────▼────────────────────────────────┐
│ Layer 2: API Gateway                                     │
│ [Authentication] [Authorization] [Throttling] [Logging] │
└────────────────────────┬────────────────────────────────┘
                         │
┌────────────────────────▼────────────────────────────────┐
│ Layer 3: Application                                     │
│ [Input Validation] [Business Logic] [Output Encoding]   │
└────────────────────────┬────────────────────────────────┘
                         │
┌────────────────────────▼────────────────────────────────┐
│ Layer 4: Data                                            │
│ [Encryption] [Access Control] [Audit Logging]           │
└─────────────────────────────────────────────────────────┘
```

### Secrets Management Flow

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│ Application │────►│   Vault/    │◄────│   Admin     │
│             │     │   Secrets   │     │             │
│ 1. Auth     │     │   Manager   │     │ - Rotate    │
│ 2. Request  │     │             │     │ - Audit     │
│ 3. Receive  │     │ - Encrypt   │     │ - Policy    │
│    Secret   │     │ - Audit     │     │             │
└─────────────┘     │ - Rotate    │     └─────────────┘
                    └─────────────┘
```
