# Integration Patterns & API Design

## Enterprise Integration Patterns

### Messaging Patterns

#### Point-to-Point Channel
```
┌──────────┐     ┌─────────┐     ┌──────────┐
│ Producer │────►│  Queue  │────►│ Consumer │
└──────────┘     └─────────┘     └──────────┘

- One message, one consumer
- Load balancing across consumers
- Guaranteed delivery
- Use: Task distribution, work queues
```

#### Publish-Subscribe Channel
```
                              ┌──────────────┐
                         ┌───►│ Subscriber A │
┌──────────┐     ┌───────┴─┐  └──────────────┘
│ Publisher│────►│  Topic  │
└──────────┘     └───────┬─┘  ┌──────────────┐
                         └───►│ Subscriber B │
                              └──────────────┘

- One message, multiple consumers
- Decoupled producers and consumers
- Use: Events, notifications, fan-out
```

#### Dead Letter Queue
```
┌──────────┐     ┌─────────┐     ┌──────────┐
│ Producer │────►│  Queue  │────►│ Consumer │
└──────────┘     └────┬────┘     └────┬─────┘
                      │               │
                      │    Failed     │
                      │   Processing  │
                      │               │
                      ▼               │
                ┌─────────────┐       │
                │ Dead Letter │◄──────┘
                │    Queue    │
                └─────────────┘
                      │
                      ▼
                ┌─────────────┐
                │   Monitor   │
                │   & Alert   │
                └─────────────┘

- Capture failed messages
- Prevent message loss
- Enable investigation and replay
```

---

### Message Routing Patterns

#### Content-Based Router
```
                         ┌──────────────┐
                    ┌───►│  Handler A   │  (type = "order")
┌─────────┐   ┌─────┴──┐ └──────────────┘
│ Message │──►│ Router │
└─────────┘   └─────┬──┘ ┌──────────────┐
                    └───►│  Handler B   │  (type = "refund")
                         └──────────────┘
```

#### Message Filter
```
┌─────────┐     ┌────────┐     ┌──────────┐
│ All     │────►│ Filter │────►│ Matching │
│ Messages│     │        │     │ Messages │
└─────────┘     └────┬───┘     └──────────┘
                     │
                     ▼
                ┌─────────┐
                │ Discard │
                └─────────┘
```

#### Splitter & Aggregator
```
              Splitter                    Aggregator
┌─────────┐   ┌───────┐   ┌─────────┐   ┌───────┐   ┌─────────┐
│ Batch   │──►│ Split │──►│Process 1│──►│       │──►│Combined │
│ Message │   │       │   ├─────────┤   │Combine│   │ Result  │
└─────────┘   └───────┘   │Process 2│──►│       │   └─────────┘
                          ├─────────┤   └───────┘
                          │Process 3│──►
                          └─────────┘
```

---

### Transformation Patterns

#### Message Translator
```
┌─────────────┐     ┌────────────┐     ┌─────────────┐
│ Source      │────►│ Translator │────►│ Target      │
│ Format (A)  │     │            │     │ Format (B)  │
└─────────────┘     └────────────┘     └─────────────┘

Examples:
- XML to JSON
- v1 API to v2 API
- External format to internal canonical
```

#### Canonical Data Model
```
┌─────────┐                           ┌─────────┐
│System A │──┐                    ┌──►│System X │
└─────────┘  │    ┌───────────┐   │   └─────────┘
             ├───►│ Canonical │───┤
┌─────────┐  │    │   Model   │   │   ┌─────────┐
│System B │──┘    └───────────┘   └──►│System Y │
└─────────┘                           └─────────┘

Benefits:
- N transformations instead of N×M
- Single source of truth for data model
- Easier to add new systems
```

---

## API Design Patterns

### REST API Best Practices

**Resource Naming**
```
Good:
GET    /users                    # List users
GET    /users/{id}               # Get user
POST   /users                    # Create user
PUT    /users/{id}               # Replace user
PATCH  /users/{id}               # Update user
DELETE /users/{id}               # Delete user
GET    /users/{id}/orders        # User's orders

Avoid:
GET    /getUsers
POST   /createUser
GET    /users/list
POST   /users/{id}/delete
```

**Query Parameters**
```
# Pagination
GET /users?page=2&limit=20
GET /users?cursor=abc123&limit=20  # Cursor-based (preferred)

# Filtering
GET /users?status=active&role=admin

# Sorting
GET /users?sort=created_at:desc,name:asc

# Field selection
GET /users?fields=id,name,email

# Search
GET /users?q=john
```

