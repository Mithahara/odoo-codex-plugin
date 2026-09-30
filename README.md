# Odoo for Codex

Codex skills for [MCP Server for Odoo](https://apps.odoo.com/apps/modules/20.0/mh_mcp_server), an Odoo add-on from Mithahara. The add-on is the paid part and is required: this plugin only adds read-only skills that call its tools.

Skills: `find-overdue-invoices`, `who-can-see-model`, `record-history`. They use only `odoo_search`, `odoo_read` and `odoo_fields`, and each works only on models your MCP profile allows:

- `find-overdue-invoices`: `account.move`
- `record-history`: `mail.message`. On Odoo 20, field changes show up as tracking messages. On Odoo 19 they sit in `mail.tracking.value`, which Odoo restricts to administrators, so a least-privilege profile gets the chatter only and the skill says so.
- `who-can-see-model`: `ir.access` on Odoo 20, `ir.model.access` and `ir.rule` on Odoo 19. Access rules are admin data, so the profile's Odoo user must be in the Access Rights group.

## Install

1. Install the add-on on your Odoo (19.0 or 20.0), create a profile and an API key with scope `odoo.mcp`.
2. Add the marketplace and install the plugin:

```bash
codex plugin marketplace add Mithahara/odoo-codex-plugin
```

3. Point Codex at your Odoo in `~/.codex/config.toml` (the plugin cannot carry your URL):

```toml
[mcp_servers.odoo]
url = "https://YOUR-ODOO-HOST/mcp"
bearer_token_env_var = "ODOO_MCP_KEY"
```

```bash
export ODOO_MCP_KEY=...   # the odoo.mcp API key
```

Tested with Codex CLI 0.155, all three skills end to end against Odoo 19 and Odoo 20. The Codex desktop app has not been tested. Support: support@mithahara.com
