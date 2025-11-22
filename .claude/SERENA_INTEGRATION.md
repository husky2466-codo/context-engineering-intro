# Serena MCP Integration Guide

This document explains how to use Serena MCP server with the subagent workflow in this workspace.

## What is Serena?

Serena is an MCP (Model Context Protocol) server that provides:
- **Project management** - Track tasks and progress
- **RAG capabilities** - Search and retrieve documentation
- **Persistent history** - Keep track of decisions and context
- **Multi-agent coordination** - Manage subagent workflows

## Setup

Serena MCP server is configured in VSCode settings:
```json
{
  "chat.mcp.servers": {
    "serena": {
      "command": "npx",
      "args": ["-y", "@serenaai/mcp-server"]
    }
  }
}
```

After adding this configuration:
1. Reload VSCode window (Ctrl+Shift+P → "Reload Window")
2. Serena MCP tools will be available to Claude Code
3. Check with: `/mcp list` or ask "Is Serena available?"

## Using Serena with Subagents

### Workflow with Serena

When Serena is available, the workflow becomes:

```
1. CREATE PROJECT in Serena
   - Project name: "[Feature Name]"
   - Description: Brief overview
   - Tags: relevant tags (python, android, etc.)

2. CREATE TASKS for each phase
   - Task 1: "Requirements analysis"
   - Task 2: "Implementation - [component]"
   - Task 3: "Testing"
   - Task 4: "Code review"
   - Task 5: "Documentation"

3. UPDATE TASK STATUS as work progresses
   - Set to "doing" when starting
   - Set to "done" when complete
   - Add notes about decisions

4. PASS PROJECT ID to subagents
   - Include in subagent prompts
   - Subagents can reference for context

5. USE RAG for documentation
   - Search Pydantic AI docs
   - Search Android/Kotlin docs
   - Search project-specific patterns
```

### Example: Feature Implementation with Serena

**User Request**: "Add table extraction to PDF processor"

**With Serena**:
```markdown
## Step 1: Create Serena Project
- Project: "PDF Table Extraction Feature"
- Description: "Add table extraction capability to Audio Excel Database PDF processor"
- Tags: python, pdf-processing, feature

## Step 2: Create Tasks
1. "Analyze requirements and existing code" - Assigned to Main Agent
2. "Implement table extraction logic" - Assigned to python-developer
3. "Create comprehensive tests" - Assigned to test-engineer
4. "Code quality review" - Assigned to code-reviewer
5. "Update documentation" - Assigned to documentation-writer

## Step 3: Execute with Status Updates
[Main Agent]
- Update Task 1 to "doing"
- Analyze existing code
- Update Task 1 to "done" with notes

[Parallel Execution]
- Update Tasks 2, 3, 5 to "doing"
- Invoke python-developer (Task 2)
- Invoke test-engineer (Task 3)
- Invoke documentation-writer (Task 5)
- Wait for completion
- Update Tasks 2, 3, 5 to "done"

[Sequential Review]
- Update Task 4 to "doing"
- Invoke code-reviewer
- Update Task 4 to "done"

## Step 4: Project Summary
- All tasks complete
- Feature delivered
- Serena project has full history
```

## MCP Tools Available

### Project Management
- `mcp__serena__create_project` - Create a new project
- `mcp__serena__list_projects` - List all projects
- `mcp__serena__get_project` - Get project details
- `mcp__serena__update_project` - Update project info

### Task Management
- `mcp__serena__create_task` - Create a new task
- `mcp__serena__list_tasks` - List tasks in project
- `mcp__serena__update_task` - Update task status/details
- `mcp__serena__complete_task` - Mark task complete

### RAG / Search
- `mcp__serena__search` - Search documentation and resources
- `mcp__serena__query` - Query specific topics

### Health Check
- `mcp__serena__health_check` - Verify Serena is available

## Best Practices

### 1. Always Check Availability First
```markdown
Before starting a complex workflow, check if Serena is available:
- If available: Create project and use full workflow
- If not available: Use local TodoWrite for tracking
```

