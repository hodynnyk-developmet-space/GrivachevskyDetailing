# Cloudflare GitHub deployment settings

Canonical names for this project:

- GitHub repository: `GrivachevskyDetailing`
- Cloudflare Worker: `grivachevsky-detailing`
- D1 database: `grivachevsky-detailing`
- D1 binding: `DB`
- Telegram bot: `@GrivachevskyDetailing_bot`

## Git integration

Connect the GitHub repository `GrivachevskyDetailing` to the Cloudflare Worker **`grivachevsky-detailing`**.

Use:

- Production branch: `main` (or your actual default branch)
- Root directory: `/`
- Build command: `npm run build`
- Deploy command: `npx wrangler deploy`
- Wrangler configuration: `/wrangler.jsonc`

The repository's `wrangler.jsonc` has `name = grivachevsky-detailing`, so Wrangler deploys to that Worker instead of a starter Worker.

## If the URL says Hello world

`Hello world` is **not** produced anywhere by this repository. It means one of these is true:

1. You opened the URL of another Worker.
2. The Cloudflare Git integration is attached to a starter Worker instead of `grivachevsky-detailing`.
3. Cloudflare did not run `npx wrangler deploy` from this repository root.
4. An older deployment is still active.

Open the deployment URL shown on the latest successful deployment for **`grivachevsky-detailing`**, not a previously created `*.workers.dev` project.

## Verification

After a successful deployment open:

`https://grivachevsky-detailing.<your-subdomain>.workers.dev/__version`

Expected response:

```json
{
  "app": "GrivachevskyDetailing",
  "version": "1.0.3",
  "database": "grivachevsky-detailing",
  "worker": true
}
```

Then open the root URL. The React/Vite Mini App must render instead of plain text.

## D1

Create the database with:

```bash
npx wrangler d1 create grivachevsky-detailing
```

After Cloudflare returns its database UUID, add the D1 binding to `wrangler.jsonc` using binding `DB`. Do not invent a database ID.
