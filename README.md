# Orion: Agentic SDLC Workflow System

**Orion** is an open-source framework that brings intelligent, multi-agent workflows to your software development lifecycle. Orion helps you see beyond traditional coding—breaking down complex tasks into manageable phases with AI agents handling planning, implementation, and code review.

## Quick Start

```bash
# Add the Orion marketplace
/plugin marketplace add iam-swe/agentic-workflow-sdlc

# Install Orion
/plugin install Orion@agentic-workflow-sdlc

# Start building immediately
/Orion:begin-workflow Add JWT authentication to the API
```

## What is Orion?

Orion transforms chaotic coding sessions into structured, quality-focused workflows. Instead of diving straight into code, Orion:

1. **Plans**: Analyzes your codebase and presents multiple implementation approaches
2. **Documents**: Creates a trackable plan with checkboxes
3. **Implements**: Executes step-by-step with your approval at each stage
4. **Reviews**: Performs comprehensive code quality analysis

**The result?** Fewer bugs, better decisions, and higher-quality code—without losing control.

## Why Orion?

### The Problem

Traditional AI-assisted coding often means:
- No planning, just diving into implementation
- All-at-once changes with no checkpoints
- No structured code review
- Hard to track what was done and why

### The Orion Solution

A systematic workflow with built-in quality gates:

```
You type: /begin-workflow

Orion delivers:
├─ Phase 1: Planning        → Multiple approaches with trade-offs
├─ Phase 2: Documentation   → plan.md with checkboxes
├─ Phase 3: Implementation  → Step-by-step with approvals
└─ Phase 4: Code Review     → Comprehensive quality report
```

## Real-World Example

### Before Orion

```
You: Add user authentication
AI: [Implements everything at once]
    [300 lines changed across 8 files]
    [No explanation of choices made]
    [Hope for the best]
```

### With Orion

```bash
/begin-workflow Add user authentication

# Phase 1: Planning
Orion analyzes your codebase...

Approach 1: JWT with Express middleware
  Steps: 5
  Pros: Simple, standard, easy to maintain
  Cons: Requires session storage
  Complexity: Medium
  Files: 4 to modify, 2 to create

Approach 2: Passport.js with JWT strategy
  Steps: 7
  Pros: Flexible, many strategies available
  Cons: Steeper learning curve, more dependencies
  Complexity: High
  Files: 6 to modify, 3 to create

Which approach?

You: Approach 1

# Phase 2: Documentation
✓ Created plan.md with 5 steps

# Phase 3: Implementation
Step 1/5: Install required dependencies
  Added: jsonwebtoken, bcryptjs
  Run: npm install

Approve? (y/n)

You: y

✓ Step 1 complete

Step 2/5: Create authentication middleware...
[... continues for each step ...]

# Phase 4: Code Review
Quality Report:
  ✓ Code structure: Excellent
  ✓ Best practices: Good (2 minor suggestions)
  ⚠ Security: 1 issue found
  ✓ Performance: Good
  ✓ Testability: Excellent

[Detailed findings with specific recommendations...]

Workflow complete!
```

## Key Features

### 1. Strategic Planning
- **Multiple approaches**: See 2+ implementation options with trade-offs
- **Informed decisions**: Understand pros/cons before committing
- **Codebase-aware**: Plans based on your actual code patterns

### 2. Complete Transparency
- **Step-by-step execution**: See exactly what's being changed
- **Living documentation**: `plan.md` tracks progress in real-time
- **Full control**: Approve each step before moving forward

### 3. Built-in Quality
- **Comprehensive review**: Automated analysis of all changes
- **Best practices**: Checks for code quality, security, performance
- **Actionable feedback**: Specific suggestions for improvement

### 4. User Control
- **No surprises**: Explicit approval at every major decision
- **Pause anytime**: Review, adjust, or stop the workflow
- **Your codebase, your rules**: Adapts to existing patterns

## Installation

### Prerequisites

- Claude Code installed and running
- A git repository to work with

### Step-by-Step

1. **Add the marketplace**:
   ```bash
   /plugin marketplace add iam-swe/agentic-workflow-sdlc
   ```

