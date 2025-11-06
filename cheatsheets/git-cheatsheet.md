# Git Cheatsheet: View-only Commands

## Repository Information
```bash
git remote -v                # List remotes
git status                   # Check working directory status
git status -s                # Short status format
git log --oneline            # Show commit history (compact)
git log --graph --oneline    # Show commit history with graph
git log --follow <file>      # Show history of specific file
git log -p                   # Show commit with patch/diff
git log --stat               # Show commit with file stats
git log --author="name"      # Show commits by author
git log --since="2 weeks ago" # Show commits since date
git log --until="2023-01-01" # Show commits until date
git branch                   # List local branches
git branch -a                # List all branches (local + remote)
git branch -r                # List remote branches only
git branch --merged          # List merged branches
git branch --no-merged       # List unmerged branches
git tag                      # List tags
git tag -l "pattern"         # List tags matching pattern
git tag -l "v1.*"            # List v1.x.x tags
git tag -l "feature/*"       # List feature tags
git tag -l "*-alpha.*"       # List pre-release tags
git tag -n                   # List tags with messages
git tag --sort=-creatordate  # Sort by newest first
git describe                 # Describe current commit with tag
git describe --tags          # Describe with lightweight tags
```

## Viewing Changes
```bash
git diff                     # Show unstaged changes
git diff --staged            # Show staged changes
git diff <commit1> <commit2> # Show differences between commits
git diff HEAD~1              # Show changes in last commit
git show <commit>            # Show commit details
git blame <file>             # Show who changed each line
git grep "pattern"           # Search for pattern in tracked files
```

## Bisecting
*Bisect means "binary search" - it helps you find the exact commit that introduced a bug by systematically testing commits. Think of it as a detective tool that narrows down the problematic commit through a process of elimination.*

### Basic Concept
```bash
You know:
- Commit A (good): Feature works
- Commit Z (bad): Feature is broken

Git bisect will test commits in between:
A → B → C → D → E → F → G → H → I → J → K → L → M → N → O → P → Q → R → S → T → U → V → W → X → Y → Z
```

### Common Bisect Commands
```bash
git bisect start             # Start binary search for bug
git bisect good <commit>     # Mark commit as good
git bisect bad <commit>      # Mark commit as bad
git bisect skip <commit>     # Skip commit (if can't test)
git bisect good              # Mark current commit as good
git bisect bad               # Mark current commit as bad
git bisect skip              # Skip current commit
git bisect reset             # End bisect session
git bisect run <script>      # Automate bisect with script
git bisect visualize         # Show bisect progress
git bisect log               # Show bisect log
```

### Bisect Use Cases
```bash
# Find when a bug or regression was introduced
git bisect start
git bisect good <known-good-commit>
git bisect bad <known-bad-commit>
# Test each commit, mark good/bad
git bisect reset

# Find security vulnerability introduction
git bisect start
git bisect good <commit-without-vulnerability>
git bisect bad HEAD
# Test performance, mark good/bad
git bisect reset

# Find when a breaking change or dependency issue started
git bisect start
git bisect good <known-working-commit>
git bisect bad HEAD
# Run tests e.g., `npm run` or `npm install && npm start` and mark good/bad
git bisect reset

# Automated bisect with script
echo '#!/bin/bash
npm test
exit $?' > test-script.sh
chmod +x test-script.sh
git bisect run ./test-script.sh
```

## Bisect vs Log vs Blame
### Use **bisect** for:
- Finding bug introduction points
- Performance regression analysis
- Test failure root cause
- Build breakage investigation
- Security vulnerability tracking

### Use **log** for:
- Viewing commit history
- Finding specific commits
- Understanding changes

