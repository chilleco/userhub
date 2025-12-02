# Repository Guidelines

## Project Structure & Module Organization
- Core package: `userhub/` with `auth.py`, `model.py`, and `__init__.py` (exports and version).
- Packaging: `pyproject.toml` (primary) and `setup.py` (legacy shim for installers).
- Docs: `docs/` (e.g., `USERHUB_DOC.md`, this file).
- Builds/artifacts land in `dist/` and `build/` when created; keep them out of PRs.

## Build, Test, and Development Commands
- Install for development: `pip install -e .[dev]` (uses `pyproject.toml` extras).
- Build distributions: `python -m build` (produces sdist/wheel in `dist/`).
- Quick syntax check: `python -m compileall userhub`.
- Legacy make targets exist but rely on old requirements files; prefer the commands above.

## Coding Style & Naming Conventions
- Python 3.8+ only; keep code async-friendly (network calls are awaited).
- Follow the existing module layout and keep public exports wired via `userhub/__init__.py`.
- Use clear, imperative function names; keep logging through `libdev.log.log` and HTTP via `libdev.req.fetch`.
- Defaults (e.g., locale) should honor `libdev.cfg` to stay consistent with consumers.

## Testing Guidelines
- No test suite is present; add `pytest` cases under `tests/` when modifying behavior.
- Name files `tests/test_<feature>.py`; prefer async tests where applicable.
- For new flows, cover both success and non-200/error return paths (functions return fallbacks instead of raising).

## Commit & Pull Request Guidelines
- Commits: concise, imperative summaries (e.g., “Add social token handling”); group related changes.
- PRs: include purpose, key changes, and any platform/API assumptions; link issues if available.
- Screenshots are unnecessary; code snippets or sample payloads are helpful for API changes.
- Keep diffs focused; avoid committing build artifacts or virtualenvs.

## Security & Configuration Tips
- Tokens are issued/rotated by the Chill platform; never hardcode secrets or tokens in the repo.
- Respect platform status semantics (0–8) and do not repurpose them locally.
- Validate new inputs using existing preprocessing/helpers to stay aligned with backend expectations.
