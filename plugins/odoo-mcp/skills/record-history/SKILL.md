---
name: record-history
description: Show what changed on an Odoo record, from its chatter and tracked field changes. Read-only.
---

Use the `odoo` MCP server. Read only.

1. Identify the model and record id (search by name with `odoo_search` if the user gave a name).
2. Call `odoo_fields` on `mail.message`. If it is not offered by the MCP profile, say so and stop.
3. Call `odoo_search` on `mail.message` with domain `[["model","=","<model>"],["res_id","=",<id>]]`, order `date desc`, limit 30, fields `date, author_id, message_type, body`, plus `tracking_value_ids` only if `odoo_fields` listed it (Odoo 19 and earlier).
4. If `tracking_value_ids` came back and `mail.tracking.value` is offered, read them with `odoo_read` for `field_id, old_value_char, new_value_char`. In Odoo 20 there is no such field: field changes are the messages whose `message_type` is `tracking`, so read the change from their `body`.
5. Report newest first: when, who, and what changed (old value to new value). Strip HTML from bodies. If tracked changes could not be read, say that only the chatter is shown.
