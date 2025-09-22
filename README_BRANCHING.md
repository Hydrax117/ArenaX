# 🏹 ArenaX Git Branching Strategy

This document explains how we manage branches, commits, and releases for the **ArenaX Monorepo** (frontend + backend + shared code).

---

## 🔹 Main Branches
- **`main`**
  - Always production-ready.
  - Only merge here when `dev` is stable and tested.
  - Tagged with release versions (`v1.0.0`, `v1.1.0`, etc.).

- **`dev`**
  - Integration branch (staging).
  - All feature branches are merged here first.
  - Deployed to staging environment.

---

## 🔹 Feature Branches
Used for building new features.  
Format:
```
feature/<scope>-<description>
```

Examples:
- `feature/frontend-auth-ui`
- `feature/backend-tournament-routes`
- `feature/shared-types`

**Workflow:**
```bash
# Start from dev
git checkout dev
git pull origin dev

# Create feature branch
git checkout -b feature/frontend-auth-ui

# Push branch
git push origin feature/frontend-auth-ui
```

When done → create a **Pull Request (PR)** into `dev`.

---

## 🔹 Bugfix Branches
Used for fixing non-critical bugs.  
Format:
```
bugfix/<scope>-<description>
```

Examples:
- `bugfix/frontend-login-redirect`
- `bugfix/backend-db-connection`

---

## 🔹 Hotfix Branches
Used for urgent production fixes (from `main`).  
Format:
```
hotfix/<short-description>
```

Examples:
- `hotfix/fix-payment-api`
- `hotfix/security-patch`

---

## 🔹 Release Flow
1. Develop features in `feature/*`.
2. Merge to `dev`.
3. Test `dev` (staging).
4. Merge `dev` → `main` when stable.
5. Tag the release:
   ```bash
   git tag -a v1.0.0 -m "ArenaX Initial Release"
   git push origin v1.0.0
   ```

---

## 🔹 Commit Guidelines
- Use clear, concise messages.
- Format:
  ```
  <type>(<scope>): <short description>
  ```
- Examples:
  - `feat(frontend): add login UI`
  - `fix(backend): correct DB connection string`
  - `chore(shared): update constants`

---

## 🔹 Branch Naming Cheat-Sheet

| Branch Type  | Prefix     | Example                            | Purpose                          |
|--------------|-----------|------------------------------------|----------------------------------|
| Main         | `main`    | `main`                             | Production-ready code            |
| Development  | `dev`     | `dev`                              | Integration / staging            |
| Feature      | `feature/`| `feature/frontend-auth-ui`          | New features (frontend/backend)  |
| Bugfix       | `bugfix/` | `bugfix/backend-db-connection`      | Non-critical bug fixes           |
| Hotfix       | `hotfix/` | `hotfix/fix-payment-api`            | Urgent production fixes          |
| Release Tag  | `vX.Y.Z`  | `v1.0.0`                           | Tagged production release        |

---

## 🔹 Quick Commands
```bash
# Switch to dev
git checkout dev

# Create a new feature branch
git checkout -b feature/<scope>-<description>

# Push branch to remote
git push origin feature/<scope>-<description>

# Merge latest dev into your branch
git pull origin dev
```

---

## ✅ Summary
- `main` → production (stable)  
- `dev` → integration (staging)  
- `feature/*` → new development  
- `bugfix/*` → bug fixes  
- `hotfix/*` → urgent production fixes  

> Always open PRs for merging. Direct commits to `main` are **not allowed**.
