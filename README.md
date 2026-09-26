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
