# All About Git & GitHub — Interview Questions and Answers

> A placement-focused Git & GitHub interview guide for freshers and junior developers.
>
> **How to use this:** Learn the concepts first, then practice the commands in a small repository. Interviewers often ask a concept question followed by a practical scenario.

---

## Table of Contents

1. [Git vs GitHub](#1-git-vs-github)
2. [Git Architecture](#2-git-architecture)
3. [Basic Git Questions](#3-basic-git-questions)
4. [Git Workflow and Commands](#4-git-workflow-and-commands)
5. [Branching](#5-branching)
6. [Merge, Rebase, and Cherry-Pick](#6-merge-rebase-and-cherry-pick)
7. [Remote Repositories and GitHub](#7-remote-repositories-and-github)
8. [Pull, Fetch, and Push](#8-pull-fetch-and-push)
9. [Merge Conflicts](#9-merge-conflicts)
10. [Git Reset, Revert, and Restore](#10-git-reset-revert-and-restore)
11. [Stash](#11-stash)
12. [Git Log and Debugging](#12-git-log-and-debugging)
13. [GitHub Pull Requests](#13-github-pull-requests)
14. [GitHub Actions and CI/CD](#14-github-actions-and-cicd)
15. [Tags and Releases](#15-tags-and-releases)
16. [`.gitignore`](#16-gitignore)
17. [Undoing Common Mistakes](#17-undoing-common-mistakes)
18. [Advanced Git Questions](#18-advanced-git-questions)
19. [Security Questions](#19-security-questions)
20. [Scenario-Based Interview Questions](#20-scenario-based-interview-questions)
21. [Practical Git Command Cheat Sheet](#21-practical-git-command-cheat-sheet)
22. [Most Important Questions for Freshers](#22-most-important-questions-for-freshers)

---

# 1. Git vs GitHub

## Q1. What is Git?

**Answer:**

Git is a **distributed version control system (DVCS)** used to track changes in source code and other files.

It allows developers to:

- Track file changes.
- Create branches.
- Work on features independently.
- Compare versions.
- Revert unwanted changes.
- Collaborate with other developers.
- Maintain the history of a project.

Git works locally, so most Git operations do not require an internet connection.

---

## Q2. What is GitHub?

**Answer:**

GitHub is a **cloud-based platform for hosting Git repositories** and collaborating on software projects.

GitHub provides features such as:

- Remote Git repositories.
- Pull requests.
- Code reviews.
- Issues.
- GitHub Actions.
- Releases.
- Project management.
- Access control.
- Team collaboration.

**Simple difference:**

| Git | GitHub |
|---|---|
| Version control system | Hosting and collaboration platform |
| Usually runs locally | Cloud service |
| Created by the Git project | A platform built around Git |
| Tracks code history | Hosts repositories and adds collaboration features |
| `git commit`, `git branch`, etc. | Pull requests, Issues, Actions, etc. |

### Interview one-liner

> **Git is the version control tool; GitHub is a platform that hosts Git repositories and provides collaboration features.**

---

## Q3. Is GitHub the same as Git?

**Answer:**

No.

Git is the version control system. GitHub is a platform that uses Git repositories and provides additional collaboration and hosting functionality.

Other Git hosting platforms include GitLab and Bitbucket.

---

# 2. Git Architecture

## Q4. Explain the Git working architecture.

Git commonly involves four important areas:

1. Working Directory
2. Staging Area
3. Local Repository
4. Remote Repository

```text
                 Git Workflow

┌──────────────────────┐
│   Working Directory  │
│                      │
│  Files you modify    │
└──────────┬───────────┘
           │
           │ git add
           ▼
┌──────────────────────┐
│    Staging Area      │
│      (Index)         │
│                      │
│ Changes selected     │
│ for next commit      │
└──────────┬───────────┘
           │
           │ git commit
           ▼
┌──────────────────────┐
│   Local Repository   │
│                      │
│ Commit history       │
│ Branches             │
│ Tags                 │
└──────────┬───────────┘
           │
           │ git push
           ▼
┌──────────────────────┐
│   Remote Repository  │
│      GitHub          │
└──────────────────────┘
```

---

## Q5. What is the Working Directory?

**Answer:**

The working directory is the current copy of the project files that you are working on.

When you edit a file, the change initially exists in the working directory.

---

## Q6. What is the Staging Area?

**Answer:**

The staging area is an intermediate area where you select changes that should be included in the next commit.

Example:

```bash
git add app.js
```

This stages `app.js`.

You can stage multiple files:

```bash
git add .
```

---

## Q7. What is the Git repository?

**Answer:**

A Git repository is a directory containing the project's Git metadata and history.

A local repository is created using:

```bash
git init
```

Git stores repository metadata inside the hidden `.git` directory.

---

## Q8. What is `.git`?

**Answer:**

`.git` is the hidden directory created when Git initializes a repository.

It contains important Git information such as:

- Commit data.
- References.
- Branch information.
- Configuration.
- Object database.
- HEAD information.

**Never manually delete `.git` unless you intentionally want to remove Git tracking from that directory.**

---

# 3. Basic Git Questions

## Q9. How do you check whether Git is installed?

```bash
git --version
```

Example output:

```text
git version 2.x.x
```

---

## Q10. How do you configure your Git username?

```bash
git config --global user.name "Your Name"
```

---

## Q11. How do you configure your Git email?

```bash
git config --global user.email "you@example.com"
```

---

## Q12. How do you see Git configuration?

```bash
git config --list
```

For a specific value:

```bash
git config user.name
git config user.email
```

---

## Q13. How do you create a new Git repository?

Go inside the project:

```bash
cd my-project
```

Then:

```bash
git init
```

This creates a `.git` directory.

---

## Q14. How do you check the status of a Git repository?

```bash
git status
```

It tells you about:

- Modified files.
- Untracked files.
- Staged files.
- Current branch.
- Changes ready to commit.

---

## Q15. What is an untracked file?

**Answer:**

A file that Git has not started tracking is called an untracked file.

Example:

```text
?? notes.txt
```

You can start tracking it with:

```bash
git add notes.txt
```

---

## Q16. What is a commit?

**Answer:**

A commit is a recorded snapshot of selected changes in the Git repository.

Example:

```bash
git add .
git commit -m "Add login API"
```

A good commit message explains what the commit changes.

---

## Q17. What is a commit hash?

**Answer:**

A commit hash is a unique identifier generated for a Git commit.

Example:

```text
a83f91c...
```

You can use it to inspect or reference a specific commit.

---

## Q18. What is HEAD in Git?

**Answer:**

`HEAD` is a reference that indicates the commit or branch currently checked out.

Normally:

```text
HEAD
  │
  ▼
main
  │
  ▼
latest commit
```

When you switch branches, `HEAD` moves to that branch.

---

# 4. Git Workflow and Commands

## Q19. Explain the basic Git workflow.

A common workflow is:

```text
Create/Edit files
      │
      ▼
git status
      │
      ▼
git add
      │
      ▼
Staging Area
      │
      ▼
git commit
      │
      ▼
Local Repository
      │
      ▼
git push
      │
      ▼
GitHub
```

Typical commands:

```bash
git status
git add .
git commit -m "Add feature"
git push
```

---

## Q20. What does `git add` do?

**Answer:**

`git add` moves selected changes from the working directory to the staging area.

Example:

```bash
git add index.js
```

All suitable changes:

```bash
git add .
```

---

## Q21. What does `git commit` do?

**Answer:**

`git commit` records the staged changes in the local repository.

Example:

```bash
git commit -m "Fix authentication bug"
```

Important:

> `git commit` does **not** normally upload changes to GitHub.

---

## Q22. What does `git push` do?

**Answer:**

`git push` sends local commits to a remote repository.

Example:

```bash
git push origin main
```

---

## Q23. What does `git clone` do?

**Answer:**

`git clone` creates a local copy of a remote repository.

Example:

```bash
git clone https://github.com/user/project.git
```

It normally creates:

- Project files.
- Git history.
- Local Git configuration for the clone.
- A remote named `origin`.

---

## Q24. What does `git init` do?

**Answer:**

`git init` turns an existing directory into a Git repository by creating Git metadata.

```bash
git init
```

### `git init` vs `git clone`

| `git init` | `git clone` |
|---|---|
| Starts a new repository in an existing directory | Copies an existing remote repository |
| Does not download remote history by itself | Downloads repository history |
| Common for a new local project | Common when joining an existing project |

---

# 5. Branching

## Q25. What is a branch?

**Answer:**

A branch is a movable reference to a line of development.

Branches allow developers to work on features or fixes without directly modifying the main development line.

Example:

```text
                 feature/login
                     ●──●──●
                    /
●──●──●────────────●──────── main
```

---

## Q26. Why are branches used?

**Answer:**

Branches are used to:

- Develop features independently.
- Fix bugs safely.
- Experiment with changes.
- Review code before merging.
- Allow multiple developers to work simultaneously.

---

## Q27. How do you create a branch?

```bash
git branch feature-login
```

Create and switch to it:

```bash
git switch -c feature-login
```

Older/common syntax:

```bash
git checkout -b feature-login
```

---

## Q28. How do you list branches?

Local branches:

```bash
git branch
```

Remote branches:

```bash
git branch -r
```

All branches:

```bash
git branch -a
```

---

## Q29. How do you switch branches?

Modern command:

```bash
git switch feature-login
```

Older command:

```bash
git checkout feature-login
```

---

## Q30. How do you delete a branch?

Local branch:

```bash
git branch -d feature-login
```

Force deletion:

```bash
git branch -D feature-login
```

Remote branch:

```bash
git push origin --delete feature-login
```

---

## Q31. What is the difference between `git switch` and `git checkout`?

**Answer:**

`git checkout` is an older, multi-purpose command used for switching branches and restoring files.

`git switch` was introduced specifically for branch switching, making the intention clearer.

For example:

```bash
git switch main
```

is clearer for switching branches.

---

# 6. Merge, Rebase, and Cherry-Pick

## Q32. What is merging?

**Answer:**

Merging combines changes from one branch into another.

Example:

```bash
git switch main
git merge feature-login
```

Conceptually:

```text
feature
   ●──●
  /    \
 ●──────●  main
```

Depending on the history, Git may perform a fast-forward merge or create a merge commit.

---

## Q33. What is a fast-forward merge?

**Answer:**

A fast-forward merge occurs when the target branch has no divergent commits and Git can simply move the target branch pointer forward.

```text
Before:

main:    A──B
              \
feature:       C──D

After:

main:    A──B──C──D
feature:       C──D
```

No merge commit is required.

---

## Q34. What is a merge conflict?

**Answer:**

A merge conflict occurs when Git cannot automatically combine changes.

A common example is when two branches modify the same part of the same file differently.

Git marks the conflicting section:

```text
<<<<<<< HEAD
Current branch code
=======
Incoming branch code
>>>>>>> feature
```

You manually choose the correct code, then:

```bash
git add <file>
git commit
```

For a merge conflict, the exact continuation depends on whether you are merging, rebasing, or performing another operation.

---

## Q35. What is rebasing?

**Answer:**

Rebase moves or reapplies commits onto a new base commit.

Example:

```text
Before:

A──B──C  main
    \
     D──E  feature

After rebase:

A──B──C──D'──E'  feature
```

The commits are recreated, so their hashes change.

---

## Q36. Merge vs Rebase?

| Merge | Rebase |
|---|---|
| Combines histories | Replays commits on a new base |
| Can create a merge commit | Usually creates a linear history |
| Preserves existing commit topology | Rewrites commit history |
| Safer for shared history | Be careful with already-pushed shared commits |

### Interview answer

> I prefer merging when preserving the exact branch history is important. I use rebase to keep a private feature branch up to date and maintain a cleaner linear history, but I avoid rebasing commits that other developers are already relying on.

---

## Q37. What is interactive rebase?

**Answer:**

Interactive rebase allows you to modify a sequence of commits.

Example:

```bash
git rebase -i HEAD~3
```

You can:

- Reorder commits.
- Squash commits.
- Edit commit messages.
- Drop commits.
- Edit commits.

Common commands in the interactive editor:

```text
pick
reword
edit
squash
fixup
drop
```

---

## Q38. What is cherry-pick?

**Answer:**

`git cherry-pick` applies the changes introduced by a specific commit onto the current branch.

Example:

```bash
git cherry-pick abc1234
```

Useful when you need one particular fix without merging an entire branch.

---

# 7. Remote Repositories and GitHub

## Q39. What is a remote repository?

**Answer:**

A remote repository is another copy of a Git repository, commonly hosted on services such as GitHub.

You can view remotes using:

```bash
git remote -v
```

---

## Q40. What is `origin`?

**Answer:**

`origin` is the conventional default name given to the remote repository when a repository is cloned.

For example:

```bash
git push origin main
```

Here:

- `origin` = remote name
- `main` = branch name

`origin` is only a name; it is not a special Git protocol.

---

## Q41. How do you add a remote?

```bash
git remote add origin https://github.com/user/project.git
```

Check it:

```bash
git remote -v
```

---

## Q42. How do you change a remote URL?

```bash
git remote set-url origin https://github.com/user/new-project.git
```

---

## Q43. What is `origin/main`?

**Answer:**

`origin/main` is a remote-tracking reference representing the `main` branch as last known from the `origin` remote.

It is not the same thing as your local `main` branch.

```text
Local:
main

Remote-tracking:
origin/main
```

---

# 8. Pull, Fetch, and Push

## Q44. What is `git fetch`?

**Answer:**

`git fetch` downloads new objects and updated remote-tracking references from a remote repository without automatically merging those changes into your current branch.

Example:

```bash
git fetch origin
```

You can then inspect:

```bash
git log main..origin/main
```

---

## Q45. What is `git pull`?

**Answer:**

`git pull` generally performs:

```text
git fetch
+
integrate fetched changes
```

The integration may be a merge or, depending on configuration/options, a rebase.

Example:

```bash
git pull origin main
```

---

## Q46. Difference between `git fetch` and `git pull`?

| `git fetch` | `git pull` |
|---|---|
| Downloads remote updates | Downloads and integrates updates |
| Does not change current branch files by itself | May change current branch/files |
| Safer for inspecting changes first | Convenient for routine synchronization |

### Good interview answer

> `fetch` lets me see what changed on the remote before integrating it. `pull` fetches and then integrates the changes into my current branch.

---

## Q47. What is `git push -u origin main`?

**Answer:**

It pushes the local `main` branch to `origin` and sets its upstream tracking branch.

```bash
git push -u origin main
```

After that, you can often use:

```bash
git push
git pull
```

without specifying the remote and branch every time.

---

# 9. Merge Conflicts

## Q48. How do you resolve a merge conflict?

**Answer:**

Typical process:

### Step 1 — Check conflicts

```bash
git status
```

### Step 2 — Open conflicting files

Look for:

```text
<<<<<<< HEAD
your changes
=======
incoming changes
>>>>>>> branch-name
```

### Step 3 — Edit the file

Keep the desired code and remove conflict markers.

### Step 4 — Stage the resolved file

```bash
git add filename
```

### Step 5 — Finish the operation

For a merge:

```bash
git commit
```

For a rebase:

```bash
git rebase --continue
```

### Abort if necessary

Merge:

```bash
git merge --abort
```

Rebase:

```bash
git rebase --abort
```

---

## Q49. How can you reduce merge conflicts?

**Answer:**

- Keep branches short-lived.
- Pull/rebase from the latest target branch regularly when appropriate.
- Make small commits.
- Avoid unnecessary formatting changes in feature branches.
- Communicate when multiple developers are editing the same area.
- Keep files/modules reasonably separated.

---

# 10. Git Reset, Revert, and Restore

## Q50. What is `git reset`?

**Answer:**

`git reset` moves the current branch reference and can also change the staging area and working tree depending on the mode.

Three important modes:

```bash
git reset --soft
git reset --mixed
git reset --hard
```

---

## Q51. Explain `git reset --soft`.

```bash
git reset --soft HEAD~1
```

It moves `HEAD` back by one commit while keeping the changes staged.

Useful when you want to redo or combine the last commit.

---

## Q52. Explain `git reset --mixed`.

```bash
git reset HEAD~1
```

This is the default reset mode.

It moves the branch back and unstages the changes, while keeping the working-tree changes.

---

## Q53. Explain `git reset --hard`.

```bash
git reset --hard HEAD~1
```

It moves the branch back and resets the index and working tree to match the target commit.

**Warning:** uncommitted changes can be lost.

Do not use it casually.

---

## Q54. What is `git revert`?

**Answer:**

`git revert` creates a **new commit** that reverses the effect of an earlier commit.

Example:

```bash
git revert abc1234
```

This is generally safer than rewriting shared history.

---

## Q55. Reset vs Revert?

| Reset | Revert |
|---|---|
| Moves branch history | Creates a new reversing commit |
| Can rewrite history | Preserves existing history |
| Useful for local/private cleanup | Good for shared/public branches |
| `reset --hard` can discard local changes | Usually safer for collaboration |

### Interview rule

> If the commit has already been pushed and other people may have based work on it, prefer `git revert` over history-rewriting commands.

---

## Q56. What is `git restore`?

**Answer:**

`git restore` is used to restore files in the working tree or staging area.

Discard working-tree changes to a file:

```bash
git restore app.js
```

Unstage a file:

```bash
git restore --staged app.js
```

---

# 11. Stash

## Q57. What is Git stash?

**Answer:**

`git stash` temporarily saves uncommitted changes so you can get a clean working directory.

Example:

```bash
git stash
```

Later:

```bash
git stash pop
```

---

## Q58. When would you use stash?

**Scenario:**

You are working on a feature, but suddenly need to switch to another branch for an urgent bug fix. Your current changes are incomplete.

You can:

```bash
git stash
git switch main
```

Work on the bug, then return and restore your changes:

```bash
git switch feature
git stash pop
```

---

## Q59. Difference between `git stash pop` and `git stash apply`?

**Answer:**

```bash
git stash pop
```

applies the stash and removes it from the stash list if successful.

```bash
git stash apply
```

applies the stash but keeps the stash entry.

---

## Q60. How do you list stashes?

```bash
git stash list
```

Example:

```text
stash@{0}
stash@{1}
stash@{2}
```

---

# 12. Git Log and Debugging

## Q61. How do you view commit history?

```bash
git log
```

Compact version:

```bash
git log --oneline
```

Graph:

```bash
git log --oneline --graph --decorate --all
```

---

## Q62. How do you see what changed in a commit?

```bash
git show <commit-hash>
```

---

## Q63. How do you compare two commits?

```bash
git diff commit1 commit2
```

---

## Q64. How do you compare your working directory with the last commit?

```bash
git diff
```

---

## Q65. How do you find which commit introduced a bug?

**Answer:**

A very useful Git command is:

```bash
git bisect
```

Example:

```bash
git bisect start
git bisect bad
git bisect good <known-good-commit>
```

Git checks out candidate commits. You test each one and tell Git whether it is good or bad.

Eventually Git identifies the commit that introduced the problem.

---

## Q66. What is `git blame`?

**Answer:**

`git blame` shows which commit and author last modified each line of a file.

```bash
git blame app.js
```

It is useful for understanding the history of a particular line.

---

# 13. GitHub Pull Requests

## Q67. What is a Pull Request (PR)?

**Answer:**

A Pull Request is a GitHub collaboration mechanism used to propose merging changes from one branch into another.

Typical workflow:

```text
Feature Branch
      │
      ▼
Push to GitHub
      │
      ▼
Create Pull Request
      │
      ▼
Code Review
      │
      ▼
CI / Tests
      │
      ▼
Approval
      │
      ▼
Merge
```

---

## Q68. Is a Pull Request a Git command?

**Answer:**

No.

A Pull Request is a platform feature commonly provided by GitHub and similar hosting services.

Git itself provides commands such as:

```bash
git branch
git merge
git rebase
git push
```

---

## Q69. What happens in a typical GitHub PR?

**Answer:**

A team may:

1. Create a feature branch.
2. Make commits.
3. Push the branch.
4. Open a Pull Request.
5. Run automated checks.
6. Ask teammates for review.
7. Make requested changes.
8. Get approval.
9. Merge the PR.
10. Delete the feature branch if appropriate.

---

## Q70. What is a code review?

**Answer:**

Code review is the process of having other developers inspect proposed code changes before they are merged.

Reviewers commonly check:

- Correctness.
- Readability.
- Security.
- Performance.
- Testing.
- Maintainability.
- Coding standards.

---

# 14. GitHub Actions and CI/CD

## Q71. What is GitHub Actions?

**Answer:**

GitHub Actions is GitHub's automation platform.

It can automatically perform tasks such as:

- Running tests.
- Building applications.
- Linting.
- Deploying applications.
- Creating releases.
- Running scheduled jobs.

---

## Q72. What is CI?

**Answer:**

CI means **Continuous Integration**.

Developers frequently integrate code changes into a shared repository, and automated checks such as builds and tests verify those changes.

Example:

```text
Developer pushes code
        │
        ▼
GitHub
        │
        ▼
GitHub Actions
        │
        ├── Build
        ├── Test
        └── Lint
        │
        ▼
Pass / Fail
```

---

## Q73. What is CD?

**Answer:**

CD can mean Continuous Delivery or Continuous Deployment depending on context.

- **Continuous Delivery:** software is kept ready for release, often with a manual production approval.
- **Continuous Deployment:** successful changes can automatically be deployed to production.

---

## Q74. Where are GitHub Actions workflows stored?

**Answer:**

Workflow files are normally stored under:

```text
.github/workflows/
```

Example:

```text
.github/
└── workflows/
    └── ci.yml
```

---

# 15. Tags and Releases

## Q75. What is a Git tag?

**Answer:**

A tag is a reference used to mark a specific point in Git history, often for releases.

Example:

```bash
git tag v1.0.0
```

Push it:

```bash
git push origin v1.0.0
```

---

## Q76. Why are tags useful?

**Answer:**

Tags make important versions easy to identify.

Example:

```text
v1.0.0
v1.1.0
v2.0.0
```

You can later inspect or check out a tagged version.

---

## Q77. What is a GitHub Release?

**Answer:**

A GitHub Release is a GitHub feature built around a Git tag.

It can contain:

- Version information.
- Release notes.
- Downloadable assets.
- Changelog information.

---

# 16. `.gitignore`

## Q78. What is `.gitignore`?

**Answer:**

`.gitignore` is a file that tells Git which files or patterns should normally not be tracked.

For a Node.js project:

```gitignore
node_modules/
.env
dist/
coverage/
```

---

## Q79. Why should `.env` usually be in `.gitignore`?

**Answer:**

`.env` files commonly contain secrets such as:

- Database passwords.
- API keys.
- JWT secrets.
- Cloud credentials.

These should not be committed to a public repository.

Important:

> `.gitignore` does not remove a file that is already tracked.

---

## Q80. I added `.env` to `.gitignore`, but Git still tracks it. Why?

**Answer:**

Because `.gitignore` mainly affects untracked files.

If `.env` was already committed, remove it from Git tracking while keeping the local file:

```bash
git rm --cached .env
git commit -m "Stop tracking environment file"
```

Then ensure:

```gitignore
.env
```

is present.

If the secret was already pushed, **removing the file in a later commit does not make the old secret safe**. The credential should be rotated/revoked and, when necessary, the repository history should be cleaned.

---

# 17. Undoing Common Mistakes

## Q81. I accidentally staged a file. How do I unstage it?

```bash
git restore --staged filename
```

---

## Q82. I modified a file but want to discard the change.

```bash
git restore filename
```

**Warning:** this discards the uncommitted working-tree change.

---

## Q83. I committed locally but want to change the commit message.

If it is the latest commit:

```bash
git commit --amend -m "New commit message"
```

---

## Q84. I committed a file that should not have been committed.

If you want to remove it from the latest commit while keeping the file locally:

```bash
git rm --cached filename
git commit --amend
```

Then add it to `.gitignore` if appropriate.

If a secret was committed, treat it as compromised and rotate it.

---

## Q85. I accidentally committed to the wrong branch. What should I do?

A common approach:

1. Create the correct branch from the current commit.
2. Move the wrong branch back if appropriate.
3. Push the correct branch.
4. Be careful if the incorrect branch was already shared.

Example for a local-only mistake:

```bash
git branch feature-login
git switch main
git reset --hard HEAD~1
git switch feature-login
```

If the wrong branch was already pushed/shared, coordinate with the team before rewriting history.

---

# 18. Advanced Git Questions

## Q86. What is a detached HEAD?

**Answer:**

A detached HEAD state occurs when `HEAD` points directly to a commit rather than a branch.

Example:

```bash
git checkout <commit-hash>
```

You can inspect and experiment with that commit.

If you make commits and want to keep them, create a branch:

```bash
git switch -c my-experiment
```

---

## Q87. What is a remote-tracking branch?

**Answer:**

A remote-tracking branch is a local reference that records the state of a branch on a remote as last fetched.

Example:

```text
origin/main
origin/develop
```

It updates when you fetch from the remote.

---

## Q88. What is the difference between local and remote branches?

**Answer:**

A local branch is a branch you work with directly in your local repository.

A remote-tracking branch such as `origin/main` represents the state of a remote branch as known locally.

The actual remote repository is hosted elsewhere.

---

## Q89. What is a Git object?

**Answer:**

Git internally stores information as objects.

Important object types include:

- Blob — file contents.
- Tree — directory structure and file names.
- Commit — snapshot metadata and parent information.
- Tag — annotated tag information.

Conceptually:

```text
Commit
  │
  ▼
 Tree
 ├── Blob
 ├── Blob
 └── Tree
      └── Blob
```

---

## Q90. What is the Git object database?

**Answer:**

Git stores repository objects in its internal object database, historically under:

```text
.git/objects/
```

Objects are addressed using cryptographic hash identifiers.

---

## Q91. What is `git reflog`?

**Answer:**

`git reflog` records movements of local references such as `HEAD`.

It can help recover commits that appear to have been lost after operations such as:

- Reset.
- Rebase.
- Amend.

Example:

```bash
git reflog
```

You may find an earlier commit and recover it by creating a branch:

```bash
git branch recovery <commit-hash>
```

---

## Q92. What is `git clean`?

**Answer:**

`git clean` removes untracked files from the working tree.

Preview first:

```bash
git clean -n
```

Actually remove:

```bash
git clean -f
```

Be careful because these files are not part of normal Git history.

---

## Q93. What is a Git alias?

**Answer:**

A Git alias creates a shortcut for a command.

Example:

```bash
git config --global alias.co checkout
```

Then:

```bash
git co main
```

can act as a shortcut for:

```bash
git checkout main
```

---

## Q94. What is a shallow clone?

**Answer:**

A shallow clone downloads limited commit history instead of the complete repository history.

Example:

```bash
git clone --depth 1 <repository-url>
```

It can reduce download time and storage requirements, especially in CI environments.

---

## Q95. What is a bare repository?

**Answer:**

A bare repository contains Git repository data without a normal working directory.

It is commonly used as a server-side repository.

Example:

```bash
git init --bare
```

---

## Q96. What is Git LFS?

**Answer:**

Git Large File Storage (Git LFS) is an extension for managing large files by storing lightweight pointer files in Git while the large file content is handled separately.

It is useful for large assets such as:

- Videos.
- Large datasets.
- Design files.
- Binary assets.

---

# 19. Security Questions

## Q97. How should you handle API keys in GitHub?

**Answer:**

Do not hard-code secrets into source code.

Bad:

```javascript
const API_KEY = "my-secret-key";
```

Better:

```javascript
const API_KEY = process.env.API_KEY;
```

Store the secret securely, such as:

- Environment variables for local development.
- GitHub Actions Secrets for workflows.
- A cloud secret manager for production.

---

## Q98. What should you do if you accidentally push a password or API key?

**Answer:**

Treat the secret as compromised.

### Immediate actions

1. Revoke or rotate the secret.
2. Stop using the exposed credential.
3. Remove it from the current code.
4. If necessary, remove it from Git history.
5. Check logs and access records where appropriate.
6. Prevent future commits with secret scanning and good repository practices.

Important:

> Deleting the secret in a new commit does not erase it from previous Git history.

---

## Q99. What is SSH in GitHub?

**Answer:**

SSH provides an authenticated way to connect to GitHub using an SSH key pair.

Typical setup:

```text
Your computer
   │
   │ private key
   │
   ▼
SSH authentication
   │
   ▼
GitHub
   ▲
   │
public key
```

The private key should remain secret.

---

## Q100. HTTPS vs SSH for GitHub?

| HTTPS | SSH |
|---|---|
| Uses HTTPS remote URL | Uses SSH remote URL |
| Authentication typically uses GitHub credentials/token mechanisms | Uses SSH keys |
| Easy to understand for beginners | Convenient for repeated developer use |
| Works well in many environments | Requires SSH key setup |

---

# 20. Scenario-Based Interview Questions

## Q101. Your teammate pushed changes to `main`, and your local `main` is outdated. What do you do?

**Answer:**

First, make sure I don't have uncommitted work that would be affected.

Then:

```bash
git switch main
git fetch origin
git pull origin main
```

Or I can fetch first and inspect:

```bash
git fetch origin
git log main..origin/main
```

Then integrate the changes appropriately.

---

## Q102. You are working on a feature and receive an urgent bug-fix task. Your feature is incomplete. What do you do?

**Answer:**

If the feature changes are not ready to commit, I can temporarily stash them:

```bash
git stash
git switch main
```

After completing the bug fix:

```bash
git switch feature
git stash pop
```

Another option is to make a temporary WIP commit if that fits the team's workflow.

---

## Q103. Two developers modified the same line. What happens?

**Answer:**

If Git cannot automatically determine the correct result, a merge/rebase conflict occurs.

I would:

1. Run `git status`.
2. Open the conflicting file.
3. Understand both changes.
4. Resolve the conflict.
5. Remove conflict markers.
6. Stage the file.
7. Complete the merge or rebase.
8. Run tests.

---

## Q104. You need only one bug fix from another branch. Would you merge the whole branch?

**Answer:**

Not necessarily.

If only one specific commit is needed, I could use:

```bash
git cherry-pick <commit-hash>
```

This applies that commit to my current branch.

---

## Q105. You pushed a bad commit to a shared branch. Should you use reset?

**Answer:**

Usually, no.

For a shared/public branch, I would generally prefer:

```bash
git revert <commit-hash>
```

This creates a new commit that reverses the bad change while preserving shared history.

---

## Q106. You made five small commits and want one clean commit before opening a PR. What can you use?

**Answer:**

Interactive rebase:

```bash
git rebase -i HEAD~5
```

Then use `squash` or `fixup` as appropriate.

I would only rewrite history if those commits are not already being relied upon by others.

---

## Q107. Your latest commit has the wrong message. What do you do?

**Answer:**

If it has not been shared or rewriting it is acceptable:

```bash
git commit --amend -m "Correct message"
```

If the commit was already pushed, be careful because amending changes the commit hash and may require a history-rewriting push.

---

## Q108. You deleted a commit using reset. Is it always lost?

**Answer:**

Not necessarily.

The commit may still be reachable through the local reflog.

```bash
git reflog
```

Find the previous commit and create a recovery branch:

```bash
git branch recovery <commit-hash>
```

---

## Q109. Your `.gitignore` contains `node_modules/`, but Git still shows changes inside it. Why?

**Answer:**

Most likely `node_modules` was already tracked before it was added to `.gitignore`.

Remove it from tracking:

```bash
git rm -r --cached node_modules
git commit -m "Stop tracking node_modules"
```

Then keep:

```gitignore
node_modules/
```

in `.gitignore`.

---

## Q110. How would you safely update your feature branch with the latest `main`?

**Answer:**

One option is merge:

```bash
git fetch origin
git switch feature
git merge origin/main
```

Another option is rebase, if the branch is private or team policy permits:

```bash
git fetch origin
git switch feature
git rebase origin/main
```

After a rebase of an already-pushed branch, pushing may require:

```bash
git push --force-with-lease
```

Use force pushing carefully.

---

# 21. Practical Git Command Cheat Sheet

## Create repository

```bash
git init
```

## Clone repository

```bash
git clone <url>
```

## Check status

```bash
git status
```

## Stage a file

```bash
git add filename
```

## Stage all changes

```bash
git add .
```

## Commit

```bash
git commit -m "message"
```

## View history

```bash
git log
git log --oneline
git log --oneline --graph --decorate --all
```

## Create branch

```bash
git branch feature
```

## Create + switch

```bash
git switch -c feature
```

## Switch branch

```bash
git switch main
```

## Merge

```bash
git merge feature
```

## Rebase

```bash
git rebase main
```

## Fetch

```bash
git fetch origin
```

## Pull

```bash
git pull origin main
```

## Push

```bash
git push origin main
```

## Push and set upstream

```bash
git push -u origin main
```

## Add remote

```bash
git remote add origin <url>
```

## View remote

```bash
git remote -v
```

## Stash

```bash
git stash
git stash list
git stash pop
git stash apply
```

## View commit details

```bash
git show <commit>
```

## Compare changes

```bash
git diff
git diff <commit1> <commit2>
```

## Revert commit

```bash
git revert <commit>
```

## Reset

```bash
git reset --soft HEAD~1
git reset HEAD~1
git reset --hard HEAD~1
```

## Restore

```bash
git restore filename
git restore --staged filename
```

## Tags

```bash
git tag v1.0.0
git push origin v1.0.0
```

## Reflog

```bash
git reflog
```

## Find a bug with bisect

```bash
git bisect start
git bisect bad
git bisect good <commit>
```

---

# 22. Most Important Questions for Freshers

If you have limited interview preparation time, prioritize these:

### Tier 1 — Must Know

1. What is Git?
2. What is GitHub?
3. Git vs GitHub.
4. What is version control?
5. What is a repository?
6. What is `git init`?
7. What is `git clone`?
8. What is `git add`?
9. What is `git commit`?
10. What is `git push`?
11. What is `git pull`?
12. What is `git fetch`?
13. `fetch` vs `pull`.
14. What is a branch?
15. How do you create/switch branches?
16. What is merging?
17. What is a merge conflict?
18. How do you resolve conflicts?
19. What is `.gitignore`?
20. What is a Pull Request?

### Tier 2 — Very Important

21. Merge vs rebase.
22. Reset vs revert.
23. `git restore`.
24. Git stash.
25. `git cherry-pick`.
26. Local vs remote branch.
27. What is `origin`?
28. What is `HEAD`?
29. What is `origin/main`?
30. How do you undo a commit?
31. How do you undo staged changes?
32. How do you discard local changes?
33. How do you handle accidentally committed secrets?
34. What is code review?
35. What is GitHub Actions?
36. What is CI/CD?

### Tier 3 — Good for Stronger Interviews

37. Interactive rebase.
38. Detached HEAD.
39. Reflog.
40. Git bisect.
41. Git blame.
42. Git object model.
43. Shallow clone.
44. Bare repository.
45. Git LFS.
46. Force push vs `--force-with-lease`.

---

# Quick Interview Revision

Remember this workflow:

```text
              LOCAL MACHINE
┌───────────────────────────────────────────┐
│                                           │
│  Working Directory                        │
│        │                                  │
│        │ git add                          │
│        ▼                                  │
│  Staging Area                             │
│        │                                  │
│        │ git commit                       │
│        ▼                                  │
│  Local Repository                         │
│        │                                  │
│        │ git push                         │
└────────┼──────────────────────────────────┘
         ▼
      GitHub
      Remote
         │
         │ git fetch / git pull
         ▼
      Local Git
```

## The 10 commands you should be able to use without thinking

```bash
git status
git add .
git commit -m "message"
git log --oneline
git branch
git switch -c feature
git switch main
git fetch
git pull
git push
```

## Golden interview rules

- **Git ≠ GitHub.**
- `git add` → staging.
- `git commit` → local history.
- `git push` → upload local commits to remote.
- `git fetch` → download remote updates without integrating them into your current branch.
- `git pull` → fetch + integrate.
- `git merge` → combine histories.
- `git rebase` → replay commits onto another base and rewrite commit IDs.
- `git revert` → create a new commit that reverses an earlier commit.
- `git reset` → move branch history/reference; use carefully on shared branches.
- `.gitignore` does not automatically untrack files already tracked.
- Never commit secrets.
- For shared branches, prefer safe history-preserving operations.
- A Pull Request is a GitHub collaboration feature, not a Git command.
- Before saying a Git command is "safe," consider whether the branch is private or shared.

---

# Final Interview Tip

For a fresher interview, don't just memorize commands. Be able to explain a realistic workflow:

```text
"I create a feature branch,
make changes,
check git status,
stage the required files,
commit with a meaningful message,
push the branch to GitHub,
create a Pull Request,
resolve review comments,
pass CI checks,
and merge the branch into the target branch."
```

If you can confidently explain this workflow **and** handle merge conflicts, stash, reset/revert, fetch/pull, branching, `.gitignore`, and Pull Requests, you will cover a large portion of common Git/GitHub interview questions.
