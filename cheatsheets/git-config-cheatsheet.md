# Git Config Cheatsheet
*Git Config is the configuration system that controls how Git behaves - you can customize everything from your identity to how Git handles files, merges, and more.*

## Quick Reference

### Configuration Levels
- **System** (`/etc/gitconfig`): All users on machine
- **Global** (`~/.gitconfig`): Current user, all repositories  
- **Local** (`.git/config`): Current repository only

### View Configuration
```bash
git config --list                    # List all config
git config --global --list           # List global config
git config --local --list            # List local config
git config user.name                 # Get specific value
git config --get user.name           # Get single value (script-safe)
git config --show-origin user.name   # Show config source
```

### Edit Configuration
```bash
git config --global --edit           # Edit global config
git config --local --edit            # Edit local config
git config --unset user.name         # Remove value
git config --unset-all user.name     # Remove all values
```

## Essential Setup

### User Identity
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

### Editor & Tools
```bash
git config --global core.editor "code --wait"                   # VS Code
git config --global merge.tool vscode                           # VS Code merge tool
git config --global mergetool.vscode.cmd 'code --wait $MERGED'  # VS Code merge
git config --global diff.tool vscode                            # VS Code diff tool
git config --global difftool.vscode.cmd 'code --wait --diff $LOCAL $REMOTE' # VS Code diff
```

### Branch & Merge Behavior
```bash
git config --global init.defaultBranch main
git config --global branch.autosetupmerge always
git config --global branch.autosetuprebase always
git config --global pull.rebase false                           # Use merge (default)
git config --global pull.rebase true                            # Use rebase
git config --global pull.ff only                                # Fast-forward only
git config --global push.default simple
git config --global push.autoSetupRemote true
```

## Visual & UI Configuration

### Colors
```bash
git config --global color.ui auto
git config --global color.branch auto
git config --global color.diff auto
git config --global color.status auto

# Custom branch colors
git config --global color.branch.current yellow reverse
git config --global color.branch.local green
git config --global color.branch.remote red

# Custom diff colors
git config --global color.diff.meta yellow bold
git config --global color.diff.frag magenta bold
git config --global color.diff.old red bold
git config --global color.diff.new green bold
```

### Log & History
```bash
git config --global log.date iso
git config --global log.decorate short
git config --global log.showroot true
git config --global log.abbrevCommit true
git config --global log.follow true
git config --global log.all true
```

## Merge & Rebase Configuration

### Merge Settings
```bash
git config --global merge.conflictstyle diff3                   # 3-way conflict markers
git config --global merge.ours.driver true                      # Use ours strategy
```

### Rebase Settings
```bash
git config --global rebase.autoStash true                       # Auto-stash before rebase
git config --global rebase.autoSquash true                      # Auto-squash fixup commits
git config --global rebase.updateRefs true                      # Update refs during rebase
```

## Cross-Platform Development

### Line Endings
```bash
git config --global core.autocrlf true                          # Windows
git config --global core.autocrlf input                         # Mac/Linux
git config --global core.autocrlf false                         # Disable conversion
git config --global core.eol lf                                 # Unix line endings
git config --global core.eol crlf                               # Windows line endings
```

### File Handling
```bash
git config --global core.ignorecase true                        # Case insensitive
git config --global core.ignorecase false                       # Case sensitive
git config --global core.filemode true                          # Track file permissions
git config --global core.filemode false                         # Ignore file permissions
git config --global core.quotepath false
git config --global core.precomposeunicode true
```

### Global .gitignore
```bash
# Create global .gitignore file
touch ~/.gitignore_global

# Add common patterns
echo "node_modules/" >> ~/.gitignore_global
echo "*.log" >> ~/.gitignore_global
echo ".DS_Store" >> ~/.gitignore_global
echo "*.tmp" >> ~/.gitignore_global

# Configure Git to use global .gitignore
git config --global core.excludesfile ~/.gitignore_global
```

### Help & Autocorrect
```bash
git config --global help.autocorrect 50                         # Auto-correct typos (5 second delay)
git config --global help.format html                            # HTML help format
git config --global help.browser firefox                        # Set help browser
```

## Network & Security

### Proxy Configuration
```bash
git config --global http.proxy http://proxy.company.com:8080
git config --global https.proxy https://proxy.company.com:8080
git config --global http.proxy http://user:pass@proxy.company.com:8080
```

### Credential Management
```bash
git config --global credential.helper store                     # Store credentials
git config --global credential.helper cache --timeout=3600      # Cache for 1 hour
git config --global credential.helper manager-core              # Windows credential manager
git config --global credential.helper osxkeychain               # Mac keychain
git config --global credential.helper ""                        # Disable caching
```

