# Candosa — Client Summary Daily Report

A self-contained daily report of the five Candosa dashboard metrics, with a 7-day
trend line for each. Data comes from **candobro** (Slack), which reconstructs it
from the production database and event logs.

**Metrics tracked**
- Clientes activos (total)
- En onboarding
- Migrados
- No migrados (activos)
- Trimestre presentado

## Files
| File | Purpose |
|------|---------|
| `index.html` | The published report (generated — do not edit by hand). |
| `data.json` | Source of truth. Edit this each day with the latest values. |
| `template.html` | HTML template with a `/*__DATA__*/` placeholder. |
| `build.js` | Injects `data.json` into `template.html` → `index.html`. |

## Daily update
1. Ask candobro in Slack for the latest 7-day trend.
2. Update `data.json` (append today's row to `days`, bump `lastUpdated`).
3. Rebuild and publish:
   ```bash
   node build.js
   git add -A && git commit -m "Report: $(date +%F)" && git push
   ```

The report keeps a rolling window — append each new day and the charts/KPIs
update automatically.
