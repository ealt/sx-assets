# sx Workflow for Sharing AI Assets

This guide covers how to use sx to share AI assets (skills, commands, MCPs)
from this toolchain repository with your projects and team.

## Prerequisites

- Git configured with SSH keys for GitHub access
- sx installed (see [Installation](#installation))

## Installation

### Using Homebrew (macOS/Linux)

```bash
brew tap sleuth-io/tap
brew install sx
```

### Using Install Script

```bash
curl -fsSL https://raw.githubusercontent.com/sleuth-io/sx/main/install.sh | bash
```

## How sx Works

sx uses a **vault-based** system:

1. **Vault**: A git repository containing assets (this toolchain repo)
2. **Lock file**: Stored in `~/.cache/sx/lockfiles/` (not in your project)
3. **Installation**: Assets are installed to `~/.claude/` (skills, commands, etc.)

There is no project-level `sx.txt` or `sx.lock` file - sx manages everything
centrally.

## Initial Setup (One-Time per Machine)

Configure sx to use this toolchain repository as a vault:

```bash
# Initialize with this git repository as the vault
sx init --type git --repo-url git@github.com:ealt/toolchain.git

# Or use interactive mode
sx init
```

### Using Multiple Profiles

If you need to switch between different vaults (personal, team, etc.):

```bash
# Create a named profile
sx profile add team

# Switch to that profile and initialize its vault
sx profile use team
sx init --type git --repo-url git@github.com:TEAM-ORG/toolchain.git

# Switch between profiles
sx profile list
sx profile current
sx profile use personal
```

## Adding and Installing Assets

### From the Vault (by name)

Once your vault is configured, add assets by name:

```bash
# List available assets in the vault
sx vault list

# Add a skill (will prompt for scope)
sx add docs-manager

# Add with defaults, install globally
sx add docs-manager --yes --scope-global

# Install all assets in your lock file
sx install
```

### From a Local Path (during development)

When developing new assets locally:

```bash
# Add from local directory (use explicit flags to avoid detection issues)
sx add skills/my-skill --yes --name my-skill --type skill

# Install
sx install
```

### Browsing Available Assets

```bash
# List all assets in the vault
sx vault list

# Show details for a specific asset (versions, etc.)
sx vault show docs-manager
```

## Publishing New Skills

### 1. Create the Skill

```bash
cd ~/Documents/toolchain

# Copy the template
cp -r skills/_template skills/my-new-skill

# Edit the files:
# - skills/my-new-skill/metadata.toml (name, version)
# - skills/my-new-skill/SKILL.md (skill documentation)
```

### 2. Test Locally

```bash
# Add to your local installation (use explicit flags)
sx add skills/my-new-skill --yes --name my-new-skill --type skill

# Install
sx install

# Test the skill in Claude Code...
```

### 3. Publish to Vault

```bash
cd ~/Documents/toolchain

git add skills/my-new-skill
git commit -m "Add my-new-skill"
git push
```

### 4. Others Can Install

After pushing, others with the same vault configured can:

```bash
# Sync vault to see new assets
sx vault list

# Add and install
sx add my-new-skill --yes --scope-global
sx install
```

## Updating Assets

### For Asset Authors

1. Make changes in the toolchain repo
2. Update version in `metadata.toml`
3. Add as new version: `sx add skills/my-skill --yes --name my-skill --type skill`
4. Commit and push

### For Asset Consumers

```bash
# Remove old version
sx remove my-skill

# Re-add (gets latest from vault)
sx add my-skill --yes --scope-global

# Re-install
sx install
```

## Team Workflow (Fork Model)

For teams, fork the toolchain repository to your organization:

### Initial Setup

1. Fork `ealt/toolchain` to `TEAM-ORG/toolchain`
2. Team members configure the team vault:

```bash
# Create and switch to team profile
sx profile add team
sx profile use team

# Initialize with the team repo
sx init --type git --repo-url git@github.com:TEAM-ORG/toolchain.git
```

### Contributing Skills

1. Create feature branch in team fork
2. Add/modify skills
3. Open PR for review
4. Merge to main = available to team via `sx vault list`

## Troubleshooting

### sx Not Found

```bash
# Check PATH
echo $PATH

# Verify installation
which sx
sx --version
```

### Check Configuration

```bash
# Display current configuration and installed assets
sx config

# Show current profile
sx profile current
```

### Asset Not Showing After Install

1. Restart Claude Code (or your editor)
2. Check installation: `ls ~/.claude/skills/` or `ls ~/.claude/commands/`
3. Try repair: `sx install --repair`

### Wrong Version Installing

```bash
# Check what versions exist
sx vault show asset-name

# Remove and re-add
sx remove asset-name
sx add asset-name --yes --scope-global
sx install
```

## Quick Reference

| Command | Description |
|---------|-------------|
| `sx init` | Initialize vault configuration (interactive) |
| `sx init --type git --repo-url URL` | Initialize with git vault |
| `sx profile add NAME` | Create a named profile |
| `sx profile use NAME` | Switch to a profile |
| `sx vault list` | List available assets in vault |
| `sx vault show NAME` | Show asset versions and details |
| `sx add NAME` | Add asset from vault |
| `sx add PATH --name N --type T` | Add from local path |
| `sx install` | Install assets from lock file |
| `sx install --repair` | Verify and fix installations |
| `sx remove NAME` | Remove asset from lock file |
| `sx config` | Show configuration and status |

## See Also

- [sx Documentation](https://github.com/sleuth-io/sx)
- [Toolchain README](../README.md)
- [Skill Template](../skills/_template/README.md)
