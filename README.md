# SMC Sniper Indicator

A multi-timeframe Smart Money Concepts (SMC) × Price Action confluence indicator for TradingView (Pine Script v5).

## Strategy Overview

Top-down CRT-based SMC reversal strategy. Trade only exists when a Daily CRT sweep occurs.

**Instruments:** XAUUSD · EURUSD · ETHUSDT

## Timeframe Stack

| Timeframe | Role |
|-----------|------|
| Daily (1D) | Bias — CRT sweep + DFVG rejection |
| 4H | Structure — FVG + major S&R levels |
| 1H | Setup — MSS/CHoCH + 1H OB |
| 30m | Refine — 30m OB + killzone timing |
| 15m | Entry — DFVG rejection candle |

## Core Confluences (8-Point Score)

| # | Confluence | Timeframe |
|---|-----------|-----------|
| 1 | Daily CRT High/Low Sweep | 1D |
| 2 | Daily DFVG rejection | 1D |
| 3 | 4H FVG in bias direction | 4H |
| 4 | Major 4H/Daily S&R rejection | 4H/1D |
| 5 | 1H MSS / CHoCH confirmed | 1H |
| 6 | Inside ICT Killzone | 30m |
| 7 | Price tapping OB or DFVG | 15m |
| 8 | 15m rejection candle | 15m |

**Score 6–8 = Take the trade · 4–5 = Wait · 0–3 = Skip**

## ICT Killzones (UTC)

- London: 02:00–05:00
- New York AM: 07:00–10:00
- New York PM: 13:00–16:00
- Asian = NO ENTRY

## Project Structure

```
smc-sniper-indicator/
├── src/
│   └── SMC_Sniper.pine          ← Main Pine Script (complete implementation)
├── docs/
│   └── strategy_rules.md        ← Full strategy documentation
├── prompts/
│   └── gemini_build_prompt.md   ← AI build prompt for Gemini 2.5 Flash
└── examples/
    └── trade_examples.md        ← Annotated real trade examples
```

## How to Use

1. Open TradingView → Pine Editor
2. Paste contents of `src/SMC_Sniper.pine`
3. Click **Add to chart**
4. Set chart to **15m timeframe**
5. The indicator auto-pulls Daily, 4H, 1H, 30m data

## Alerts

- `SMC Entry Signal — SELL`
- `SMC Entry Signal — BUY`
- `SMC Setup Forming — Watch`
- `CRT Sweep Detected`
- `Major S&R Rejection`

## Tools Used Alongside

- LuxAlgo ICT Killzones Toolkit
- AsianRange Nico948

## Versions

- v1.0 — Initial structure + complete indicator logic
