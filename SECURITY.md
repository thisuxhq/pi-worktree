# Security Policy

## Supported versions

| Version | Supported |
| ------- | --------- |
| `main` / latest release (`1.x`) | Yes |
| Older tags | No — please upgrade |

Security fixes land on `main` and ship in the next npm release of `@thisux/pi-worktree`.

## Reporting a vulnerability

**Do not open a public GitHub issue for security-sensitive findings.**

Email **hello@thisux.com** with subject:

```text
[security] thisuxhq/pi-worktree
```

Include:

1. Description of the issue and potential impact
2. Steps to reproduce (or a proof of concept)
3. Affected version / commit if known
4. Any suggested fix

We will acknowledge within a few business days and work with you on a fix and disclosure timeline.

## Scope notes

This package is a [Pi](https://pi.dev) extension that runs `git` / `gh` via the coding agent. Reports that matter most:

- Unsafe command construction or argument injection
- Worktree remove/force paths that destroy data without confirmation
- Path traversal outside expected worktree layout
- Supply-chain issues in published tarballs
