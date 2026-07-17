# RonakOS — Setup Guide
<!-- Complete deployment instructions for your GitHub Profile -->

```
┌─────────────────────────────────────────────────────────────────────────────┐
│   RonakOS v2.0 · Deployment Guide                                           │
│   Get your premium GitHub profile live in under 10 minutes                  │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## `$ prerequisites`

```
[ ]  GitHub account
[ ]  A repository named exactly: YOUR_USERNAME/YOUR_USERNAME
[ ]  Repository visibility: Public
[ ]  README.md in the root of that repository
```

---

## `$ step-01 — create-special-repo`

GitHub displays your profile README from a **special repository** that must be named exactly the same as your username.

```bash
# Your username: ronakpremjani
# Create a repo named: ronakpremjani/ronakpremjani
```

1. Go to [github.com/new](https://github.com/new)
2. Repository name: `ronakpremjani` (your exact username)
3. Check **Public**
4. Check **Add a README file**
5. Click **Create repository**

---

## `$ step-02 — upload-files`

Upload all files from this project into the root of your special repo.

**Folder structure:**
```
ronakpremjani/           ← your special repo root
├── README.md            ← the main profile file
├── assets/
│   ├── banner.svg
│   ├── footer.svg
│   ├── divider.svg
│   ├── terminal.svg
│   ├── project-chatvia.svg
│   └── project-portfolio.svg
├── customization.md
└── setup.md
```

**Via GitHub web interface:**
1. Open your new repo
2. Click **Add file → Upload files**
3. Drag the entire `assets/` folder + `README.md`
4. Commit directly to `main`

**Via Git CLI:**
```bash
git clone https://github.com/ronakpremjani/ronakpremjani.git
cd ronakpremjani
# Copy all files from this project into the cloned folder
git add .
git commit -m "feat: launch RonakOS profile v2.0"
git push origin main
```

---

## `$ step-03 — update-username`

Before deploying, search and replace `ronakpremjani` with your actual GitHub username across:

| File         | What to update                          |
|--------------|-----------------------------------------|
| `README.md`  | All stat URLs, visitor counter, shields |
| SVG files    | Not needed (no username references)     |

**Quick find & replace in VS Code:**
```
Ctrl+Shift+H → Find: ronakpremjani → Replace: YOUR_USERNAME
```

---

## `$ step-04 — contribution-snake`

The snake animation requires a GitHub Actions workflow that auto-generates the snake SVG.

**Create this file in your repo:**

```
.github/
└── workflows/
    └── snake.yml
```

**Contents of `snake.yml`:**

```yaml
name: Generate Snake Animation

on:
  schedule:
    - cron: "0 */12 * * *"    # Runs every 12 hours
  workflow_dispatch:            # Manual trigger
  push:
    branches:
      - main

jobs:
  generate:
    permissions:
      contents: write
    runs-on: ubuntu-latest
    timeout-minutes: 10

    steps:
      - name: Generate snake.svg
        uses: Platane/snk/svg-only@v3
        with:
          github_user_name: ${{ github.repository_owner }}
          outputs: |
            dist/github-contribution-grid-snake.svg
            dist/github-contribution-grid-snake-dark.svg?palette=github-dark

      - name: Push snake.svg to output branch
        uses: crazy-max/ghaction-github-pages@v3.1.0
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

**After pushing this file:**
1. Go to your repo → **Actions** tab
2. Click **Generate Snake Animation**
3. Click **Run workflow**
4. Wait ~30 seconds
5. Check the `output` branch for the generated SVGs

The README already points to the correct URL:
```
https://raw.githubusercontent.com/ronakpremjani/ronakpremjani/output/github-contribution-grid-snake-dark.svg
```

---

## `$ step-05 — update-links`

Update these placeholder values in `README.md`:

| Placeholder               | Replace with              |
|---------------------------|---------------------------|
| `ronak@example.com`       | Your real email           |
| `linkedin.com/in/ronakpremjani` | Your LinkedIn URL   |
| `x.com/ronakpremjani`     | Your X/Twitter handle     |
| `ronakpremjani.dev`       | Your portfolio URL        |
| `github.com/ronakpremjani/chatvia` | Your Chatvia repo  |

---

## `$ step-06 — verify`

After deploying, visit:
```
https://github.com/YOUR_USERNAME
```

Confirm:
```
[✓]  Banner animates on page load
[✓]  ASCII RONAK logo displays correctly
[✓]  Typing SVG rotates through all lines
[✓]  Visitor counter increments
[✓]  Project cards display side by side
[✓]  GitHub stats load (may take a few seconds)
[✓]  Footer animates on load
```

---

## `$ troubleshooting`

### Stats cards show "not found"
→ Your GitHub username in the stat URLs is incorrect. Double-check every URL.

### SVGs look broken on GitHub
→ GitHub sanitizes some SVG attributes. All SVGs in this project use only GitHub-safe attributes.

### Snake animation returns 404
→ The Actions workflow hasn't run yet, or the `output` branch doesn't exist. Run the workflow manually (Step 04).

### Typing SVG doesn't animate
→ GitHub caches images. Hard refresh: `Ctrl+Shift+R`. Also confirm the URL is correct.

### ASCII art looks misaligned
→ Ensure your browser is using a monospace font for README code blocks. This is standard GitHub behavior.

---

## `$ performance`

All SVGs in this project are:
- **Self-contained** — no external font loads
- **Animation-safe** — GitHub allows CSS animations in SVGs
- **Size-optimized** — all under 10KB each
- **GitHub-sanitized** — no JavaScript, no `<script>` tags, no `foreignObject`

---

_RonakOS v2.0 · Keep building._
