---
name: sync-upstream
description: Sync this fork with the upstream openclaw/openclaw repo. Fetches upstream, fast-forwards main, rebases my-customizations onto main, and force-pushes both branches.
disable-model-invocation: true
allowed-tools: Bash(git *)
---

Sync this fork with upstream following the workflow in AGENTS.md. Run these steps in order:

1. **Record the current branch** so you can return to it at the end.

2. **Fetch upstream:**

   ```
   git fetch upstream
   ```

3. **Update main to match upstream:**

   ```
   git checkout main
   ```

   Try `git merge upstream/main --ff-only` first. If that fails because main has diverged (e.g. local commits), use `git rebase upstream/main` instead.

   ```
   git push origin main --force-with-lease
   ```

4. **Rebase customizations onto updated main:**

   ```
   git checkout my-customizations
   git rebase main
   git push origin my-customizations --force-with-lease
   ```

5. **Return to the original branch** you recorded in step 1.

6. **Report** what happened: how many new upstream commits were pulled in, whether any conflicts occurred, and the final state of both branches.

If a rebase has conflicts you cannot resolve, abort with `git rebase --abort` and report the conflict to the user.
