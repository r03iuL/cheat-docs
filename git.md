# 🧰 Git & GitHub Cheatsheet (2025)

> :bulb: This is a quick reference for daily Git/GitHub daily used commands.

> :book: Official Docs: **[Git Book](https://git-scm.com/doc) • [Git Reference](https://git-scm.com/docs) • [GitHub Docs](https://docs.github.com)**

## 📑 Table of Contents

- [Workflow overview (diagram)](#-workflow-overview-diagram)
- [Install \& first-time setup](#install--first-time-setup)
- [Create a repo / clone a repo](#create-a-repo--clone-a-repo)
- [.gitignore essentials](#gitignore-essentials)
- [Manage remotes (add / set-url / remove)](#manage-remotes-add--set-url--remove)
- [Check status \& changes](#check-status--changes)
- [Stage files (selective vs all)](#stage-files-selective-vs-all)
- [Write commits (good messages)](#write-commits-good-messages)
- [View history \& inspect commits](#view-history--inspect-commits)
- [Branch: create, switch, delete](#branch-create-switch-delete)
- [Sync with remotes (fetch / pull / push)](#sync-with-remotes-fetch--pull--push)
- [Merge vs rebase (when to use which)](#merge-vs-rebase-when-to-use-which)
- [Resolve merge conflicts](#resolve-merge-conflicts)
- [Quick undo options (restore / reset / revert)](#quick-undo-options-restore--reset--revert)
- [Stash work-in-progress](#stash-work-in-progress)
- [Tags \& releases](#tags--releases)
- [Safe force-push policy (--force-with-lease)](#safe-force-push-policy---force-with-lease)
- [Recover work (reflog \& rescue branches)](#recover-work-reflog--rescue-branches)
- [Cherry-pick targeted fixes](#cherry-pick-targeted-fixes)
- [GitHub — daily collaboration](#github--daily-collaboration)
  - [GitHub: create repo \& connect](#github-create-repo--connect)
  - [GitHub: forks and keeping fork updated](#github-forks-and-keeping-fork-updated)
  - [Pull requests \& basic code review](#pull-requests--basic-code-review)
  - [Reading CI/checks on PRs](#reading-cichecks-on-prs)
  - [Auth choices (SSH vs HTTPS tokens)](#auth-choices-ssh-vs-https-tokens)
  - [Daily safety rules \& branch protection](#daily-safety-rules--branch-protection)

---

## Workflow overview (diagram)

```ASCII
Working tree --git add--> Staging (index) --git commit--> Local (HEAD) --git push--> Remote (GitHub)
Remote (GitHub) --git fetch/pull--> Local (HEAD)
```

---

## Install & first-time setup

Install Git, then set your identity and sane defaults globally so every repo inherits them. Keep pulls merge-by-default (beginner-safe), prune stale branches on fetch, and use your editor for commit messages.

```bash
git --version                                   # verify install

# Identity (appears on every commit)
git config --global user.name "<your-name>"
git config --global user.email "<your-email>"

# Defaults
git config --global init.defaultBranch main     # new repos use 'main'
git config --global pull.rebase false           # pulls merge by default (team-friendly)
git config --global fetch.prune true            # drop stale remote branches on fetch
git config --global core.editor "code --wait"   # VS Code for messages (adjust if you use another)
git config --list --global                      # review your global config
```

**Keyword breakdown**

- `<your-name>` / `<your-email>` — Commit identity (use the email GitHub verifies for “Verified”).
- `pull.rebase false` — Avoids rewriting history when pulling (easier for beginners).
- `fetch.prune true` — Cleans up branches deleted on the server.

> [!NOTE]  
> Line endings: **Windows** → `git config --global core.autocrlf true` • **macOS/Linux** → `input`.

> :bulb: **Tip**  
> Keep a dotfiles repo with your `.gitconfig` so a new machine is one command away.

---

## Create a repo / clone a repo

Start a new project locally or copy an existing one. Seed with a README so your first push isn’t empty.

```bash
# New local repo
mkdir <project> && cd <project>
git init                                       # start Git here
printf "# <project>\n" > README.md
git add README.md                              # stage first file
git commit -m "init"                           # first commit

# Or clone an existing repo
# HTTPS:
git clone https://github.com/<owner>/<repo>.git
# SSH:
git clone git@github.com:<owner>/<repo>.git
cd <repo>
```

**Keyword breakdown**

- `<project>` — New folder/repo name.
- `<owner>/<repo>` — GitHub namespace and repository.

> :bulb: **Tip**  
> Prefer **SSH** after you set keys (fewer prompts). Use **HTTPS** if your org mandates tokens.

---

## .gitignore essentials

Ignore generated files (build outputs, logs, env files) so they don’t clutter history.

```bash
printf "node_modules/\n*.log\n.env\n.DS_Store\n" >> .gitignore
git rm -r --cached .                           # stop tracking existing ignored files (kept on disk)
git add .gitignore
git commit -m "chore: add .gitignore"
```

**Keyword breakdown**

- `.gitignore` — Patterns excluded from version control.
- `git rm -r --cached .` — Untracks current matches without deleting files.

**Basic .gitignore example: **

```
# Node.js
node_modules/
*.log
.env
.DS_Store
```

> [!NOTE]  
> Generate stack-specific templates at **https://gitignore.io**, then trim to fit.

---

## Manage remotes (add / set-url / remove)

Connect your local repo to GitHub and adjust URLs later if they change.

```bash
git remote -v                                  # list remotes

# Add 'origin' (both forms shown)
git remote add origin https://github.com/<owner>/<repo>.git
git remote add origin git@github.com:<owner>/<repo>.git   # SSH

git push -u origin main                        # first publish + set upstream

git remote set-url origin <new-repo-url>       # update URL
git remote remove <name>                       # remove a remote
```

**Keyword breakdown**

- `<new-repo-url>` — New HTTPS/SSH URL from GitHub.
- `<name>` — Remote name (usually `origin`; `upstream` for the source repo).
- `-u` — Records tracking so future `git push`/`git pull` know where to go.

> :bulb: **Tip**  
> For forks, keep `origin` (your fork) and add `upstream` (the source project).

---

## Check status & changes

Before you commit, quickly see what changed and exactly what lines will be recorded.

```bash
git status -sb                                 # concise status + branch
git diff                                       # unstaged changes
git diff --staged                              # what will be committed
```

**Keyword breakdown**

- `-s -b` — Short format; show branch header.
- `--staged` — Compare index to last commit.

> :bulb: **Tip**  
> Add a pretty log alias once:  
> `git config --global alias.lg "log --oneline --graph --decorate --all"` → then run `git lg`.

---

## Stage files (selective vs all)

Curate exactly what goes into a commit; unstage safely without losing work.

```bash
git add <file>                                 # stage a specific file
git add -p                                     # interactively stage hunks
git restore --staged <file>                    # unstage but keep edits
git add .                                      # stage everything under CWD (be cautious)
```

**Keyword breakdown**

- `<file>` — Path to stage/unstage.
- `-p` — Patch (interactive) mode to choose hunks.

> [!NOTE]  
> In large repos, prefer `git add -p` + `git status` over `git add .`.

---

## Write commits (good messages)

Make small, focused commits with clear messages. Amend only before sharing.

```bash
git commit -m "<subject>"                      # short imperative summary
git commit -m "<subject>" -m "<body>"          # include why/how
git commit --amend                             # fix last commit (before pushing)
```

**Keyword breakdown**

- `<subject>` — Imperative, ~50 chars (e.g., “Add login form”).
- `<body>` — Why/how, wrap ~72; link tickets/docs if helpful.
- `--amend` — Rewrites the last local commit.

> :bulb: **Tip:**  Reference issues like `Fixes #123` to auto-close when the PR merges.

> :link: **https://conventionalcommits.org** for detailed commit message style.

---

## View history & inspect commits

Skim history, view a specific commit, or see who changed a line.

```bash
git lg                                          # if you set the alias; else use the long form
git show <sha>                                  # view a commit (message + patch)
git blame <file>                                # last modifier per line
```

**Keyword breakdown**

- `<sha>` — Commit hash (7+ chars OK).
- `<file>` — File to annotate.

> [!NOTE]  
> View a file at a commit: `git show <sha>:<path/to/file>`.

---

## Branch: create, switch, delete

Use a branch per task; switch safely; delete after merge to keep things tidy.

```bash
git branch                                      # list local branches
git switch -c <branch>                          # create + switch
git switch <branch>                             # switch existing
git branch -d <branch>                          # delete merged branch
```

**Keyword breakdown**

- `<branch>` — e.g., `feat/login`, `fix/crash`.

> [!NOTE]  
> `git branch -D <branch>` force-deletes (danger—ensure work is merged/backed up).

> :bulb: **Tip**  
> Prefix branches (`feat/`, `fix/`, `chore/`) so PRs group nicely.

---

## Sync with remotes (fetch / pull / push)

Keep local and remote in sync; publish your work.

```bash
git fetch --all --prune                         # update refs; drop stale branches
git pull                                        # fetch + merge into current branch
git push                                        # publish local commits
git push -u origin <branch>                     # first push of a new branch
```

**Keyword breakdown**

- `--prune` — Remove deleted remote branches locally.
- `<branch>` — Your feature/fix branch.

> :bulb: **Tip**  
> Want tidy local history on your own branch? Use `git pull --rebase` there (but keep `pull.rebase=false` globally for safety).

---

## Merge vs rebase (when to use which)

**Merge** preserves a true timeline (best for shared branches). **Rebase** cleans up your _personal_ branch before pushing by replaying your commits onto the latest base.

```bash
git merge <branch>                              # bring <branch> into current
git rebase main                                 # replay your work atop main
git rebase --continue                           # after resolving conflicts
git rebase --abort                              # cancel and return
```

**Keyword breakdown**

- `<branch>` — Source branch to combine into current.

> [!NOTE]  
> Don’t rebase commits others already pulled—rebasing rewrites history.

---

## Resolve merge conflicts

When Git can’t auto-merge, fix the marked files, stage them, then continue.

```bash
git status                                      # see conflicted files
git diff                                        # inspect conflict hunks
# edit files to resolve <<<<<<< ======= >>>>>> markers
git add <file>                                  # mark resolved
git merge --continue                            # or: git rebase --continue
```

**Keyword breakdown**

- `<file>` — Conflicted file to resolve.

> :bulb: **Tip**  
> Use your editor’s 3-way merge UI. Commit early and often during big resolutions.

---

## Quick undo options (restore / reset / revert)

Pick the least-destructive option that fits the mistake.

```bash
git restore <file>                              # discard unstaged changes to a file
git restore --staged <file>                     # unstage but keep edits
git reset --soft HEAD~1                         # move back 1 commit; keep changes staged
git revert <sha>                                # new commit that undoes <sha> (safe on shared)
```

**Keyword breakdown**

- `<sha>` — Commit to reverse.

> [!NOTE]  
> Avoid `git reset --hard` unless you’re absolutely sure—it permanently discards work.

---

## Stash work-in-progress

Park changes temporarily to switch tasks; reapply later.

```bash
git stash push -m "<note>"                      # save WIP with a label
git stash list                                  # view stashes
git stash show -p <stash-ref>                   # preview contents
git stash apply <stash-ref>                     # reapply (keeps stash)
git stash drop <stash-ref>                      # delete when done
```

**Keyword breakdown**

- `<note>` — Short description (e.g., “wip: form layout”).
- `<stash-ref>` — Like `stash@{0}`.

> :bulb: **Tip**  
> Use `git stash push -k` to keep staged changes staged.

---

## Tags & releases

Tag important points (e.g., versions) and share them.

```bash
git tag -a <tag> -m "<message>"                 # annotated tag (preferred)
git tag                                         # list tags
git push origin <tag>                           # push one
git push origin --tags                          # or push all
```

**Keyword breakdown**

- `<tag>` — e.g., `v1.2.3`.

> [!NOTE]  
> Annotated tags store author, date, and message—best for releases.

---

## Safe force-push policy (--force-with-lease)

If you must overwrite remote history (e.g., after rebasing your local branch), use a lease to avoid clobbering teammates.

```bash
git push --force-with-lease                     # safer than --force
```

**Keyword breakdown**

- `--force-with-lease` — Aborts if the remote advanced since your last fetch.

> [!NOTE]  
> Coordinate on team chat; protected branches should block force pushes entirely.

---

## Recover work (reflog & rescue branches)

Find “lost” commits/branches via the reflog and save them immediately onto a safety branch.

```bash
git reflog                                      # timeline of HEAD/branch movements
git branch rescue/<name> <sha>                  # create a safety branch at that point
git switch rescue/<name>                        # check it out to continue work
```

**Keyword breakdown**

- `reflog` — Local pointer history; lifesaver after bad resets or branch deletes.

> :bulb: **Tip**  
> Create the rescue branch as soon as you find the commit so it won’t get garbage-collected.

---

## Cherry-pick targeted fixes

Apply a specific commit onto another branch (e.g., hotfix onto `main`).

```bash
git switch main
git fetch origin                                # ensure up to date
git cherry-pick <sha>                           # copy just that change
```

**Keyword breakdown**

- `cherry-pick` — Replays one commit’s changes as a new commit on the current branch.

> [!NOTE]  
> Resolve conflicts, then `git cherry-pick --continue`.

---

## GitHub — daily collaboration

### GitHub: create repo & connect

Use the web UI to create a repo, then link and push from local.

- **GitHub (web):** New → Repository → Name, description, visibility. Add a README unless you already committed one locally.
- Copy the repo URL (HTTPS or SSH), then:

```bash
# If you already have a local repo:
git remote add origin https://github.com/<owner>/<repo>.git  # HTTPS
git remote add origin git@github.com:<owner>/<repo>.git      # SSH
git push -u origin main                                      # first publish
```

**Keyword breakdown**

- `<owner>/<repo>` — GitHub namespace + repository.

> :bulb: **Tip**  
> Add a LICENSE to clarify usage; a README helps teammates get started fast.

---

### GitHub: forks and keeping fork updated

Fork when you don’t have write access; periodically sync your fork with the source (upstream) so your branches build on the latest.

- **GitHub (web):** Fork the repo to your account.
- Locally, add the source as `upstream` and bring its updates in:

```bash
git remote add upstream https://github.com/<source-owner>/<repo>.git   # or SSH form
git fetch upstream
git switch main && git merge upstream/main
git push origin main
```

**Keyword breakdown**

- `upstream` — Remote pointing to the source project (read-only for you).

> :bulb: **Tip**  
> On your feature branch, `git pull --rebase upstream/main` keeps your history tidy.

---

### Pull requests & basic code review

Open a PR to discuss changes, run CI, and get review before merging.

- **GitHub (web):** Compare & pull request (from your branch into `main` or the target branch).
- Write a clear title/body; link issues; mark as draft if not ready; request reviewers.
- Push new commits to the same branch—your PR updates automatically.

**Keyword breakdown**

- PR (pull request) — A proposal to merge one branch into another with discussion and checks.

> [!NOTE]  
> Keep PRs small and focused. Add screenshots/GIFs for UI changes.

---

### Reading CI/checks on PRs

The **Checks** tab shows build/test/security statuses. Click failing checks to open logs; fix locally and push to re-run CI.

**Keyword breakdown**

- Required checks — Must pass before merge (depends on repo settings).

> :bulb: **Tip**  
> Re-run flaky jobs from the checks UI instead of pushing empty commits.

---

### Auth choices (SSH vs HTTPS tokens)

Both are viable; pick what fits your workflow/policy.

- **SSH** (set once, then seamless):
  ```bash
  ssh-keygen -t ed25519 -C "<email>"           # create key pair
  # GitHub (web): Settings → SSH and GPG keys → New SSH key → paste ~/.ssh/id_ed25519.pub
  ssh -T git@github.com                         # test SSH access
  ```
- **HTTPS** (uses Personal Access Token):
  - GitHub (web): Settings → Developer settings → **Fine-grained token** → minimal scopes.
  - Git prompts for username (`<owner>`) and token on first push/clone.

**Keyword breakdown**

- `ed25519` — Modern SSH key type.
- `<email>` — Label for your key (doesn’t have to be your GitHub email).

> [!NOTE]  
> Store credentials securely: Windows **Credential Manager**, macOS **Keychain**, Linux **libsecret/gnome-keyring**.

---

### Daily safety rules & branch protection

Protect `main` and enforce review/CI to keep history healthy.

- **GitHub (web):** Settings → Branches → Add rule for `main`.
- Require PRs, 1+ reviewer, passing status checks; restrict who can push/force-push.
- Optionally require linear history if your project forbids merge commits.

**Keyword breakdown**

- Branch protection — Server-side rules that block risky pushes/merges.

> :bulb: **Tip**  
> Turn on “Include administrators” so rules apply to everyone.
