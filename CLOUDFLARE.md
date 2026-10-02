# Host Papertrail on Cloudflare for free

This project is configured as one Cloudflare Worker with static app files and a private server-side AI route. It uses Cloudflare Workers AI, so there is no OpenAI key to put in the app or repository.

## Create the host

1. Sign in or create a free Cloudflare account at <https://dash.cloudflare.com/>.
2. Open **Workers & Pages** and choose **Create application**.
3. Choose **Import an existing Git repository** and connect GitHub.
4. Select `thankgodizime/papertrail`. Keep the project root as `/`.
5. Deploy using the repository's `wrangler.jsonc` configuration. If prompted for a build command, use `npx wrangler deploy`.
6. Cloudflare will give the app a URL ending in `.workers.dev`. Open that URL on your phone and add it to the home screen.

The worker exposes `/api/chat` on the same HTTPS host as the app. It uses the `@cf/meta/llama-3.2-3b-instruct` model and sends only the question and readable document text needed to answer it. Original uploaded files remain in the browser's IndexedDB.

## Free usage

Cloudflare's current Free plan includes up to 100,000 Worker requests per day. Workers AI includes 10,000 Neurons per day at no charge; when that daily AI allocation runs out, Papertrail reports that AI is temporarily unavailable until it resets. Cloudflare may change these limits, so check its pricing pages before a public launch.

## Keep GitHub Pages available

The existing GitHub Pages site remains as a static fallback. Its chat continues to use local text matching. The live AI endpoint is enabled when Papertrail is served from its Cloudflare HTTPS host.
