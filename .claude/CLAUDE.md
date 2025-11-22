# Multi-Project Workspace Orchestration

This workspace contains multiple projects spanning different technologies. Use specialized subagents to optimize development workflow with parallel execution and focused expertise.

## 🎯 Core Principle

When working on tasks in this workspace, **leverage subagents for specialized work** to achieve:
- **Parallel execution** - Multiple agents work simultaneously
- **Focused expertise** - Each agent has specialized knowledge
- **Better context management** - Each agent has dedicated context
- **Faster delivery** - Reduce sequential bottlenecks

## 📁 Workspace Structure

```
c:\dev\projects\
├── AI-Tech-Agent/               # AI agent data and schemas
├── context-engineering-intro/   # Context engineering resources
├── myro-productions-workspace/  # Python tools (Excel/PDF processing)
└── .claude/                     # Claude Code configuration
    ├── agents/                  # Specialized subagents
    ├── commands/                # Slash commands
    └── CLAUDE.md               # This file
```

## 🤖 Available Subagents

### python-developer
**Use for**: Python implementation, data processing, PDF/Excel tools
**Expertise**:
- PDF processing (pdfplumber, PyPDF2)
- Excel manipulation (openpyxl)
- File monitoring (watchdog)
- Testing with pytest

**Invoke when**:
- Implementing Python features
- Working on Audio/Lighting Excel Database tools
- Processing PDFs or Excel files
- Setting up Python virtual environments

### documentation-writer
**Use for**: README files, API docs, user guides
**Expertise**:
- Technical documentation
- Setup instructions
- API documentation
- Troubleshooting guides

**Invoke when**:
- Creating or updating README files
- Documenting new features
- Writing setup instructions
- Creating user guides

### code-reviewer
**Use for**: Code quality, security, best practices
**Expertise**:
- Security analysis
- Performance optimization
- Best practice adherence
- Test coverage verification

**Invoke when**:
- After implementing significant features
- Before committing major changes
- When refactoring code
- Security-sensitive changes

### test-engineer
**Use for**: Test suite creation, quality assurance
**Expertise**:
- pytest for Python
- Test fixtures and mocks
- Coverage analysis

**Invoke when**:
- Need comprehensive test suites
- Testing complex workflows
- Verifying edge cases
- Setting up test infrastructure

## 🔄 Workflow Patterns

### Pattern 1: New Feature Implementation

When implementing a new feature across multiple projects:

```
1. PLAN: Main agent breaks down the feature
2. PARALLEL IMPLEMENTATION:
   - Invoke python-developer for backend/processing
3. TESTING:
   - Invoke test-engineer to create comprehensive tests
4. REVIEW:
   - Invoke code-reviewer for quality check
5. DOCUMENTATION:
   - Invoke documentation-writer for docs
```

**Example**:
User: "Add PDF table extraction to the Audio Excel Database tool"

Response:
```
I'll implement PDF table extraction for the Audio Excel Database. Let me coordinate the work:

1. First, I'll invoke the python-developer to implement the feature
2. Then, test-engineer will create comprehensive tests
3. Finally, code-reviewer will ensure quality

[Invoke python-developer in parallel with test infrastructure setup]
```

### Pattern 2: Bug Fix Workflow

```
1. ANALYZE: Main agent identifies the issue
2. IMPLEMENT: Invoke python-developer specialist
3. TEST: Invoke test-engineer to prevent regression
4. REVIEW: Invoke code-reviewer to verify fix
```

### Pattern 3: Documentation Sprint

```
1. AUDIT: Main agent identifies documentation gaps
2. PARALLEL DOCUMENTATION:
   - Invoke documentation-writer for all projects simultaneously
   - Each gets its own context and focus
```

### Pattern 4: Refactoring Project

```
1. PLAN: Main agent creates refactoring strategy
2. REVIEW FIRST: Invoke code-reviewer to identify issues
3. IMPLEMENT: Invoke python-developer
4. TEST: Invoke test-engineer to ensure no regression
5. DOCUMENT: Invoke documentation-writer to update docs
```

## 🚀 Parallel Execution Guidelines

### When to Use Parallel Execution

**ALWAYS use parallel execution when**:
- Tasks are independent (different files/modules)
- Different specializations needed simultaneously
- Documentation can be written alongside implementation
- Multiple projects need similar updates

**Example - Parallel Invocation**:
```python
# In a single message, invoke multiple subagents:
Task(subagent_type="python-developer", prompt="Implement PDF extraction in Audio Excel Database...")
Task(subagent_type="documentation-writer", prompt="Document the PDF extraction feature...")
Task(subagent_type="test-engineer", prompt="Create tests for PDF extraction...")
```

### When to Use Sequential Execution

**Use sequential when**:
- Later task depends on earlier output
- Code review needs completed implementation
- Testing requires finished code
- Documentation needs final API

## 🎨 Serena MCP Integration

When Serena MCP server is available (configured in VSCode settings):

### Project Creation
For significant features or refactors:
```
1. Use Serena to create a project tracking the work
2. Create tasks for each phase/subagent
3. Update task status as subagents complete work
4. Use Serena's RAG for documentation lookup
```

