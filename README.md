# Lifepath RPG API (Vercel)

Serverless API for your Custom GPT Actions: dice roll, state get/update, rules endpoints.
Deployed on Vercel Functions (Node.js 18). CORS enabled, JSON guaranteed.

## Endpoints
- `GET /api/__health` → health check
- `GET /api/__echo` → echo request (debug)
- `POST /api/roll` → body: `{ "formula":"1d100", "mod":0, "seed":123, "context":"..." }`
- `GET /api/state/get?playerId=default-player`
- `POST /api/state/update` → body: `{ "playerId":"...", "patch": { ... } }`
- `GET /api/rules/list`
- `GET /api/rules/get?id=R-11`
- `GET /api/rules/version`

## Deploy
1. Push this folder to GitHub.
2. Vercel → New Project → Import.
3. After deploy, take your domain (ex: `https://lifepath-rpg-api.vercel.app`).
4. Open `openapi.yaml` and set:
   ```
   servers:
     - url: https://lifepath-rpg-api.vercel.app/api
   ```
5. Import `openapi.yaml` to your Custom GPT (Actions → Import from OpenAPI).

## Notes
- This uses an in-memory Map for state (non-persistent). Use Vercel KV/Upstash/Supabase for persistence.
- CORS is open (`*`) for development. Restrict in production.
- `/roll` currently supports only `1d100` with optional `mod` and `seed`.
