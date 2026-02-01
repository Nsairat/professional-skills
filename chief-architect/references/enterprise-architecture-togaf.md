# Enterprise Architecture & TOGAF

## TOGAF 10 Overview

### Architecture Development Method (ADM) Phases

#### Preliminary Phase
**Purpose**: Establish architecture capability

**Key Activities**
- Define architecture principles
- Identify stakeholders
- Establish architecture governance
- Select tools and frameworks
- Define architecture repository structure

**Deliverables**
- Architecture Principles Catalog
- Organization Model for EA
- Tailored Architecture Framework
- Architecture Repository Structure

---

#### Phase A: Architecture Vision

**Purpose**: Establish scope and obtain approval

**Key Activities**
- Identify stakeholders and concerns
- Confirm business goals and drivers
- Define scope and constraints
- Develop Architecture Vision
- Obtain approval to proceed

**Deliverables**
- Stakeholder Map
- Architecture Vision Document
- Statement of Architecture Work
- Business Scenario Documentation

**Vision Document Template**
```
1. Executive Summary
2. Business Context
   - Business goals and objectives
   - Business drivers
   - Business constraints
3. Scope
   - In scope / Out of scope
   - Stakeholders
   - Architecture domains
4. Vision Statement
   - Target state description
   - Value proposition
5. Risks and Mitigations
6. High-Level Roadmap
7. Approval and Sign-off
```

---

#### Phase B: Business Architecture

**Purpose**: Develop target Business Architecture

**Key Activities**
- Develop baseline Business Architecture
- Develop target Business Architecture
- Perform gap analysis
- Define roadmap components

**Deliverables**
- Business Capability Map
- Value Stream Map
- Organization Map
- Business Process Models
- Gap Analysis Report

**Business Capability Model**
```
Level 0: Enterprise
├── Level 1: Strategic Capabilities
│   ├── Level 2: Business Capabilities
│   │   ├── Level 3: Component Capabilities
│   │   │   └── Level 4: Detailed Capabilities
```

**Example Capability Map**
```
┌─────────────────────────────────────────────────────────────────┐
│                    Enterprise Capabilities                       │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐ │
│  │   Customer      │  │   Product       │  │   Operations    │ │
│  │   Management    │  │   Management    │  │                 │ │
│  │                 │  │                 │  │                 │ │
│  │ - Acquisition   │  │ - Development   │  │ - Fulfillment   │ │
│  │ - Onboarding    │  │ - Pricing       │  │ - Supply Chain  │ │
│  │ - Service       │  │ - Lifecycle     │  │ - Quality       │ │
│  │ - Retention     │  │ - Portfolio     │  │ - Support       │ │
│  └─────────────────┘  └─────────────────┘  └─────────────────┘ │
│                                                                  │
│  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐ │
│  │   Finance       │  │   Human         │  │   Technology    │ │
│  │                 │  │   Resources     │  │                 │ │
│  │                 │  │                 │  │                 │ │
│  │ - Accounting    │  │ - Recruitment   │  │ - Infrastructure│ │
│  │ - Treasury      │  │ - Development   │  │ - Applications  │ │
│  │ - Planning      │  │ - Compensation  │  │ - Data          │ │
│  │ - Compliance    │  │ - Performance   │  │ - Security      │ │
│  └─────────────────┘  └─────────────────┘  └─────────────────┘ │
└─────────────────────────────────────────────────────────────────┘
```

---

#### Phase C: Information Systems Architecture

**Purpose**: Develop Data and Application Architectures

**Data Architecture Activities**
- Define data entities and relationships
- Develop conceptual data model
- Define data governance
- Identify data migration needs

**Application Architecture Activities**
- Define application portfolio
- Develop application interaction matrix
- Define application services
- Identify application rationalization opportunities

**Deliverables**
- Data Entity Catalog
- Conceptual Data Model
- Application Portfolio Catalog
- Application Interaction Matrix
- Interface Catalog

---

#### Phase D: Technology Architecture

**Purpose**: Develop Technology Architecture

**Key Activities**
- Define technology standards
- Develop technology portfolio
- Define platform services
- Identify infrastructure requirements

**Deliverables**
- Technology Standards Catalog
- Technology Portfolio Catalog
- Platform Decomposition Diagram
- Infrastructure Requirements

