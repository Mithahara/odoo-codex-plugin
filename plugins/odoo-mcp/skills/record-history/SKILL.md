---
name: record-history
description: Show what changed on an Odoo record, from its chatter and tracked field changes. Read-only.
---

Use the `odoo` MCP server. Read only.

1. Identify the model and record id (search by name with `odoo_search` if the user gave a name).
2. Call `odoo_search` on `mail.message` with domain `[["model","=","<model>"],["res_id","=",<id>]]`, fields `date, author_id, message_type, body, tracking_value_ids`, order `date desc`, limit 30. If `mail.message` is not offered by the MCP profile, say so and stop.
3. If `tracking_value_ids` are present and `mail.tracking.value` is offered, read them with `odoo_read` for `field_id, old_value_char, new_value_char`.
4. Report newest first: when, who, and what changed (old value to new value). Strip HTML from bodies.
