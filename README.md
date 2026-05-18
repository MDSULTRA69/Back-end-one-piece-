# One Piece Daily — Backend

Express + Drizzle ORM API server. Deploy to **Render**.

## Setup

1. Install dependencies:
   ```bash
   npm install
   ```

2. Copy the env file and fill in your values:
   ```bash
   cp .env.example .env
   ```

3. Push the database schema:
   ```bash
   npm run db:push
   ```

4. Build and run locally:
   ```bash
   npm run build
   npm start
   ```

## Deploy to Render

### Using render.yaml (recommended)
1. Push this folder to a GitHub repo
2. In Render dashboard → New → Blueprint
3. Connect the repo — Render reads `render.yaml` automatically
4. After deploy, update `FRONTEND_URL` to your Netlify URL
5. Run `npm run db:push` once via the Render Shell to create tables

### Manual setup
1. Create a new **Web Service** on Render
2. Set build command: `npm install && npm run build`
3. Set start command: `npm start`
4. Add a **PostgreSQL** database on Render and copy the connection string
5. Set environment variables (see below)

## Environment Variables

| Variable | Required | Description |
|---|---|---|
| `DATABASE_URL` | Yes | PostgreSQL connection string from Render |
| `SESSION_SECRET` | Yes | Random string (min 32 chars) for signing cookies |
| `FRONTEND_URL` | Yes | Your Netlify URL, e.g. `https://onepiecedaily.netlify.app` |
| `NODE_ENV` | Yes | Set to `production` on Render |
| `PORT` | Auto | Render sets this automatically |

## Database Migrations

After deploying, open the Render Shell for your service and run:
```bash
npm run db:push
```
This creates the `users` and `game_results` tables.

## API Endpoints

| Method | Path | Description |
|---|---|---|
| POST | `/api/auth/register` | Register new user |
| POST | `/api/auth/login` | Login |
| POST | `/api/auth/logout` | Logout |
| GET | `/api/auth/me` | Get current user |
| POST | `/api/game/result` | Submit game result + earn XP |
| GET | `/api/leaderboard` | Top players by XP |
| GET | `/api/healthz` | Health check |
