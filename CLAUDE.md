# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

**kiki** is a Claude Code plugin that provides an intelligent git commit agent to create focused, well-structured commits from your changes. The plugin is distributed via the Claude Code plugin marketplace as `ki@kiki`.

**GitHub**: targc/kiki

## Plugin Architecture

This is a **plugin repository**, not a traditional code repository. It contains:

- **Agent**: The git-commiter agent (markdown file in `agents/`)
- **Command**: Slash command to invoke the agent (markdown file in `commands/`)
- **Configuration**: Plugin metadata in `plugin.json`

The plugin is designed to be installed in other projects via:
```bash
/plugin marketplace add targc/kiki
/plugin install ki@kiki
```

## Core Functionality

The plugin provides a git-commiter agent that analyzes your uncommitted changes and creates multiple focused commits instead of batching everything into one large commit.

**Key principle**: Small, focused commits make git history useful and code review easier.

## Agent

### git-commiter

- **Purpose**: Analyzes uncommitted changes and creates multiple focused commits instead of batching into one
- **Tools**: Read, Bash (restricted to git commands only)
- **Model**: sonnet
- **Key behavior**:
  - **READ-ONLY for code**: Never modifies any code files
  - **WRITE-ONLY for commits**: Only creates git commits
  - Groups changes logically by type, scope, or purpose
  - Creates one commit per logical change
  - Uses conventional commit format
  - Verifies all changes are committed (nothing lost)
- **Safety rules**:
  - Only uses safe git commands: `status`, `diff`, `add`, `commit`, `log`
  - Never uses destructive git commands: `reset`, `checkout`, `restore`, `stash`, `clean`, `commit --amend`
  - Never modifies files (no Edit, Write, formatters, linters)
  - Verifies working tree is clean after all commits
- **Output**: Multiple focused git commits with clear messages
- **When to use**:
  - Multiple unrelated changes uncommitted
  - Preparing for PR with clean git history
  - Making code review easier
  - Organizing work after implementing multiple things

## Slash Command

### /spawn-git-commiter

- **Trigger**: `/spawn-git-commiter [optional description]`
- **Agent**: git-commiter
- **Purpose**: Analyze uncommitted changes and create multiple focused commits
- **Behavior**:
  1. Analyzes `git status` and `git diff` to understand changes
  2. Groups changes logically (by type, scope, or purpose)
  3. Shows commit plan to user
  4. Creates commits in sequence
  5. Verifies all changes are committed (nothing lost)
- **Examples**:
  - `/spawn-git-commiter` - Analyze and commit all changes
  - `/spawn-git-commiter organize my feature work` - Commit with context
- **Use cases**:
  - Multiple unrelated changes to organize
  - Preparing clean commits for PR
  - Creating logical git history for code review

## Design Philosophy

The plugin follows these principles:

- **Lean and Simple** - Focused on one task: creating good commits
- **Safety First** - Never modifies code, only creates commits
- **Focused Commits** - One logical change per commit
- **Clear History** - Makes git log useful for understanding changes
- **Conventional Format** - Uses standard commit message format

## File Structure

```
kiki/
├── agents/
│   └── git-commiter.md               # Git commit agent
├── commands/
│   └── spawn-git-commiter.md         # Slash command to invoke agent
├── plugin.json                       # Plugin metadata and configuration
├── README.md                         # Plugin documentation
└── CLAUDE.md                         # This file
```

## Commit Message Format

The agent uses conventional commit format:

```
type(scope): short description

Longer explanation if needed (why, not what).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

Co-Authored-By: Claude <noreply@anthropic.com>
```

### Commit Types
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `refactor`: Code refactoring
- `test`: Test additions/changes
- `chore`: Maintenance tasks
- `style`: Code style changes

### Examples
```
feat(auth): add password reset endpoint
fix(api): correct validation in user creation
docs(readme): update installation steps
refactor(db): simplify query builder
test(auth): add login flow tests
chore(deps): update dependencies
```

## Working with This Plugin Repository

### Making Changes to the Agent

1. **Edit** `agents/git-commiter.md`
2. **Agent structure**:
   ```markdown
   ---
   name: git-commiter
   description: What this agent does
   model: sonnet
   color: blue
   tools: [Read, Bash]
   ---

   Agent instructions here...
   ```
3. **Test changes** by using the agent in a project where the plugin is installed

### Making Changes to the Command

1. **Edit** `commands/spawn-git-commiter.md`
2. **Command structure**:
   ```markdown
   ---
   description: What this command does
   ---

   Command instructions here...
   ```

### Updating Plugin Metadata

Edit `plugin.json` to update:
- Version number
- Description
- Agent/command configuration
- Keywords and categories
- Compatibility information

### Publishing Updates

After making changes:
1. Commit changes to git
2. Push to GitHub
3. Users with the plugin installed will need to reinstall to get updates
4. New installations automatically get the latest version from the marketplace

## Common Development Tasks

### Testing Agent Changes Locally

1. Make edits to `agents/git-commiter.md`
2. In a test project with the plugin installed:
   ```
   /spawn-git-commiter
   ```
3. Verify behavior matches expectations

### Updating Agent Behavior

1. Edit `agents/git-commiter.md` to modify instructions
2. Test in a project with uncommitted changes
3. Verify commits are created correctly
4. Check commit messages follow format

## Integration with Target Projects

When this plugin is installed in a project, it installs to:

```
target-project/
├── .claude/
│   ├── agents/
│   │   └── git-commiter.md          # Git commit agent
│   └── commands/
│       └── spawn-git-commiter.md    # Slash command
└── (your project files)             # Agent only reads and commits these
```

The agent operates on your existing git repository:
- Reads uncommitted changes via `git status` and `git diff`
- Creates commits via `git add` and `git commit`
- Never modifies your code files
- Only creates commits in your git history

## Quality Standards

### For Commits (git-commiter)

**Safety:**
- ✅ NO code files modified (read-only operation)
- ✅ NO destructive git commands used
- ✅ ALL uncommitted changes are committed (nothing lost)
- ✅ `git status` shows "working tree clean" after completion

**Commit Quality:**
- ✅ Each commit represents one logical change
- ✅ Commit messages are clear and descriptive
- ✅ Uses conventional commit format
- ✅ Git history is clean and readable
- ✅ No unrelated changes batched together
- ✅ Includes Claude Code attribution in every commit

**Verification:**
- ✅ Each commit verified with `git log -1 --stat` after creation
- ✅ Final `git status` check shows all changes committed
- ✅ Summary of all commits shown to user at the end

## Notes for Claude Code Instances

- **This is a plugin repository**: You're not implementing application code here; you're modifying the git-commiter agent and command
- **Agent file is instructions**: The markdown file in `agents/` becomes the prompt for the git-commiter sub-agent
- **Safety is paramount**: The agent must NEVER modify code files, only create commits
- **Focused commits**: The agent's goal is to create multiple small commits, not one large commit
- **Conventional format**: All commits should follow conventional commit message format
- **User safety**: Agent verifies all changes are committed (nothing lost) before completing
