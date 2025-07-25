# NautilusTrader Test Environment Makefile
# Simplified version based on nautilus_trader/Makefile

.DEFAULT_GOAL := help

# Colors for output
GREEN  := $(shell tput -Txterm setaf 2)
YELLOW := $(shell tput -Txterm setaf 3)
BLUE   := $(shell tput -Txterm setaf 4)
RESET  := $(shell tput -Txterm sgr0)

.PHONY: help
help:  ## Show this help message
	@echo "$(BLUE)NautilusTrader Test Environment$(RESET)"
	@echo "Available targets:"
	@grep -E '^[a-zA-Z_-]+:.*?## .*$$' $(MAKEFILE_LIST) | sort | awk 'BEGIN {FS = ":.*?## "}; {printf "  $(GREEN)%-20s$(RESET) %s\n", $$1, $$2}'

.PHONY: install
install: ## Install all dependencies with uv
	@echo "$(BLUE)Installing dependencies...$(RESET)"
	uv sync --all-extras

.PHONY: test
test: ## Run tests
	@echo "$(BLUE)Running tests...$(RESET)"
	uv run pytest tests/

.PHONY: format
format: ## 🚀 Revolutionary formatting (recent files)
	@echo "$(BLUE)🚀 Revolutionary formatting (recent files)...$(RESET)"
	@python scripts/format_code.py

.PHONY: format-all
format-all: ## 🚀 Revolutionary formatting (all files)
	@echo "$(BLUE)🚀 Revolutionary formatting (all files)...$(RESET)"
	@python scripts/format_code.py --all

.PHONY: format-recent
format-recent: ## 🚀 Revolutionary formatting (last 30 minutes)
	@echo "$(BLUE)🚀 Revolutionary formatting (last 30 minutes)...$(RESET)"
	@python scripts/format_code.py --recent 30

.PHONY: lint
lint: ## Lint code with ruff
	@echo "$(BLUE)Linting code...$(RESET)"
	uv run ruff check src/ tests/ examples/ strategies/

.PHONY: typecheck
typecheck: ## Run type checking with mypy
	@echo "$(BLUE)Type checking...$(RESET)"
	uv run mypy src/

.PHONY: clean
clean: ## Clean build artifacts and cache
	@echo "$(BLUE)Cleaning build artifacts...$(RESET)"
	rm -rf build/
	rm -rf dist/
	rm -rf src/*.egg-info/
	find . -type d -name __pycache__ -exec rm -rf {} +
	find . -type f -name "*.pyc" -delete

.PHONY: run-example
run-example: ## Run basic sandbox example
	@echo "$(BLUE)Running basic sandbox example...$(RESET)"
	uv run python examples/sandbox/basic_test.py

.PHONY: git-status
git-status: ## Show git status and branch information
	@echo "$(BLUE)Git Repository Status$(RESET)"
	@echo "$(YELLOW)Current branch:$(RESET) $$(cd /workspaces/nt && git branch --show-current)"
	@echo "$(YELLOW)Remote:$(RESET) $$(cd /workspaces/nt && git remote get-url origin 2>/dev/null || echo 'No remote configured')"
	@echo "$(YELLOW)Scope:$(RESET) Entire workspace (/workspaces/nt/)"
	@cd /workspaces/nt && git status --short
	@echo ""
	@if [ -n "$$(cd /workspaces/nt && git status --porcelain)" ]; then \
		echo "$(YELLOW)Uncommitted changes detected$(RESET)"; \
	else \
		echo "$(GREEN)Working tree clean$(RESET)"; \
	fi

.PHONY: git-commit
git-commit: ## Commit changes with standard format (requires message via COMMIT_MSG)
	@if [ -z "$(COMMIT_MSG)" ]; then \
		echo "$(YELLOW)Usage: make git-commit COMMIT_MSG='Your commit message'$(RESET)"; \
		exit 1; \
	fi
	@git add .
	@git commit -m "$(COMMIT_MSG)

🤖 Generated with [Claude Code](https://claude.ai/code)

Co-Authored-By: Claude <noreply@anthropic.com>"
	@echo "$(GREEN)Committed successfully$(RESET)"

.PHONY: git-push
git-push: ## Push changes to remote repository
	@echo "$(BLUE)Pushing to remote repository...$(RESET)"
	@cd /workspaces/nt && git push origin $$(git branch --show-current)
	@echo "$(GREEN)Pushed successfully$(RESET)"

.PHONY: dev-workflow
dev-workflow: format lint typecheck test git-status ## Complete development workflow check