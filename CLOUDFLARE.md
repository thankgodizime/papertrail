# Papertrail's free AI server

Papertrail's AI endpoint is hosted as a Cloudflare Worker:

- App: <https://thankgodizime.github.io/papertrail/>
- AI chat endpoint: <https://papertrail-ai.mrtiago807.workers.dev/api/chat>
- Automatic document review: <https://papertrail-ai.mrtiago807.workers.dev/api/analyze>
- Worker source: `worker/index.js`

The Worker is connected to Cloudflare Workers AI using the `AI` binding and the `@cf/meta/llama-3.2-3b-instruct` model. No OpenAI key or other model secret is stored in the public app or repository. OCR and text extraction run in the browser. After a readable file is uploaded, the app sends extracted text to Cloudflare for a summary and suggested next steps; chat sends extracted text with the user's question. The original uploaded file remains in browser storage on the user's device. Suggested tasks are stored in local browser storage.

## Updating the server

The server currently uses Cloudflare's dashboard code editor. After changing `worker/index.js`, open the `papertrail-ai` Worker in Cloudflare, choose **Edit code**, paste the updated source, and choose **Deploy**. To deploy from a local checkout instead, use the included `wrangler.jsonc` after signing Wrangler in to the same Cloudflare account.

## Free usage

Cloudflare's current Free plan includes up to 100,000 Worker requests per day. Workers AI includes 10,000 Neurons per day at no charge. When the free daily AI allocation runs out, Papertrail reports that AI is temporarily unavailable until it resets. Cloudflare may change these limits; check its [Workers pricing](https://developers.cloudflare.com/workers/platform/pricing/) and [Workers AI pricing](https://developers.cloudflare.com/workers-ai/platform/pricing/) before a public launch.
