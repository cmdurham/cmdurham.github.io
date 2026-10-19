# cmdurham.com

Personal site for Chris Durham — currently a portal to browser games, with room to
grow into other creative projects.

## Structure

| Path | What it is |
|---|---|
| `index.html` | Landing page |
| `arcade/index.html` | The Arcade — the games portal |
| `styles.css` | All site styling (shared by landing + arcade) |
| `CNAME` | Tells GitHub Pages to serve this site at cmdurham.com |
| `exodus/index.html` | EXODUS: The Long Drift — copied from `~/Dev/2077-theme/exodus.html` |
| `fretkeys/` | Fretkeys download page, the Mac `.dmg` and the Windows installer |

Bass Technique lives in its own repo (`cmdurham/bass-technique`) and is served at
`/bass-technique/`; it's linked from the nav and the landing page.

Fretkeys (`fretkeys/`) is a download page for the Mac and Windows builds of the app, which
lives in the private `cmdurham/fretkeys` repo. The `.dmg` and the Windows `…-setup.exe` are
committed alongside the page.

**Updating Fretkeys:** both installers come from GitHub Actions in the fretkeys repo. After
bumping the version there, `git push origin main:release` builds them; when the run finishes,
`git fetch origin builds` in `~/Dev/fretkeys` and take `Fretkeys_<version>_aarch64.dmg` and
`Fretkeys_<version>_x64-setup.exe` from that branch (`git show origin/builds:STATUS` says whether
every build succeeded). Copy both into `fretkeys/`, delete the old ones, and update the version,
build date, sizes, download links and both SHA-256 lines (`shasum -a 256 <file>`) in
`fretkeys/index.html`.

Extinction Fighters lives in its own repo (`cmdurham/extinction-fighters`); GitHub Pages
serves it at `/extinction-fighters/` under this domain, so it's linked rather than bundled.

**Updating EXODUS:** after rebuilding the game (`./build.sh` in `~/Dev/2077-theme`),
re-copy it into the site:

```bash
cp ~/Dev/2077-theme/exodus.html ~/Dev/cmdurham.com/exodus/index.html
```

## Hosting on GitHub Pages

1. Create a **public** repo on GitHub named `cmdurham.github.io` (user site repo —
   this makes the site the root of your GitHub Pages).
2. From this folder:

   ```bash
   git init
   git add -A
   git commit -m "Initial site"
   git remote add origin git@github.com:cmdurham/cmdurham.github.io.git
   git push -u origin main
   ```

3. On GitHub: repo **Settings → Pages** — confirm it's deploying from the `main`
   branch (user site repos deploy automatically). The site will appear at
   `https://cmdurham.github.io` within a minute or two.

## Pointing cmdurham.com at it

At your DNS provider (wherever you registered cmdurham.com), add:

- **Four A records** on the apex (`@` / `cmdurham.com`) pointing to GitHub Pages:
  - `185.199.108.153`
  - `185.199.109.153`
  - `185.199.110.153`
  - `185.199.111.153`
- **One CNAME record** for `www` pointing to `cmdurham.github.io`

Then on GitHub: **Settings → Pages → Custom domain**, enter `cmdurham.com`, and once
DNS check passes, tick **Enforce HTTPS**. DNS can take from minutes to a few hours
to propagate. The `CNAME` file in this repo keeps the custom domain setting from
being lost on future pushes.
