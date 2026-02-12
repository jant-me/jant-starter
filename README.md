# Jant Starter

A personal microblog powered by [Jant](https://github.com/jant-me/jant). Deploy to Cloudflare Workers in one click.

[![Deploy to Cloudflare](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/jant-me/jant-starter)

## One-Click Deploy

1. Click the **Deploy to Cloudflare** button above
2. Authorize Cloudflare to access your GitHub account
3. Name your Worker, D1 database, and R2 bucket
4. Set `AUTH_SECRET` to a random 32+ character string (generate one: `openssl rand -base64 32`)
5. Deploy!

After deploying, set `SITE_URL` in Cloudflare dashboard → your Worker → Settings → Variables.

## Local Development

```bash
# Install dependencies
npm install

# Copy environment template and set AUTH_SECRET
cp .dev.vars.example .dev.vars

# Start development server
npm run dev
```

Visit http://localhost:9019 to see your site.

## Manual Deployment

If you prefer to deploy manually instead of using the button:

### 1. Prerequisites

Install [Wrangler CLI](https://developers.cloudflare.com/workers/wrangler/install-and-update/) and log in:

```bash
wrangler login
```

### 2. Create D1 Database

```bash
wrangler d1 create jant-starter-db
# Copy the database_id from the output!
```

### 3. Update Configuration

Edit `wrangler.toml`:

- Replace `database_id = "local"` with the ID from step 2
- Set `SITE_URL` to your production URL

### 4. Set Production Secrets

```bash
# Generate and set AUTH_SECRET
openssl rand -base64 32
wrangler secret put AUTH_SECRET
```

### 5. Deploy

```bash
npm run deploy
```

## Custom Domain

1. Go to [Cloudflare Dashboard](https://dash.cloudflare.com) → Workers & Pages
2. Select your worker → Settings → Domains & Routes
3. Click **Add → Custom domain** and enter your domain

## Commands

| Command                      | Description                        |
| ---------------------------- | ---------------------------------- |
| `npm run dev`                | Start development server           |
| `npm run build`              | Build for production               |
| `npm run deploy`             | Migrate, build, and deploy         |
| `npm run preview`            | Preview production build           |
| `npm run typecheck`          | Run TypeScript checks              |
| `npm run db:migrate:remote`  | Apply database migrations (remote) |

## Environment Variables

| Variable      | Description                               | Location         |
| ------------- | ----------------------------------------- | ---------------- |
| `AUTH_SECRET` | Secret key for authentication (32+ chars) | `.dev.vars` file |
| `SITE_URL`    | Your site's public URL                    | `wrangler.toml`  |

For all available variables, see the **[Configuration Guide](https://github.com/jant-me/jant/blob/main/docs/configuration.md)**.

## Documentation

- [Jant Documentation](https://jant.me/docs)
- [GitHub Repository](https://github.com/jant-me/jant)
