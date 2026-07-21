## Summary

<!-- What does this PR change, and why? -->

## Type of change

- [ ] Bug fix
- [ ] New feature / command behavior
- [ ] Documentation
- [ ] Chore / tooling / release plumbing

## Test plan

- [ ] `pi install` / local path load works after change
- [ ] `/worktree help` shows expected commands
- [ ] Exercised relevant path(s):
  - [ ] `ls` / interactive pick
  - [ ] `add` (local / remote / new branch)
  - [ ] `open`
  - [ ] `rm` (confirm + dirty force)
  - [ ] `pr` (if `gh` change)
- [ ] Did not break safety: no main-worktree remove, no force without confirm

## Notes

<!-- Edge cases, screenshots, follow-ups -->
