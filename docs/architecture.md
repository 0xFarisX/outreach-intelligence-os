# Architecture

```mermaid
flowchart TB
    subgraph Sources
        A[Customer records]
        B[Relationship history]
    end

    subgraph Intelligence
        C[Prospect builder]
        D[Website checker]
        E[Scoring engine]
        F[(SQLite)]
    end

    subgraph Drafting
        G[Context builder]
        H[Local language model]
        I[Validation rules]
        J[Template fallback]
    end

    subgraph Delivery
        K[Human review]
        L[Gmail drafts]
    end

    A --> C
    B --> C
    C --> F
    D <--> F
    E <--> F
    F --> G
    G --> H
    H --> I
    H -. unavailable .-> J
    J --> I
    I --> K
    K --> L
```

## Components

### Prospect builder

Matches customer profiles with relationship records, applies eligibility rules
and maintains a reviewable prospect store without discarding existing workflow
state during rebuilds.

### Scoring engine

Combines deterministic relationship, operating-pressure and automation-
opportunity signals. It stores the result and supporting rationale so the
interface can explain the recommendation.

### Website checker

Records whether a supplied business website appears reachable. This supports
qualification and prevents outreach from relying blindly on stale URLs.

### Drafting engine

Builds constrained context for a local model, parses the result and applies
content validation. A deterministic template maintains workflow continuity when
model output is unavailable or unsuitable.

### Gmail adapter

Creates individual or bounded-batch drafts using compose permissions. Delivery
ends at draft creation; no automatic-send operation is part of the workflow.

