---
name: project-manager
description: "Use when starting a new feature or project. Orchestrates the full lifecycle: brainstorm → plan → RFC → tickets. Requires superpowers plugin and a documentation/PM MCP server."
---

# Project Manager

Orchestrate the complete project lifecycle from idea to actionable tickets.

**Announce at start:** "Using shipwright:project-manager to orchestrate project planning."

## Prerequisites

This skill requires:
- **superpowers plugin** - For brainstorming and writing-plans skills
- **Documentation MCP server** - Atlassian (Confluence), Notion, or similar
- **Project Management MCP server** - Atlassian (Jira), Linear, GitHub, or similar

## Workflow Overview

```
┌─────────────────┐     ┌─────────────────┐
│   BRAINSTORM    │────▶│   WRITE PLAN    │
│  (interactive)  │     │  (structured)   │
└────────┬────────┘     └────────┬────────┘
         │ design                │ tasks
         └──────────┬────────────┘
                    ▼
            ┌───────────────┐
            │  CREATE RFC   │  ← Single source of truth
            │  (published)  │
            └───────┬───────┘
                    │
                    ▼
            ┌───────────────┐
            │CREATE TICKETS │  ← Epic + Stories
            │  (tracked)    │
            └───────────────┘
```

## Phase 1: Discovery & Design

**Use:** `@superpowers:brainstorming`

The brainstorming skill will:
1. Analyze codebase structure and existing patterns
2. Ask clarifying questions one at a time
3. Explore 2-3 approaches with trade-offs
4. Present design in sections for validation

**Important:** Do NOT write design to local files. Keep in memory for RFC.

**Completion criteria:** User approves complete design.

**Transition:** "Design approved. Moving to implementation planning."

## Phase 2: Implementation Planning

**Use:** `@superpowers:writing-plans`

The writing-plans skill will:
1. Break design into bite-sized tasks (2-5 minutes each)
2. Include exact file paths and code
3. Follow TDD pattern (test → implement → verify)
4. Organize into logical phases

**Important:** Do NOT write plan to local files. Keep in memory for RFC.

**Completion criteria:** User approves implementation plan.

**Transition:** "Plan approved. Ready to create RFC?"

## Phase 3: RFC Creation

### Provider Detection

Check for available documentation MCP servers:

| Provider   | Detection Pattern        | Create Function         |
|------------|-------------------------|-------------------------|
| Atlassian  | `mcp__atlassian__*`     | `createConfluencePage`  |
| Notion     | `mcp__notion__*`        | `create_page`           |
| GitHub     | `mcp__github__*`        | `create_or_update_file` |

**If multiple detected:** Ask user which to use.
**If none detected:** Inform user and offer to output RFC as markdown.

### RFC Structure

Use the embedded template from `rfc-template.md` in this skill directory.

The RFC combines:
- **From brainstorming:** Problem statement, goals, architecture, alternatives
- **From writing-plans:** Implementation phases, tasks, dependencies

### Publishing

1. Prompt user for target location (space/folder/path)
2. Create RFC using detected provider
3. Return published URL

**Transition:** "RFC published at [URL]. Ready to create tickets?"

## Phase 4: Ticket Creation

### Provider Detection

Check for available PM MCP servers:

| Provider   | Detection Pattern        | Epic Function       | Story Function      |
|------------|-------------------------|---------------------|---------------------|
| Atlassian  | `mcp__atlassian__*`     | `createJiraIssue`   | `createJiraIssue`   |
| Linear     | `mcp__linear__*`        | `create_issue`      | `create_issue`      |
| GitHub     | `mcp__github__*`        | `create_issue`      | `create_issue`      |

**If multiple detected:** Ask user which to use.
**If none detected:** Inform user and offer to output tickets as markdown.

### Ticket Structure

**Epic:**
- Title from RFC title
- Description links to RFC
- Labels: from RFC keywords

**Stories (per implementation phase):**
- Title: Task description
- Description: Full task details from plan
- Acceptance criteria: Verification steps
- Parent: Link to Epic
- Labels: Phase number, component

### Creation Flow

1. Prompt user for target project/board
2. Create Epic first
3. Create Stories linked to Epic
4. Return summary with all ticket URLs

**Completion:** "Project setup complete! Epic: [URL], Stories: [count] created."

## Interactive Prompts

At each phase transition, ask for explicit approval:

```
Phase 1 → 2: "Design looks complete. Proceed to planning? (y/n)"
Phase 2 → 3: "Plan ready. Create RFC now? (y/n)"
Phase 3 → 4: "RFC published. Create tickets now? (y/n)"
```

User can exit at any phase. Partial progress is retained in conversation.

## Error Handling

**MCP server unavailable:**
- Inform user which provider is missing
- Offer markdown output as fallback
- Suggest MCP server installation

**API failures:**
- Report specific error
- Offer retry or skip
- Continue with remaining items

**Partial completion:**
- Track what was created
- Offer to resume from failure point

## Key Principles

- **Single source of truth** - RFC is the canonical document
- **No local artifacts** - Design and plan live in RFC, not local files
- **Provider agnostic** - Works with any supported MCP server
- **Graceful degradation** - Falls back to markdown if no MCP available
- **User control** - Explicit approval at each phase transition
