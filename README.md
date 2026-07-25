# Karl's Paper Portfolio

Paper trading dashboard tracking a 50/50 strategy over 12 months.

**Live site:** https://karlmaximilienkohler.github.io/paper-portfolio

---

## Strategy

| Side | Ticker | Rule |
|---|---|---|
| Anchor (50%) | QQQ | Buy Aug 1, hold 12 months, never sell |
| Active (50%) | NVDA, TSLA, META | MA20 crossover — buy when price crosses above 20-day moving average, sell when it crosses below |

### Why MA20 crossover?

The 20-day moving average crossover is one of the most well-studied simple trading signals. When a stock's price moves above its 20-day average, short-term momentum is positive. When it falls below, momentum is negative. It filters out daily noise while staying responsive enough for swing trading.

---

## How to update data (daily)

Find the `DATA` block in `index.html`'s `<script>` tag and update:

```js
const DATA = {
  lastUpdated: '2026-08-04',
  qqq: { price: 531.20 },
  stocks: {
    nvda: { price: 148.30, chgPct: 1.83, ma20: 141.50, aboveMa: true,  crossedAbove: true,  crossedBelow: false },
    tsla: { price: 312.40, chgPct: -2.1, ma20: 318.00, aboveMa: false, crossedAbove: false, crossedBelow: true  },
    meta: { price: 628.00, chgPct: 0.74, ma20: 615.00, aboveMa: true,  crossedAbove: false, crossedBelow: false },
  }
};
```

- `crossedAbove: true` → **BUY** signal (only on the day it crosses up)
- `crossedBelow: true` → **SELL** signal (only on the day it crosses down)
- `aboveMa: true` → **HOLD** (above MA, already in position)
- `aboveMa: false` → **WATCH** (below MA, no position)

---

## Enable GitHub Pages

Settings → Pages → Deploy from branch → `main` → `/ (root)` → Save.

Live at: `https://karlmaximilienkohler.github.io/paper-portfolio`