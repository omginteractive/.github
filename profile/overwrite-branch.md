# Overwriting a branch with another (e.g. making `dev` match `main`)

Use this when you want one branch to become an exact mirror of another — same files **and** same commit history. The example below resets `dev` to match `main`, but swap in whatever branches you need.

## Steps

```bash
# 1. Switch to the branch you want to reset
git checkout dev

# 2. Make sure you have the latest from remote
git fetch origin

# 3. Hard reset the branch to your target
git reset --hard origin/main

# 4. Force-push the result back up to remote
git push --force-with-lease
```

After this, `dev` is a mirror of `main` — the entire commit history matches.

## A note on the force push

Use `--force-with-lease`, not plain `--force`.

- `--force-with-lease` refuses to overwrite the remote if someone else has pushed to `dev` since your last fetch. It protects you from clobbering a teammate's work.
- `--force` overwrites unconditionally, no questions asked.

Same end result when you're the only one touching the branch, but `--force-with-lease` is the safer default.

## Heads up

`reset --hard` discards any uncommitted local changes on the branch you're sitting on, and the force-push **permanently** replaces the remote branch's history. Make sure nothing on `dev` is worth keeping before you run this.