### Security Settings
```bash
git config --global safe.directory /path/to/repo                # Trust specific directory
git config --global safe.directory '*'                          # Trust all directories
git config --global user.signingkey <gpg-key-id>                # GPG signing key
git config --global commit.gpgsign true                         # Sign commits
git config --global tag.gpgsign true                            # Sign tags
git config --global gpg.program gpg                             # GPG program path
git config --global transfer.fsckObjects true                   # Check object integrity
git config --global receive.fsckObjects true                    # Check received objects
```

### Additional Core Settings
```bash
git config --global core.compression 9                          # Maximum compression
git config --global core.loosecompression 1                     # Loose object compression
git config --global core.deltaBaseCacheLimit 128m               # Delta base cache limit
git config --global core.bigFileThreshold 2m                    # Big file threshold
git config --global core.attributesfile ~/.gitattributes_global # Global attributes file
```

## Performance Optimization

### Large Repositories
```bash
git config --global core.preloadindex true
git config --global core.fscache true
git config --global gc.auto 256
git config --global pack.packSizeLimit 2g
git config --global pack.windowMemory 256m
git config --global pack.deltaCacheSize 128m
git config --global pack.threads 0                              # Use all available cores
git config --global pack.indexVersion 2                         # Use index version 2
git config --global repack.useDeltaBaseOffset true              # Use delta base offset
```

### Advanced Performance
```bash
git config --global core.multiPackIndex true                    # Enable multi-pack index
git config --global core.sparseCheckout true                    # Enable sparse checkout
git config --global index.threads 0                             # Use all cores for index operations
git config --global merge.renameLimit 1000                      # Rename detection limit
git config --global diff.renameLimit 1000                       # Diff rename limit
```

## Useful Aliases

### Basic Aliases
```bash
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.unstage 'reset HEAD --'
git config --global alias.last 'log -1 HEAD'
git config --global alias.visual '!gitk'
```

### Advanced Aliases
```bash
git config --global alias.lg "log --oneline --graph --decorate --all"
git config --global alias.lga "log --oneline --graph --decorate --all --author"
git config --global alias.uncommit 'reset --soft HEAD~1'
git config --global alias.amend 'commit --amend --no-edit'
git config --global alias.wip 'commit -am "WIP"'
git config --global alias.unwip 'reset HEAD~1'
```

### Workflow Aliases
```bash
# Quick commit and push
git config --global alias.cp '!f() { git commit -am "$1" && git push; }; f'

# Add, commit, and push
git config --global alias.acp '!f() { git add . && git commit -m "$1" && git push; }; f'

# Amend and push
git config --global alias.ap '!f() { git commit --amend --no-edit && git push --force-with-lease; }; f'

# Quick push current branch
git config --global alias.qp '!f() { git push origin $(git branch --show-current); }; f'

# Smart commit (only if changes exist)
git config --global alias.smart '!f() { 
  if [ -n "$(git status --porcelain)" ]; then
    git add . && git commit -m "$1" && git push;
  else
    echo "No changes to commit";
  fi
}; f'

# Commit with current branch push
git config --global alias.cpb '!f() { 
  git commit -am "$1" && git push origin $(git branch --show-current);
}; f'

# Commit with upstream push
git config --global alias.cpu '!f() { 
  git commit -am "$1" && git push -u origin $(git branch --show-current);
}; f'
```

## Using Aliases

```bash
git cp "Add new feature"                    # Quick commit and push
git acp "Fix bug in authentication"         # Add, commit, and push
git ap                                      # Amend and push
git qp                                      # Quick push current branch
git smart "Update documentation"            # Smart commit (checks for changes)
git cpb "Add new feature"                   # Commit and push current branch
git cpu "Initial commit"                    # Commit and set upstream
```

## Quick Setup Scripts

### New Developer Setup
```bash
# Basic setup
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
git config --global core.editor "code --wait"
git config --global init.defaultBranch main
git config --global pull.rebase false
git config --global push.default simple
git config --global help.autocorrect 50                         # Auto-correct typos

# Essential aliases
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.lg "log --oneline --graph --decorate --all"
```

### Team Development Setup
```bash
# Merge and conflict resolution
git config --global merge.conflictstyle diff3
git config --global merge.tool vscode
git config --global mergetool.vscode.cmd 'code --wait $MERGED'

# Branch management
git config --global branch.autosetupmerge always
git config --global push.autoSetupRemote true

# Visual improvements
git config --global color.ui auto
git config --global log.decorate short
```

### Security-Focused Setup
```bash
# GPG signing
git config --global user.signingkey <gpg-key-id>
git config --global commit.gpgsign true
git config --global tag.gpgsign true

# Safe directories
git config --global safe.directory '*'

# Credential management
git config --global credential.helper cache --timeout=3600
```