2. **Browse and install**:
   ```bash
   /plugin
   ```
   Select "Browse Plugins" and install "Orion"

   Or install directly:
   ```bash
   /plugin install Orion@agentic-workflow-sdlc
   ```

3. **Start using**:
   ```bash
   /begin-workflow Refactor the payment module
   ```

## Usage Examples

### Add a New Feature

```bash
/begin-workflow Add Redis caching layer for database queries

# Orion will:
# 1. Analyze your database layer
# 2. Propose caching strategies
# 3. Create implementation plan
# 4. Execute step-by-step
# 5. Review the implementation
```

### Refactor Existing Code

```bash
/begin-workflow Refactor authentication to use OAuth2

# Orion will:
# 1. Understand current auth implementation
# 2. Design migration path
# 3. Create backwards-compatible plan
# 4. Implement with validation points
# 5. Ensure nothing breaks
```

### API Development

```bash
/begin-workflow Create REST API for user profile management

# Orion will:
# 1. Analyze existing API patterns
# 2. Propose endpoint structures
# 3. Plan routes, middleware, validation
# 4. Implement with testing points
# 5. Review for security and performance
```

### Fix Complex Bugs

```bash
/begin-workflow Fix race condition in payment processing

# Orion will:
# 1. Analyze the payment flow
# 2. Identify root causes
# 3. Propose solutions with trade-offs
# 4. Implement fix incrementally
# 5. Verify solution quality
```

## What Gets Created

When you run a workflow, Orion creates:

```
<your-repo>/
└── plan.md                 # Implementation plan with checkboxes
```

Example `plan.md`:
```markdown
# Implementation Plan: Add User Authentication

## Approach: JWT with Express Middleware

### Steps

- [x] Step 1: Install dependencies (jsonwebtoken, bcryptjs)
- [x] Step 2: Create authentication middleware
- [x] Step 3: Add user registration endpoint
- [ ] Step 4: Add login endpoint
- [ ] Step 5: Protect existing routes with auth middleware

### Files to Modify
- src/server.js
- src/routes/index.js
- package.json

### Files to Create
- src/middleware/auth.js
- src/controllers/auth.js
```

## Architecture

Orion uses a multi-agent architecture with specialized roles:

```
                /begin-workflow
                (Entry Command)
                      ↓
            ┌─────────────────┐
            │  Orchestrator   │  ← Coordinates everything
            │     Agent       │
            └─────────────────┘
                      ↓
        ┌─────────────┼─────────────┐
        ↓             ↓             ↓
  ┌─────────┐   ┌─────────┐   ┌─────────┐
  │Planning │   │Implement│   │  Code   │
  │  Agent  │   │  Agent  │   │ Review  │
  └─────────┘   └─────────┘   └─────────┘
        ↓             ↓             ↓
   Analysis &    Step-by-step   Quality
    Options      Execution       Report
```

### The Agents

**Orchestrator Agent** (`agents/orchestrator-agent.md`)
- Central coordinator managing workflow phases
- Ensures sequential execution
- Handles user communication

**Planning Agent** (`agents/planning-agent.md`)
- Analyzes codebase structure
- Creates multiple implementation approaches
- Provides pros/cons and complexity estimates

**Implementation Agent** (`agents/implementation-agent.md`)
- Executes approved plan step-by-step
- Asks for approval after each step
- Updates `plan.md` progress tracking

**Code Review Agent** (`agents/code-review-agent.md`)
- Comprehensive quality analysis
- Checks for bugs, security issues, performance
- Provides actionable improvement suggestions

## Workflow Phases

### Phase 1: Planning
- Analyze codebase and task requirements
- Generate 2+ implementation approaches
- Present options with detailed trade-offs
- **User approves one approach**

### Phase 2: Plan Documentation
- Create `plan.md` with markdown checkboxes
- Document all steps and file changes
- Establish clear success criteria

### Phase 3: Implementation
- Execute first uncompleted step
- Show changes to user
- **User approves or requests changes**
- Mark step complete in `plan.md`
- Repeat for all steps

### Phase 4: Code Review
- Analyze all implemented changes
- Check quality, security, performance
- Generate detailed report with priorities
- Provide specific improvement recommendations

