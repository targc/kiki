# Quick Start Guide

Get started with the ki plugin in 5 minutes.

## Installation (30 seconds)

### Via /plugin Command (Easiest!)

```bash
# Add the marketplace
/plugin marketplace add targc/kiki

# Install the plugin
/plugin install ki@kiki

# Restart Claude Code
```

### Via Direct Copy (Alternative)

```bash
# Navigate to your project
cd /path/to/your/project

# Create .claude directory if needed
mkdir -p .claude/agents .claude/commands

# Copy plugin files
cp /path/to/kiki/agents/* .claude/agents/
cp /path/to/kiki/commands/* .claude/commands/
```

## Your First Commit (1 minute)

Make some changes to your files, then:

```
/spawn-git-commiter
```

Watch as the plugin:
1. ✅ Analyzes your uncommitted changes
2. ✅ Groups changes logically
3. ✅ Shows you the commit plan
4. ✅ Creates focused commits
5. ✅ Verifies all changes are committed

## What It Does

The ki plugin creates **multiple focused commits** instead of one large commit.

**Example:**

You've changed:
- `src/auth.ts` (new login feature)
- `src/api.ts` (bug fix)
- `README.md` (docs update)

**Without ki:**
```bash
git add .
git commit -m "various updates"
```
Result: 1 commit with everything mixed together

**With ki:**
```
/spawn-git-commiter
```
Result: 3 commits:
```
feat(auth): add login functionality
fix(api): correct validation error
docs(readme): update installation steps
```

## How It Works

1. **Analyzes Changes**
   ```bash
   git status
   git diff
   ```

2. **Groups Logically**
   - By type (feat, fix, docs)
   - By scope (auth, api, database)
   - By purpose (what the change does)

3. **Shows Plan**
   ```
   I'll create 3 commits:
   1. feat(auth): add login functionality
   2. fix(api): correct validation error
   3. docs(readme): update installation steps
   ```

4. **Creates Commits**
   - One at a time
   - Uses conventional commit format
   - Verifies each commit

5. **Final Check**
   - Ensures all changes are committed
   - Shows summary of commits created

## Safety Features

The agent is designed to be **completely safe**:

- ✅ **Never modifies your code** (read-only)
- ✅ **Only creates commits** (write-only for git)
- ✅ **Uses safe git commands** only
- ✅ **Verifies nothing is lost**

No destructive commands like:
- ❌ `git reset`
- ❌ `git checkout`
- ❌ `git restore`
- ❌ `git stash`
- ❌ `git clean`
- ❌ `git commit --amend`

## Common Usage

### Basic Usage
```
/spawn-git-commiter
```

### With Context
```
/spawn-git-commiter organize my authentication feature work
```

### After Making Changes
```
# You make changes to multiple files
git add .

# Use ki to create focused commits
/spawn-git-commiter
```

## Example Session

```
User: /spawn-git-commiter

Agent:
Analyzing changes...

I found the following changes:
- src/components/Login.tsx (new file)
- src/api/auth.ts (modified)
- src/types/user.ts (new file)
- README.md (modified)
- package.json (modified)

I'll create 3 commits:

1. feat(auth): add login component and authentication
   - src/components/Login.tsx
   - src/api/auth.ts
   - src/types/user.ts

2. docs(readme): add authentication setup instructions
   - README.md

3. chore(deps): add jwt-decode dependency
   - package.json

Proceeding with commits...

✅ Created commit 1/3: feat(auth): add login component and authentication
✅ Created commit 2/3: docs(readme): add authentication setup instructions
✅ Created commit 3/3: chore(deps): add jwt-decode dependency

All changes committed successfully!
Working tree is clean.
```

## Commit Message Format

The agent uses **conventional commits**:

```
type(scope): description

Optional longer explanation.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

Co-Authored-By: Claude <noreply@anthropic.com>
```

### Commit Types

- `feat` - New feature
- `fix` - Bug fix
- `docs` - Documentation
- `refactor` - Code refactoring
- `test` - Tests
- `chore` - Maintenance
- `style` - Code style

## When to Use

**Use ki when:**
- ✅ You have multiple unrelated changes
- ✅ You want clean git history
- ✅ You're preparing for code review
- ✅ You want to organize your work

**Skip ki when:**
- ❌ All changes are related (one commit is fine)
- ❌ Changes are trivial (single typo)
- ❌ You specifically want one commit

## Troubleshooting

**Command not found?**
- Restart Claude Code session
- Check files are in `.claude/commands/`

**Agent not working?**
- Verify files in `.claude/agents/`
- Run `git status` to confirm you have changes

**No changes to commit?**
- Use `git add` to stage changes first
- Or let the agent analyze unstaged changes

## Philosophy

**Small, focused commits make git history useful.**

Each commit should tell a story:
- What changed?
- Why did it change?
- What's the scope/impact?

## Next Steps

After your first successful commit:

1. **Review the commits**: `git log --oneline -5`
2. **See the history**: `git log -p`
3. **Use it regularly**: Better git history = easier debugging

## Need Help?

- **Full documentation**: [README.md](README.md)
- **More examples**: [EXAMPLES.md](EXAMPLES.md)
- **Agent details**: `agents/git-commiter.md`

---

That's it! You're ready to create focused commits with ki.

Happy committing! 🚀