### Task Management
```
- Create task: "Implement PDF table extraction"
- Assign to: python-developer
- Status updates: todo → doing → done
- Add notes about decisions and issues
```

### Benefits
- Track multi-agent workflow progress
- Persistent history of decisions
- RAG-powered documentation access
- Cross-project insights

## 📋 Common Task Triggers

### Python Project Work
**Triggers**: "implement", "fix", "optimize" + Python files
**Action**: Invoke python-developer
**Also consider**: test-engineer (parallel), code-reviewer (after)

### Documentation Tasks
**Triggers**: "document", "README", "guide", "instructions"
**Action**: Invoke documentation-writer
**Can run**: Parallel with implementation

### Code Quality
**Triggers**: "review", "security", "optimize", "refactor"
**Action**: Invoke code-reviewer first
**Then**: Invoke specialist based on language

### Testing
**Triggers**: "test", "coverage", "validation"
**Action**: Invoke test-engineer
**Consider**: After implementation complete

## 🛡️ Quality Standards

### Before Marking Work Complete

All work should meet these standards:

**Python Projects**:
- [ ] Virtual environment set up
- [ ] requirements.txt updated
- [ ] Tests passing (80%+ coverage)
- [ ] Type hints present
- [ ] Error handling comprehensive
- [ ] README updated

**Documentation**:
- [ ] Installation steps clear
- [ ] Usage examples included
- [ ] API documented
- [ ] Troubleshooting section present

## 🔍 Subagent Communication Protocol

### Invoking Subagents

**Include in prompt**:
1. **Context**: What you're working on
2. **Task**: Specific deliverable
3. **Constraints**: File locations, standards to follow
4. **Output location**: Where to place files
5. **Serena project ID** (if applicable)

**Example**:
```
Task(
  subagent_type="python-developer",
  prompt="""
  Implement PDF table extraction feature for Audio Excel Database.

  Context:
  - Project: myro-productions-workspace/Audio Excel Database
  - Existing code uses pdfplumber and openpyxl
  - Users upload PDFs with equipment tables

  Task:
  - Add table extraction using camelot-py
  - Validate extracted data
  - Handle edge cases (rotated tables, multi-page)
  - Update requirements.txt

  Constraints:
  - Follow existing code structure
  - Use type hints
  - Add comprehensive error handling
  - Minimum 80% test coverage

  Output:
  - myro-productions-workspace/Audio Excel Database/
  - Update src/pdf_processor.py
  - Create tests/test_table_extraction.py

  Serena Project: [project-id if available]
  """
)
```

### Receiving Subagent Output

After subagent completes:
1. Review deliverables
2. Verify quality standards met
3. Run tests if applicable
4. Update Serena project status
5. Report to user with summary

## 🎯 Best Practices

### Do's ✅
- **Use parallel execution** when tasks are independent
- **Provide clear context** to subagents
- **Specify output locations** explicitly
- **Update task status** in Serena
- **Review subagent work** before delivery
- **Combine outputs** coherently for user

### Don'ts ❌
- **Don't invoke sequentially** when parallel is possible
- **Don't omit context** in subagent prompts
- **Don't skip quality checks** after subagent work
- **Don't forget to update** Serena project status
- **Don't invoke subagents** for trivial tasks
- **Don't create subagents** for everything (use judgment)

## 📊 Success Metrics

Track and optimize:
- **Time to delivery** - Parallel execution should reduce time
- **Code quality** - Code reviewer findings
- **Test coverage** - Should exceed 80%
- **Documentation completeness** - All projects well-documented
- **Bug regression** - Proper testing prevents issues

## 🔄 Continuous Improvement

### After each multi-agent workflow:
1. **Analyze** what worked well
2. **Identify** bottlenecks or issues
3. **Update** this CLAUDE.md with learnings
4. **Refine** subagent prompts if needed
5. **Share** patterns that work

### Feedback Loop
- Which subagents were most valuable?
- Did parallel execution save time?
- Were handoffs clean?
- Did quality standards hold?

## 🚨 Emergency Protocols

### If Subagent Fails
1. Review error message
2. Attempt recovery with adjusted prompt
3. If persistent, fall back to main agent
4. Document issue for future improvement

### If Parallel Execution Causes Conflicts
1. Identify the conflict (file, logic)
2. Resolve manually or re-invoke sequentially
3. Update this file with pattern to avoid

### If Output Quality Is Poor
1. Review subagent prompt clarity
2. Add more specific constraints
3. Consider breaking into smaller tasks
4. Invoke code-reviewer to identify issues

---

## 🎓 Quick Reference

**New Python Feature**: python-developer → test-engineer → code-reviewer → documentation-writer
**Bug Fix**: python-developer → test-engineer → code-reviewer
**Refactor**: code-reviewer → python-developer → test-engineer
**Documentation Only**: documentation-writer (parallel across projects)

**Parallel Pattern**: Implementation + Testing + Documentation (all at once when possible)
**Sequential Pattern**: Review → Implement → Test → Document (when dependencies exist)
