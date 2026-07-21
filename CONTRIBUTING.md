# Contributing

Thanks for helping improve `@thisux/pi-worktree`.

By contributing, you agree that your contributions are licensed under the same
[MIT License](LICENSE) and copyrighted to **THISUX Private Limited**
(or assigned as needed so the project stays MIT under THISUX).

Please follow the [Code of Conduct](CODE_OF_CONDUCT.md).

## What this project is

A [Pi](https://pi.dev) package that registers the `/worktree` slash command.
Source lives in `extensions/git-worktree.ts` and is loaded by Pi as TypeScript
(no build step).

## Prerequisites

- [Bun](https://bun.sh/) (install + hooks)
- [Pi](https://pi.dev) CLI
- Git 2.20+ (worktree features)
- Optional: [GitHub CLI](https://cli.github.com/) for `/worktree pr`

## Local setup

```bash
git clone https://github.com/thisuxhq/pi-worktree.git
cd pi-worktree
bun install
```

Load the package into Pi from this checkout (no publish needed):

```bash
pi install /absolute/path/to/pi-worktree
```

Or one-off:

```bash
pi -e ./extensions/git-worktree.ts
```

In a session on a real git repo:

```text
/reload
/worktree help
/worktree ls
```

If you previously copied the extension into `~/.pi/agent/extensions/`, remove
the loose file so it does not load twice:

```bash
rm -f ~/.pi/agent/extensions/git-worktree.ts
```

## Making changes

1. Edit `extensions/git-worktree.ts` (and docs as needed).
2. Keep safety guarantees:
   - refuse removing the main worktree
   - confirm before remove; second confirm before force-remove on dirty trees
   - never force-push, hard-reset, or `clean -fdx`
3. Exercise the happy paths and failure paths in a throwaway repo with worktrees.
4. Use [conventional commits](https://www.conventionalcommits.org/):
   - `feat:` new command behavior
   - `fix:` wrong path/branch handling
   - `docs:` README / contributing only
   - `chore:` tooling, release plumbing

Commit hooks run `commitlint` on the message style.

## Pull requests

1. Fork (or branch from `main`).
2. Keep PRs focused — one behavior change per PR when possible.
3. Describe what you tested (`/worktree add`, `rm`, `pr`, dirty force path, etc.).
4. Do not bump `package.json` version by hand — [release-please](https://github.com/googleapis/release-please) opens the release PR after conventional commits land on `main`.

Use the PR template checklist.

## Release

Maintainers only:

1. Merge feature PRs to `main` with conventional commits.
2. Merge the release-please PR → tag + GitHub Release → CI publishes to npm (`NPM_TOKEN` secret).
3. Manual republish: Actions → **Release** → **Run workflow** with an existing tag.

## Security

See [SECURITY.md](SECURITY.md). Private reports: **hello@thisux.com**.

## Questions

Open a GitHub Discussion/issue, or email **hello@thisux.com**.
