# 🚀 Setup — Rudra's animated GitHub profile

Total time: ~5 minutes.

## 1. Create the magic repo

GitHub shows a README on your profile only if the repo name **exactly matches your username**.

- Go to https://github.com/new
- Repository name: **your GitHub username** (e.g. if the username is `rudra-patel`, the repo must be `rudra-patel`)
- Set it to **Public**, don't add anything else, create it.

## 2. Replace the username placeholder

Every dynamic widget (stats, streak, trophies, snake, view counter) needs the real username. Open a terminal in this folder and run:

```bash
# macOS / Linux  (replace ACTUAL_USERNAME with the real one)
sed -i '' 's/RUDRA_GITHUB_USERNAME/ACTUAL_USERNAME/g' README.md   # macOS
sed -i 's/RUDRA_GITHUB_USERNAME/ACTUAL_USERNAME/g' README.md      # Linux
```

Or just open `README.md` in any editor and Find & Replace `RUDRA_GITHUB_USERNAME` → the real username.

## 3. Push everything

```bash
git init
git add .
git commit -m "feat: animated profile"
git branch -M main
git remote add origin https://github.com/ACTUAL_USERNAME/ACTUAL_USERNAME.git
git push -u origin main
```

(Or simply drag-and-drop all files — **including the `assets` folder and the hidden `.github` folder** — via GitHub's web "Add file → Upload files".)

## 4. Wake up the snake 🐍

1. Repo → **Settings → Actions → General → Workflow permissions** → select **Read and write permissions** → Save.
2. Repo → **Actions** tab → "Generate contribution snake" → **Run workflow**.
3. Wait ~1 minute. It creates an `output` branch with the snake SVGs, and the README picks them up automatically.

## 5. Final touches

- [ ] **TryHackMe**: the badge assumes the username `CyberPayl0ad` — if it's different, replace it in README.md (2 places).
- [ ] **CodeAlpha repos**: search README.md for `ADD REPO LINK` and link the actual task repos.
- [ ] **Email**: uncomment the email badge in the "Reach me" section and add the real address.
- [ ] **Pin repos**: on the profile page, pin the best repos (DhanRakshak, TAAR, CodeAlpha tasks).
- [ ] **Skill icons**: edit the `skillicons.dev` URL if you want to add/remove languages.

## If a stats widget goes blank

Every dynamic widget is hosted by a free third-party service, so any of them can go
down without warning. Current state (checked 2026-08-10) and what to do:

| Widget | Host in use | Note |
|--------|-------------|------|
| Stats + Top languages | `github-profile-summary-cards.vercel.app` | ✅ working. The original `github-readme-stats.vercel.app` is **paused by its maintainer** (503) — if it comes back, you can switch to it for a closer palette match, since it accepts custom hex colors and this one only accepts a `theme=` name. |
| Streak | `streak-stats.demolab.com` | ✅ working, custom colors. |
| Trophies | `profile-trophy.vercel.app` | ✅ working **mirror**. The official `github-profile-trophy.vercel.app` is disabled (402 Payment required). If the mirror dies too, `github-trophies.vercel.app` is a second mirror with the same URL parameters. |
| TryHackMe badge | `img.shields.io` (static) | The live THM badge **cannot work anymore**: the S3 bucket returns 403 and TryHackMe now sits behind bot protection that blocks GitHub's image proxy. The rank/room count in those badges is hardcoded — **edit the numbers by hand** as they change. |
| Snake | your own `output` branch | ✅ self-hosted by the workflow, no third party. |

To diagnose a blank image, just `curl -I` the URL — anything other than `HTTP 200`
with an `image/svg+xml` content type means the host is down, not your README.

## How the animations work (no JavaScript!)

GitHub READMEs strip all JS — so everything here is **hand-coded animated SVG** (SMIL animations), which GitHub renders natively:

| File | What it does |
|------|--------------|
| `assets/header.svg` | Matrix rain, RGB-split glitch on the name, scanline sweep, scrolling tool ticker, pulsing HUD brackets |
| `assets/terminal.svg` | Types `whoami`, then runs a fake `nmap` scan of Rudra's own skills — every port "open" 😎 — character-by-character typing, staggered output, blinking cursor |
| `assets/divider.svg` | Packet "comets" (green →, red ←) racing along a circuit line |
| `assets/footer.svg` | `exit` → connection closed, with drifting signal waves |

Want to change any text/colors? They're plain SVG files — open in any editor.