**Response Structure**
```json
// Success (single resource)
{
  "data": {
    "id": "123",
    "type": "user",
    "attributes": { ... }
  }
}

// Success (collection)
{
  "data": [ ... ],
  "meta": {
    "total": 100,
    "page": 1,
    "limit": 20
  },
  "links": {
    "next": "/users?page=2",
    "prev": null
  }
}

// Error
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Invalid input",
    "details": [
      { "field": "email", "message": "Invalid email format" }
    ]
  }
}
```

---

### API Versioning Strategies

**URL Path Versioning** (Recommended)
```
GET /v1/users
GET /v2/users

Pros: Clear, cacheable, easy routing
Cons: URL pollution, breaks REST purists
```

**Header Versioning**
```
GET /users
Accept: application/vnd.api+json;version=2

Pros: Clean URLs
Cons: Hidden, harder to test, cache challenges
```

**Query Parameter**
```
GET /users?version=2

Pros: Easy to use
Cons: Optional feels wrong, cache key complexity
```

**Version Lifecycle**
```
┌─────────┐     ┌──────────┐     ┌────────────┐     ┌────────┐
│  Alpha  │────►│   Beta   │────►│   Stable   │────►│ Sunset │
│         │     │          │     │            │     │        │
│- Breaking│    │- Breaking│     │- No breaking│    │- Deprec│
│ changes │     │ possible │     │  changes   │     │ warning│
│ expected│     │          │     │- Bug fixes │     │- EOL   │
└─────────┘     └──────────┘     └────────────┘     └────────┘
```

---

### GraphQL Patterns

**Schema Design**
```graphql
type Query {
  user(id: ID!): User
  users(filter: UserFilter, pagination: Pagination): UserConnection!
}

type Mutation {
  createUser(input: CreateUserInput!): CreateUserPayload!
  updateUser(id: ID!, input: UpdateUserInput!): UpdateUserPayload!
}

type User {
  id: ID!
  email: String!
  orders(first: Int, after: String): OrderConnection!
}

# Relay-style pagination
type UserConnection {
  edges: [UserEdge!]!
  pageInfo: PageInfo!
  totalCount: Int!
}
```

**Performance Considerations**
```
# N+1 Problem: Use DataLoader
query {
  users {
    orders {      # Without DataLoader: N queries
      items {     # With DataLoader: Batched to 1 query
        product
      }
    }
  }
}

# Query Complexity Limiting
query {
  users {           # depth: 1, complexity: 10
    orders {        # depth: 2, complexity: 50
      items {       # depth: 3, complexity: 100
        product {   # depth: 4, complexity: 200 (LIMIT!)
          reviews
        }
      }
    }
  }
}
```

---

### gRPC Patterns

**Service Definition**
```protobuf
syntax = "proto3";

service UserService {
  // Unary
  rpc GetUser(GetUserRequest) returns (User);
  
  // Server streaming
  rpc ListUsers(ListUsersRequest) returns (stream User);
  
  // Client streaming
  rpc CreateUsers(stream CreateUserRequest) returns (CreateUsersResponse);
  
  // Bidirectional streaming
  rpc Chat(stream ChatMessage) returns (stream ChatMessage);
}

message User {
  string id = 1;
  string email = 2;
  google.protobuf.Timestamp created_at = 3;
}
```

**When to Use**
- Internal service-to-service communication
- High performance requirements
- Streaming data
- Strong typing needed
- Polyglot environments

---

## Async Communication Patterns

### Saga Pattern

**Choreography (Event-Driven)**
```
┌─────────┐    OrderCreated    ┌───────────┐    InventoryReserved    ┌─────────┐
│  Order  │──────────────────►│ Inventory │─────────────────────────►│ Payment │
│ Service │                    │  Service  │                         │ Service │
└────┬────┘                    └─────┬─────┘                         └────┬────┘
     │                               │                                    │
     │◄──────OrderCompleted──────────┼◄───────PaymentProcessed───────────┘
     │                               │
     │◄──────OrderFailed─────────────┼◄───────PaymentFailed
                                     │
                                     └────────InventoryReleased
```

**Orchestration (Coordinator)**
```
                    ┌─────────────┐
              ┌────►│   Order     │◄────┐
              │     │ Orchestrator│     │
              │     └──────┬──────┘     │
              │            │            │
         Response      Commands     Response
              │            │            │
     ┌────────┴──┐    ┌───┴────┐    ┌──┴────────┐
     │  Order    │    │Inventory│   │  Payment  │
     │  Service  │    │ Service │   │  Service  │
     └───────────┘    └─────────┘   └───────────┘
```

