---
description: Analyze uncommitted changes and create focused commits (direct invocation of git-commiter agent)
---

You are being asked to invoke the **git-commiter** agent.

## Your Task

Take the user's request and invoke the git-commiter agent with it.

The user has provided a task description after the `/spawn-git-commiter` command. Pass this entire task to the git-commiter agent using the Task tool.

## Instructions

1. **Parse the task**: Everything after `/spawn-git-commiter` is the task description (can be empty)
2. **Invoke the agent**: Use the Task tool to invoke `git-commiter`
3. **Pass the task**: Send the complete task description to the agent

## Examples

**Example 1: Basic Commit Request**
```
User: /spawn-git-commiter commit my changes

You should invoke:
Agent: git-commiter
Prompt: "commit my changes"
```

**Example 2: No Additional Context**
```
User: /spawn-git-commiter

You should invoke:
Agent: git-commiter
Prompt: "Analyze uncommitted changes and create focused commits"
```

**Example 3: Specific Grouping Strategy**
```
User: /spawn-git-commiter group by feature and commit

You should invoke:
Agent: git-commiter
Prompt: "group by feature and commit"
```

## What This Agent Does

The git-commiter agent is a **utility agent** that:
- Analyzes uncommitted changes in the git repository
- Groups changes logically (by type, scope, or purpose)
- Creates multiple focused commits instead of one large commit
- Follows conventional commit message format
- Makes git history more readable and useful
- **NEVER modifies code files** (read-only for code analysis)
- Uses only safe git commands (`status`, `diff`, `add`, `commit`, `log`)

**Key Safety Features:**
- Read-only for code (only analyzes existing changes)
- Write-only for git commits
- No destructive git operations allowed
- Verifies all changes are committed (nothing lost)

**Use when:**
- You have multiple unrelated changes uncommitted
- You want clean, granular git history
- You're preparing for a PR and want focused commits

Now invoke the git-commiter agent with the user's task.
