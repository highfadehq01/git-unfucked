# Git Unfucked

[![MIT License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![GitHub Stars](https://img.shields.io/github/stars/highfadehq01/git-unfucked?style=social)](https://github.com/highfadehq01/git-unfucked/stargazers)

**10 real-world Git rescue scenarios.** Each one: what happened, what to do, and why it works.

No fluff. No theory. Just the commands you need when Git has you cornered.

## ⚡ Get the full version — 32 scenarios, $2

This repo is a free sampler. The full **Git Unfucked** reference covers all 32 rescue scenarios including rebase disasters, cherry-pick gone wrong, squash/split commits, bisect workflows, and remote tracking fixes.

**[Get Git Unfucked on Gumroad →](https://sadafade.gumroad.com/l/wqlrx)**

---

## Free guides on our blog

- [5 Git Mistakes Every Developer Makes (And How to Fix Them)](https://highfadefree.vercel.app/blog/git-mistakes)
- [The Git Recovery Cheatsheet](https://highfadefree.vercel.app/blog/git-recovery-cheatsheet)
- [How to Undo a Git Commit (The Right Way)](https://highfadefree.vercel.app/blog/undo-git-commit)
- [How to Recover a Deleted Git Branch](https://highfadefree.vercel.app/blog/recover-deleted-git-branch)
- [How to Fix git stash pop Conflicts](https://highfadefree.vercel.app/blog/fix-git-stash-pop-conflicts)

---

## 1. I committed to main instead of my branch

```bash
# Create the branch you meant to use (keeps your commits)
git branch my-feature

# Reset main back to origin
git reset --hard origin/main

# Switch to your branch
git checkout my-feature
```

**Why:** `git branch` creates a new branch pointing at your current commit. `reset --hard` moves main back. Your work is safe on the new branch.

---

## 2. I need to undo the last commit but keep changes

```bash
git reset --soft HEAD~1
```

**Why:** `--soft` moves the HEAD pointer back but leaves your changes staged. You can re-commit with a better message or continue editing.

---

## 3. I committed the wrong file

```bash
git reset --soft HEAD~1
git reset HEAD path/to/wrong-file
git commit -c ORIG_HEAD
```

**Why:** Soft reset undoes the commit, then you unstage the wrong file, then re-commit with the original message.

---

## 4. I need to change the last commit message

```bash
git commit --amend -m "New message here"
```

**Warning:** Only do this if you haven't pushed. If you have, use `git revert` instead.

---

## 5. I need to undo a commit that's already been pushed

```bash
git revert <commit-hash>
git push
```

**Why:** `revert` creates a new commit that undoes the changes. History is preserved. Safe for shared branches.

---

## 6. I'm in a merge conflict and want to abort

```bash
git merge --abort
```

**Why:** Takes you back to the state before you started the merge. No harm done.

---

## 7. I need to stash changes including untracked files

```bash
git stash -u
```

**Why:** Default `git stash` ignores untracked files. `-u` includes them.

---

## 8. I deleted a branch I still needed

```bash
# Find the branch tip in reflog
git reflog

# Recreate the branch at that commit
git branch recovered-branch <commit-hash>
```

**Why:** Git keeps commits in reflog for ~30 days even after branch deletion.

---

## 9. I need to remove a file from Git without deleting it

```bash
git rm --cached path/to/file
echo "path/to/file" >> .gitignore
git commit -m "Remove tracked file, add to gitignore"
```

---

## 10. I accidentally added a huge file and can't push

```bash
# If it's in the last commit
git reset --soft HEAD~1
git reset HEAD large-file.bin
echo "large-file.bin" >> .gitignore
git add .gitignore
git commit -c ORIG_HEAD
```

**If it's in older history, use BFG or git-filter-repo.**

---

## Quick Reference: The Reset Spectrum

| Command | HEAD | Index | Working Dir | Use when |
|---------|------|-------|-------------|----------|
| `reset --soft` | Moves | Unchanged | Unchanged | Re-commit differently |
| `reset` (mixed) | Moves | Reset | Unchanged | Unstage and re-organize |
| `reset --hard` | Moves | Reset | Reset | Nuclear option |

---

## Want all 32 scenarios?

This is 10 of 32 scenarios from **Git Unfucked** — the complete interactive Git recovery reference.

The full version includes:
- **32 real-world scenarios** (cherry-pick, rebase undo, bisect, squash, split commits, and more)
- **Interactive HTML reference** — searchable, works offline
- **Quick-reference cheat sheet**

**[$2 on Gumroad →](https://sadafade.gumroad.com/l/wqlrx)**

---

Built by **[High Fade Free](https://highfadefree.vercel.app)** — minimal, precision developer tools.

*Ship clean. Stay sharp.*
