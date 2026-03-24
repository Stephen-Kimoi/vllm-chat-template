# vLLM Chat Template

A single-file HTML chat UI for any **OpenAI-compatible** inference endpoint (vLLM, Ollama, LM Studio, etc.).
No build step, no dependencies — open the file in a browser and start chatting.

## Quick start

```bash
git clone https://github.com/YOUR_USERNAME/vllm-chat-template
cd vllm-chat-template
open index.html   # or just double-click the file
```

## Configuration

Everything you need to change lives in one place at the top of the `<script>` block in `index.html`:

```js
const CONFIG = {
  // Required
  apiUrl: 'http://YOUR_SERVER:8000/v1/chat/completions',
  model:  'your-model-id',   // as returned by GET /v1/models

  // Optional UI labels
  badge:       'vLLM',
  headerTitle: 'Chat — Live Demo',
  statusText:  'Connected',
  footerInfo:  'vLLM · OpenAI-Compatible API',
  heroTitle:   'vLLM\nChat — Live',   // \n = line break in the big heading

  // Optional spec grid (right panel)
  specs: [
    { label: 'Endpoint', value: 'your-host:8000', accent: true },
    { label: 'Model',    value: 'Your Model' },
  ],

  // Optional hero meta tags (shown under the big heading)
  heroMeta: [
    'OpenAI-Compatible API',
    'vLLM Inference Engine',
  ],
};
```

Change `apiUrl` and `model`, save the file, refresh the browser — done.

## CORS

If your server and the HTML file are on different origins, enable CORS on your server.
For vLLM:

```bash
vllm serve YOUR_MODEL --allowed-origins '["*"]'
```

## Deploying

Because it's a single file, you can host it anywhere:

- **GitHub Pages** — push to a repo, enable Pages, it's live instantly.
- **Any static host** — Netlify, Vercel, S3, Cloudflare Pages, etc.
- **Local** — just open `index.html` directly.

## What it shows

| Left panel | Right panel |
|---|---|
| Chat interface with message history | Infrastructure spec grid |
| Typing indicator | Raw request JSON sent to your endpoint |
| Light / dark mode toggle | Raw response JSON from your endpoint |

## Converting to another stack

The whole UI is plain HTML + vanilla JS. To port it:
- **React / Vue / Svelte** — the `CONFIG` block maps 1-to-1 to props/state; the `sendMessage` function is your API call.
- **Python (Gradio / Streamlit)** — use the same `fetch` logic as a reference for your `requests.post` call.
- **Mobile** — the layout is a simple two-column CSS Grid that collapses to one column on small screens.
