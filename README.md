# CLI Tools Collection

A collection of useful command-line tools for developers to streamline daily workflows and boost productivity.

Mine lives at `~/.cli_tools`, but you can put it wherever if you take that into account when setting up the global pathing.

## 🛠️ Tools Overview

| Tool | Description | Usage |
|------|-------------|-------|
| `clean-branches` | Clean up merged Git branches | `./clean-branches [options]` |
| `open-pr` | Open or create pull requests | `./open-pr [options]` |
| `create-gh-issue` | Create GitHub issues | `./create-gh-issue [options]` |

## 📋 Prerequisites

- **Git**: Required for Git-related tools
- **GitHub CLI (`gh`)**: Required for GitHub integration tools
  - Install from: https://cli.github.com/
  - Authenticate with: `gh auth login`

## 🚀 Installation

1. Clone or download this repository
2. Make scripts executable:
   ```bash
   chmod +x clean-branches open-pr create-gh-issue
   ```

## 🌐 Global Access (Add to PATH)

To run these tools from anywhere on your system, add the directory to your PATH:

### macOS & Linux

**Option 1: Add to your shell profile (Recommended)**

1. **Find your shell profile file:**
   ```bash
   # For bash users
   echo $HOME/.bashrc
   
   # For zsh users (macOS default)
   echo $HOME/.zshrc
   
   # For other shells
   echo $HOME/.profile
   ```

2. **Add the path to your profile:**
   ```bash
   # Replace with your actual path
   export PATH="$PATH:/Users/yourusername/.cli-tools"
   ```

3. **Reload your profile:**
   ```bash
   # For bash
   source ~/.bashrc
   
   # For zsh
   source ~/.zshrc
   
   # For other shells
   source ~/.profile
   ```

**Option 2: One-liner setup**
```bash
# For zsh (macOS default)
echo 'export PATH="$PATH:/Users/yourusername/.cli-tools"' >> ~/.zshrc && source ~/.zshrc

# For bash
echo 'export PATH="$PATH:/Users/yourusername/.cli-tools"' >> ~/.bashrc && source ~/.bashrc
```

### Windows

**Option 1: System Environment Variables (GUI)**
1. Open System Properties → Advanced → Environment Variables
2. Edit the `Path` variable
3. Add your CLI tools directory path
4. Restart your terminal

**Option 2: Command line**
```cmd
# Add to user PATH
setx PATH "%PATH%;C:\path\to\your\.cli-tools"

# Or add to system PATH (requires admin)
setx PATH "%PATH%;C:\path\to\your\.cli-tools" /M
```

### Verify Installation

After adding to PATH, you should be able to run tools from anywhere:

```bash
# Test from any directory
clean-branches --help
open-pr --help
create-gh-issue --help
```

### Troubleshooting PATH Issues

**Check if PATH is set correctly:**
```bash
echo $PATH | grep cli-tools
```

**Find the full path to your tools:**
```bash
# From the cli-tools directory
pwd
```

**Test a specific tool:**
```bash
which clean-branches
```

**If tools aren't found:**
1. Verify the path is correct in your profile
2. Make sure you've reloaded your shell profile
3. Check that scripts are executable: `ls -la /path/to/cli-tools`

## 📖 Tool Documentation

### 🔧 clean-branches

Deletes local and remote Git branches that have been merged into the main branch.

**Features:**
- ✅ Safe deletion with confirmation prompts
- 🔍 Dry-run mode to preview changes
- 🎯 Selective cleanup (local/remote only)
- 🎨 Colored output for better UX
- 🛡️ Automatic main branch detection

**Usage:**
```bash
# Interactive cleanup (recommended)
clean-branches

# Preview what would be deleted
clean-branches --dry-run

# Force delete without confirmation
clean-branches --force

# Only clean local branches
clean-branches --local

# Only clean remote branches
clean-branches --remote
```

**Options:**
- `-f, --force` - Skip confirmation prompts
- `-r, --remote` - Only clean up remote branches
- `-l, --local` - Only clean up local branches
- `-d, --dry-run` - Show what would be deleted without actually deleting
- `-h, --help` - Show help message

### 🚀 open-pr

Opens or creates a pull request for the current branch in your browser.

**Features:**
- 🔄 Automatically detects existing PRs
- 📝 Smart title generation from branch names
- 📄 Auto-populates description with commit messages
- 🌐 Opens PR in browser after creation

**Usage:**
```bash
# Open existing PR or create new one
open-pr

# Show help
open-pr --help
```

