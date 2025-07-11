# NautilusTrader Development Environment

## Package Management
- **Preferred**: Use `uv` package manager (NautilusTrader's official recommendation)
- **Installation**: `uv sync --all-extras` for development dependencies
- **Not supported**: Conda and other Python distributions

## Development Tools
- **Package Manager**: uv
- **Code Formatter**: black (line-length: 100)
- **Linter**: ruff
- **Type Checker**: mypy
- **Testing**: pytest

## Environment Setup
- **Python**: 3.11-3.13 (64-bit)
- **Rust**: Required via rustup
- **Clang**: Required compiler
- **Virtual Environment**: Strongly recommended

## Build Commands
- `make install` - Install all dependencies with uv
- `make format` - Format code with black/ruff
- `make lint` - Lint code with ruff
- `make typecheck` - Type check with mypy
- `make test` - Run tests
- `make git-status` - Show git repository status
- `make dev-workflow` - Complete development check

## Project Structure
```
nautilus_test/
   pyproject.toml      # uv configuration with NautilusTrader conventions
   main.py            # Main application entry point
   uv.lock           # Dependency lock file
   README.md
```

## Code Conventions
- Line length: 100 characters
- Target Python version: 3.11+
- Use type hints for all functions
- Follow NautilusTrader's coding standards

## DevContainer
- Configured with Rust toolchain
- Pre-installed uv package manager
- VS Code extensions: Python, Rust Analyzer, Ruff
- Auto-formatting and linting enabled

## Version Control
- **Repository**: https://github.com/terrylica/nautilus-trader-workspace
- **Scope**: Entire workspace (`/workspaces/nt/`) is tracked
- **Working Directory**: Always work in `/workspaces/nt/nautilus_test/`
- **Git Commands**: Use `make git-status`, `make git-push` from nautilus_test/

## Memory Notes
- Always use `uv` instead of pip for package management
- Follow NautilusTrader's 100-character line length
- Include type hints in all code
- Use virtual environments for isolation
- Use `make` commands instead of direct uv/git commands
- All workspace files are version controlled (except nt_reference/)

## Session Management Principles
### Memory Hierarchy
- **CLAUDE.md**: Principles, templates, conventions, and guidance only
- **session_logs/LATEST.md**: Auto-discovery symlink to current session
- **session_logs/INDEX.md**: Session registry and navigation
- **Session Handoff**: LATEST.md automatically points to current context

### Session Workflow Template
1. **Session Start**: LATEST.md automatically loads current session context
2. **During Work**: Update current session log with progress
3. **Session End**: Create summary entry with clear handoff instructions
4. **New Session**: Copy template, update symlink, add to INDEX.md

### Required Session Documentation
- Current feature/task being worked on
- Files modified and their purpose
- Commands executed
- Issues encountered and solutions
- Clear next steps for following session

### Enhanced Session Structure
- **Format**: `session_logs/YYYY/MM/YYYY-MM-DD-NNN.md`
- **Example**: `session_logs/2025/07/2025-07-11-001.md`
- **Auto-discovery**: LATEST.md symlink eliminates manual import updates
- **Registry**: INDEX.md tracks all sessions and topics

### Session Creation Process
1. `cp session_logs/templates/session.md session_logs/YYYY/MM/YYYY-MM-DD-NNN.md`
2. `ln -sf YYYY/MM/YYYY-MM-DD-NNN.md session_logs/LATEST.md`
3. Add entry to INDEX.md
4. Begin session work

## Claude Code Configuration

### Permission Settings
- **Mode**: `bypassPermissions` - Skips all confirmation prompts for maximum workflow freedom
- **Location**: `.claude/settings.local.json` - Project-specific permissions
- **Coverage**: All tools (Bash, Edit, Write, Grep, Task, etc.) pre-approved

### Benefits
- Zero interruption development workflow
- Task agents operate with full permissions
- Eliminates repetitive confirmations
- Safe environment with project isolation

## Session Memory Imports
@./session_logs/LATEST.md