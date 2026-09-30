---
name: who-can-see-model
description: Explain which Odoo users and groups can read, write, create or delete a given model, from its access rules. Read-only.
---

Use the `odoo` MCP server. Read only.

1. Ask which model if the user gave a name, not a technical name; map it (for example "sales orders" is `sale.order`).
2. Odoo 19 and earlier keep access in two models, Odoo 20 in one. Call `odoo_fields` on `ir.access`; if it is offered, use the Odoo 20 path, otherwise the Odoo 19 path. If neither path's models are offered by the MCP profile, say so and stop.
   - **Odoo 20:** call `odoo_search` on `ir.access` with domain `[["model_id.model","=","<model>"]]`, fields `name, group_id, operation, domain, kind, for_read, for_write, for_create, for_unlink`. `kind` tells permissions (who is allowed) from restrictions (record filters that narrow access); `domain` on a restriction is the filter.
   - **Odoo 19:** call `odoo_search` on `ir.model.access` with domain `[["model_id.model","=","<model>"]]`, fields `name, group_id, perm_read, perm_write, perm_create, perm_unlink`; then on `ir.rule` with the same domain, fields `name, groups, domain_force, perm_read, perm_write, perm_create, perm_unlink`. If only one of the two is offered, say which and that the answer is incomplete.
3. Summarise per group: what it can do, and which record filters narrow it (quote the domain as written, do not interpret it beyond plain wording). An empty group means everyone.
4. Never claim the result is a full security audit.
