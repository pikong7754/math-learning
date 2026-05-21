# alice-math-learning

This is a personal learning repository for `zhizhi-math-coach`.

Open this repository as the OpenClaw workspace for daily grading, diagnosis, worksheet generation, and learning-record updates.

## Directory Roles

- `memory/`: long-term and short-term learning memory.
- `curriculum/`: grade, semester, textbook, calendar, and progress scope.
- `knowledge-points/`: reusable explanation cards and mastery rules.
- `weak-points/`: durable weak-point history.
- `mistakes/`: school and system-generated mistake books.
- `records/`: dated diagnosis and progress records.
- `worksheets/`: generated worksheet specs, printable HTML, and answer keys.
- `site/`: optional child-facing public pages only.

## Public Repository Mode

If this repository is public for GitHub Pages, every tracked file is viewable on GitHub, not only `site/`. Non-collaborators cannot push by default, so public viewing does not let others edit `main`. Keep collaborators empty, protect `main` against force pushes and deletion, and avoid required-pull-request rules if OpenClaw should push directly.

Recommended ruleset: `main protect`, Active, bypass `Deploy keys` and `Repository admin` as `Always allow`, target `main` or `Default`, enable `Restrict updates`, `Restrict deletions`, and `Block force pushes`, and leave PR/status/signed-commit/deployment requirements disabled.

After Pages and the writable Deploy key are configured, new generated worksheets should be automatically published:

```bash
python3 skills/zhizhi-math-coach/scripts/publish_and_wait_pages.py   worksheets/<date-topic>   --workspace .   --base-url https://<user>.github.io/alice-math-learning
```

## Daily Use

Run OpenClaw in this repository and invoke:

```text
$zhizhi-math-coach 批改这张练习卷，记录薄弱项。
$zhizhi-math-coach 根据最近错题生成变式练习。
```

Sync to GitHub explicitly:

```bash
git add curriculum knowledge-points memory mistakes records weak-points worksheets site
git commit -m "Update learning records"
git push
```

## GitHub Sync Setup

OpenClaw may not have GitHub CLI, saved credentials, or a provider-level token setting. Prefer a repository-scoped GitHub Deploy key:

```bash
python3 skills/zhizhi-math-coach/scripts/prepare_github_deploy_key.py   --workspace .   --configure-remote
```

If `origin` is not configured yet, add the repository explicitly:

```bash
python3 skills/zhizhi-math-coach/scripts/prepare_github_deploy_key.py   --workspace .   --github-owner <user>   --repo alice-math-learning   --configure-remote
```

Send only the printed public key to the parent. The parent adds it in GitHub repository Settings -> Deploy keys -> Add deploy key, with `Allow write access` enabled.

After the key is added:

```bash
python3 skills/zhizhi-math-coach/scripts/check_git_sync.py --workspace . --check-push
```

If this repository is public, commit only files that are safe to expose.