### Use **blame** for:
- Finding who changed specific lines
- Understanding file changes
```

# Git Cheatsheet: Edit Commands

## Repository Setup
```bash
git init                     # Initialize new repository
git clone <url>              # Clone existing repository
git remote add <name> <url>  # Add remote repository
git remote remove <name>     # Remove remote
```

## Basic Workflow
```bash
git add <file>               # Stage file
git add .                    # Stage all changes
git add -A                   # Stage all (including deletions)
git add -u                   # Stage only tracked files
git add -p                   # Stage changes interactively
git commit -m "message"      # Commit staged changes
git commit -am "message"     # Stage and commit all tracked files
git commit --amend           # Amend last commit (edit message)
git commit --amend --no-edit # Amend last commit (keep message)
git commit --allow-empty     # Create empty commit
git commit --fixup <commit>  # Create fixup commit
```

## Branching
```bash
git branch <name>            # Create new branch
git checkout <branch>        # Switch to branch
git checkout -b <branch>     # Create and switch to new branch
git switch <branch>          # Switch to branch (newer syntax)
git switch -c <branch>       # Create and switch to new branch
git merge <branch>           # Merge branch into current
git branch -d <branch>       # Delete local branch
git branch -D <branch>       # Force delete local branch
```

## Remote Operations
```bash
git fetch                    # Download changes from remote
git fetch origin             # Fetch from specific remote
git fetch --all              # Fetch from all remotes
git fetch --prune            # Fetch and remove deleted remote branches
git pull                     # Fetch and merge from remote
git pull origin <branch>     # Pull from specific remote branch
git pull --rebase            # Pull with rebase instead of merge
git push                     # Push to remote
git push -u origin <branch>  # Push and set upstream
git push origin --delete <branch> # Delete remote branch
git push --force-with-lease  # Force push safely
git push --force             # Force push (dangerous)
git push --tags              # Push all tags
git push --follow-tags       # Push commits and tags
```

## Undoing Changes
```bash
git reset HEAD <file>        # Unstage file
git reset --soft HEAD~1      # Undo last commit (keep changes)
git reset --hard HEAD~1      # Undo last commit (discard changes)
git reset --hard <branch>    # Reset to specific branch/commit
git reset --mixed HEAD~1     # Undo last commit (unstage changes)
git checkout -- <file>       # Discard changes to file
git checkout HEAD -- <file>  # Restore file from last commit
git revert <commit>          # Create new commit that undoes changes
git clean -fd                # Remove untracked files and directories
git clean -n                 # Preview files to be removed
```

## Stashing
```bash
git stash                    # Stash current changes
git stash push -m "msg"      # Stash with message
git stash list               # List stashes
git stash pop                # Apply and remove latest stash
git stash apply              # Apply latest stash (keep stash)
git stash apply stash@{n}    # Apply specific stash
git stash drop               # Delete latest stash
git stash clear              # Delete all stashes
```

## Tagging
*Tags are named references to specific commits - they're like bookmarks that point to important moments in your project's history.*
*Tags are essential for release management and provide permanent reference points for releases, milestones, or significant commits.*

### Basic Concept
```
Commits: A---B---C---D---E---F---G---H---I---J
Tags:    v1.0.0    v1.1.0        v2.0.0
```

### Common Tagging Commands
```bash
git tag <name>                    # Create lightweight tag
git tag -a <name> -m "msg"        # Create annotated tag
git tag -a <name> <commit-hash> -m "msg" # Create tag for a specific/previous commit
git tag -s <name> -m "msg"        # Create signed tag
git tag -d <tag>                  # Delete local tag
git push origin <tag>             # Push specific tag to remote
git push origin --tags            # Push all tags to remote
git push origin --delete <tag>    # Delete remote tag
git checkout <tag>                # Checkout specific tag
git checkout -b <branch> <tag>    # Create branch from tag
```

### Tagging Use Cases
```bash
# Release versioning
git tag -a v1.0.0 -m "Release version 1.0.0"
git push origin v1.0.0

# Semantic versioning
git tag -a v1.0.1 -m "Fix critical security bug"
git tag -a v1.1.0 -m "Add user authentication feature"
git tag -a v2.0.0 -m "Major release with breaking changes"
git push origin v1.0.1 v1.1.0 v2.0.0

# Pre-release versions
git tag -a v1.1.0-alpha.1 -m "Alpha release for testing"
git tag -a v1.1.0-beta.1 -m "Beta release for user testing"
git tag -a v1.1.0-rc.1 -m "Release candidate 1"
git push origin v1.1.0-alpha.1 v1.1.0-beta.1 v1.1.0-rc.1

# Feature milestones
git tag -a feature/user-auth -m "User authentication feature completed"
git tag -a milestone/api-v2 -m "API v2 milestone reached"
git push origin feature/user-auth milestone/api-v2

# Hotfix markers
git tag -a hotfix/security-patch -m "Critical security patch"
git tag -a fix/memory-leak -m "Fix memory leak in user service"
git push origin hotfix/security-patch fix/memory-leak

# Development branches
git tag -a dev/experimental -m "Experimental features"
git tag -a staging/v1.2.0 -m "Staging version 1.2.0"
git push origin dev/experimental staging/v1.2.0

# Documentation updates
git tag -a docs/api-update -m "API documentation updated"
git tag -a docs/readme-v2 -m "README updated for v2.0"
git push origin docs/api-update docs/readme-v2

# Database migrations
git tag -a db/migration-v1.1 -m "Database migration for v1.1"
git tag -a db/schema-v2.0 -m "Database schema update for v2.0"
git push origin db/migration-v1.1 db/schema-v2.0

