# RFC Template

Use this template when creating RFCs. Replace placeholders with actual content from brainstorming and planning phases.

---

# RFC: {TITLE}

| Field | Value |
|-------|-------|
| **Status** | Draft |
| **Author(s)** | {AUTHORS} |
| **Created** | {DATE} |
| **Last Updated** | {DATE} |
| **Ticket** | {EPIC_LINK} |

---

## Executive Summary

{2-3 sentences summarizing the proposal. What are we building and why?}

---

## Problem Statement

### Current State

{Describe the current situation and its limitations.}

### Pain Points

{Bullet list of specific problems being solved.}

### Impact

{Who is affected and how? Include metrics if available.}

---

## Goals and Non-Goals

### Goals

{Numbered list of what this RFC aims to achieve.}

### Non-Goals

{Explicit list of what is out of scope. This prevents scope creep.}

### Success Metrics

{How will we measure success? Include specific, measurable criteria.}

---

## Proposed Solution

### Overview

{High-level description of the solution approach.}

### Architecture

{System architecture description. Include diagrams if helpful.}

```
{ASCII diagram or description of component relationships}
```

### Key Components

{Describe each major component and its responsibility.}

#### Component 1: {Name}

- **Purpose:** {What it does}
- **Interface:** {How other components interact with it}
- **Dependencies:** {What it requires}

#### Component 2: {Name}

{Continue for each component...}

### Data Model

{Key data structures, schemas, or models.}

```
{Schema definition or example}
```

### API Design

{Key APIs being introduced or modified.}

---

## Technical Implementation

### Phase 1: {Phase Name}

**Goal:** {What this phase achieves}

**Tasks:**
{List of implementation tasks from the plan}

**Deliverables:**
- {Concrete outputs}

### Phase 2: {Phase Name}

{Continue for each phase...}

### Dependencies

{External dependencies, services, or teams required.}

### Migration Strategy

{If applicable, how existing systems/data will be migrated.}

---

## Alternatives Considered

### Alternative 1: {Name}

- **Description:** {What this approach would look like}
- **Pros:** {Benefits}
- **Cons:** {Drawbacks}
- **Why not chosen:** {Specific reason for rejection}

### Alternative 2: {Name}

{Continue for each alternative...}

---

## Trade-offs and Risks

### Trade-offs

| Decision | Trade-off | Rationale |
|----------|-----------|-----------|
| {Decision made} | {What we gain vs lose} | {Why this is acceptable} |

### Risks

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| {Risk description} | Low/Medium/High | Low/Medium/High | {How we address it} |

### Open Questions

{List any unresolved questions that need answers before/during implementation.}

---

## Security Considerations

{Security implications and how they are addressed.}

- **Authentication:** {How users/services are authenticated}
- **Authorization:** {How access is controlled}
- **Data Protection:** {How sensitive data is handled}
- **Audit:** {What is logged for compliance}

---

## Operational Considerations

### Monitoring

{What metrics and alerts will be in place.}

### Deployment

{Deployment strategy, rollout plan, feature flags.}

### Rollback

{How to rollback if issues arise.}

### Performance

{Expected performance characteristics and limits.}

---

## Implementation Plan

### Timeline Overview

| Phase | Description | Dependencies |
|-------|-------------|--------------|
| Phase 1 | {Description} | None |
| Phase 2 | {Description} | Phase 1 |
| {Continue...} | | |

### Detailed Tasks

{Full task breakdown from writing-plans phase. Each task should include:}

#### Task {N}: {Task Name}

**Files:**
- {File paths to create/modify}

**Steps:**
1. {Step-by-step implementation}

**Verification:**
- {How to verify this task is complete}

---

## Appendices

### Appendix A: Glossary

| Term | Definition |
|------|------------|
| {Term} | {Definition} |

### Appendix B: References

- {Link to related documentation}
- {Link to external resources}

### Appendix C: Code Examples

{Any reference code or examples that help clarify the design.}

---

## Approval

| Role | Name | Status | Date |
|------|------|--------|------|
| Author | {Name} | Proposed | {Date} |
| Tech Lead | | Pending | |
| Architect | | Pending | |
| Product | | Pending | |

---

## Changelog

| Date | Author | Changes |
|------|--------|---------|
| {Date} | {Author} | Initial draft |
