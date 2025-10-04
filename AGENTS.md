# VinoculusAI Sandbox Project Context

## Repository Structure

- src/agentic/ - Multi-agent AI framework experiments
- src/patty/ - PowerPoint CV reformatter for consulting
- src/research/ - arXiv paper search and download
- src/util/ - File conversion utilities (CSV, JSON, Markdown)
- src/app/ - Streamlit chat playground
- tests/ - PyTest suites matching src/ structure
- notebooks/ - Jupyter experiments (ChromaDB, LangChain)
- input/ - Sample data (CVs, templates, JDs)
- doc/ - Architecture and technical documentation

## Critical Rules

- NEVER commit directly to main branch
- Create feature branches: feat/issue-123-description or fix/issue-456-bug
- Pre-commit hooks MUST pass before push
- Maintain 80% test coverage minimum
- Use Pydantic for all data models
- Type hints required for public functions

## Key Commands

```bash
# Development
uv sync --dev                    # Install dependencies
uv run pytest                    # Run tests
uv run ruff format .            # Format code
uv run ruff check --fix .       # Lint and fix
uv run mypy src/                # Type check
pre-commit run --all-files      # Run all quality checks

# Module-specific
python src/patty/main.py extract --input input/cvs/file.pptx
python -m src.research.cli      # Interactive arXiv search
streamlit run src/app/chat_playground.py

# Git workflow
git checkout -b feat/new-feature
gh pr create --title "feat: description" --body "Closes #123"
```

## Technologies

- Python 3.13+, uv package manager
- LangChain/LangGraph for AI orchestration
- ChromaDB for vector storage
- python-pptx for PowerPoint processing
- Pydantic for data validation
- Ruff for formatting/linting
- MyPy for type checking (strict mode on src/)
- PyTest with coverage requirements

## Testing

- Markers: @pytest.mark.slow, @pytest.mark.integration, @pytest.mark.unit
- Fast tests run on commit (skip slow)
- Full suite runs on push
- Coverage: 80% minimum required
- HTML report: htmlcov/

## Pre-commit Hooks

1. **On commit**: ruff format, ruff check --fix, mypy (src/), pytest (fast)
2. **On push**: bandit security scan, safety dependency check, pytest (full)

## Commit Messages

```text
feat(scope): add new feature
fix(scope): fix bug in component
docs: update documentation
test: add missing tests
refactor: restructure code
chore: update dependencies
```

## Project Patterns

- Pydantic models in */models/ directories
- CV extraction logic in src/util/cv_utils.py
- PowerPoint utilities in src/util/pptx_utils.py
- CLI interfaces use Click or argparse
- Async operations for agent communication
- Google-style docstrings

## Security

- No secrets in code (use .env files)
- Parameterized database queries only
- Input validation on all user data
- bandit security scanning enabled

## Dependencies

- Core: pydantic, python-dotenv, requests
- AI/ML: langchain, langchain-openai, chromadb
- Documents: python-pptx, pypdf, markitdown
- Testing: pytest, pytest-cov, pytest-asyncio
- Dev: ruff, mypy, pre-commit, bandit, safety

## Related Documentation

- README.md - Project overview and setup
- doc/ARCHITECTURE.md - System design details
- doc/tech_stack_framework.md - Technology decisions
- Module READMEs in src/*/README.md
