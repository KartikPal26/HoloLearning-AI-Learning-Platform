Deployment steps — Frontend on Netlify, Backend on Render

Prerequisites
- GitHub account and git installed
- Netlify account (for frontend)
- Render (or Railway/Heroku) account (for backend)
- Make sure sensitive keys are NOT in `.env` when pushing

1) Push repository to GitHub
```bash
git add .
git commit -m "Prepare app for deployment"
git push origin main
```

2) Backend (Render)
- In Render: New → Web Service → connect your GitHub repo.
- Environment: Python
- Build command: `pip install -r requirements.txt`
- Start command: `gunicorn -w 4 -b 0.0.0.0:$PORT main:app` (or use `Procfile`)
- Add environment variables in Render dashboard: `CEREBRAS_API_KEY`, any Stability/OpenAI keys, etc.
- Deploy — Render provides a public URL (e.g. `https://your-app.onrender.com`)

3) Frontend (Netlify)
Option A — Connect repo via Netlify UI:
- New site from Git → choose repo
- Build command: `npm run build`
- Publish directory: `build`
- Environment variables → add `REACT_APP_API_URL` = `https://your-app.onrender.com`
- Deploy

Option B — Netlify CLI (local deploy):
```bash
npm install -g netlify-cli
npm run build
netlify login
netlify deploy --dir=build --prod
```
(Use `netlify init` to link to a site)

4) Verify
- Open your Netlify URL and test the assistant; network requests should go to `${REACT_APP_API_URL}/generate` and images should load from `/pipeline_outputs/generated_images/`.

Notes
- CORS: `main.py` already calls `CORS(app)`, so cross-origin requests should work.
- If image generation is long-running, consider turning `/generate` into an async job with polling or websockets.
