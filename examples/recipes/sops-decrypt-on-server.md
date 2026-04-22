# SOPS decrypt fails silently on the server after deploy

**Problem:** `sops -d secrets.enc.yaml` works locally but returns an empty file on the production VPS, with no error. Services start with blank env vars and fail downstream in confusing ways (connection refused, "DB_URL is undefined").

**Context:** Ubuntu 22.04 VPS, SOPS 3.8, age key at `/home/deploy/.config/sops/age/keys.txt`. Deploy runs over SSH as `deploy`. Works fine when run interactively; fails on the non-interactive SSH path the deploy script uses.

**Solution:**

Set `SOPS_AGE_KEY_FILE` explicitly in the deploy script, before any SOPS call:

```bash
export SOPS_AGE_KEY_FILE=/home/deploy/.config/sops/age/keys.txt
sops -d secrets.enc.yaml > .env
```

Non-interactive SSH doesn't load `~/.profile` or `~/.bashrc`, so the env var that's set there for interactive use isn't present. SOPS then can't find the key, and — this is the trap — it doesn't fail loudly. It just produces an empty file.

**Why it works:** SOPS looks at `SOPS_AGE_KEY_FILE` first, then falls back to `~/.config/sops/age/keys.txt`. The fallback path is resolved against `$HOME`, which *is* set in non-interactive SSH, so you'd expect this to work. But on this machine the deploy user's actual key lives at a path SOPS's default search doesn't check. Explicit env var removes the ambiguity.

**Gotchas:**

- The silent failure is the worst part. Add `test -s .env || { echo "SOPS produced empty file"; exit 1; }` right after decryption to fail loud.
- If you rotate the age key, update this path everywhere — the deploy script, any systemd unit, and the recipe.
- Local SOPS via `brew` sometimes uses a different default path than the Linux binary. Don't assume "works locally" means the path is right.
