<div align="center" markdown>

![copier-release](https://socialify.git.ci/liblaf/copier-release/image?description=1&forks=1&issues=1&logo=https%3A%2F%2Fraw.githubusercontent.com%2Fcopier-org%2Fcopier%2Frefs%2Fheads%2Fmaster%2Fimg%2Flogo.svg&name=1&owner=1&pattern=Transparent&pulls=1&stargazers=1&theme=Auto)

[![Made with Copier](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/copier-org/copier/master/img/badge/badge-black.json)](https://github.com/copier-org/copier)
[![Release PR](https://github.com/liblaf/copier-release/actions/workflows/release-pr.yaml/badge.svg)](https://github.com/liblaf/copier-release/actions/workflows/release-pr.yaml)
[![Release Publish](https://github.com/liblaf/copier-release/actions/workflows/release-publish.yaml/badge.svg)](https://github.com/liblaf/copier-release/actions/workflows/release-publish.yaml)
[![MegaLinter](https://github.com/liblaf/copier-release/actions/workflows/shared-mega-linter.yaml/badge.svg)](https://github.com/liblaf/copier-release/actions/workflows/shared-mega-linter.yaml)
[![pre-commit.ci status](https://results.pre-commit.ci/badge/github/liblaf/copier-release/main.svg)](https://results.pre-commit.ci/latest/github/liblaf/copier-release/main)

[Copier Docs](https://copier.readthedocs.io/) · [Changelog](https://github.com/liblaf/copier-release/blob/main/CHANGELOG.md) · [Report Bug](https://github.com/liblaf/copier-release/issues) · [Request Feature](https://github.com/liblaf/copier-release/issues)

![Rule](https://cdn.jsdelivr.net/gh/andreasbm/readme/assets/lines/rainbow.png)

</div>

## ✨ Features

`copier-release` is a compact Copier template for GitHub repositories that want a conventional-commit release loop without carrying release workflow boilerplate by hand.

- 🚀 **Release PRs from `main`**: calculates the next semantic version with `git-cliff`, writes `CHANGELOG.md`, bumps `package.json` when present, and opens a signed `release-please/*` pull request.
- 🏷️ **GitHub Releases after merge**: watches merged release PRs, creates the version tag, and publishes the GitHub Release from the PR body.
- 📌 **Pinned release configuration**: renders `release-pr.yaml` with a raw `cliff.toml` URL tied to the Copier-selected template revision.
- 🧹 **Legacy cleanup**: removes superseded release-please config and older release workflow names during generation.
- 🧩 **Narrow responsibility**: handles changelogs, tags, and GitHub Releases while leaving package publishing, artifacts, and deployment to the consuming repository.

## 📦 Apply The Template

> [!IMPORTANT]
> Use `--trust` when applying or updating this template. The template runs cleanup tasks during generation.

```bash
copier copy --trust gh:liblaf/copier-release .
```

Generated repositories receive:

| File | Purpose |
| --- | --- |
| `.github/workflows/release-pr.yaml` | Finds the next version, generates the changelog and release PR body, optionally bumps `package.json`, and opens the release PR. |
| `.github/workflows/release-publish.yaml` | Runs after a merged `release-please/*` PR, then pushes the tag and creates the GitHub Release. |
| `.config/copier/.copier-answers.release.yaml` | Stores the template source and rendered answers for reproducible recopy runs. |

## 🔄 Update The Template

Generated repositories keep release-template answers in `.config/copier/.copier-answers.release.yaml`.

```bash
copier recopy --force --skip-answered --trust --answers-file '.config/copier/.copier-answers.release.yaml'
```

Repositories that also use [`copier-shared`](https://github.com/liblaf/copier-shared) can update every configured template with the shared task:

```bash
mise run copier-update --skip-answered --trust --force
```

## 🔐 Required GitHub Setup

Create a GitHub Actions environment named `release-please`, then configure these repository or environment values:

- `vars.APP_CLIENT_ID`: the GitHub App Client ID from the app settings.
- `secrets.APP_PRIVATE_KEY`: a private key for the same GitHub App.

Those credentials are passed to [`liblaf/actions/auth`](https://github.com/liblaf/actions) so the workflows can open release PRs, push tags, and create GitHub Releases as a GitHub App. If a repository was configured for the older v1 workflow inputs, replace the numeric `vars.APP_ID` value with the app's Client ID in `vars.APP_CLIENT_ID`, and move or recreate `secrets.PRIVATE_KEY` as `secrets.APP_PRIVATE_KEY` before applying this template update.

## 🔁 Release Flow

1. Push Conventional Commits to `main`, such as `feat:`, `fix:`, `docs:`, or `ci:`.
2. `release-pr.yaml` calculates the next version and opens `release-please/main` when a release is needed.
3. Review and merge the release PR after CI is green.
4. `release-publish.yaml` tags the merged release commit and creates the GitHub Release.
5. Run project-specific publish, artifact, or deploy workflows from the consuming repository.

## 🧭 Commit Guidance

Use Conventional Commits for predictable version bumps and changelog grouping.

## 🤝 Contributing

Ideas, fixes, and improvements are welcome. Open an issue or pull request if you want to refine the template, release workflow, or generated changelog format.

[![PR WELCOME](https://img.shields.io/badge/%F0%9F%A4%AF%20PR%20WELCOME-%E2%86%92-ffcb47?labelColor=black&style=for-the-badge)](https://github.com/liblaf/copier-release/pulls)
[![Contributors](https://gh-contributors-gamma.vercel.app/api?repo=liblaf/copier-release)](https://github.com/liblaf/copier-release/graphs/contributors)

## 🔗 More Copier Templates

- **[Shared](https://github.com/liblaf/copier-shared)** - shared automation for code quality, maintenance, and repository hygiene
- **[Python](https://github.com/liblaf/copier-python)** - a modern Python project template with tooling, docs, and CI
- **[Rust](https://github.com/liblaf/copier-rust)** - a Rust template with cross-compilation, CI, and release automation
- **[TypeScript](https://github.com/liblaf/copier-typescript)** - a TypeScript template built around modern tooling and GitHub automation

---

#### 📝 License

Copyright © 2024 [liblaf](https://github.com/liblaf). <br />
This project is [MIT](https://github.com/liblaf/copier-release/blob/main/LICENSE) licensed.
