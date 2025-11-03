# Usage Examples

This document provides practical examples of using the ki plugin for creating focused git commits.

## Table of Contents

- [Basic Usage](#basic-usage)
- [Grouping Strategies](#grouping-strategies)
- [Real-World Scenarios](#real-world-scenarios)
- [Common Patterns](#common-patterns)

## Basic Usage

### Example 1: Simple Multiple File Changes

**Scenario:** You've made changes to multiple unrelated files.

**Command:**
```
/spawn-git-commiter
```

**What happens:**

```
Agent:
Analyzing changes...

I found the following changes:
- src/auth.ts (modified)
- src/api.ts (modified)
- README.md (modified)

I'll create 3 commits:

1. feat(auth): add password reset functionality
   - src/auth.ts

2. fix(api): correct validation in user creation
   - src/api.ts

3. docs(readme): update API documentation
   - README.md

Proceeding with commits...

✅ Created commit 1/3: feat(auth): add password reset functionality
✅ Created commit 2/3: fix(api): correct validation in user creation
✅ Created commit 3/3: docs(readme): update API documentation

All changes committed successfully!
```

**Result:** 3 focused commits instead of one large commit.

---

### Example 2: Feature Across Multiple Files

**Scenario:** You've implemented a feature that spans multiple files.

**Command:**
```
/spawn-git-commiter
```

**What happens:**

```
Agent:
Analyzing changes...

I found the following changes:
- src/components/Login.tsx (new file)
- src/components/LoginForm.tsx (new file)
- src/api/auth.ts (new file)
- src/types/user.ts (modified)
- src/hooks/useAuth.ts (new file)

I'll create 1 commit:

1. feat(auth): add login functionality
   - src/components/Login.tsx
   - src/components/LoginForm.tsx
   - src/api/auth.ts
   - src/types/user.ts
   - src/hooks/useAuth.ts

Proceeding with commits...

✅ Created commit 1/1: feat(auth): add login functionality

All changes committed successfully!
```

**Result:** 1 focused commit for the entire feature.

---

## Grouping Strategies

### Strategy 1: By Type

**Scenario:** You've made various types of changes.

**Changes:**
- New feature in `src/dashboard.tsx`
- Bug fix in `src/api.ts`
- Updated docs in `README.md`
- Refactored `src/utils.ts`

**Result:**
```
Commit 1: feat(dashboard): add user statistics widget
Commit 2: fix(api): handle null response correctly
Commit 3: docs(readme): add deployment instructions
Commit 4: refactor(utils): simplify date formatting
```

---

### Strategy 2: By Scope/Component

**Scenario:** Changes to different parts of the application.

**Changes:**
- Multiple files in auth system
- Multiple files in payment system
- Multiple files in notification system

**Result:**
```
Commit 1: feat(auth): add two-factor authentication
  - src/auth/2fa.ts
  - src/auth/middleware.ts
  - src/auth/validation.ts

Commit 2: feat(payment): add subscription management
  - src/payment/subscription.ts
  - src/payment/billing.ts
  - src/payment/plans.ts

Commit 3: feat(notifications): add email templates
  - src/notifications/templates/welcome.html
  - src/notifications/templates/reset.html
  - src/notifications/sender.ts
```

---

### Strategy 3: By Dependency Order

**Scenario:** Changes that build on each other.

**Changes:**
- Database schema
- Data models
- API endpoints
- Tests
- Documentation

**Result:**
```
Commit 1: feat(db): add user preferences table
  - migrations/001_add_preferences.sql

Commit 2: feat(models): add user preferences model
  - src/models/preferences.ts

Commit 3: feat(api): add preferences endpoints
  - src/api/preferences.ts

Commit 4: test(preferences): add preferences tests
  - tests/preferences.test.ts

Commit 5: docs(preferences): document preferences API
  - README.md
```

---

## Real-World Scenarios

### Scenario 1: Feature Development Day

**Context:** You spent the day working on a new feature but also fixed some bugs and updated docs along the way.

**Command:**
```
/spawn-git-commiter
```

**Changes:**
- Main feature files (5 files)
- Bug fix in unrelated file (1 file)
- Documentation update (1 file)
- Dependency update (package.json)

**Result:**
```
Commit 1: feat(profiles): add user profile management
  - src/components/Profile.tsx
  - src/api/profiles.ts
  - src/types/profile.ts
  - src/hooks/useProfile.ts
  - src/pages/ProfilePage.tsx

Commit 2: fix(validation): handle empty email correctly
  - src/utils/validation.ts

Commit 3: docs(profiles): add profile API documentation
  - README.md

Commit 4: chore(deps): add react-hook-form dependency
  - package.json
```

**Benefit:** Clean separation of feature work, bug fixes, docs, and dependencies.

---

### Scenario 2: Refactoring Session

**Context:** You refactored several parts of the codebase.

**Command:**
```
/spawn-git-commiter
```

**Changes:**
- Renamed functions in multiple files
- Moved utility functions
- Simplified complex logic
- Updated imports

**Result:**
```
Commit 1: refactor(auth): rename validateUser to verifyCredentials
  - src/auth/validation.ts
  - src/auth/middleware.ts
  - tests/auth.test.ts

Commit 2: refactor(utils): extract date helpers to separate file
  - src/utils/dates.ts (new)
  - src/utils/helpers.ts (modified)
  - src/components/Calendar.tsx

Commit 3: refactor(api): simplify error handling logic
  - src/api/errors.ts
  - src/api/middleware.ts
```

**Benefit:** Each refactoring is isolated, making it easy to review or revert if needed.

---

### Scenario 3: Bug Fix Marathon

**Context:** You fixed multiple unrelated bugs.

**Command:**
```
/spawn-git-commiter
```

**Changes:**
- Fix in login logic
- Fix in API error handling
- Fix in UI rendering
- Fix in data validation

**Result:**
```
Commit 1: fix(auth): prevent login with empty credentials
  - src/auth/login.ts

Commit 2: fix(api): handle network timeout errors
  - src/api/client.ts

Commit 3: fix(ui): correct button alignment on mobile
  - src/components/Button.tsx
  - src/styles/button.css

Commit 4: fix(validation): validate email format correctly
  - src/utils/validation.ts
```

**Benefit:** Each bug fix is isolated, making it easy to cherry-pick or backport specific fixes.

---

### Scenario 4: PR Preparation

**Context:** You've been working locally for a while and want to organize commits before creating a PR.

**Command:**
```
/spawn-git-commiter
```

**Changes:**
- Feature implementation (8 files)
- Tests (3 files)
- Documentation (2 files)
- Configuration (1 file)

**Result:**
```
Commit 1: feat(search): add full-text search functionality
  - src/api/search.ts
  - src/components/SearchBar.tsx
  - src/components/SearchResults.tsx
  - src/hooks/useSearch.ts
  - src/types/search.ts
  - src/utils/searchUtils.ts
  - src/pages/SearchPage.tsx
  - src/index.ts

Commit 2: test(search): add comprehensive search tests
  - tests/search.test.ts
  - tests/searchUtils.test.ts
  - tests/fixtures/searchData.ts

Commit 3: docs(search): document search API and usage
  - README.md
  - docs/SEARCH.md

Commit 4: chore(config): add search index configuration
  - config/search.json
```

**Benefit:** Clean, logical git history that makes code review easy.

---

## Common Patterns

### Pattern 1: New Feature

**Before:**
```bash
git add .
git commit -m "add user settings"
```

**With ki:**
```
/spawn-git-commiter

Result:
feat(settings): add user settings page
feat(settings): add settings API endpoints
test(settings): add settings tests
docs(settings): document settings feature
```

---

### Pattern 2: Multiple Bug Fixes

**Before:**
```bash
git add .
git commit -m "bug fixes"
```

**With ki:**
```
/spawn-git-commiter

Result:
fix(auth): prevent duplicate login
fix(api): handle 500 errors gracefully
fix(ui): correct responsive layout
```

---

### Pattern 3: Documentation Updates

**Before:**
```bash
git add .
git commit -m "update docs"
```

**With ki:**
```
/spawn-git-commiter

Result:
docs(readme): update installation steps
docs(api): add API endpoint examples
docs(contributing): add contribution guidelines
```

---

### Pattern 4: Dependency Management

**Before:**
```bash
git add .
git commit -m "update dependencies"
```

**With ki:**
```
/spawn-git-commiter

Result:
chore(deps): upgrade react to v18
chore(deps): add axios for HTTP requests
chore(deps): remove unused lodash dependency
```

---

### Pattern 5: Refactoring

**Before:**
```bash
git add .
git commit -m "refactor"
```

**With ki:**
```
/spawn-git-commiter

Result:
refactor(auth): extract validation logic
refactor(api): simplify error handling
refactor(utils): rename helper functions
```

---

## Tips and Best Practices

### Tip 1: Stage All Changes First

```bash
# Stage all changes
git add .

# Then use ki to create organized commits
/spawn-git-commiter
```

The agent will unstage and restage files to create focused commits.

---

### Tip 2: Review the Plan

When the agent shows you the commit plan, review it carefully:
- Are the groupings logical?
- Are commit messages clear?
- Is anything missing?

If needed, you can adjust and run again.

---

### Tip 3: Use After Each Feature

Don't let changes pile up. Use ki regularly:

```bash
# Implement feature
# ... coding ...

# Commit immediately
/spawn-git-commiter

# Start next feature
```

---

### Tip 4: Combine with Code Review

Create focused commits before PR:

```bash
# You've been working on a branch
git status  # Many files changed

# Organize commits
/spawn-git-commiter

# Create PR
git push origin feature-branch
```

Your reviewers will thank you!

---

### Tip 5: Don't Overthink It

The agent will handle the grouping. Just run it:

```bash
/spawn-git-commiter
```

If the grouping isn't perfect, that's okay. It's still better than one large commit.

---

## Commit Message Examples

### Good Commit Messages

```
feat(auth): add two-factor authentication
fix(api): handle timeout errors gracefully
docs(readme): add deployment instructions
refactor(db): simplify query builder
test(auth): add login flow tests
chore(deps): update dependencies to latest
style(ui): fix button spacing
```

### What the Agent Creates

```
type(scope): short description

Optional longer explanation of why this change was made
and what problem it solves.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

Co-Authored-By: Claude <noreply@anthropic.com>
```

---

## Advanced Scenarios

### Scenario 1: Mixed Work Types

**Context:** Feature work, bug fixes, and refactoring all mixed together.

**Changes:**
- New feature (3 files)
- Bug fix (1 file)
- Refactoring (2 files)
- Tests (2 files)
- Docs (1 file)

**Result:** Agent groups by type:
```
Commit 1: feat(dashboard): add analytics widget
Commit 2: fix(auth): prevent session timeout
Commit 3: refactor(utils): extract helper functions
Commit 4: test(dashboard): add widget tests
Commit 5: docs(dashboard): document analytics API
```

---

### Scenario 2: Large Refactoring

**Context:** Renamed files and updated imports throughout codebase.

**Changes:**
- 15 files affected
- Mix of renames and import updates

**Result:** Agent groups logically:
```
Commit 1: refactor(structure): rename components directory
  - All component renames

Commit 2: refactor(imports): update component imports
  - All import updates

Commit 3: refactor(types): update type definitions
  - All type updates
```

---

## Troubleshooting Examples

### Issue: Too Many Small Commits

**Problem:** Agent creates too many small commits.

**Solution:** Some changes should naturally be grouped together. The agent will recognize related changes and group them.

**Example:**
If you created multiple files for one feature, they'll be in one commit:
```
feat(auth): add login system
  - LoginForm.tsx
  - LoginPage.tsx
  - useLogin.ts
  - types.ts
```

---

### Issue: Commits Not Logical

**Problem:** Grouping doesn't make sense for your case.

**Solution:** The agent tries its best, but you can always:
1. Manually stage specific files and commit
2. Use `git reset HEAD~1` to undo last commit and regroup
3. Provide context when invoking: `/spawn-git-commiter group by feature`

---

## Next Steps

After trying these examples:

1. Use ki regularly in your daily workflow
2. Notice how code reviews become easier
3. Appreciate clean git history when debugging
4. Share with your team!

For more information:
- [README.md](README.md) - Full documentation
- [QUICKSTART.md](QUICKSTART.md) - Quick start guide
- [CLAUDE.md](CLAUDE.md) - Technical details
