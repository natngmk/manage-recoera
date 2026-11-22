---
name: order-report
description: Summarise Recoera orders and sales for a period — revenue, order count, AOV, top products, refunds. Use when asked for a sales/order report, daily/weekly/monthly summary, or "how are sales".
---

# Order report

1. **Confirm the period** (default: last 7 days) and the channel(s).
2. **Get the data** from the store connector, or from an export file the user points to (CSV in `data/`).
   If neither is available, say so and stop. Don't estimate.
3. **Calculate:**
   - Total revenue, order count, average order value
   - Top 5 products by units and by revenue
   - Refunds / cancellations (count and value)
   - Comparison with the previous period of equal length, if the data allows
4. **Write the report** as a short markdown summary: headline numbers first, then tables, then 2–3 notable
   observations.
5. **Save** to `data/reports/<YYYY-MM-DD>-orders-<period>.md`. Keep customer names, emails and
   addresses out of the report. If those are needed, use `data/private/`.
