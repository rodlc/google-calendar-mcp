# Gcal MCP — Rename accounts + add 2nd

## Context
`bun run auth` saved first OAuth token as `normal` (upstream default).
Gmail MCP uses `rodlecoent`/`rodolphe` naming. Align gcal to match.

## Steps

### 1. Rename `normal` → `rodlecoent` in tokens.json
► `~/.config/google-calendar-mcp/tokens.json`
- `jq` rename key: `{rodlecoent: .normal} + (del(.normal))`

### 2. Auth 2nd account
```bash
cd mcp-servers/google-calendar-mcp
GOOGLE_OAUTH_CREDENTIALS=~/.config/gcal-mcp/gcp-oauth.keys.json \
  bun run auth rodolphe
```
→ Browser OAuth → user clicks "Allow" on rodolphe-lecoent account

### 3. Verify
```bash
jq 'keys' ~/.config/google-calendar-mcp/tokens.json
# → ["rodlecoent", "rodolphe"]
```

## Files modified
- `~/.config/google-calendar-mcp/tokens.json` (rename key + new account)

═══════════════════════════════════════════════
Résultat
═══════════════════════════════════════════════
Status: Complété ✓
Tokens alignés avec convention Gmail MCP: `rodlecoent` + `rodolphe`

═══════════════════════════════════════════════
Progression
═══════════════════════════════════════════════
✓ Renamed `normal` → `rodlecoent` via jq
✓ OAuth `rodolphe` — browser flow completed
✓ Verified: `jq 'keys'` → `["rodlecoent", "rodolphe"]`

═══════════════════════════════════════════════
Next Steps
═══════════════════════════════════════════════
► Test gcal MCP tools with both accounts (list-events, list-calendars)
► Update memory if gcal convention worth persisting
