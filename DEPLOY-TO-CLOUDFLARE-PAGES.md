# Deploying the food-ordering app to `*.pages.dev`

For anyone building the Deka's Kitchen exercise with OpenCode + DeepSeek.

## Why it usually fails

1. **`*.pages.dev` is not your domain.** It belongs to Cloudflare, so it never shows up on the "Authorize" page of `cloudflared tunnel login`. Tunnels and DNS records need a domain you own, so that route fails (often with `Failed to fetch resource`).
2. **Pages does not run Python or Node servers.** It serves static files only. A Flask, FastAPI, Express or `http.server` backend will never run there. The backend has to be rewritten as **Pages Functions** (JavaScript files in a `functions/` folder), and the data has to live in **D1** (Cloudflare's SQLite). A plain SQLite file does not exist on Cloudflare.
3. **The agent can't click "Allow".** `wrangler login` opens a browser and waits. Run it inside the agent and it hangs or times out. **Log in yourself in a normal terminal first.**
4. **Several Cloudflare accounts on one login.** Wrangler stops with "More than one account available" and the agent can't answer the prompt. Set `CLOUDFLARE_ACCOUNT_ID`.
5. **Interactive questions hang the agent.** `wrangler pages deploy` without a project or branch asks questions. Use the exact flags given below.
6. **Old commands from the model's memory.** `wrangler publish` and `wrangler pages publish` are gone. The current command is `wrangler pages deploy`.
7. **Small traps:**
   - The `database_id` in `wrangler.toml` is left as a placeholder.
   - `functions/` is placed inside the static folder instead of the project root.
   - `compatibility_date` is newer than the local test runtime supports (`wrangler pages dev` then refuses to start).
   - Test scripts using Python `urllib` get `403` from Cloudflare's bot check unless they send a `User-Agent`.

## Step 1: do this yourself, in a normal terminal (not in OpenCode)

```
npx wrangler@4 login
npx wrangler@4 whoami
```

Click **Allow** in the browser tab. `whoami` prints your account name(s) and **Account ID(s)**. Copy the ID of the account you want to use.

## Step 2: paste this prompt into OpenCode

Replace `<ACCOUNT_ID>` and `<PROJECT_NAME>` first. The project name becomes `https://<PROJECT_NAME>.pages.dev`; use lowercase letters, digits and hyphens.

````text
Deploy this project to Cloudflare Pages on a *.pages.dev address. I am already logged in to wrangler (I ran `npx wrangler@4 login` myself). Do NOT run `wrangler login`, `cloudflared`, or anything involving tunnels, DNS or custom domains. *.pages.dev needs none of that.

Fixed values:
- CLOUDFLARE_ACCOUNT_ID = <ACCOUNT_ID>   (set this env var in EVERY shell command that runs wrangler)
- Pages project name and D1 database name = <PROJECT_NAME>
- Always use `npx wrangler@4 ...`. Never use `wrangler publish` or `wrangler pages publish`; they no longer exist.

Facts you must respect:
- Cloudflare Pages serves static files and runs JavaScript "Pages Functions" from a `functions/` folder at the PROJECT ROOT. It cannot run Python, Flask, FastAPI, Express or any long-running server. There is no filesystem, so a local SQLite file will not work. Use Cloudflare D1 instead, bound as `env.DB`.
- Your shell is non-interactive. Any command that asks a question will hang. Use the flags given below, and add `--yes` to `d1 execute`.

Step 0: verify the login. Run `npx wrangler@4 whoami` with CLOUDFLARE_ACCOUNT_ID set. If it says not logged in, STOP and tell me to run `npx wrangler@4 login` in my own terminal. Do not try to log in yourself.

Step 1: understand the app. Read the whole project. Write me a short list of: every page (HTML) and every API endpoint (method, path, request body, response, status codes), the database tables, and how the kitchen/admin login works. Everything below must keep exactly this behaviour and these URLs, so the frontend keeps working unchanged.

Step 2: lay out the files like this:
- `static/` (or the existing frontend folder): all HTML/CSS/JS, served as is. Asset URLs in the HTML must resolve inside this folder (e.g. a file at static/style.css is served at /style.css). A page `static/kitchen.html` is served at `/kitchen`.
- `functions/api/[[path]].js`: ONE catch-all file exporting `export async function onRequest({ request, env })` that routes every /api/* endpoint. Port the backend logic to this file, using `env.DB` (D1: `env.DB.prepare(sql).bind(...).all() / .first() / .run()`, and `env.DB.batch([...])` for multi-statement writes that must be atomic). Create the file with your file-writing tool, not the shell, because the brackets in the name break PowerShell and bash.
- `functions/_middleware.js`: if the app has a kitchen/admin password, enforce HTTP Basic auth here for paths starting with `/kitchen` and `/api/kitchen` (or the app's admin paths). Return 401 with header `WWW-Authenticate: Basic realm="Kitchen"` when it is missing or wrong. Read the password from `env.KITCHEN_PASSWORD`, otherwise call `next()`.
- `schema.sql`: CREATE TABLE IF NOT EXISTS for every table, plus the fictional demo menu inserted only when the items table is empty (INSERT ... SELECT ... WHERE NOT EXISTS (SELECT 1 FROM items)), so it is safe to run twice.
- `wrangler.toml` at the project root:
    name = "<PROJECT_NAME>"
    pages_build_output_dir = "static"
    compatibility_date = "2026-04-01"
    [vars]
    KITCHEN_PASSWORD = "demo"
    [[d1_databases]]
    binding = "DB"
    database_name = "<PROJECT_NAME>"
    database_id = "PLACEHOLDER"

Keep these rules from the original app: the server computes order totals from DB prices (never trust prices from the browser), it rejects unavailable items, the customer status endpoint never returns phone or address, a repeated submit with the same client key returns the same order instead of a duplicate, and inputs are validated with 400 + {"error": "..."} on bad data.

Step 3: test locally before touching the cloud.
  npx wrangler@4 d1 execute <PROJECT_NAME> --local --file schema.sql --yes
  npx wrangler@4 pages dev --port 8788      (run it in the background)
Then with curl: GET /api/menu returns the menu JSON; POST an order and GET its status; GET /api/kitchen/orders returns 401 without a password and 200 with `-u x:demo`; GET / returns the HTML page. If the project has a test script, run it against http://localhost:8788. Python urllib tests must send a User-Agent header. Fix everything before continuing. Stop the dev server afterwards.

Step 4: create the cloud resources and deploy (CLOUDFLARE_ACCOUNT_ID set on every line):
  npx wrangler@4 d1 create <PROJECT_NAME>
      -> copy the printed database_id into wrangler.toml, replacing PLACEHOLDER. Confirm the file changed.
      (If it says the database already exists, get the id from `npx wrangler@4 d1 list`.)
  npx wrangler@4 d1 execute <PROJECT_NAME> --remote --file schema.sql --yes
  npx wrangler@4 pages project create <PROJECT_NAME> --production-branch main
      (If the name is taken, pick <PROJECT_NAME>-2, update `name` in wrangler.toml, and tell me.)
  npx wrangler@4 pages deploy --branch main --commit-dirty=true

Step 5: verify the live site at https://<PROJECT_NAME>.pages.dev (it can take ~30 seconds to appear). Run the same curl checks as step 3 against it. Then remove the test orders you created:
  npx wrangler@4 d1 execute <PROJECT_NAME> --remote --yes --command "DELETE FROM order_items; DELETE FROM orders; UPDATE items SET available = 1;"
(adjust the table names to this project's schema).

Troubleshooting, in this order:
- "More than one account available": CLOUDFLARE_ACCOUNT_ID was not set on that command.
- "Not logged in" / authentication error: STOP and ask me to run `npx wrangler@4 login` myself.
- "requires compatibility date ... newest supported is ...": lower compatibility_date in wrangler.toml to a date at or before the one in the message.
- API returns 500 and `env.DB` is undefined: wrangler.toml is missing `pages_build_output_dir` or the [[d1_databases]] block, or you deployed from a different folder. Run deploy from the project root.
- API returns HTML instead of JSON: functions/ is not at the project root, or the filename is not exactly `[[path]].js` inside `functions/api/`.
- 403 from Cloudflare in a Python test: add a User-Agent header.

Finish by telling me: the live URL, the kitchen URL and password, what you changed and why, and the redeploy command. Do not claim it works unless the step 5 checks actually passed. Paste their output.
````

## Afterwards

- **Redeploy after a change:** `npx wrangler@4 pages deploy --branch main` (with `CLOUDFLARE_ACCOUNT_ID` set).
- **Before any real use**, replace the demo password: `npx wrangler@4 pages secret put KITCHEN_PASSWORD`, then delete the `[vars]` line from `wrangler.toml` and redeploy.
- **Working reference:** if their app has the same API as this repo, they can copy `functions/`, `schema.sql` and `wrangler.toml` from it directly and skip to step 3. They still need to put their own `name`, `database_name` and `database_id` in `wrangler.toml`.
