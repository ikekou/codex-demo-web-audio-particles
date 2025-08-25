# Repository Guidelines

## Project Structure & Module Organization
- `src/`: application/library code organized by domain (e.g., `src/api/`, `src/core/`).
- `tests/`: mirrors `src/` with matching test files.
- `scripts/`: repeatable tasks (e.g., `dev`, `build`, `test`).
- `docs/`: architecture notes and ADRs.
- `assets/` or `public/`: static files if applicable.

Example layout:
```
src/
  core/
  api/
tests/
  core/
  api/
scripts/
```

## Build, Test, and Development Commands
Use the commands provided by the project tooling if present. Common options:
- Build: `make build` or `npm run build`
- Test (all): `make test` or `pytest -q` or `npm test`
- Lint/Format: `make lint` or `ruff check .` / `eslint .` and `black .` / `prettier -w .`
- Local run: `make run` or `npm start` / `python -m src`

Prefer `scripts/*` wrappers for consistency (e.g., `scripts/test`).

## Coding Style & Naming Conventions
- Indentation: 2 spaces (no tabs); max line length 100.
- Filenames: `lower_snake_case` for modules, `UpperCamelCase` for classes, `lowerCamelCase` for variables.
- JS/TS: Prettier + ESLint. Python: Black + Ruff. Keep imports sorted.
- Avoid large PRs; keep changes cohesive and incremental.

## Testing Guidelines
- Place tests in `tests/` mirroring `src/` structure.
- Naming: Python `tests/test_*.py`; JS/TS `**/*.test.(js|ts)`.
- Aim for coverage on core logic and edge cases; add regression tests with fixes.
- Run the full suite and linters before opening a PR.

## Commit & Pull Request Guidelines
- Commit message (mandatory): follow Conventional Commits in Japanese.
  - Subject: `type(scope)?: 要約`（ASCIIコロン）。例: `feat(api): ユーザー一覧にページネーションを追加`
  - Body: 1行空けて、丁寧かつ具体的に説明を書くこと（何を/なぜ/どのように/影響/移行/参考）。必要なら箇条書き。
  - Footer: 課題連携や破壊的変更を明記（例: `Closes #123`、`BREAKING CHANGE: ...`）。
- Branch naming: `feature/<slug>` or `fix/<issue-id>-<slug>`。
- Pull Requests: 概要、スクリーンショット（UI変更）、テスト/カバレッジ影響、移行手順、リリース注意点を含める。
- Gate: 本規約に従わないコミット/PRはリジェクトされます。

Example commit:
```
feat(api): ユーザー一覧にページネーションを追加

何を: `GET /users` に `page`/`perPage` を追加し、既存のレスポンスに `total`/`pages` を含める。
なぜ: 大量データ環境での応答時間短縮と一覧UIのUX改善のため。
どうやって: クエリバリデーションを追加し、リポジトリ層で `LIMIT/OFFSET` を適用。既存のクライアントを壊さないようデフォルト値を設定。
影響: 既存の無限スクロールはそのまま動作。新規パラメータ利用時はUI側でページャを表示。
関連: Closes #123
```

## Branch 運用ルール
- `main`: 常にリリース可能。直接コミット禁止、PR経由のみ。タグは `vMAJOR.MINOR.PATCH`。
- 作業ブランチ: `feature/<slug>` / `fix/<issue-id>-<slug>` / `hotfix/<slug>`。小さく短命（~1週間以内）を推奨。
- 更新方法: 定期的に `git fetch origin && git rebase origin/main` で最新化。
- マージ方針: 原則 Squash Merge。PRタイトルを規約準拠のサブジェクトにし、squash後のコミットメッセージに採用。
- リリース/ホットフィックス: 重要修正は `hotfix/*` を `main` にPR → パッチタグ付与。

## Security & Configuration
- Never commit secrets. Use `.env.example` and local overrides (`.env.local`).
- Validate inputs and handle errors explicitly; log without sensitive data.

## Agent-Specific Tips
- Keep patches minimal and focused; update docs when behavior changes.
- Prefer `rg` for search; read files in ≤250-line chunks.
- Use small, verifiable steps and explain assumptions in PRs.
