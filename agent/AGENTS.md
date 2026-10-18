# Working conventions

## Plans
- Plans go in `/home/pi/projects/plans/` (top level, **not** inside any repository worktree).
- Naming: `<short-slug>-YYYY-MM-DD.md`.

## Worktrees (git bare-repo layout)
- Repos under `/home/pi/projects/` may be bare with worktrees as siblings, e.g.
  `pi-box/main`, `pi-box/bump-pi`, `pi-box/ssh-agent`.
- When creating a worktree for a change, put it **inside the repo's bare directory,
  as a sibling of `main`** (e.g. `pi-box/<short-branch-slug>`), not outside the repo
  (not `pi-box-<slug>` under `projects/`).
- Branch name: short imperative slug, e.g. `bump-pi-to-1.3.0`, `ssh-agent-hook`.

## pi-box project (`/home/pi/projects/pi-box`)
- `main` keeps the current published state; changes land in sibling worktrees first.
- Conventions established in the image:
  - pi pinned in the Dockerfile (reproducibility); drop `@<version>` to track latest.
  - One ssh-agent for the container lifetime: `~/.pi-box/ssh-agent.sh` sourced from
    `~/.bashrc`, socket at `/tmp/ssh-agent.sock` (agent + keys in `/tmp`/memory,
    not `~/.ssh`).
- No root podman/docker on this host: image builds and in-image verification happen
  elsewhere; verify npm resolution and `pi` behavior locally when possible.
- Uncommitted changes stay uncommitted until explicitly asked to commit/push
  (pushing `main` publishes `ghcr.io/skagget77/pi-box:latest`).
