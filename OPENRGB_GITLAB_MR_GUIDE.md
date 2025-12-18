# OpenRGB GitLab Merge Request Guide (first contribution)

This is a practical, low-stress checklist to submit the Legion Gen10 patch to OpenRGB without “looking like an idiot”.  Maintainability and clarity matter more than perfection.

## 1) Before you start

- Read `CONTRIBUTING.md` in the OpenRGB repo (it’s short and tells you exactly what they expect).
- Goal: one focused MR that only touches Lenovo controller code for Gen10 support.

## 2) Fork OpenRGB on GitLab

1. Log into GitLab.
2. Open the upstream OpenRGB project: `https://gitlab.com/CalcProgrammer1/OpenRGB`
3. Click **Fork** and fork it to your own account.

## 3) Clone your fork locally

Replace `YOURNAME` with your GitLab username:

```bash
git clone https://gitlab.com/YOURNAME/OpenRGB.git
cd OpenRGB
```

Add the upstream remote (this is important):

```bash
git remote add upstream https://gitlab.com/CalcProgrammer1/OpenRGB.git
git remote -v
```

## 4) Create a feature branch (do NOT use `master`)

```bash
git checkout -b lenovo-legion-gen10
```

## 5) Apply the patch (from this workspace)

From the repo that contains `openrgb-legion-gen10.patch`, run either:

### Option A (recommended): apply patch file

```bash
cd /path/to/your/OpenRGB/clone
git apply /home/Idiom/Repos/MyRepos/OpenRGBPatch/openrgb-legion-gen10.patch
```

Then verify what changed:

```bash
git status
git diff --stat
```

### Option B: manually copy the 5 changed files

If patch application fails, copy the corresponding files from `patched/OpenRGB/...` into your clone (same paths), then verify with `git diff`.

## 6) Build and do a quick sanity test

Use your normal OpenRGB build steps. On Linux this is typically:

```bash
qmake OpenRGB.pro
make -j"$(nproc)"
```

Then run:

```bash
./openrgb --list-devices
```

If you can, confirm the device appears and the UI/Direct mode behaves as expected.

## 7) Commit your changes with a clear message

Check the diff one more time:

```bash
git diff
```

Commit:

```bash
git add Controllers/LenovoControllers
git commit -m "Lenovo: Add Legion 7 Gen 10 (C197) support"
```

Tips:
- Keep it one commit if possible (GitLab can squash, but a clean commit helps).
- Don’t “cleanup” unrelated formatting; maintainers hate drive-by reformatting.

## 8) Push your branch to your fork

```bash
git push -u origin lenovo-legion-gen10
```

## 9) Create the Merge Request on GitLab

1. Go to your fork on GitLab.
2. GitLab should show a banner to create an MR from your pushed branch — click it.
3. Target branch: `master` (upstream).
4. Title suggestion:
   - `Lenovo: Add Legion 7 Gen 10 (C197) support`

Paste the contents of `OPENRGB_MR_DESCRIPTION.md` into the MR description and tweak any details you want.

## 10) What to say (and what not to say)

**Good MR description includes:**
- Your exact laptop model + VID/PID
- What was broken (Gen10 protocol differences)
- What you changed (direct mode `D0` + `A1`, payload length, zones)
- What you tested (GUI modes, brightness, persistence, per-key, streaming)

**Avoid:**
- Over-explaining or apologizing
- Huge walls of logs
- Unrelated refactors

If maintainers ask for changes, it’s normal. Reply briefly, push updates to the same branch, and GitLab will update the MR automatically.

## 11) Updating your branch later (use rebase, not merge)

OpenRGB prefers linear history. When upstream changes while you’re working:

```bash
git fetch upstream
git rebase upstream/master
git push --force-with-lease
```

(`--force-with-lease` is the safe way to update your branch after a rebase.)

