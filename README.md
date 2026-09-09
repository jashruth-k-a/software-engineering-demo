cat << 'EOF' > README.md

\# Git Lab: Simulating and Resolving a Detached HEAD State



\## 1. Objective

Demonstrate an understanding of Git internal pointers (`HEAD`, branch references) by:

\- Simulating a detached `HEAD` state via historical checkout.

\- Creating commits detached from any branch reference.

\- Recovering the detached commits using `git reflog` and restoring them to a dedicated branch.



\---



\## 2. Theoretical Overview

\- \*\*Normal State:\*\* `HEAD` points to a branch reference (e.g., `HEAD -> master`), which in turn points to the latest commit.

\- \*\*Detached HEAD State:\*\* `HEAD` points directly to a commit hash rather than a named branch. Any new commits created in this state lack branch references.

\- \*\*The "Lost" Commit Risk:\*\* Switching away leaves those commits orphaned and invisible to standard logs, risking garbage collection.

\- \*\*Recovery Mechanism:\*\* `git reflog` tracks every update made to `HEAD`. By finding the SHA-1 hash of the orphaned commit, a new branch reference can reconnect it.



\---



\## 3. Step-by-Step Reproduction



\### Step 1: Base Repository Setup

```bash

git init

echo "Base line 1" > app.txt \&\& git add . \&\& git commit -m "Commit 1: base setup"

echo "Base line 2" >> app.txt \&\& git add . \&\& git commit -m "Commit 2: added feature"

echo "Base line 3" >> app.txt \&\& git add . \&\& git commit -m "Commit 3: finalized base"

