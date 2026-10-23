# Vercel deployment

Import `Big-jpg/yt-dlp-wasm` in Vercel with the **repository root** as Root Directory. The root `vercel.json` builds the local Python wheel before Vite and publishes `apps/demo/dist`. Use Node.js 25 if available in Vercel; otherwise use the supported Node.js version for build (the browser runtime requires JSPI in the user's browser, not Node on the static host).

Configure `VITE_DEMO_PROXY_URL` with **your own** CORS proxy URL. The UI also supports a custom proxy under Proxy settings. Do not use the upstream project's demo proxy for a public deployment: it is rate-limited and intended for its own demo.

Deploy the proxy independently from `packages/cors-proxy` following its README. Restrict `ALLOWED_ORIGINS` to your production Vercel hostname, plus explicit preview origins as needed, and use an access key. An embedded frontend key is visible to visitors; it is not a secret. For a public site use a controlled proxy with effective rate limits. YouTube can reject cloud/datacenter IPs even when CORS is handled.

The client does not upload files for conversion. yt-dlp, Pyodide, and ffmpeg.wasm run in the browser; network traffic passes through the configured proxy. Chrome 137+, Firefox 153+, or Safari 27+ is required for JSPI.

For the MVP, paste a single video URL and select Audio > MP3. Search is intentionally deferred until download reliability has been confirmed.
