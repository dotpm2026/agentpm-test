# Report: LOC-3 git rerere: reuse recorded resolution of merge conflicts

Light Research: light-research · web

> [!IMPORTANT]
> **git rerere auto-applies your earlier resolution to repeat conflicts.**
> (high)
>
> - It stores your hand resolution after a conflicted merge, then reapplies
>   it.
> - Enable via rerere.enabled; merge, rebase and commits invoke it
>   automatically.
> - Records live in the repo-local .git/rr-cache; review before git add.
>
> Next step: run `git config --global rerere.enabled true`.
>
> Risk: cache is per-repo and marker-sensitive; review autoresolved files.

## Findings

<details>
<summary>Findings (10)</summary>

### What git rerere is

**A built-in command that replays recorded conflict resolutions.**

- Records the conflicted merge and your resolution; replays on repeats.
  (high; [1][2])
- For long-lived topic branches merged into a moving master. (high; [1][2])
- git rebase's fallback merge and merge commits also run rerere. (high; [1])

### Enable and manage

**Enable by config; manage records with subcommands.**

- Set rerere.enabled, or create .git/rr-cache, to enable it. (high; [1][2])
- Subcommands: clear, forget, diff, status, remaining, gc. (high; [1])
- gc prunes conflicts older than 15 days unresolved, 60 resolved. (high; [1])

### Limits

**Marker-sensitive and per-repository.**

- Detection needs conflict markers. (high; [1])
- Marker-like file content breaks it; use conflict-marker-size. (high; [1])
- Leaves the index alone: review with git diff, then git add. (high; [1])
- Records live in .git/rr-cache, so nothing is shared between clones.
  (medium; [1][2])

</details>

## Sources

<details>
<summary>Sources (2)</summary>

1. [git-rerere manual](https://git-scm.com/docs/git-rerere) (primary)
2. [Pro Git: Git Tools - Rerere](https://git-scm.com/book/en/v2/Git-Tools-Rerere) (secondary)

</details>

## Board proposal

LOC-4: cancel: description matches this request verbatim; same scope.
