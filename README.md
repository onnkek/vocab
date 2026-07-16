# VocabFlow Frontend

Standalone Webpack/React frontend. The backend URL is a build-time setting.

## Commands

```bash
npm install
npm run dev
npm run build:nas
npm run build:pages
npm run deploy
npm run typecheck
```

### Local development

Run the backend on `http://localhost:3001`, then:

```bash
npm run dev
```

Webpack serves the frontend on `http://localhost:3000` and proxies `/api`, `/uploads`, `/image-cache`, and `/audio-cache` to the local backend.

To use another local backend:

```bash
VOCABFLOW_DEV_API_URL=http://192.168.1.20:3001 npm run dev
```

### NAS production build

Legacy same-origin mode (frontend still requests `/api/...`):

```bash
npm run build:nas
```

NAS static frontend talking to an external backend:

```bash
VOCABFLOW_API_URL=https://YOUR-PUBLIC-BACKEND.example.com npm run build:nas
```

A standalone nginx Docker image is included. Build argument `VOCABFLOW_API_URL` controls the API origin.

### GitHub Pages

The Pages build uses `HashRouter`, so deep routes work without server rewrites. The repository name is inferred from the git remote and used as webpack `publicPath`.

```bash
VOCABFLOW_API_URL=https://YOUR-PUBLIC-BACKEND.example.com npm run deploy
```

The deploy script builds the Pages target and publishes `build/` to the `gh-pages` branch.

On Windows PowerShell:

```powershell
$env:VOCABFLOW_API_URL="https://YOUR-PUBLIC-BACKEND.example.com"
npm run deploy
```

Then open GitHub repository **Settings → Pages → Build and deployment**, choose **Deploy from a branch**, branch `gh-pages`, folder `/ (root)`.

For a custom Pages base path, set `VOCABFLOW_PAGES_BASE_PATH`. Normally this is not needed.