**How it works:**
1. Checks if a PR already exists for the current branch
2. If no PR exists or it's closed/merged, creates a new one
3. Generates title from branch name (e.g., `feature/PROJ-123-add-thing` → `PROJ-123 Add Thing`)
4. Uses commit messages since branching from main as the description
5. Opens the PR in your default browser

### 🐛 create-gh-issue

Creates GitHub issues with interactive or non-interactive input.

**Features:**
- 💬 Interactive mode for guided issue creation
- ⚡ Non-interactive mode for automation
- 🔍 Automatic GitHub repository detection
- ✅ Validation of prerequisites

**Usage:**
```bash
# Interactive mode
create-gh-issue

# Non-interactive mode
create-gh-issue --title "Bug fix needed" --body "This is the issue description"

# Interactive title, non-interactive body
create-gh-issue --body "Issue description here"
```

**Options:**
- `--title` - Issue title (if not provided, will prompt interactively)
- `--body` - Issue body (if not provided, will prompt interactively)
- `-h, --help` - Show help message

## 🔧 Advanced Usage

### Automation Examples

**Create issues from command line:**
```bash
# Create a bug report
create-gh-issue --title "Fix login bug" --body "Users cannot log in with valid credentials"

# Create a feature request
create-gh-issue --title "Add dark mode" --body "Request to add dark theme option to the application"
```

**Clean up branches in CI/CD:**
```bash
# Clean merged branches without prompts
clean-branches --force
```

**Create PRs from scripts:**
```bash
# Create and open PR
open-pr
```

### Integration with Other Tools

**Combine with Git aliases:**
```bash
# Add to your .gitconfig
[alias]
    cleanup = !clean-branches
    pr = !open-pr
    issue = !create-gh-issue
```

**Use in shell functions:**
```bash
# Add to your .bashrc or .zshrc
function cleanup() {
    clean-branches "$@"
}

function pr() {
    open-pr "$@"
}

function issue() {
    create-gh-issue "$@"
}
```

## 🛠️ Troubleshooting

### Common Issues

**"GitHub CLI (gh) not installed"**
```bash
# Install GitHub CLI
# macOS
brew install gh

# Ubuntu/Debian
sudo apt install gh

# Windows
winget install GitHub.cli
```

**"This is not a git repository"**
- Make sure you're in a Git repository directory
- Run `git init` if needed

**"No GitHub remote found"**
- Ensure your repository has a GitHub remote
- Check with: `git remote -v`

**Permission denied errors**
```bash
# Make scripts executable
chmod +x clean-branches open-pr create-gh-issue
```

**"Command not found" after adding to PATH**
- Verify the path is correct: `echo $PATH`
- Check if the directory exists: `ls /path/to/cli-tools`
- Reload your shell profile: `source ~/.zshrc` or `source ~/.bashrc`
- Restart your terminal

### Debug Mode

For troubleshooting, you can run scripts with bash debugging:
```bash
bash -x clean-branches
```

## 🤝 Contributing

Feel free to submit issues, feature requests, or pull requests to improve these tools!

### Adding New Tools

When adding new tools to this collection:

1. **Follow the existing naming convention** - Use descriptive, lowercase names
2. **Include comprehensive help text** - Every tool should have `-h` or `--help`
3. **Add error handling and validation** - Check prerequisites and provide clear error messages
4. **Use consistent colored output** - Follow the color scheme used in existing tools
5. **Update this README** - Document new tools with usage examples
6. **Make it executable** - Ensure the script has proper permissions

### Tool Categories

This collection can include tools for:

- **Git & Version Control** - Branch management, commit helpers, etc.
- **Development Workflows** - Build tools, testing helpers, deployment scripts
- **System Utilities** - File management, system monitoring, cleanup tools
- **Productivity** - Time tracking, note-taking, automation helpers
- **API & Web Tools** - API testing, web scraping, data processing
- **Database Tools** - Backup scripts, migration helpers, query tools
- **Docker & Containers** - Container management, image cleanup, orchestration
- **Cloud Services** - AWS, GCP, Azure helpers
- **Text Processing** - Log analysis, data transformation, search tools

### Script Guidelines

- **Portability**: Write for bash/sh compatibility
- **Documentation**: Include usage examples and help text
- **Error Handling**: Graceful failure with helpful messages
- **User Experience**: Clear output and progress indicators
- **Configuration**: Support environment variables or config files when appropriate

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

## 🙏 Acknowledgments

- Built with ❤️ for the developer community
- Inspired by the need for better development workflows
- Uses various CLI tools and APIs for integration 
