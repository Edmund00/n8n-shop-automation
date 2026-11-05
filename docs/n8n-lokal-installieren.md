# Run n8n locally for testing (free)

Short notes from testing the workflows on Windows with Node 24 (no Docker, no account).

1. Create a folder and a `package.json`:
   - dependency: `n8n` (tested with 2.46.6)
   - `overrides`: pin `@playwright/test`, `playwright` and `playwright-core` to `1.64.1`
     (plain `npx n8n` failed because a helper package asked for `playwright-core@1.65.0`, which was not available in the npm registry at the time)
2. `npm install`
3. Set `N8N_USER_FOLDER` to a data folder and disable telemetry (`N8N_DIAGNOSTICS_ENABLED=false`).
4. Import: `n8n import:workflow --input=workflow.json`
5. Run a test variant: `n8n execute --id=<workflow id> --rawOutput`

Keep the runtime and data folders out of version control (see `.gitignore`).