### 2. Create Meaningful Projects
```markdown
Good project names:
- "PDF Table Extraction Feature"
- "Android Dark Mode Implementation"
- "Refactor Excel Database Architecture"

Poor project names:
- "Fix bug"
- "Update code"
- "Changes"
```

### 3. Granular Task Creation
```markdown
Create tasks for each distinct phase:
✅ "Implement PDF parsing logic"
✅ "Create unit tests for PDF parser"
✅ "Document PDF parser API"

❌ "Do everything"
❌ "Complete feature"
```

### 4. Update Status Religiously
```markdown
Always update task status:
- BEFORE starting: Set to "doing"
- AFTER completing: Set to "done"
- Add notes about any issues or decisions
```

### 5. Use RAG for Research
```markdown
Before implementing, search for patterns:
- "How to extract tables from PDFs in Python"
- "Jetpack Compose best practices"
- "Pydantic AI tool decorator usage"
```

### 6. Pass Context to Subagents
```markdown
When invoking subagents, include Serena project ID:

Task(
  subagent_type="python-developer",
  prompt="""
  Implement PDF table extraction.

  Serena Project ID: abc-123
  Serena Task ID: task-456

  [rest of prompt...]
  """
)
```

## Workflow Comparison

### Without Serena
```
User request
  ↓
Main agent plans
  ↓
TodoWrite tracking
  ↓
Invoke subagents
  ↓
Manual status updates
  ↓
Deliver to user
```

### With Serena
```
User request
  ↓
Check Serena availability
  ↓
Create Serena project
  ↓
Create tasks
  ↓
Main agent plans
  ↓
Update task status ("doing")
  ↓
Invoke subagents (with project ID)
  ↓
Subagents use RAG for research
  ↓
Update task status ("done")
  ↓
Complete project
  ↓
Deliver to user (with Serena project link)
```

## Benefits of Serena Integration

### 1. Persistent Context
- Full history of what was built
- Decisions documented
- Easy to resume work later

### 2. Better Coordination
- Clear task ownership
- Status visibility
- Progress tracking

### 3. Knowledge Access
- RAG for documentation
- Search existing patterns
- Find solutions faster

### 4. Audit Trail
- What was done
- Why decisions were made
- When tasks completed

### 5. Multi-Session Support
- Work can span multiple sessions
- Context preserved between sessions
- Easy handoff between agents

## Example Commands

### Check if Serena is Available
```
Is Serena MCP available?
```

### Create Project for Feature
```
Create a Serena project called "PDF Table Extraction"
for adding table extraction to the Audio Excel Database
```

### Use RAG During Implementation
```
Search Serena for Python PDF table extraction examples
```

### Update Task Status
```
Mark task "Implementation" as done in the current Serena project
```

## Troubleshooting

### Serena Not Available
**Symptom**: MCP tools not working
**Solutions**:
1. Check VSCode settings.json has Serena configured
2. Reload VSCode window
3. Verify npx can run @serenaai/mcp-server
4. Fall back to TodoWrite for local tracking

### Tasks Not Updating
**Symptom**: Status changes not persisting
**Solutions**:
1. Verify project ID is correct
2. Check task ID is valid
3. Ensure using correct MCP tool name
4. Review Serena logs if available

### RAG Not Finding Results
**Symptom**: Search returns no results
**Solutions**:
1. Try broader search terms
2. Check spelling
3. Use different phrasing
4. Fall back to web search

## Integration Checklist

Before starting a complex feature with Serena:

- [ ] Verify Serena MCP is configured in VSCode
- [ ] Test Serena availability with health check
- [ ] Create a Serena project for the work
- [ ] Create tasks for each workflow phase
- [ ] Include project ID in subagent prompts
- [ ] Update task statuses as work progresses
- [ ] Use RAG for documentation lookup
- [ ] Complete project when done
- [ ] Provide user with Serena project link

## Future Enhancements

Potential improvements to Serena integration:
- Automatic project creation on workflow triggers
- Subagent auto-reporting to Serena
- Cross-project insights and patterns
- Automated project summaries
- Integration with git commits
- Team collaboration features
