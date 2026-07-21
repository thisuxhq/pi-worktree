# @thisux/pi-worktree

Git worktree slash commands for [Pi](https://pi.dev).

Create, list, open, remove, and PR-checkout worktrees without leaving the session.

## Layout

```text
~/AGI/mobile/               ← main checkout
~/AGI/mobile-fix-login/     ← worktree for fix/login
```

Sibling folders next to the main repo: `<repo>-<branch-slug>`.

## Install

```bash
pi install npm:@thisux/pi-worktree
```

Already in a session?

```text
/reload
```

One-off try (no settings write):

```bash
pi -e npm:@thisux/pi-worktree
```

Update later:

```bash
pi update npm:@thisux/pi-worktree
```

## Usage

| Command | What it does |
|---|---|
| `/worktree` | List worktrees; pick one to copy path |
| `/worktree ls` | Same as above |
| `/worktree <branch>` | Create worktree for branch |
| `/worktree add <branch>` | Same as above |
| `/worktree open <branch>` | Show path (+ copy on macOS) |
| `/worktree rm <branch>` | Remove worktree (keeps branch; confirms) |
| `/worktree pr <number>` | Fetch PR via `gh`, create worktree |
| `/worktree help` | Show help |

### Create behavior

1. Local branch exists → attach worktree to it
2. Else remote `origin/<branch>` → track it
3. Else new branch off default (`origin/main` / `main` / `master`)

Path already taken by that branch → shows existing path (copied).

### Remove safety

- Refuses main worktree
- Refuses locked worktrees
- Always confirms
- Dirty tree needs a second confirm before `--force`
- Branch is kept; only the worktree directory is removed

### PR checkout

Needs [GitHub CLI](https://cli.github.com/) (`gh`) authenticated.

```text
/worktree pr 42
```

Fetches `pull/42/head` and creates a worktree on the PR head branch.

## Notes

- Must be inside a git repo.
- Never force-pushes, hard-resets, or `clean -fdx`.
- Prefer the package over a hand-copied `~/.pi/agent/extensions/git-worktree.ts` — remove the loose file so it doesn't load twice:

  ```bash
  rm -f ~/.pi/agent/extensions/git-worktree.ts
  ```

- Enable/disable via `pi config`. Confirm with `pi list`.

## Links

- [npm](https://www.npmjs.com/package/@thisux/pi-worktree)
- [pi package catalog](https://pi.dev/packages)
- [Repo](https://github.com/thisuxhq/pi-worktree)

## Release flow

Same automation as [@thisux/pi-double-esc-clear](https://github.com/thisuxhq/pi-double-esc-clear):

1. Land PRs on `main` with [conventional commits](https://www.conventionalcommits.org/) (`feat:`, `fix:`, `docs:`, …).
2. [release-please](https://github.com/googleapis/release-please) opens a release PR (version bump + `CHANGELOG.md`).
3. Merge the release PR → GitHub Release/tag → CI runs `bun publish`.

Manual republish: Actions → **Release** → **Run workflow** (pass an existing tag).

Needs repo secret `NPM_TOKEN` (npm automation token allowed to publish under `@thisux`).

## License

MIT · [ThisUX](https://thisux.com/)