# Configuration changes
git tag -a config/prod-v1.1 -m "Production configuration for v1.1"
git tag -a config/env-staging -m "Staging environment configuration"
git push origin config/prod-v1.1 config/env-staging

# Testing milestones
git tag -a test/coverage-80 -m "Test coverage reached 80%"
git tag -a test/performance-v1.1 -m "Performance benchmark for v1.1"
git push origin test/coverage-80 test/performance-v1.1

# Trigger CI/CD pipelines with tags
git tag -a deploy/production -m "Deploy to production" # Tag to trigger deployment
git tag -a test/integration -m "Run integration tests" # Tag to trigger testing
git push origin deploy/production test/integration

# Mark rollback points
git tag -a rollback/v1.0.0 -m "Rollback point for v1.0.0"
git tag -a stable/v1.0.0 -m "Stable version v1.0.0"
git push origin rollback/v1.0.0 stable/v1.0.0
```

### Tag Management
```bash
# Delete old tags
git tag -d v1.0.0-alpha.1                # Delete local tag
git push origin --delete v1.0.0-alpha.1  # Delete remote tag

# Clean up old pre-release tags
git tag -l "*-alpha.*" | xargs git tag -d
git tag -l "*-beta.*" | xargs git tag -d
```

## Tag vs Branch vs Commit

### Use **tag** for:
- Release versioning
- Feature milestones
- Hotfix markers
- Rollback points
- CI/CD triggers

### Use **branch** for:
- Active development
- Feature work
- Experimental changes
- Collaboration

### Use **commit** for:
- Change tracking
- History navigation
- Code review
- Merge operations

## Rebasing

### Common Rebase Commands
```bash
git rebase <branch>          # Rebase current branch onto target branch
git rebase -i HEAD~3         # Interactive rebase of last 3 commits
git rebase -i main           # Interactive rebase from main
git rebase --onto <newbase> <upstream> <branch> # Rebase onto different commit e.g. main~1 main feature
git rebase --continue        # Continue after resolving conflicts
git rebase --abort           # Abort rebase and return to original state
git rebase --skip            # Skip current commit during rebase
git rebase --autosquash      # Automatically squash fixup commits
git rebase --no-ff           # Force non-fast-forward rebase
```

### Rebase Use Cases
```bash
# Keep feature branch up-to-date with main
git checkout feature
git rebase main
# Result: Your feature branch sits on a linear, up-to-date main branch without merge commits

# Clean up a specific number of recent commits
git rebase -i HEAD~3        # Edit last 3 commits
# Result: Quick local cleanup of a few recent commits

# Clean up entire commit history before submitting a PR
git checkout feature
git rebase -i main
# In editor: pick, reword, edit, squash, drop
# Result: Clean, linear history ready for PR

# Update fork with upstream
git remote add upstream <url>
git fetch upstream
git rebase upstream/main
git push --force-with-lease origin <branch>
# Result: Your fork is now up-to-date with upstream
```

## Cherry-Picking

### Common Cherry-Pick Commands
```bash
git cherry-pick <commit>          # Apply specific commit to current branch
git cherry-pick <commit1> <commit2> <commit3> # Apply multiple commits
git cherry-pick <start>..<end>    # Apply range of commits
git cherry-pick --no-commit <commit> # Apply without committing
git cherry-pick -e <commit>       # Edit commit message
git cherry-pick -s <commit>       # Add sign-off
git cherry-pick -x <commit>       # Add reference to original commit
git cherry-pick --continue        # Continue after resolving conflicts
git cherry-pick --abort           # Abort cherry-pick operation
git cherry-pick --skip            # Skip current commit
```

### Cherry-Pick Use Cases
```bash
# Apply hotfix to multiple branches
git checkout release-v1.0
git cherry-pick <hotfix-commit>
# Result: The fix is now in both branches

# Move commit from wrong branch
git checkout feature-branch
git cherry-pick <commit>
git checkout main
git reset --hard HEAD~1
# Result: Commit is now on the correct branch

# Backport feature to older version
git checkout release-v2.1
git cherry-pick <feature-commit>
# Result: Feature is now available in v2.1
```

## Cherry-Pick vs Rebase vs Merge

### Use **cherry-pick** for:
- Hotfixes to multiple branches
- Moving specific commits
- Backporting features
- Selective integration

### Use **rebase** for:
- Clean linear history
- Keeping feature branch up-to-date
- Interactive history editing
- Before sharing commits

### Use **merge** for:
- Preserving branch history
- Shared/public branches
- Collaborative development
- Seeing merge points