**Technology Reference Model**
```
┌─────────────────────────────────────────────────────────────────┐
│                   Technology Reference Model                     │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  Application Platform Services                                   │
│  ┌─────────────────────────────────────────────────────────────┐│
│  │ API Management | Integration | Workflow | Analytics         ││
│  └─────────────────────────────────────────────────────────────┘│
│                                                                  │
│  Data Platform Services                                          │
│  ┌─────────────────────────────────────────────────────────────┐│
│  │ Databases | Data Lake | Streaming | ML Platform             ││
│  └─────────────────────────────────────────────────────────────┘│
│                                                                  │
│  Infrastructure Services                                         │
│  ┌─────────────────────────────────────────────────────────────┐│
│  │ Compute | Storage | Network | Security | Observability      ││
│  └─────────────────────────────────────────────────────────────┘│
│                                                                  │
│  Foundation Services                                             │
│  ┌─────────────────────────────────────────────────────────────┐│
│  │ Identity | Secrets | Configuration | Deployment             ││
│  └─────────────────────────────────────────────────────────────┘│
└─────────────────────────────────────────────────────────────────┘
```

---

#### Phase E: Opportunities & Solutions

**Purpose**: Initial implementation planning

**Key Activities**
- Consolidate gaps from B, C, D phases
- Group into work packages
- Identify transition architectures
- Evaluate build vs buy vs reuse

**Deliverables**
- Project List
- Transition Architecture State Descriptions
- Implementation Factor Assessment
- Consolidated Gap Analysis

---

#### Phase F: Migration Planning

**Purpose**: Detailed implementation roadmap

**Key Activities**
- Prioritize projects
- Develop implementation roadmap
- Define transition architectures
- Coordinate with project portfolio

**Deliverables**
- Architecture Roadmap
- Implementation and Migration Plan
- Transition Architecture Definitions
- Architecture Contract

**Roadmap Visualization**
```
Year 1                 Year 2                 Year 3
┌─────────────────────┬─────────────────────┬─────────────────────┐
│ Foundation          │ Modernization       │ Innovation          │
│                     │                     │                     │
│ ▪ Cloud Platform    │ ▪ Core System       │ ▪ AI/ML Platform    │
│ ▪ DevOps Pipeline   │   Replacement       │ ▪ Advanced Analytics│
│ ▪ Data Platform     │ ▪ API Gateway       │ ▪ New Products      │
│ ▪ Identity Platform │ ▪ Integration Hub   │ ▪ Ecosystem         │
│                     │ ▪ Legacy Migration  │                     │
└─────────────────────┴─────────────────────┴─────────────────────┘
```

---

#### Phase G: Implementation Governance

**Purpose**: Provide architecture oversight

**Key Activities**
- Confirm scope of deployment projects
- Ensure conformance with architecture
- Perform architecture compliance reviews
- Handle change requests

**Deliverables**
- Architecture Compliance Reports
- Change Requests
- Architecture Contract Updates
- Implementation Recommendations

---

#### Phase H: Architecture Change Management

**Purpose**: Manage architecture lifecycle

**Key Activities**
- Monitor technology changes
- Assess architecture change requests
- Manage architecture governance
- Activate new ADM cycle if needed

**Deliverables**
- Architecture Change Requests
- Architecture Updates
- New Request for Architecture Work

---

## Enterprise Architecture Artifacts

### Architecture Repository Structure

```
Architecture Repository
├── Architecture Metamodel
├── Architecture Capability
│   ├── Skills and Roles
│   ├── Governance Model
│   └── Tools and Methods
├── Architecture Landscape
│   ├── Strategic Architectures
│   ├── Segment Architectures
│   └── Capability Architectures
├── Standards Information Base
│   ├── Industry Standards
│   ├── Product Standards
│   └── Organization Standards
├── Reference Library
│   ├── Reference Architectures
│   ├── Patterns Catalog
│   └── Best Practices
└── Governance Log
    ├── Decision Log
    ├── Compliance Assessments
    └── Capability Assessments
```

### Catalogs, Matrices, and Diagrams

**Catalogs** (Lists of building blocks)
- Actor Catalog
- Application Catalog
- Business Service Catalog
- Data Entity Catalog
- Technology Standards Catalog

**Matrices** (Relationships between catalogs)
- Business Interaction Matrix
- Actor/Role Matrix
- Application/Data Matrix
- Application/Technology Matrix

**Diagrams** (Visual representations)
- Business Footprint Diagram
- Application Communication Diagram
- Data Dissemination Diagram
- Platform Decomposition Diagram

---

## Architecture Governance

### Governance Framework

