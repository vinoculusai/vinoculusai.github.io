# Claude Code Development Guide

## Overview

This guide provides essential development practices for projects using Claude Code at VinoculusAI.

**Key Technologies:**

* Python 3.11+, pip, Ruff, PyTest, mypy
* GitHub Flow workflow with feature branches
* Google-style docstrings

## Quick Setup

```bash
# Install essential tools
pip install ruff pytest mypy pytest-cov

# Project structure
your-project/
├── src/your_package/       # Main code
├── tests/                  # Tests
├── requirements.txt        # Dependencies
├── requirements-dev.txt    # Dev dependencies
└── README.md
```

## Core Development Workflow

### 1. Branch Management (CRITICAL)

**⚠️ NEVER work directly on `main` branch**

```bash
# Start new work
git checkout main && git pull
git checkout -b feat/issue-123-description

# When ready
git push -u origin feat/issue-123-description
gh pr create --title "feat: description" --body "Closes #123"
```

**Branch naming:** `feat/issue-123-description`, `fix/issue-456-bug-name`

### 2. Code Quality

```bash
# Before committing - run these checks
ruff check --fix .          # Format & lint
mypy src/                   # Type check  
pytest --cov=src           # Test & coverage
```

**Minimum standards:**

* All code must pass `ruff check`
* Type hints required for public functions
* 80% test coverage minimum

### 3. Testing Basics

```python
# Test file: tests/test_module.py
def test_function_should_behavior_when_condition():
    """Clear test description."""
    # Arrange
    input_data = {"key": "value"}
    
    # Act
    result = your_function(input_data)
    
    # Assert
    assert result == expected_value
```

Run tests: `pytest -v --cov=src`

## Essential Code Standards

### Type Hints & Docstrings

```python
def process_data(data: list[dict], threshold: float = 0.5) -> dict[str, int]:
    """Process input data above threshold.
    
    Args:
        data: List of data dictionaries
        threshold: Minimum value to include
        
    Returns:
        Dictionary with processed results
    """
    # Implementation here
    pass
```

### Error Handling

```python
import logging

logger = logging.getLogger(__name__)

def safe_operation(data: dict) -> dict:
    """Handle errors gracefully."""
    try:
        return process(data)
    except ValueError as e:
        logger.error("Invalid data: %s", e)
        raise
    except Exception as e:
        logger.exception("Unexpected error")
        raise ProcessingError(f"Failed: {e}") from e
```

### Security Essentials

* Never commit secrets or API keys
* Use parameterized database queries
* Validate all user inputs

```python
# Good: Parameterized query
cursor.execute("SELECT * FROM users WHERE id = ?", (user_id,))

# Bad: String formatting (SQL injection risk)  
cursor.execute(f"SELECT * FROM users WHERE id = {user_id}")
```

## Commit Guidelines

Use [Conventional Commits](https://www.conventionalcommits.org/):

```text
feat(scope): add new feature
fix(scope): fix bug in component  
docs: update documentation
test: add missing tests
```

**Examples:**

```text
feat(auth): add user login endpoint
fix(parser): handle empty input files
docs: update API documentation
```

## Claude Code Workflow

### 1. Understand First

* Read existing code before changes
* Use search tools to understand project structure
* Check for existing patterns to follow

### 2. Plan & Branch

* Create feature branch for any GitHub issue
* Break complex tasks into small steps
* Use TodoWrite tool for task tracking

### 3. Implement Safely

* Write tests first when possible
* Make focused, single-purpose commits
* Run quality checks before pushing

### 4. Validate & Ship

* All tests pass: `pytest`
* Code quality: `ruff check`  
* Type checking: `mypy src/`
* Create PR linking to issue

## Pre-Commit Checklist

**Before every commit:**

* [ ] Working on feature branch (not main)
* [ ] Tests pass: `pytest`
* [ ] Linting passes: `ruff check`
* [ ] Type checking passes: `mypy src/`
* [ ] Coverage meets minimum (80%)

**Before creating PR:**

* [ ] Branch up to date with main
* [ ] PR title/description clear
* [ ] Links to GitHub issue: "Closes #123"
* [ ] Ready for review

## Common Commands

```bash
# Quality checks
ruff check --fix .          # Fix formatting/linting
mypy src/                   # Type checking
pytest --cov=src           # Run tests with coverage

# Git workflow  
git checkout -b feat/new-feature    # New branch
git add . && git commit -m "..."    # Commit changes
git push -u origin feat/new-feature # Push branch
gh pr create                        # Create PR

# Troubleshooting
python -c "import sys; print(sys.path)"  # Check Python path
pip list                                   # Check installed packages
```

## Getting Help

* **Ruff**: [https://docs.astral.sh/ruff/](https://docs.astral.sh/ruff/)
* **PyTest**: [https://docs.pytest.org/](https://docs.pytest.org/)
* **Conventional Commits**: [https://www.conventionalcommits.org/](https://www.conventionalcommits.org/)
* **GitHub Flow**: [https://docs.github.com/en/get-started/quickstart/github-flow](https://docs.github.com/en/get-started/quickstart/github-flow)

---

**Focus on these essentials first. Advanced topics like CI/CD, pre-commit hooks, and detailed security practices can be added as your project matures.**
