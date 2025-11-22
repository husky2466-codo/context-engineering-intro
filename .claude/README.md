# Claude Code Workspace Configuration

This directory contains the Claude Code configuration for the multi-project workspace.

## 📁 Structure

```
.claude/
├── agents/                      # Specialized subagent definitions
│   ├── python-developer.md      # Python implementation specialist
│   ├── documentation-writer.md  # Documentation specialist
│   ├── code-reviewer.md         # Code quality and security
│   └── test-engineer.md         # Testing specialist
├── commands/                    # Slash commands for common workflows
│   ├── implement-feature.md     # Feature implementation workflow
│   ├── fix-bug.md              # Bug fixing workflow
│   ├── review-code.md          # Code review workflow
│   ├── create-tests.md         # Test creation workflow
│   ├── update-docs.md          # Documentation workflow
│   └── parallel-dev.md         # Parallel development workflow
├── CLAUDE.md                    # Main orchestration rules
├── SERENA_INTEGRATION.md        # Serena MCP integration guide
├── README.md                    # This file
└── settings.local.json          # Local settings

```

## 🚀 Quick Start

### Using Subagents

Subagents are automatically invoked based on the work you're doing:

**Python work**:
```
"Implement PDF table extraction in Audio Excel Database"
→ Invokes: python-developer, test-engineer, documentation-writer
```

**Code review**:
```
"Review the PDF processor code for security issues"
→ Invokes: code-reviewer
```

### Using Slash Commands

Slash commands provide structured workflows:

- `/implement-feature` - Feature implementation with subagents
- `/fix-bug` - Bug fixing workflow
- `/review-code` - Comprehensive code review
- `/create-tests` - Test suite creation
- `/update-docs` - Documentation updates
- `/parallel-dev` - Parallel development across projects

Example:
```
/implement-feature

I want to add table extraction to the PDF processor
```

## 🤖 Available Subagents

### python-developer
**Expertise**: Python, PDF processing, Excel manipulation, file monitoring
**Use for**: Implementing Python features, data processing, testing

### documentation-writer
**Expertise**: Technical writing, README files, API docs, user guides
**Use for**: Creating/updating documentation, setup instructions

### code-reviewer
**Expertise**: Code quality, security analysis, best practices, performance
**Use for**: Reviewing code, security audits, quality checks

### test-engineer
**Expertise**: pytest, test design, coverage analysis
**Use for**: Creating test suites, ensuring quality, edge case testing

## 🔄 Workflow Patterns

### Standard Feature Implementation
```
1. Plan feature
2. [Parallel] Invoke python-developer
3. [Parallel] Invoke test-engineer
4. [Parallel] Invoke documentation-writer
5. [Sequential] Invoke code-reviewer
6. Deliver
```

### Bug Fix
```
1. Analyze bug
2. Invoke python-developer specialist
3. Invoke test-engineer for regression tests
4. Invoke code-reviewer
5. Deliver
```

### Documentation Sprint
```
1. Identify documentation gaps
2. [Parallel] Invoke documentation-writer for all projects
3. Deliver
```

## 📊 Workspace Projects

### myro-productions-workspace
- **Tech**: Python, PDF processing, Excel manipulation
- **Subagent**: python-developer
- **Focus**: Audio and Lighting Excel Database tools for equipment management

### AI-Tech-Agent
- **Tech**: Mixed (documentation, schemas, data)
- **Subagent**: documentation-writer, python-developer
- **Focus**: AI agent resources and examples

### context-engineering-intro
- **Tech**: Documentation and examples
- **Subagent**: documentation-writer
- **Focus**: Context engineering patterns and best practices

## 🎨 Serena MCP Integration

If Serena MCP server is available:

### Benefits
- Project management and task tracking
- RAG-powered documentation search
- Persistent history across sessions
- Multi-agent coordination

### Quick Start
```
1. Verify Serena is configured in VSCode settings
2. Check availability: "Is Serena available?"
3. Use workflows with automatic project creation
```

See [SERENA_INTEGRATION.md](SERENA_INTEGRATION.md) for detailed guide.

## 📝 Configuration

### settings.local.json
Contains local permissions for CLI commands:
- WSL installation commands
- Echo for debugging

### CLAUDE.md
Main orchestration file defining:
- Workflow patterns
- Subagent invocation rules
- Quality standards
- Best practices

## 🎯 Best Practices

### Do's ✅
- Use parallel execution when tasks are independent
- Provide clear context to subagents
- Review subagent output before delivery
- Update Serena project status (if available)
- Invoke specialized subagents for their expertise

### Don'ts ❌
- Don't invoke subagents for trivial tasks
- Don't use sequential when parallel is possible
- Don't skip quality checks (code review)
- Don't omit testing phase
- Don't forget to update documentation

## 🔍 Examples

### Example 1: Add Feature to Python Project
```
User: "Add OCR support to PDF processor"

Claude Code:
1. Analyzes requirements
2. [Parallel execution]:
   - Invokes python-developer to implement OCR
   - Invokes test-engineer to create tests
   - Invokes documentation-writer to document feature
3. Invokes code-reviewer to verify quality
4. Delivers complete feature with tests and docs
```

### Example 2: Documentation Update
```
User: "Update README for all Python projects"

Claude Code:
1. [Parallel execution]:
   - Invokes documentation-writer for myro-productions-workspace
   - Invokes documentation-writer for AI-Tech-Agent
2. Delivers updated documentation for all projects
```

## 🚨 Troubleshooting

### Subagent Not Found
**Issue**: "Subagent X not found"
**Solution**: Verify agent file exists in `.claude/agents/`

### Slash Command Not Working
**Issue**: Command doesn't trigger
**Solution**:
1. Ensure markdown file exists in `.claude/commands/`
2. Check frontmatter has `description` field
3. Reload VSCode if needed

### Serena Not Available
**Issue**: MCP tools not working
**Solution**:
1. Check VSCode settings.json configuration
2. Reload VSCode window
3. Fall back to TodoWrite for local tracking

## 📚 Additional Resources

- [CLAUDE.md](CLAUDE.md) - Full orchestration rules
- [SERENA_INTEGRATION.md](SERENA_INTEGRATION.md) - Serena MCP guide
- [Context Engineering Intro](../context-engineering-intro/) - Context engineering patterns

## 🔄 Continuous Improvement

This configuration is designed to evolve:
- Update subagent prompts based on experience
- Add new slash commands for common patterns
- Refine workflow based on what works
- Share learnings across projects

---

**Version**: 1.0
**Last Updated**: 2025-11-22
**Workspace**: c:\dev\projects\
