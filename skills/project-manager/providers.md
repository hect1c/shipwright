# Provider Integration Guide

Shipwright uses MCP (Model Context Protocol) servers to integrate with documentation and project management tools. This guide documents supported providers and how to add new ones.

## Provider Detection

Providers are detected by checking for MCP tool patterns in the current session.

### Detection Logic

```
1. Scan available MCP tools for known patterns
2. If multiple providers of same type detected, prompt user
3. If no provider detected, offer markdown fallback
```

## Documentation Providers

### Atlassian Confluence

**Detection:** Tools matching `mcp__atlassian__*Confluence*`

**Required Tools:**
- `mcp__atlassian__getConfluenceSpaces` - List available spaces
- `mcp__atlassian__createConfluencePage` - Create RFC page

**Configuration Prompts:**
- Cloud ID or site URL
- Space key (e.g., "PAM", "ENG")
- Parent page ID (optional, for nesting under RFCs folder)

**Example Usage:**
```
createConfluencePage({
  cloudId: "your-site.atlassian.net",
  spaceId: "12345",
  parentId: "67890",  // RFCs parent page
  title: "RFC: Feature Name",
  body: "{RFC content in markdown}",
  contentFormat: "markdown"
})
```

### Notion

**Detection:** Tools matching `mcp__notion__*`

**Required Tools:**
- `mcp__notion__search` - Find database/page
- `mcp__notion__create_page` - Create RFC page

**Configuration Prompts:**
- Database ID or parent page ID
- Workspace selection (if multiple)

### GitHub (Wiki/Markdown)

**Detection:** Tools matching `mcp__github__*`

**Required Tools:**
- `mcp__github__create_or_update_file` - Create RFC file

**Configuration Prompts:**
- Repository (owner/repo)
- Path (e.g., "docs/rfcs/")
- Branch (default: main)

**Note:** Creates RFC as markdown file in repository.

---

## Project Management Providers

### Atlassian Jira

**Detection:** Tools matching `mcp__atlassian__*Jira*`

**Required Tools:**
- `mcp__atlassian__getVisibleJiraProjects` - List projects
- `mcp__atlassian__getJiraProjectIssueTypesMetadata` - Get issue types
- `mcp__atlassian__createJiraIssue` - Create Epic/Story

**Configuration Prompts:**
- Cloud ID or site URL
- Project key (e.g., "PM", "ENG")
- Epic issue type ID
- Story issue type ID

**Epic Creation:**
```
createJiraIssue({
  cloudId: "your-site.atlassian.net",
  projectKey: "PM",
  issueTypeName: "Epic",
  summary: "RFC Title",
  description: "Link to RFC and summary"
})
```

**Story Creation:**
```
createJiraIssue({
  cloudId: "your-site.atlassian.net",
  projectKey: "PM",
  issueTypeName: "Story",
  summary: "Task title",
  description: "Task details",
  parent: "PM-123"  // Epic key
})
```

### Linear

**Detection:** Tools matching `mcp__linear__*`

**Required Tools:**
- `mcp__linear__list_teams` - List teams
- `mcp__linear__create_issue` - Create issue

**Configuration Prompts:**
- Team ID
- Project ID (optional)

**Note:** Linear uses labels or projects for Epic-like grouping.

### GitHub Issues

**Detection:** Tools matching `mcp__github__create_issue`

**Required Tools:**
- `mcp__github__list_issues` - List existing issues
- `mcp__github__create_issue` - Create issue

**Configuration Prompts:**
- Repository (owner/repo)
- Labels for Epic simulation
- Milestone (optional)

**Note:** GitHub doesn't have native Epics. Use labels or milestones for grouping.

---

## Adding New Providers

To add support for a new provider:

### 1. Documentation Provider

Add to the detection table in `SKILL.md`:

```markdown
| Provider | Detection Pattern | Create Function |
|----------|-------------------|-----------------|
| NewTool  | `mcp__newtool__*` | `create_page`   |
```

Document required tools and configuration prompts in this file.

### 2. Project Management Provider

Add to the PM detection table in `SKILL.md`:

```markdown
| Provider | Detection Pattern | Epic Function | Story Function |
|----------|-------------------|---------------|----------------|
| NewTool  | `mcp__newtool__*` | `create_epic` | `create_task`  |
```

Document:
- How Epics are represented (native or simulated)
- How Stories link to Epics
- Required configuration prompts

### 3. Test the Integration

1. Install the MCP server locally
2. Run shipwright:project-manager
3. Verify detection works
4. Test full workflow: RFC → Tickets

---

## Fallback Behavior

When no provider is detected:

### Documentation Fallback
- Output RFC as markdown to console
- User can manually copy to their documentation system

### PM Fallback
- Output ticket specifications as markdown
- Include suggested title, description, labels
- User can manually create in their PM tool

---

## MCP Server Installation

### Atlassian
```bash
# Via Claude Code MCP settings
claude mcp add atlassian
```

### Notion
```bash
claude mcp add notion
```

### GitHub
```bash
claude mcp add github
```

### Linear
```bash
claude mcp add linear
```

Refer to each MCP server's documentation for authentication setup.
