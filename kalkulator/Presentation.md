---
defaultTemplate: "[[DefaultTemplate]]"
---

# Mimir Kalkulator

---

```mermaid
gitGraph
    commit id: "Initial Mimir setup"
    commit id: "Add Norne bronze layer"
    
    branch feature/bronze-ingestion
    checkout feature/bronze-ingestion
    commit id: "Raw data ingestion"
    commit id: "Data validation rules"
    commit id: "Unit tests"
    
    checkout main
    merge feature/bronze-ingestion
    commit id: "Bronze layer deployed" type: HIGHLIGHT
    
    branch feature/silver-transformation
    checkout feature/silver-transformation
    commit id: "Data cleansing logic"
    commit id: "Schema standardization"
    commit id: "Integration tests"
    
    checkout main
    merge feature/silver-transformation
    commit id: "Silver layer deployed" type: HIGHLIGHT
    
    branch feature/gold-analytics
    checkout feature/gold-analytics
    commit id: "Business metrics"
    commit id: "Aggregations"
    commit id: "Performance tests"
    
    checkout main
    merge feature/gold-analytics
    commit id: "Gold layer deployed" type: HIGHLIGHT
    
    branch hotfix/data-quality
    checkout hotfix/data-quality
    commit id: "Fix bronze validation"
    
    checkout main
    merge hotfix/data-quality
    commit id: "Hotfix deployed" type: REVERSE
    
    commit id: "Production ready" type: HIGHLIGHT
```

---
::: title

## CI/CD Pipeline Flow

:::

<grid drop="left" border="4px solid white">

```mermaid
graph TD
    A[Developer creates feature branch] --> B[Commits code changes]
    B --> C[Push to GitHub]
    C --> D{PR Created?}
    D -->|Yes| E[GitHub Actions triggers]
    E --> F[Run Unit Tests]
    F --> G[Data Quality Checks]
    G --> H[Schema Validation]
    H --> I{Tests Pass?}
    I -->|No| J[Block merge]
    I -->|Yes| K[Deploy to Dev Environment]
    K --> L[Integration Tests]

    style E fill:#e1f5fe
    style K fill:#f3e5f5

```

</grid>

<grid drop="right">
```mermaid
graph TD
    L[Integration Tests] --> M{Ready for Review?}
    M -->|No| N[Request changes]
    M -->|Yes| O[Code Review]
    O --> P[Merge to main]
    P --> Q[Deploy to Test Environment]
    Q --> R[Run E2E Tests]
    R --> S[Deploy to Production]
    S --> T[Monitor Data Quality]

    style Q fill:#fff3e0
    style S fill:#e8f5e8

```

</grid>

---

## Medallion Architecture Deployment

```mermaid
graph LR
    subgraph "GitHub Repository"
        A[Source Code] --> B[Databricks Notebooks]
        A --> C[Configuration Files]
        A --> D[Tests]
    end
    
    subgraph "CI/CD Pipeline"
        E[GitHub Actions] --> F[Build & Test]
        F --> G[Package Assets]
        G --> H[Deploy to Databricks]
    end
    
    subgraph "Databricks Workspace"
        I[Bronze Layer - Raw Norne Data]
        J[Silver Layer - Cleansed Data]
        K[Gold Layer - Analytics Ready]
    end
    
    B --> E
    H --> I
    I --> J
    J --> K
    
    style I fill:#8d6e63
    style J fill:#90a4ae
    style K fill:#ffc107
```
