# Deploying the playable game website (web mode) on GitHub Pages

This is the browser-playable Open Historia build. It is a static app: saves stay in
the browser, AI keys go directly to the player's provider, and map bytes are fetched
from content nodes.

**Chosen setup:** deploy the app on **GitHub Pages**.

Prerequisites: Node 18+ and a GitHub repository with Pages enabled.

---

## 1. Build the web app for your repository path

GitHub Pages serves project sites under `/<repo>/`, so set Vite's base path to your
repository name.

```bash
# macOS/Linux
node scripts/seed-web-defaults.mjs
npx vite build --mode web --base "/<repo>/" --outDir dist-web --emptyOutDir

# Windows PowerShell
node scripts/seed-web-defaults.mjs
npx vite build --mode web --base "/<repo>/" --outDir dist-web --emptyOutDir
```

Replace `<repo>` with your repository name (for example, `open-historia-testing`).

## 2. Publish `dist-web/` to GitHub Pages

Use your repository's Pages workflow to deploy `dist-web/` (or copy it into the
workflow artifact directory if your workflow expects a different folder). In this repo,
`.github/workflows/deploy-site.yml` handles deployment through GitHub Pages actions.

## 3. Run at least one content node (optional, for map availability)

If no node serves map content, the map can be empty. Run a node from
**open-historia-node** and add it to your signed directory when you want map delivery
from the node network.

## 4. Play

Open your GitHub Pages URL. Players can pick their AI provider and paste their own
key in Settings. Games remain client-side.

---

## Notes

- The default `public/node-directory.json` can be empty; the app still boots.
- Updating the game is just rebuilding and redeploying.
- Local single-player desktop usage is unchanged by web deployment choices.
