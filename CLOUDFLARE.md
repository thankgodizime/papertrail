# Papertrail's free AI server

Papertrail's AI endpoint is hosted as a Cloudflare Worker:

- App: <https://thankgodizime.github.io/papertrail/>
- AI endpoint: <https://papertrail-ai.mrtiago807.workers.dev/api/chat>
- Worker source: `worker/index.js`

The Worker is connected to Cloudflare Workers AI using the `AI` binding and the `@cf/meta/llama-3.2-3b-instruct` model. No OpenAI key or other model secret is stored in the public app or repository. The app sends the user's question and up to 14,000 characters of extracted document text to Cloudflare for an answer. The original uploaded file remains in browser storage on the user's device.

## Updating the server

The server currently uses Cloudflare's dashboard code editor. After changing `worker/index.js`, open the `papertrail-ai` Worker in Cloudflare, choose **Edit code**, paste the updated source, and choose **Deploy**. To deploy from a local checkout instead, use the included `wrangler.jsonc` after signing Wrangler in to the same Cloudflare account.

## Free usage

Cloudflare's current Free plan includes up to 100,000 Worker requests per day. Workers AI includes 10,000 Neurons per day at no charge. When the free daily AI allocation runs out, Papertrail reports that AI is temporarily unavailable until it resets. Cloudflare may change these limits; check its [Workers pricing](https://developers.cloudflare.com/workers/platform/pricing/) and [Workers AI pricing](https://developers.cloudflare.com/workers-ai/platform/pricing/) before a public launch.