**Choreography vs Orchestration**

| Aspect | Choreography | Orchestration |
|--------|--------------|---------------|
| Coupling | Loose | Tighter to orchestrator |
| Visibility | Distributed, harder to trace | Centralized, easier to monitor |
| Complexity | Grows with services | Contained in orchestrator |
| Single point of failure | No | Yes (orchestrator) |
| Best for | Simple flows | Complex, long-running flows |

---

### Event-Driven Architecture

**Event Types**
```
1. Domain Events (Business facts)
   - OrderPlaced, PaymentReceived, UserRegistered
   - Immutable, past tense
   
2. Integration Events (Cross-service)
   - Published to message broker
   - Versioned schema
   
3. Event Notifications (Lightweight)
   - Signal that something happened
   - Consumer fetches details if needed
```

**Event Schema**
```json
{
  "eventId": "uuid",
  "eventType": "OrderPlaced",
  "eventVersion": "1.0",
  "timestamp": "2024-01-15T10:30:00Z",
  "source": "order-service",
  "correlationId": "request-uuid",
  "data": {
    "orderId": "12345",
    "customerId": "67890",
    "totalAmount": 99.99
  },
  "metadata": {
    "userId": "user-123",
    "traceId": "trace-abc"
  }
}
```

---

## Integration Platform Comparison

### iPaaS (MuleSoft, Dell Boomi, Workato)

**Best For**
- Complex enterprise integration
- Non-technical integration developers
- Pre-built connectors to SaaS apps
- B2B/EDI integrations

**Trade-offs**
- High licensing costs
- Vendor lock-in
- Learning curve for platform
- May be overkill for simple needs

---

### API Gateway (Kong, Apigee, AWS API Gateway)

**Capabilities**
- Authentication/Authorization
- Rate limiting and throttling
- Request/response transformation
- Caching
- Analytics and monitoring
- Developer portal

**Selection Criteria**

| Feature | Kong | Apigee | AWS API Gateway |
|---------|------|--------|-----------------|
| Deployment | Self-hosted/Cloud | Cloud | AWS only |
| Extensibility | Plugins (Lua) | Policies | Lambda |
| Cost | Open source + Enterprise | Per-call pricing | Per-call + data |
| Best for | Flexibility | Enterprise features | AWS-native |

---

### Event Streaming (Kafka, Pulsar, Kinesis)

**Kafka Strengths**
- High throughput
- Strong ordering guarantees
- Mature ecosystem
- Long retention

**Pulsar Strengths**
- Multi-tenancy
- Tiered storage
- Geo-replication
- Functions built-in

**Kinesis Strengths**
- AWS-native
- Serverless option (Data Streams)
- Easy scaling
- Integrated with AWS services

---

## Data Integration

### ETL vs ELT

**ETL (Extract, Transform, Load)**
```
┌────────┐     ┌───────────┐     ┌────────────┐
│ Source │────►│ Transform │────►│ Data       │
│        │     │ (ETL Tool)│     │ Warehouse  │
└────────┘     └───────────┘     └────────────┘

- Transform before loading
- Traditional approach
- Good for: Complex transformations, data quality enforcement
```

**ELT (Extract, Load, Transform)**
```
┌────────┐     ┌────────────┐     ┌───────────┐
│ Source │────►│ Data       │────►│ Transform │
│        │     │ Warehouse  │     │ (SQL/dbt) │
└────────┘     └────────────┘     └───────────┘

- Load raw, transform in warehouse
- Modern approach
- Good for: Cloud warehouses, flexible transformation, data lake
```

### Change Data Capture (CDC)

**Log-Based CDC**
```
┌──────────┐     ┌─────────┐     ┌──────────┐     ┌──────────┐
│ Database │────►│ Debezium│────►│  Kafka   │────►│  Target  │
│ (Source) │     │         │     │          │     │          │
└──────────┘     └─────────┘     └──────────┘     └──────────┘
            Read               Publish        Consume
         transaction            CDC           and apply
            logs              events
```

**Benefits**
- Real-time data sync
- No impact on source database
- Captures all changes (insert, update, delete)
- Maintains order of operations

**Considerations**
- Requires database log access
- Schema changes need handling
- Initial snapshot for new consumers
- Exactly-once delivery complexity
