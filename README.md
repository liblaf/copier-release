<div align="center" markdown>

![copier-release](https://socialify.git.ci/liblaf/copier-release/image?description=1&forks=1&issues=1&logo=https%3A%2F%2Fraw.githubusercontent.com%2Fcopier-org%2Fcopier%2Frefs%2Fheads%2Fmaster%2Fimg%2Flogo.svg&name=1&owner=1&pattern=Transparent&pulls=1&stargazers=1&theme=Auto)

[![Made with Copier](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/copier-org/copier/master/img/badge/badge-black.json)](https://github.com/copier-org/copier)
[![Release PR](https://github.com/liblaf/copier-release/actions/workflows/release-pr.yaml/badge.svg)](https://github.com/liblaf/copier-release/actions/workflows/release-pr.yaml)
[![Release Draft](https://github.com/liblaf/copier-release/actions/workflows/release-draft.yaml/badge.svg)](https://github.com/liblaf/copier-release/actions/workflows/release-draft.yaml)
[![Release Publish](https://github.com/liblaf/copier-release/actions/workflows/release-publish.yaml/badge.svg)](https://github.com/liblaf/copier-release/actions/workflows/release-publish.yaml)

[Copier Docs](https://copier.readthedocs.io/) · [Changelog](https://github.com/liblaf/copier-release/blob/main/CHANGELOG.md) · [Report Bug](https://github.com/liblaf/copier-release/issues) · [Request Feature](https://github.com/liblaf/copier-release/issues)

![Rule](https://cdn.jsdelivr.net/gh/andreasbm/readme/assets/lines/rainbow.png)

</div>

## 🚀 Overview

`copier-release` is a Copier template for repositories that want a clean, mostly hands-off GitHub release flow.

- ✨ Opens a release PR from conventional commits pushed to `main`
- 📝 Generates and updates `CHANGELOG.md` with `git-cliff`
- 🏷️ Tags the merged release commit and creates a draft GitHub release
- ⏰ Publishes draft releases automatically after 6 hours
- 📦 Bumps `package.json` automatically when the file exists
- 🧩 Leaves package publishing and asset uploads to your own project workflows

## 📦 Apply The Template

> [!IMPORTANT]
> Use `--trust` when applying or updating this template. It runs Copier tasks during generation.

```bash
copier copy --trust gh:liblaf/copier-release .
```

## 🔄 Update The Template

```bash
copier recopy --trust --answers-file '.config/copier/.copier-answers.release.yaml'
```

## 🧱 What You Get

| File | Purpose |
| --- | --- |
| `.github/workflows/release-pr.yaml` | Calculates the next version, updates the changelog, and opens a release PR on pushes to `main`. |
| `.github/workflows/release-draft.yaml` | Runs after a merged release PR, creates the Git tag, and creates a draft GitHub release. |
| `.github/workflows/release-publish.yaml` | Runs hourly or on demand and publishes draft releases older than 6 hours. |
| `.config/copier/.copier-answers.release.yaml` | Stores Copier answers so future `copier recopy` runs stay reproducible. |

> [!NOTE]
> The changelog format is maintained centrally in this repository through a shared `git-cliff` config. Generated repositories do not need to copy a local `cliff.toml`.

## 🔐 Required GitHub Setup

Create a GitHub Actions environment named `Release Please`, then provide:

- `vars.APP_ID`
- `secrets.PRIVATE_KEY`

These credentials are used by the workflows to open release PRs, push tags, create draft releases, and publish them later.

## 🔁 Release Flow

1. Push commits using the Conventional Commits format such as `feat:`, `fix:`, `docs:`, or `ci:`.
2. `release-pr.yaml` runs on pushes to `main` and opens a release PR with changelog updates and version bumps where applicable.
3. Merge the release PR yourself, or approve it and let [`mergery[bot]`](https://github.com/apps/mergery) merge it once the merge button is green.
4. `release-draft.yaml` tags the merge commit and creates a draft GitHub release.
5. Your own workflows can publish packages, build artifacts, and upload release assets. Those jobs are intentionally not included in this template.
6. `release-publish.yaml` publishes the draft release after it has been sitting for 6 hours, which gives your publish jobs time to finish.

## 🧭 Commit Guidance

Stick to Conventional Commits if you want predictable version bumps and a well-structured changelog.

```text
feat: add OAuth login
fix(ci): retry flaky upload step
docs: clarify release setup
```

## 🤝 Contributing

Ideas, fixes, and improvements are all welcome. If you want to help refine the template or extend the release flow, open an issue or send a pull request.

[![PR WELCOME](https://img.shields.io/badge/%F0%9F%A4%AF%20PR%20WELCOME-%E2%86%92-ffcb47?labelColor=black&style=for-the-badge)](https://github.com/liblaf/copier-release/pulls)
[![Contributors](https://gh-contributors-gamma.vercel.app/api?repo=liblaf/copier-release)](https://github.com/liblaf/copier-release/graphs/contributors)

## 🔗 More Copier Templates

- **[Shared](https://github.com/liblaf/copier-shared)** - ✨ Shared automation for code quality, maintenance, and repository hygiene
- **[Python](https://github.com/liblaf/copier-python)** - 🐍 A modern Python project template with tooling, docs, and CI ready to go
- **[Rust](https://github.com/liblaf/copier-rust)** - 🦀 A Rust template with cross-compilation, CI, and release automation
- **[TypeScript](https://github.com/liblaf/copier-typescript)** - 🚀 A TypeScript template built around modern tooling and GitHub automation

---

#### 📝 License

Copyright © 2024 [liblaf](https://github.com/liblaf). <br />
This project is [MIT](./LICENSE) licensed.
