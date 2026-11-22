---
name: inventory-check
description: Check Recoera stock levels, flag low or out-of-stock items, and suggest reorder quantities. Use when asked about inventory, stock, what to reorder, or what's running out.
---

# Inventory check

1. **Get current stock** per product/variant from the store connector or an inventory export in `data/`.
2. **Get recent sales velocity** (units sold per day over the last 30 days) if available.
3. **Flag:**
   - Out of stock (0 units)
   - Low stock: fewer than 14 days of cover at current velocity (or fewer than 5 units if there's no velocity data)
   - Overstock: more than 120 days of cover
4. **Suggest a reorder quantity** for flagged items: enough for 60 days of cover minus current stock. State
   the assumptions.
5. **Present** a table sorted by urgency and save it to `data/reports/<YYYY-MM-DD>-inventory.md`.
6. **Don't change stock levels** in the store without explicit confirmation.
