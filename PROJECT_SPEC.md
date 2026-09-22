# DGuard — Project Specification

## 1. Project Overview

DGuard is an intelligent data-reliability gate for B2B procurement data.

It is designed to sit between the Bronze and Silver layers of a data pipeline and evaluate incoming procurement data before it reaches downstream systems.

DGuard combines:

- Deterministic data-quality validation
- Contextual anomaly detection
- Risk and trust scoring
- Explainable anomaly detection
- Accept, Flag, and Quarantine decisions

### High-Level Flow

Source Systems
↓
Bronze
↓
DGuard
↓
Silver
↓
Gold

DGuard acts as an additional reliability layer rather than replacing the existing data pipeline.

---

## 2. Problem Statement

Traditional data-quality systems primarily rely on predefined rules such as:

- Missing-value checks
- Duplicate detection
- Data-type validation
- Range validation
- Schema validation

These rules can identify technically invalid records, but some data can be technically valid while still being unusual or suspicious in its business context.

For example, a supplier may normally sell a product for ₹900–₹1,200, while a new transaction contains a unit price of ₹8,900.

The record may pass basic schema, type, and range validation, but its price may be highly unusual compared with the supplier's historical behaviour.

DGuard aims to identify such contextual anomalies before the data moves into the Silver layer.
---

## 3. Core Research Question

Can contextual ML-based anomaly detection complement deterministic data-quality validation to improve the reliability of B2B procurement data before it reaches downstream systems?

The central experiment will compare two approaches:

### Approach A — Traditional Rules Only

Procurement Data
↓
Deterministic Data-Quality Rules
↓
Decision

### Approach B — Rules + Contextual ML

Procurement Data
↓
Deterministic Data-Quality Rules
+
Contextual ML Anomaly Detection
↓
Decision

The purpose of this comparison is to determine whether the ML layer can identify useful anomalies that deterministic validation alone may miss.

---

## 4. Target Domain — B2B Procurement

The initial implementation of DGuard will focus on B2B procurement transactions.

A procurement record may contain fields such as:

- Purchase Order ID
- Supplier ID
- Product ID
- Department
- Warehouse
- Order Date
- Quantity
- Unit Price
- Total Amount
- Delivery Days
- Region
- Currency

Procurement data is suitable for contextual anomaly detection because transaction behaviour can depend on relationships between:

- Supplier
- Product
- Supplier + Product
- Quantity
- Price
- Department
- Warehouse
- Region
- Delivery behaviour

DGuard will use these relationships to identify records that appear unusual compared with historical or contextual behaviour.

### Initial Project Boundary

The first implementation will focus on:

B2B Procurement Data
↓
Bronze
↓
DGuard
↓
Silver

The initial goal is to demonstrate:

Data Quality
+
Contextual Anomaly Detection
+
Risk / Trust Scoring
+
Explainable Decisions
+
Accept / Flag / Quarantine

---

## 5. DGuard Architecture

DGuard operates as a reliability gate between the Bronze and Silver layers.

### High-Level Architecture

```text
Source Systems
      ↓
    Bronze
      ↓
┌─────────────────────────────┐
│           DGuard            │
│                             │
│  1. Data Quality Engine     │
│  2. Contextual Features     │
│  3. ML Anomaly Detection    │
│  4. Risk / Trust Engine     │
│  5. Decision Engine         │
│  6. Explainability          │
└──────────────┬──────────────┘
               ↓
       ┌───────┼────────┐
       ↓       ↓        ↓
    ACCEPT    FLAG   QUARANTINE
       ↓       ↓        ↓
    Silver   Review  Investigation
---

## 7. Technology Stack

DGuard will use a Python-based technology stack.

| Technology | Purpose |
|---|---|
| Python | Core application and ML pipeline |
| Pandas | Data processing and feature engineering |
| Scikit-learn | Machine learning and anomaly detection |
| FastAPI | REST API for DGuard |
| Streamlit | Monitoring and visualization interface |
| Pytest | Automated testing |
| Git | Version control |
| GitHub | Remote repository and collaboration |
| GitHub Actions | CI/CD and automated testing |

### Development Principle

Technologies will be introduced only when they become necessary for a specific phase.

The project will not add technologies simply to increase the size of the technology stack.

Additional technologies such as databases, cloud platforms, distributed processing frameworks, or orchestration tools may be considered later if they provide a clear technical benefit.

---

## 8. Development Roadmap

### Phase 0 — Foundation

- Finalize project scope
- Define the problem
- Document architecture
- Define the procurement domain
- Establish project specification
- Set up Git and GitHub

### Phase 1 — Project Setup

- Python environment
- Virtual environment
- Project structure
- Dependency management
- `.gitignore`
- Initial Git workflow

### Phase 2 — Procurement Data Foundation

- Define procurement dataset
- Data ingestion
- Bronze-layer representation
- Data profiling
- Identify relevant historical relationships

### Phase 3 — Data Quality Engine

- Schema validation
- Missing-value checks
- Duplicate detection
- Data-type validation
- Business rules
- Quality scoring

### Phase 4 — Contextual Anomaly Engine

- Contextual feature engineering
- Historical behavioural features
- Select anomaly-detection approach
- Train the initial model
- Evaluate anomaly results
- Persist the model if required

### Phase 5 — Intelligence Layer

- Risk scoring
- Trust scoring
- Explainability
- Accept / Flag / Quarantine decisions
- Human-review workflow

### Phase 6 — API Layer

- FastAPI setup
- Validation endpoint
- Batch processing
- Structured responses
- Error handling

### Phase 7 — Monitoring Interface

- Streamlit setup
- Batch overview
- Quality metrics
- Trust/risk scores
- Detected anomalies
- Quarantined records
- Historical trends

### Phase 8 — Testing

- Unit tests
- Integration tests
- API tests
- Data-quality tests
- ML pipeline tests

### Phase 9 — CI/CD and Deployment

- GitHub Actions
- Automated testing
- Build workflow
- Deployment
- Environment configuration

### Phase 10 — Evaluation and Documentation

- Rules-only baseline
- Rules + ML comparison
- Performance evaluation
- Architecture documentation
- Technical decisions
- Final README
- Demo preparation

---

## 9. Evaluation Strategy

DGuard will be evaluated by comparing two approaches.

### Approach A — Rules Only

```text
Procurement Data
      ↓
Data Quality Rules
      ↓
Decisiong