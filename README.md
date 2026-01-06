# Shipwright

> Craft the vessel that ships.

A Claude Code skill for technical program management — from RFC to JIRA ticket.

## What It Does

Shipwright orchestrates the complete project lifecycle:

```
Brainstorm → Plan → RFC → Tickets
```

1. **Discovery & Design** — Uses interactive brainstorming to refine your idea
2. **Implementation Planning** — Creates structured, TDD-focused task breakdown
3. **RFC Creation** — Publishes design document to your documentation platform
4. **Ticket Creation** — Creates Epic and Stories in your project management tool

All powered by MCP servers for provider-agnostic integration.

## Installation

### Claude Code (via Plugin Marketplace)

Register the marketplace:

```bash
/plugin marketplace add hect1c/shipwright
```

Install the plugin:

```bash
/plugin install shipwright@shipwright
```

### Verify Installation

```bash
/help
```

You should see:
```
/shipwright:project-manager - Orchestrate project lifecycle: design → RFC → tickets
```

## Prerequisites

Shipwright requires:

1. **[Superpowers](https://github.com/obra/superpowers)** plugin — For brainstorming and writing-plans skills
2. **Documentation MCP server** — Atlassian, Notion, or GitHub
3. **Project Management MCP server** — Atlassian (Jira), Linear, or GitHub

### Installing Superpowers

```bash
/plugin marketplace add obra/superpowers-marketplace
/plugin install superpowers@superpowers-marketplace
```

### Installing MCP Servers

For Atlassian (Confluence + Jira):
```bash
claude mcp add atlassian
```

For other providers, see [Provider Documentation](skills/project-manager/providers.md).

## Usage

Start a new project:

```
/shipwright:project-manager
```

Or just describe what you want to build — Shipwright activates automatically when you're starting something new.

### Example Session

```
You: I want to add a notification system to our app

Shipwright: Using shipwright:project-manager to orchestrate project planning.

[Phase 1: Discovery & Design]
Let me understand what you're building...
- What channels should notifications support?
- Should users be able to configure preferences?
...

[Phase 2: Implementation Planning]
Design approved. Creating implementation plan...
- Phase 1: Core infrastructure
- Phase 2: Notification service
...

[Phase 3: RFC Creation]
Plan approved. I detected Atlassian Confluence.
Where should I create the RFC?
> Space: PAM, Parent: RFCs folder

RFC published: https://your-site.atlassian.net/wiki/...

[Phase 4: Ticket Creation]
I detected Atlassian Jira.
Which project should I use?
> Project: PM

Created:
- Epic PM-100: Notification System
- Story PM-101: Set up message broker
- Story PM-102: Create notification schemas
... (12 more stories)

Project setup complete!
```

## Supported Providers

### Documentation
| Provider | Status | Notes |
|----------|--------|-------|
| Atlassian Confluence | Supported | Full RFC support |
| Notion | Planned | Coming soon |
| GitHub Wiki | Planned | Markdown files |

### Project Management
| Provider | Status | Notes |
|----------|--------|-------|
| Atlassian Jira | Supported | Epic + Stories |
| Linear | Planned | Coming soon |
| GitHub Issues | Planned | Labels for grouping |

## Configuration

Shipwright prompts for configuration interactively:

- **Documentation location** — Space, folder, or path for RFCs
- **Project board** — Where to create tickets
- **Issue types** — Epic and Story type mappings

No config files needed — everything is prompted at runtime.

## How It Works

### RFC Template

Shipwright uses an embedded RFC template based on industry best practices:
- Executive summary and problem statement
- Goals, non-goals, and success metrics
- Technical architecture and implementation plan
- Alternatives considered and trade-offs
- Security and operational considerations
- Approval workflow

See [rfc-template.md](skills/project-manager/rfc-template.md) for the full template.

### Provider Detection

Shipwright auto-detects available MCP servers:

```
Available MCP tools → Pattern matching → Provider selection
```

If multiple providers are available, you choose which to use.

### Graceful Degradation

No MCP server? Shipwright outputs markdown that you can manually copy to your tools.

## Contributing

Contributions welcome! See [providers.md](skills/project-manager/providers.md) for adding new provider support.

## License

MIT

## Credits

- Built on [Superpowers](https://github.com/obra/superpowers) by Jesse Vincent
- RFC template inspired by practices from Google, Uber, and Pragmatic Engineer
