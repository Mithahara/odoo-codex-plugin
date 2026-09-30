---
name: who-can-see-model
description: Explain which Odoo users and groups can read, write, create or delete a given model, from its access rules. Read-only.
---

Use the `odoo` MCP server. Read only.

1. Ask which model if the user gave a name, not a technical name; map it (for example "sales orders" is `sale.order`).
2. Call `odoo_search` on `ir.model.access` with domain `[["model_id.model","=","<model>"]]`, fields `name, group_id, perm_read, perm_write, perm_create, perm_unlink`.
3. Call `odoo_search` on `ir.rule` with domain `[["model_id.model","=","<model>"]]`, fields `name, groups, domain_force, perm_read, perm_write, perm_create, perm_unlink`.
4. Summarise per group: what it can do, and which record rules narrow it (quote `domain_force` as written, do not interpret it beyond plain wording).
5. If either model is not offered by the MCP profile, say which one and that the answer is incomplete. Never claim the result is a full security audit.
