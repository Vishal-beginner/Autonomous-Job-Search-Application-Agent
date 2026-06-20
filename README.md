# Autonomous Job Search & Application Agent

An AI-powered, browser-based agent that finds LinkedIn Easy Apply jobs, scores them against your profile, and generates tailored cover letters and application answers — so you spend ~30 seconds per application instead of 15 minutes. Supports **Claude**, **ChatGPT**, **Gemini**, and **Qwen**.

The app deliberately does **not** automate LinkedIn login or form submission (account-safety, legal, and credential-security reasons). It does the high-effort work (research, scoring, writing) and leaves the actual click-and-paste to you.

## Repo contents

This repo ships the app as two zip archives, each containing a snapshot of the same React + Vite project (`job-agent/`):

| Archive | Version | Status |
|---|---|---|
| `easy-apply-agent.zip` | `2.0.0` | **Latest — use this one.** Adds AI job search/discovery, batch scoring, and a paginated Speed Apply queue. |
| `DOC-20260510-WA0026.zip` | `1.0.0` | Earlier snapshot, kept for reference. Simpler single-job Apply flow, no job search/scoring. |

## Prerequisites

- [Node.js](https://nodejs.org/) 18+ and npm
- An API key from at least one supported provider:
  - **Claude** (recommended — only provider with built-in web search, which powers job discovery): [console.anthropic.com](https://console.anthropic.com/settings/keys)
  - OpenAI: [platform.openai.com](https://platform.openai.com/api-keys)
  - Gemini: [aistudio.google.com](https://aistudio.google.com/apikey)
  - Qwen: [dashscope.console.aliyun.com](https://dashscope.console.aliyun.com)

## Setup

1. Unzip the latest version:

   ```bash
   unzip easy-apply-agent.zip
   cd job-agent
   ```

2. Install dependencies:

   ```bash
   npm install
   ```

3. Start the dev server:

   ```bash
   npm run dev
   ```

   The app opens automatically at [http://localhost:3000](http://localhost:3000).

4. In the app's **Settings** tab, pick your AI provider and paste in your API key. Keys are stored in the browser's `localStorage`, not in any file — `.env.example` inside the archive is just a reference for which keys are supported.

### Using the app

1. **Profile** — enter your details, links, resume, and target roles.
2. **Settings** — choose a provider and enter your API key.
3. **Find Jobs** — search for matching LinkedIn Easy Apply postings, score them against your profile, select the ones you want, and batch-generate tailored materials.
4. **Speed Apply** — step through each prepared job, copy the generated text, open Easy Apply on LinkedIn, paste, and mark it applied.
5. **Tracker** — view stats and export your application history as CSV.

### Production build

```bash
npm run build     # output in dist/
npm run preview   # preview the production build locally
```

## Using the older version instead

```bash
unzip DOC-20260510-WA0026.zip
cd job-agent
npm install
npm run dev
```

Setup steps are identical; this version lacks the AI job search, scoring, and Speed Apply queue found in `easy-apply-agent.zip`.

## Tech stack

- React 18 + Vite 5
- Direct browser calls to the Claude / OpenAI / Gemini / Qwen APIs via a unified client in `src/utils/api.js`
- No backend — all state (profile, settings, application history) persists in `localStorage`

For production deployments, proxy API calls through a backend instead of calling provider APIs directly from the browser, to avoid exposing API keys client-side.

## License

MIT
