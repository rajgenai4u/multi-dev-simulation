# Multi-Dev-Simulation

A team collaboration simulation project demonstrating a real-world Git + GitHub workflow with two developers working on the same repo from **two separate local workspaces** on one machine.

## Overview

This repository simulates a two-developer workflow:

| Developer | Workspace        | Role                                  |
|-----------|------------------|---------------------------------------|
| Developer A | `dev_a_workspace` | Initial project setup, `main` branch  |
| Developer B | `dev_b_workspace` | Feature development via branch + PR   |

Both workspaces point to the same remote repository:

```
https://github.com/rajgenai4u/multi-dev-simulation.git
```

- `dev_a_workspace` uses `git@github.com:rajgenai4u/multi-dev-simulation.git` (SSH)
- `dev_b_workspace` uses `https://github.com/rajgenai4u/multi-dev-simulation.git` (HTTPS clone)

## Project Documentation

The project is a small Python app (`app.py`).

### app.py

```python
def login(username):
    return f"User {username} logged in successfully!"

def main():
    print("Welcome to Team Collaboration App!")
    print(login("Alice"))

if __name__ == "__main__":
    main()
```

### Evolution of `app.py`

**Commit 1 — `1c0750f` (Developer A · `main`)**

```python
def main():
    print("Welcome to Team Collaboration App!")

if __name__ == "__main__":
    main()
```

**Commit 2 — `52b52a1` (Developer B · `feature-auth`)**

```python
def login(username):
    return f"User {username} logged in successfully!"

def main():
    print("Welcome to Team Collaboration App!")
    print(login("Alice"))

if __name__ == "__main__":
    main()
```

### Branches

| Branch        | Working Directory  | Description                                   |
|---------------|--------------------|-----------------------------------------------|
| `main`         | `dev_a_workspace` | Default branch, holds the merged production code |
| `feature-auth` | `dev_b_workspace` | Feature branch adding login/authentication feature |

### Branch Flow

```
origin/main  ── 1c0750f ──────────────── cdd61a7 (merge PR #1)
                                          │ (via GitHub Pull Request)
origin/feature-auth        └──── 52b52a1 ─┘ (Developer B)
```

### Commit History

```
cdd61a7 Merge pull request #1 from rajgenai4u/feature-auth   (rajgenai4u · GitHub merge)
52b52a1 Add authentication feature                          (Developer B · feature-auth)
1c0750f Initial commit by Developer A                       (Developer A · main)
```

Clickable Graph:

```
*   cdd61a7 Merge pull request #1 from rajgenai4u/feature-auth
|\
| * 52b52a1 Add authentication feature
|/
* 1c0750f Initial commit by Developer A
```

### Detailed Commit Info

**Commit `1c0750f`**
- Message: `Initial commit by Developer A`
- Author: `Karre Rajesh <rajsai4us@gmail.com>`
- Files: `app.py` (`+5`)
- Note: Created the initial app and pushed it from `dev_a_workspace`

**Commit `52b52a1`**
- Message: `Add authentication feature`
- Author: `Karre Rajesh <rajsai4us@gmail.com>`
- Files: `app.py` (`+4`)
- Note: Added the `login()` function; committed on the `feature-auth` branch from `dev_b_workspace`

**Commit `cdd61a7`**
- Message: `Merge pull request #1 from rajgenai4u/feature-auth`
- Author: `rajgenai4u`
- Type: Merge commit (`1c0750f` + `52b52a1`) created from the GitHub Pull Request UI

---

## Git Commands Used

### Developer A — `dev_a_workspace` (initial setup)

```bash
# Initialize the local repository (main branch renamed to "main")
git init
git branch -M main

# Create the project file
# ... create app.py ...

# Stage and commit
git add app.py
git commit -m "Initial commit by Developer A"

# Link remote and push
git remote add origin git@github.com:rajgenai4u/multi-dev-simulation.git
git push -u origin main
```

After Developer B's PR was merged on GitHub:

```bash
# Pull the merged changes back into main
git pull origin main
```

### Developer B — `dev_b_workspace` (feature work)

```bash
# Clone the shared repository
git clone https://github.com/rajgenai4u/multi-dev-simulation.git

# Create a new feature branch
git checkout -b feature-auth

# ... update app.py with the login feature ...

# Stage, commit, and push the branch
git add app.py
git commit -m "Add authentication feature"
git push -u origin feature-auth
```

### Pull Request / Merge (done on GitHub UI)

1. Developer B pushed `feature-auth`.
2. Opened **Pull Request #1** from `feature-auth` → `main` on GitHub.
3. Merged via the GitHub web interface → created merge commit `cdd61a7`.

---

## Summary of the Collaboration Workflow

1. **Developer A** set up the repo, made the initial commit, and pushed `main` to GitHub.
2. **Developer B** cloned the repo, created a `feature-auth` branch, added the authentication feature, and pushed the branch.
3. **Developer B** opened a Pull Request; it was merged into `main` on GitHub.
4. **Developer A** pulled the merged changes to keep `main` up to date.
5. Today the repository has both branches — `main` and `feature-auth` — and a clean, merged commit history.