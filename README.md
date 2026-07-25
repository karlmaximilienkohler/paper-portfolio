# Signalboard

A simple, self-hosted paper trading dashboard anyone can fork and run. Tracks a 50/50 strategy: one anchor ETF held long-term + up to 3 active momentum positions driven by MA20 crossover signals.

**Demo:** https://karlmaximilienkohler.github.io/paper-portfolio

---

## How it works

- **No backend, no API keys, no cost** — one HTML file, hosted free on GitHub Pages
- **Strategy:** 50% into QQQ (hold 12 months), 50% into NVDA/TSLA/META momentum trades
- **Signal:** MA20 crossover — price crosses above 20-day moving average = BUY, crosses below = SELL
- **Daily update:** edit the `DATA` block in `index.html`, push to GitHub, site updates instantly

## Fork & deploy in 3 steps

1. Fork this repo
2. Go to **Settings → Pages → Deploy from branch → `main` → `/ (root)`**
3. Your dashboard is live at `https://yourusername.github.io/paper-portfolio`

## Update daily data

Find the `DATA` block in `index.html` and fill in each stock:

```js
const DATA = {
  lastUpdated: '2026-08-04',
  qqq: { price: 531.20 },
  stocks: {
    nvda: {
      price: 148.30,
      chgPct: 1.83,        // today's % change
      ma20: 141.50,        // 20-day moving average
      aboveMa: true,       // price > ma20?
      crossedAbove: true,  // just crossed up today? → BUY
      crossedBelow: false  // just crossed down today? → SELL
    },
    // tsla and meta follow the same shape
  }
};
```

| Field | Meaning | Signal produced |
|---|---|---|
| `crossedAbove: true` | Price just went above MA20 | **BUY** |
| `crossedBelow: true` | Price just went below MA20 | **SELL** |
| `aboveMa: true` | Above MA20, no fresh cross | **HOLD** |
| `aboveMa: false` | Below MA20, no fresh cross | **WATCH** |

## Customize

- Change tickers by replacing NVDA/TSLA/META in the HTML (3 places each)
- Change allocation by editing the `$550` / `$183` values in the plan table
- Change the strategy label in the `DATA` comment block

## Stack

Plain HTML + CSS + vanilla JS. No frameworks, no build step, no dependencies.