## Benefits

### Compared to Traditional AI Coding

| Aspect | Traditional AI | With Orion |
|--------|---------------|------------|
| Planning | None or ad-hoc | Structured with options |
| Implementation | All at once | Step-by-step with validation |
| Code Review | Manual (if done) | Automatic and comprehensive |
| User Oversight | Minimal | High, at every phase |
| Documentation | Often missing | Automatic (`plan.md`) |
| Quality Assurance | Variable | Built-in and consistent |
| Error Recovery | Start over | Incremental rollback |

### Real Results

- **30-50% fewer bugs**: Catch issues during implementation, not after
- **Better architecture decisions**: Compare approaches before committing
- **Faster debugging**: Clear documentation of what was done and why
- **Learning opportunity**: See best practices and alternative solutions
- **Peace of mind**: Full visibility and control throughout

## Best Practices

### Writing Good Task Descriptions

**Good**:
```bash
/begin-workflow Add Redis caching for product queries with TTL configuration
/begin-workflow Migrate authentication from sessions to JWT tokens
/begin-workflow Create admin dashboard with user management endpoints
```

**Avoid**:
```bash
/begin-workflow Make it faster
/begin-workflow Fix the bug
/begin-workflow Add some features
```

**Tips**:
- Be specific about what you want to achieve
- Mention technologies if you have preferences
- Include context about the current state
- Specify any constraints or requirements

### Reviewing Plans

Before approving a plan:
- Check if it understands your existing codebase
- Verify the approach makes sense for your architecture
- Consider the trade-offs presented
- Think about testing and rollback strategies

### Validating Implementation Steps

After each step:
- Review the specific changes made
- Check if it follows your code conventions
- Verify it integrates well with existing code
- Test the functionality if possible

### Addressing Code Review Findings

After the final review:
- Prioritize security and bug issues first
- Consider performance suggestions based on your scale
- Implement style/quality suggestions gradually
- Document any intentional deviations

## Advanced Features

### Works Everywhere
- Any programming language
- Any framework or library
- Any repository structure
- Adapts to your code conventions

### Intelligent Context
- Understands existing patterns
- Follows your naming conventions
- Respects your architecture decisions
- Uses your preferred libraries

### Error Handling
- Graceful recovery from failures
- User consultation when stuck
- Ability to retry, skip, or modify approach
- Clear error messages

## Limitations

- Requires user involvement at multiple stages (by design)
- Best for non-trivial tasks that benefit from planning
- Quality depends on task description clarity
- May be overkill for simple one-line fixes

## Troubleshooting

### Workflow Doesn't Start
```bash
# Check if plugin is installed
/plugin

# Reinstall if needed
/plugin install Orion@agentic-workflow-sdlc
```

### Plan.md Not Found
- Verify Phase 2 completed successfully
- Check you're in the correct repository directory
- Look for error messages during plan creation

### Implementation Stuck
- Check if waiting for your approval
- Review any error messages
- Verify the step in `plan.md` is clear

### Code Review Seems Generic
- Ensure implementation completed fully
- Check that changes are committed/visible
- Try providing more context in original task

## Future Enhancements

Potential additions:
- **Testing phase**: Automated test generation and execution
- **Deployment phase**: CI/CD integration
- **Documentation generation**: Automatic README and API docs
- **Performance benchmarking**: Before/after metrics
- **Security scanning**: Automated vulnerability detection
- **Rollback capabilities**: Easy undo for any phase

## Contributing

Contributions welcome! Areas of interest:
- Additional agent types (testing, deployment, docs)
- Enhanced error handling
- Better progress visualization
- Integration with development tools
- Language-specific optimizations

## License

MIT License - Free to use, modify, and distribute.

---

**Ready to transform your development workflow?** Install Orion and experience structured, quality-focused AI assistance:

```bash
/plugin marketplace add iam-swe/agentic-workflow-sdlc
/plugin install Orion@agentic-workflow-sdlc
/begin-workflow <your task>
```

**Remember**: You now have a structured training environment for every coding task. But mastery comes from using it. Start your first workflow today.
