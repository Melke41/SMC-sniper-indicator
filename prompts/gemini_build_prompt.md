# SMC Sniper — Pine Script Build Prompt
# Paste everything below into Gemini 2.5 Flash at aistudio.google.com

---

## ROLE

You are an expert Pine Script v5 developer specializing in Smart Money Concepts (SMC) and ICT-based trading indicators for TradingView. You write clean, non-repainting, production-ready Pine Script code.

---

## TASK

Build a complete multi-timeframe SMC × Price Action confluence indicator in Pine Script v5.
The indicator works on the 15-minute chart while automatically pulling data from Daily, 4H, 1H, and 30m using request.security().

---

## STRATEGY

Top-down CRT-based SMC reversal strategy.
Instruments: XAUUSD, EURUSD, ETHUSDT.
Trade ONLY exists after a Daily CRT sweep.

---

## ENTRY SEQUENCE

### STEP 1 — Daily (Bias)
- CRT High Sweep: price sweeps above prior Daily High (N=5 lookback, adjustable) → BEARISH
- CRT Low Sweep: price sweeps below prior Daily Low → BULLISH
- Bearish DFVG: candle[2].high < candle[0].low with bearish momentum
- Bullish DFVG: candle[2].low > candle[0].high with bullish momentum
- Daily CRT Sweep + DFVG rejection = HTF bias confirmed

### STEP 2 — 4H (Structure + S&R)
- Detect most recent 4H FVG aligned with bias
- Detect major S&R levels using ta.pivothigh() and ta.pivotlow() on 4H with lookback=10
- Keep last 5 pivot highs (resistance) and 5 pivot lows (support)
- If price is within 0.2% of a stored pivot = "at S&R level"
- If price was at S&R and moving away = "S&R rejection confirmed"
- Draw S&R levels as horizontal lines labeled "R" or "S"

### STEP 3 — 1H (MSS + OB)
- Bearish MSS = price breaks below most recent 1H Higher Low
- Bullish MSS = price breaks above most recent 1H Lower High
- Bearish OB = last bullish candle before bearish MSS break candle
- Bullish OB = last bearish candle before bullish MSS break candle

### STEP 4 — 30m (Refine)
- 30m OB nested inside 1H OB zone
- ICT Killzones:
  - London: 02:00–05:00 UTC
  - NY AM: 07:00–10:00 UTC
  - NY PM: 13:00–16:00 UTC
  - Asian = invalid

### STEP 5 — 15m (Entry)
- Price taps OB or DFVG zone
- Rejection candle: wick > 60% of range, or engulfing, or pin bar

---

## CONFLUENCE SCORE (8 points)

1. Daily CRT Sweep confirmed (1D)
2. Daily DFVG rejection (1D)
3. 4H FVG in bias direction (4H)
4. Price rejecting major 4H/Daily S&R level (4H/1D)
5. 1H MSS/CHoCH confirmed (1H)
6. Inside valid ICT Killzone (30m/15m)
7. Price tapping OB or DFVG zone (15m)
8. 15m rejection candle present (15m)

Score 6-8 = TAKE THE TRADE (green signal)
Score 4-5 = WAIT (orange signal)
Score 0-3 = SKIP (no signal)

---

## VISUALS ON CHART

1. Daily DFVG zone — dashed rectangle (red bearish / blue bullish)
2. 4H FVG zone — semi-transparent rectangle (orange)
3. Major S&R lines — solid horizontal lines extending right (red=resistance, green=support) labeled "R" / "S"
4. 1H OB zone — semi-transparent box labeled "1H OB"
5. 30m OB zone — smaller box inside 1H OB labeled "30m OB"
6. Entry arrow — red down arrow (sell) or green up arrow (buy) when score >= 6
7. Score label — next to arrow: "7/8 SELL" or "6/8 BUY"
8. Killzone background — London=light blue, NY AM=light yellow, NY PM=light purple, Asian=none
9. Bias label — top right: "BIAS: BEARISH" or "BIAS: BULLISH"
10. S&R rejection dot — small circle on candle when S&R rejection occurs

---

## ALERTS

1. "SMC Sniper — SELL Signal" when score >= 6 and bearish
2. "SMC Sniper — BUY Signal" when score >= 6 and bullish
3. "SMC Sniper — Setup Forming" when score = 4 or 5
4. "SMC Sniper — CRT Sweep Detected" on Daily sweep
5. "SMC Sniper — S&R Rejection" on major S&R rejection

---

## USER INPUTS

- CRT Sweep Lookback: default 5
- Show Daily DFVG Zone: bool, default true
- Show 4H FVG Zone: bool, default true
- Show Major S&R Lines: bool, default true
- S&R Pivot Lookback: default 10
- S&R Touch Threshold %: default 0.2
- Show 1H OB Zone: bool, default true
- Show 30m OB Zone: bool, default true
- Show Killzone Background: bool, default true
- Min Score for Signal: default 6
- Rejection Wick Ratio: default 0.6
- London Hours UTC: default 2 to 5
- NY AM Hours UTC: default 7 to 10
- NY PM Hours UTC: default 13 to 16

---

## PINE SCRIPT RULES

1. NO REPAINTING — request.security() with lookahead=barmerge.lookahead_off
2. Use var for persistent variables
3. No security() inside loops
4. Use box.new() for zones, delete old ones, keep only most recent per type
5. Pine Script v5: //@version=5, use indicator() not study()
6. Add strategy comment block at top
7. Keep under 600 lines
8. Confirmed bars only in all HTF calls

---

## OUTPUT

Return:
1. Complete Pine Script v5 code in one code block
2. TradingView setup instructions
3. How to set alerts
4. Recommended chart settings
5. Known limitations

---

## NOTES

- Complements LuxAlgo ICT Killzones Toolkit and AsianRange Nico948
- REVERSAL strategy — always counter to sweep direction
- S&R levels are auto-detected via pivot logic (proxy for trader's manual lines)
- Quality over quantity — fewer signals, higher accuracy

---

Build the full Pine Script v5 indicator now.
