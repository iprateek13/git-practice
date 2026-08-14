# Git Practice

A hands-on repository for learning Git workflows and CI/CD fundamentals. Use it to practice branching, pull requests, merges, and automated pipelines in a safe sandbox before applying those patterns to production projects.

**Remote:** [github.com/iprateek13/git-practice](https://github.com/iprateek13/git-practice)

## What you'll practice

- **Branching** — create feature branches, keep `main` stable, and merge via pull requests
- **Collaboration** — push changes, open PRs, review code, and resolve merge conflicts
- **CI/CD** — wire up GitHub Actions (or similar) to run checks on every push and PR
- **Infrastructure as code** — the `feature/vm` branch is set up for Terraform VM provisioning experiments

## Repository structure

```
git-practice/
├── readme.md          # Project overview (this file)
├── .gitignore         # Ignores Terraform state and secrets
└── (future)           # Terraform configs, CI workflows, etc.
```

## Getting started

### Clone the repo

```bash
git clone https://github.com/iprateek13/git-practice.git
cd git-practice
```

### Configure your identity (once per machine)

```bash
git config user.name "Your Name"
git config user.email "you@example.com"
```

### Typical feature workflow

```bash
# Start from the latest main
git checkout main
git pull origin main

# Create and switch to a feature branch
git checkout -b feature/my-change

# Make changes, then stage and commit
git add .
git commit -m "Describe what changed and why"

# Push and open a pull request
git push -u origin feature/my-change
```

On GitHub, open a **Pull Request** from your branch into `main`, get a review if working with others, then merge.

## Branches

| Branch       | Purpose                                      |
| ------------ | -------------------------------------------- |
| `main`       | Stable default branch; merge PRs here        |
| `feature/vm` | Terraform VM provisioning experiments        |

## CI/CD (coming soon)

A typical pipeline for this repo might look like:

1. **Trigger** — on push to any branch and on pull requests to `main`
2. **Validate** — lint Markdown, validate Terraform (`terraform fmt -check`, `terraform validate`)
3. **Plan** — run `terraform plan` on PRs (no apply)
4. **Apply** — deploy only from `main` after merge (with manual approval)

Example workflow location once added:

```
.github/workflows/ci.yml
```

## Terraform notes

The `.gitignore` excludes local Terraform artifacts and variable files that may contain secrets:

- `.terraform/` — provider plugins and modules cache
- `*.tfstate` / `*.tfstate.*` — local state (use remote state in real projects)
- `*.tfvars` / `*.tfvars.json` — often hold credentials; never commit these

When adding Terraform configs on `feature/vm`, keep secrets in environment variables or a secure secret store—not in the repository.

## Useful Git commands

| Command | Description |
| ------- | ----------- |
| `git status` | See changed and untracked files |
| `git log --oneline --graph --all` | Visual branch history |
| `git diff` | View unstaged changes |
| `git stash` | Temporarily save work in progress |
| `git rebase main` | Replay your branch on top of latest `main` |
| `git merge main` | Bring `main` changes into your current branch |

## Contributing

1. Branch off `main` (or an existing feature branch if coordinating work).
2. Keep commits focused—one logical change per commit when possible.
3. Write clear commit messages: *what* changed and *why*.
4. Open a PR early for feedback; mark it draft if it's not ready to merge.

## License

Practice repo — use freely for learning.
