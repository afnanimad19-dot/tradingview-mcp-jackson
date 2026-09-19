# ZTT Buy/Sell Pressure Indicator

A TradingView indicator built from the "From Zero to Trader" masterclass rules. It shows
who is in control of the market (buyers vs sellers), marks the trading sessions, draws
yesterday's key levels, flags liquidity sweeps (stop hunts), and prints **BUY** / **SELL**
labels **with Stop Loss and Take Profit levels** when the course's confluence checklist
lines up.

**This indicator never places trades.** It only shows information on the chart. You decide,
you click, you are responsible for every trade.

## How to install it (step by step, 2 minutes)

1. Open **TradingView Desktop** and open a chart — for example type `XAUUSD` (gold) or
   `BTCUSD` in the symbol box at the top left.
2. Look at the **bottom of the screen** — click the tab that says **Pine Editor**.
   (If you don't see it: menu → panels, or press the `Pine Editor` button in the bottom toolbar.)
3. The editor opens with some example code in it. **Select all of it (Ctrl+A) and delete it.**
4. Open the file [`ztt-buy-sell-pressure.pine`](ztt-buy-sell-pressure.pine), select
   **everything** (Ctrl+A), copy (Ctrl+C), and paste it into the empty Pine Editor (Ctrl+V).
5. Click **Save** (top of the editor), give it a name like `ZTT Signals`.
6. Click **Add to chart**. Done — you'll see the EMA line, session shading, level lines,
   and the dashboard in the top-right corner.
7. **Set up phone alerts (recommended):** click the ⏰ **Alert** button (top toolbar) →
   in "Condition" choose **ZTT Signals** → pick **Any alert() function call** → create.
   Now your phone gets a message with the exact Entry, SL, TP1 and TP2 prices every time
   a signal prints — you don't have to watch the screen (this is also a course rule).

## What you see on the chart

| Element | Meaning |
|---|---|
| **BUY / SELL label** | Full confluence checklist passed on a closed candle (see below) |
| **Entry / SL / TP1 / TP2 lines** | Drawn automatically at every signal. SL = just beyond the signal candle's wick (course style). TP1 = 1:2 reward, TP2 = 1:4 (the course's minimum and target) |
| **Gray shading** | Asia session — slow, spreads widen, **avoid trading** |
| **Blue shading** | London session — trend initiation, good |
| **Gold shading** | **Golden Window** (London/NY overlap, ~4:00–6:30 PM UAE time) — maximum volatility, best entries |
| **ASIA / LONDON / NY flags** | The exact bar where each session opens |
| **PDH / PDL / PDC lines** | Previous day High, Low, Close — the levels everyone watches |
| **SWEEP ✗ marks** | Liquidity sweep: a wick took out PDH/PDL or the last swing point but the candle closed back inside = stop hunt, often a reversal warning |
| **Small triangles** | Break of structure by body close (early heads-up, never an entry alone) |
| **Dashboard (top right)** | Buying % vs Selling %, structure state, EMA side, position vs previous close, current session, live sweep status |

## When does a BUY print?

All five at once, on a **closed** candle:

1. Market structure bullish — Higher High + Higher Low, judged by candle **bodies** (course rule: wicks don't count)
2. Price above the 50 EMA (the "cherry on top" confluence)
3. Buying pressure ≥ 60% of recent volume (adjustable)
4. A bullish confirmation candle just closed — Bullish Engulfing or Morning Star (the course's favorite)
5. Optional: inside the London/Golden Window session (turn this on for gold and forex pairs)

SELL is the exact mirror. Fewer signals = working as intended. The course's whole point is
one good trade beats ten impulsive ones ("One-and-Done").

## Where to put TP and SL

The indicator draws them for you at every signal, but understand the logic so you can
adjust like the course teaches:

- **Stop Loss:** just beyond the wick of the confirmation candle (default), or switch the
  setting to "Last swing point" to place it beyond the last Higher Low / Lower High —
  wider but harder to stop-hunt. Never trade without one.
- **TP1 at 1:2** — the course's minimum acceptable reward. Taking profit before 1:2 is
  how beginners stay poor.
- **TP2 at 1:4** — the course's target. At 1:4 you can lose 7 of 10 trades and still profit.
- **Set and forget:** once in, don't touch it. Price hits SL or TP. Moving stops mid-trade
  is the #1 account killer per the course.

Position size formula (before every trade): `Lot size = (Balance × Risk%) ÷ (SL pips × pip value)`.

## Recommended settings per market

| Market | Timeframe | Session filter |
|---|---|---|
| XAUUSD (gold) | 1H / 4H | **ON** |
| EUR/USD, GBP/USD and other majors | 1H / 4H | **ON** |
| BTC and crypto | 1H / 4H | **OFF** (crypto trades 24/7) |

Bias top-down like the course: check Weekly → Daily → 4H structure first, enter on 1H/4H.
Don't run this on 1-minute charts — the course calls scalping the fastest way to lose.

## Connecting Claude to your TradingView Desktop

Claude running **in the cloud** (claude.ai/code in the browser) cannot see your C drive or
your TradingView — it runs on Anthropic's servers. To let Claude read your chart, draw
levels, and analyze sessions live, run Claude Code **on your Windows PC**:

1. Install Claude Code on your PC and clone this repo there.
2. Follow [`../SETUP_GUIDE.md`](../SETUP_GUIDE.md): `npm install`, add the MCP server to
   `.mcp.json`, and start TradingView with debugging enabled:
   `%LOCALAPPDATA%\TradingView\TradingView.exe --remote-debugging-port=9222`
3. In that local session, Claude can then use `tv_health_check`, read this indicator's
   levels with the `data_get_pine_*` tools, draw AOIs/levels with `draw_shape`, and walk
   through live analysis of gold, EUR/USD, and BTC with you.

## The honest part — read this before trading

**No indicator on Earth is "80% accurate," including this one.** The edge in the course is
not win rate — it's the 1:4 risk-to-reward and the discipline rules. This indicator's job
is to make you take *fewer, better* trades, not to predict the future.

**About a sub-$10 live account:** minimum lot sizes and spread make proper risk management
nearly impossible at that balance. Prove the checklist works for you on your Fusion Markets
**demo account** first — at least 20–30 trades following every rule (one trade per week
per pair, fixed SL, minimum 1:2 RR, session window) — before risking live money.
