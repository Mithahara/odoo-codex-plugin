---
name: find-overdue-invoices
description: List overdue customer invoices from the connected Odoo, with customer, amount due and days overdue. Read-only.
---

Use the `odoo` MCP server. Read only; never call odoo_create, odoo_write or odoo_unlink.

1. Call `odoo_fields` for `account.move` to confirm field names (expect `move_type`, `invoice_date_due`, `amount_residual`, `payment_state`, `partner_id`, `name`). If `account.move` is not offered, tell the user their MCP profile does not include it and stop.
2. Call `odoo_search` on `account.move` with domain `[["move_type","=","out_invoice"],["state","=","posted"],["payment_state","in",["not_paid","partial"]],["invoice_date_due","<","<today>"]]`, using today's date, fields `name, partner_id, invoice_date_due, amount_residual, currency_id`, order `invoice_date_due asc`, limit 50.
3. Present a table: invoice, customer, due date, days overdue, amount due (with currency). Give the total per currency.
4. If 50 rows came back, say the list is capped and offer to narrow by customer or date.
