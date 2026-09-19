# ZTT Buy/Sell Pressure Indicator

A TradingView indicator built from the "From Zero to Trader" masterclass rules. It shows
who is currently in control of the market (buyers vs sellers) and prints **BUY** / **SELL**
labels only when the course's confluence checklist lines up.

## What it does

The dashboard (top-right of your chart) shows live:

| Row | Meaning |
|---|---|
| **Buying %** | Share of recent volume on the buy side (last 20 bars by default) |
| **Selling %** | The opposite side |
| **Structure** | BULLISH (Higher Highs + Higher Lows), BEARISH (Lower Lows + Lower Highs), or RANGING |
| **Price** | Above or below the 50 EMA |
| **Session** | Whether you're inside the London–New York window (9:00 AM – 6:30 PM UAE time) |

A **BUY** label prints only when ALL of these are true on a closed candle:

1. Market structure is bullish (the course's HH + HL rule, using candle **bodies**, not wicks)
2. Price is above the 50 EMA (the course's "cherry on top" confluence)
3. Buying pressure ≥ 60% (adjustable)
4. A bullish confirmation candle just closed — Bullish Engulfing or Morning Star (the course's favorite)
5. Optional: you're inside the high-volume session window

**SELL** is the exact mirror. Small triangles mark body-close breaks of structure (early
warning only — never an entry on their own).

## How to install (2 minutes)

1. Open TradingView and open any chart (e.g. `OANDA:XAUUSD` for gold, `BINANCE:BTCUSDT` for Bitcoin).
2. Click **Pine Editor** at the bottom of the screen.
3. Delete whatever is in the editor, open [`ztt-buy-sell-pressure.pine`](ztt-buy-sell-pressure.pine),
   copy the **entire file**, and paste it in.
4. Click **Save**, give it a name, then click **Add to chart**.
5. (Optional) Right-click the BUY/SELL condition in the indicator → **Add alert** so your
   phone gets notified instead of you watching the screen (this is also a course rule —
   use alerts, don't stare at charts).

## Recommended settings per market

| Market | Timeframe | Session filter |
|---|---|---|
| XAUUSD (gold) | 1H / 4H | **ON** |
| EUR/USD, GBP/USD and other majors | 1H / 4H | **ON** |
| BTC and crypto | 1H / 4H | **OFF** (crypto trades 24/7) |

The course is explicit: bias comes from Weekly → Daily → 4H, entries from 1H/2H/4H.
Don't run this on 1-minute charts — the course calls scalping the fastest way to lose.

## The honest part — read this before trading

**No indicator on Earth is "80% accurate," including this one.** Anyone selling you one is
lying. This is straight from the course you gave me: Alex's own edge comes from a ~1:4
risk-to-reward ratio, which means he can **lose 7 out of 10 trades and still be profitable**.
The win-rate is not the edge — risk management is. This indicator's job is to make you take
*fewer, better* trades, not to predict the future.

**About the $8–$10 account:** be aware of what the course actually says. Alex's Stage 1
($100 → $400) uses 100%-risk "full port" trades — that is acknowledged gambling to escape
the small-capital tier, and he expects to blow some of those. With $8 on a live account,
the minimum lot size (0.01) on XAUUSD means a single trade can swing a large share of your
balance, and the spread alone eats a meaningful percentage. The math barely works.

**Do this instead:** use your Fusion Markets **demo account** first. The course itself says
trading is a skill like a language — you wouldn't bet money on a language exam after one
week. Prove you can follow the checklist (One-and-Done rule, fixed stop loss, 1:2 minimum RR,
session window) for at least 20–30 demo trades before risking the live $8. The $10 → $100
goal is possible but it is the gambling stage of the course, not the skill stage — go in
knowing that.

**Position sizing formula (course Module 3):**

```
Risk $ = Balance × Risk %
Lot size = Risk $ / (Stop-loss pips × pip value per lot)
```

Never enter a trade without knowing the lot size and stop loss **before** clicking buy.

## Connecting this repo (TradingView MCP) — where it runs

This MCP server controls TradingView **Desktop on your own computer** through Chrome
DevTools (port 9222). It cannot run from the cloud — TradingView must be running on the
same machine as Claude Code. Setup steps are in [`../SETUP_GUIDE.md`](../SETUP_GUIDE.md).
Once connected on your machine, Claude can read this indicator's levels and labels from
the chart with the `data_get_pine_*` tools and help you analyze gold, EUR/USD, and BTC live.
