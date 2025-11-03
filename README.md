# ki - Git Commit Agent Plugin

An intelligent git commit agent for Claude Code that analyzes your uncommitted changes and creates multiple focused commits instead of batching everything into one large commit.

## Overview

The ki plugin provides a specialized git-commiter agent that:
- Analyzes your uncommitted changes
- Groups changes logically (by type, scope, or purpose)
- Creates multiple focused commits
- Uses conventional commit format
- Never modifies your code (read-only for code, write-only for commits)

**Key principle:** Small, focused commits make git history useful and code review easier.

## Features

- **Intelligent Grouping** - Automatically groups changes by type, scope, or purpose
- **Conventional Commits** - Uses standard commit message format (feat, fix, docs, etc.)
- **Safety First** - Never modifies code files, only creates git commits
- **Multiple Strategies** - Groups by file, feature, type, or dependency order
- **Verification** - Ensures all changes are committed (nothing lost)

## Installation

### Method 1: Via /plugin Command (Recommended)

```bash
# Add the marketplace
/plugin marketplace add targc/kiki

# Install the plugin
/plugin install ki@kiki
```

Then restart Claude Code.

### Method 2: Direct Copy (Single Project)

```bash
# From the plugin directory
cp -r agents/* /path/to/your/project/.claude/agents/
cp -r commands/* /path/to/your/project/.claude/commands/
```

### Method 3: Symlink (Multiple Projects)

```bash
# Clone the plugin
git clone https://github.com/targc/kiki ~/claude-plugins/ki

# Create symlinks in your project
cd /path/to/your/project/.claude/
ln -s ~/claude-plugins/ki/agents/* agents/
ln -s ~/claude-plugins/ki/commands/* commands/
```

## Usage

### Basic Usage

```
/spawn-git-commiter
```

This will:
1. Analyze uncommitted changes (`git status`, `git diff`)
2. Group changes logically
3. Show you the commit plan
4. Create commits in sequence
5. Verify all changes are committed

### Example Session

```
User: /spawn-git-commiter

Agent:
Analyzing changes...

I found the following changes:
- agents/git-commiter.md (new file)
- commands/spawn-git-commiter.md (new file)
- plugin.json (modified)
- CLAUDE.md (modified)
- README.md (modified)

I'll create 3 commits:

1. feat(agent): add git-commiter agent
   - agents/git-commiter.md
   - commands/spawn-git-commiter.md

2. chore(config): update plugin configuration
   - plugin.json

3. docs: update documentation for kiki plugin
   - CLAUDE.md
   - README.md

Proceeding with commits...

✅ Created commit 1/3: feat(agent): add git-commiter agent
✅ Created commit 2/3: chore(config): update plugin configuration
✅ Created commit 3/3: docs: update documentation for kiki plugin

All changes committed successfully!
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

### Example Commits

```
feat(auth): add password reset endpoint
fix(api): correct validation in user creation
docs(readme): update installation steps
refactor(db): simplify query builder
test(auth): add login flow tests
chore(deps): update dependencies
```

## Grouping Strategies

The agent uses different strategies based on your changes:

### Strategy 1: By File
If each file represents a distinct change:
- Commit 1: `file1.ts` changes
- Commit 2: `file2.ts` changes
- Commit 3: `file3.ts` changes

### Strategy 2: By Feature
If changes span multiple files for one feature:
- Commit 1: All authentication changes (across 5 files)
- Commit 2: All API endpoint changes (across 3 files)
- Commit 3: All documentation updates (across 2 files)

### Strategy 3: By Type
If changes are varied:
- Commit 1: All new features
- Commit 2: All bug fixes
- Commit 3: All refactoring
- Commit 4: All documentation

### Strategy 4: By Dependency Order
If changes build on each other:
- Commit 1: Database schema changes
- Commit 2: Data models
- Commit 3: API endpoints
- Commit 4: Tests

## Safety Features

The git-commiter agent is designed with safety as the top priority:

**Code Safety:**
- ✅ Never modifies any code files (read-only)
- ✅ Only uses safe git commands (`status`, `diff`, `add`, `commit`, `log`)
- ✅ Never uses destructive commands (`reset`, `checkout`, `restore`, `stash`, `clean`, `commit --amend`)
- ✅ No Edit, Write, or file modification tools available

**Verification:**
- ✅ Verifies each commit after creation with `git log -1 --stat`
- ✅ Checks `git status` after all commits
- ✅ Ensures working tree is clean (all changes committed, nothing lost)
- ✅ Shows summary of all commits created

## When to Use

Use this agent when:
- You have multiple unrelated changes uncommitted
- You want a clean, granular git history
- You're preparing for a PR and want focused commits
- You want to make code review easier
- You've been working on multiple things and need to organize commits

**Don't use when:**
- All changes are truly related and should be one commit
- Changes are trivial (single typo fix)
- You specifically want one commit

## Design Philosophy

- **Lean and Simple** - Focused on one task: creating good commits
- **Safety First** - Never modifies code, only creates commits
- **Focused Commits** - One logical change per commit
- **Clear History** - Makes git log useful for understanding changes
- **Conventional Format** - Uses standard commit message format

## Project Structure

After installation, the plugin installs to:

```
your-project/
├── .claude/
│   ├── agents/
│   │   └── git-commiter.md          # Git commit agent
│   └── commands/
│       └── spawn-git-commiter.md    # Slash command
└── (your project files)             # Agent only reads and commits these
```

## How It Works

1. **Analysis**: Runs `git status` and `git diff` to understand what changed
2. **Grouping**: Groups changes logically based on type, scope, or purpose
3. **Planning**: Shows you the commit plan and waits for confirmation
4. **Execution**: Creates commits one by one in sequence
5. **Verification**: Verifies each commit and final working tree state

The agent never modifies your code - it only reads changes and creates git commits.

## Troubleshooting

**Agent not found:**
- Ensure files are in `.claude/agents/` directory
- Restart Claude Code after installation

**No changes to commit:**
- Run `git status` to verify you have uncommitted changes
- Check that changes are in tracked files

**Commits not created:**
- Check git repository is initialized (`git status`)
- Verify you have write permissions
- Review git configuration

## Examples

### Example 1: Multiple Feature Work

```
You've implemented:
- New authentication endpoints
- Updated user profile UI
- Added tests
- Updated documentation

Result: 4 focused commits instead of one large commit
```

### Example 2: Bug Fixes and Refactoring

```
You've fixed:
- Bug in login validation
- Bug in API response handling
- Refactored database queries
- Updated error messages

Result: 2 fix commits, 1 refactor commit, 1 docs commit
```

## Contributing

To improve this plugin:

1. Fork the repository at [targc/kiki](https://github.com/targc/kiki)
2. Make your changes
3. Test with real projects
4. Submit a pull request

## License

MIT

## Credits

Created for clean, focused git commits in all types of projects.

## Support

For issues or questions:
- Open an issue on [GitHub](https://github.com/targc/kiki/issues)
- Check the agent file (`agents/git-commiter.md`) for detailed behavior
- Review CLAUDE.md for technical details
