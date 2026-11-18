# Factory project guidance

This repository hosts the Claude Code software factory configuration, agents,
scripts, and dashboard.

## Setup

There are currently no project dependencies or environment files to install.
Use Python 3.10 or newer for the dashboard and factory utilities.

## Development server

Start the dashboard with:

```bash
cd factory && python3 -m http.server 8000
```

Then open http://localhost:8000/dashboard.html.

## Validation

Run `bash factory/checks.sh`. This repository is currently an empty factory
host, so the check validates the shell script successfully; add project-specific
lint, typecheck, test, and build commands as the project grows.

## Software factory

`/factory run` builds every open GitHub issue labeled `factory` through
intake → spec → build → gate → review → approve, one PR per issue. State is in
`factory/jobs/` (gitignored); `factory/bin/job` is its only writer. Checks:
`factory/checks.sh`. Dashboard: `cd factory && python3 -m http.server`, then
open http://localhost:8000/dashboard.html.

Each job works in its own git worktree, a full checkout of the repo at
`.worktrees/<job-id>` (gitignored). A tool run from the repo root that doesn't
read `.gitignore` sees those copies too; exclude `.worktrees/` in its config.
