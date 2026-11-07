# CryptoLens AI — Netlify-ready build

This package combines the CryptoLens AI research terminal with the Aegis Lab demo module.

## Publish on Netlify

**Use Git-based deploy or Netlify CLI.** A simple static drag-and-drop upload may omit the serverless function needed for secure Gemini access.

### Option A — Git-based deploy
1. Put the contents of this folder in a GitHub repository.
2. In Netlify, choose **Add new site → Import an existing project** and connect that repository.
3. Keep the build command empty and the publish directory as `.`. `netlify.toml` already points Netlify to `netlify/functions`.
4. In **Site configuration → Environment variables**, add `GEMINI_API_KEY` with your newly generated Gemini key. Do not paste it into chat, HTML, source control, or the ZIP.
5. Trigger a new deploy after adding the variable.

### Option B — Netlify CLI
1. Install Node.js and the Netlify CLI (`npm install -g netlify-cli`).
2. From this folder, run `netlify login` and `netlify link` to link your own site.
3. Add `GEMINI_API_KEY` to that site's environment variables in the Netlify dashboard.
4. Run `netlify deploy --prod` from this folder.

### Verify Gemini
Open `https://YOUR-SITE/.netlify/functions/gemini`. It should return `ok: true` and `configured: true`; it never reveals the key. In CryptoLens, open **Data → AI settings**, leave the Gemini key field blank to use the secure hosted proxy, press **Test Gemini key**, then **Save & reload**.

## What is and is not live
- Gemini requests on a Netlify deployment are proxied through `/.netlify/functions/gemini`; the server key is not delivered to the browser. A small per-instance request throttle is included, but it is not a complete abuse-prevention or billing-quota system. Configure provider quotas and monitor usage in Google AI Studio.
- CryptoLens market-data providers are called from the browser and may have rate limits, outages, delayed data, or CORS restrictions. Check provider status and timestamps in the app; no source can guarantee 100% accuracy.
- The Aegis Lab remains an explicitly labelled simulation/demo. Its sample prices, scores, order book, hash feed, and portfolio are illustrative; it does not execute swaps or monitor alerts in the background.
- This is an educational research and security-screening tool, not financial advice or a guarantee that a token is safe. Verify important facts independently.

## Local preview
Open `index.html` for a frontend preview. The secure Gemini proxy will not work from a `file://` URL; use `netlify dev` or deploy to Netlify to test it.