```
┌─────────────────────────────────────────────────────────────────┐
│                 Architecture Governance Model                    │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ┌─────────────────────────────────────────────────────────────┐│
│  │                Executive Steering Committee                  ││
│  │  - Strategy alignment | Investment decisions | Escalations  ││
│  └─────────────────────────────────────────────────────────────┘│
│                              │                                   │
│  ┌───────────────────────────▼─────────────────────────────────┐│
│  │              Architecture Review Board (ARB)                 ││
│  │  - Architecture decisions | Standards | Compliance          ││
│  └─────────────────────────────────────────────────────────────┘│
│                              │                                   │
│         ┌────────────────────┼────────────────────┐             │
│         │                    │                    │             │
│  ┌──────▼──────┐     ┌───────▼──────┐     ┌──────▼──────┐      │
│  │  Domain     │     │   Domain     │     │  Domain     │      │
│  │  Working    │     │   Working    │     │  Working    │      │
│  │  Groups     │     │   Groups     │     │  Groups     │      │
│  └─────────────┘     └──────────────┘     └─────────────┘      │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Architecture Compliance Review

**Compliance Levels**

| Level | Description | Action |
|-------|-------------|--------|
| Compliant | Fully meets standards | Approve |
| Compliant with Deviations | Minor non-compliance | Document deviations |
| Non-Compliant | Significant gaps | Remediation required |
| Waiver Granted | Approved exception | Time-bound waiver |

**Review Checklist**
- [ ] Architecture principles followed
- [ ] Technology standards used
- [ ] Security requirements met
- [ ] Integration patterns followed
- [ ] Data standards compliance
- [ ] Performance requirements addressed
- [ ] Operational readiness confirmed

### Exception/Waiver Process

```
┌──────────────┐    ┌──────────────┐    ┌──────────────┐
│  Exception   │───►│   Domain     │───►│    ARB       │
│  Request     │    │   Review     │    │   Decision   │
└──────────────┘    └──────────────┘    └──────┬───────┘
                                               │
                    ┌──────────────────────────┴──────────────────────────┐
                    │                          │                          │
              ┌─────▼─────┐             ┌──────▼─────┐             ┌──────▼─────┐
              │  Approve  │             │  Approve   │             │  Reject    │
              │  As-Is    │             │  w/Conditions│            │            │
              └───────────┘             └────────────┘             └────────────┘
```

---

## Application Portfolio Management

### Portfolio Assessment Matrix

```
                    Business Value
                    Low         High
                ┌───────────┬───────────┐
           High │ TOLERATE  │  INVEST   │
 Technical      │           │           │
  Quality       │ Minimize  │ Strategic │
                │ investment│ priority  │
                ├───────────┼───────────┤
           Low  │ ELIMINATE │  MIGRATE  │
                │           │           │
                │ Retire or │ Modernize │
                │ replace   │ or replace│
                └───────────┴───────────┘
```

### Application Rationalization

**Rationalization Strategies**

| Strategy | When to Use | Approach |
|----------|-------------|----------|
| Retain | Strategic, modern | Continue investment |
| Rehost | Lift-and-shift viable | Move to cloud as-is |
| Replatform | Minor optimization | Leverage managed services |
| Refactor | Strategic, needs modernization | Re-architect for cloud |
| Replace | Commodity, better alternatives | Adopt SaaS/COTS |
| Retire | Low value, redundant | Decommission |

### Technical Debt Management

**Debt Categories**

| Category | Description | Example |
|----------|-------------|---------|
| Code Debt | Poor code quality | Lack of tests, complexity |
| Architecture Debt | Suboptimal design | Monolith, tight coupling |
| Infrastructure Debt | Outdated platforms | EOL systems, manual ops |
| Documentation Debt | Missing documentation | Tribal knowledge |
| Test Debt | Insufficient testing | Manual testing, low coverage |

**Debt Tracking**
```
┌────────────────────────────────────────────────────────────────┐
│                    Technical Debt Register                      │
├────────────────────────────────────────────────────────────────┤
│ ID    │ Description     │ Impact │ Effort │ Priority │ Status │
├───────┼─────────────────┼────────┼────────┼──────────┼────────┤
│ TD-001│ Legacy auth     │ High   │ Medium │ Critical │ Active │
│ TD-002│ Manual deploys  │ Medium │ Low    │ High     │ Planned│
│ TD-003│ Missing API docs│ Low    │ Low    │ Medium   │ Backlog│
└────────────────────────────────────────────────────────────────┘
```

---

## Architecture Principles

### Principle Template

```
Name: [Short descriptive name]

Statement: [Clear, unambiguous statement of principle]

Rationale: [Why this principle is important]

Implications:
- [Implication 1]
- [Implication 2]
- [Implication 3]
```

### Example Principles

**Business Principles**
1. Business Continuity
2. Compliance with Law
3. Common Use Applications
4. Data is an Asset
5. Service Orientation

**Data Principles**
1. Data Trustee Accountability
2. Data Sharing
3. Data Accessibility
4. Data Security
5. Common Vocabulary

**Application Principles**
1. Technology Independence
2. Ease of Use
3. Buy Before Build
4. API-First Design
5. Reusability

**Technology Principles**
1. Cloud-First
2. Security by Design
3. Automation First
4. Standards-Based
5. Observability Built-in
