# Changelog

All notable changes to this project are documented in this file.

---

## v1.0 (2026-02-27) -- Market Monitor 5m

- New 5-minute optimized Market Monitor variant with weighted directional bias scoring.
- Weighted scoring engine: structural conditions (EMA alignment, VWAP position, Anchor EMA) score 2x; confirmation conditions (RSI, DI, HTF, TICK, Squeeze momentum) score 1x. Configurable toggle between weighted and equal modes.
- Bias score range expanded to +/-11 (weighted) or +/-8 (equal) vs the general-purpose monitor's +/-5.
- Session phase detection: Open Drive / Morning / Midday / Power Hour / Close classification based on Eastern Time.
- TTM Squeeze integration with BB/KC compression detection, three-state classification, momentum direction, and bars-since-fired tracking.
- NYSE TICK Index integration with six-tier breadth classification and configurable thresholds.
- ATR regime classification via percentile ranking (LOW / NORMAL / HIGH / EXTREME) over configurable lookback.
- Prior Day VWAP latched from previous session close and plotted as reference level.
- 15-minute Anchor EMA (50 EMA) plotted as institutional trend reference line.
- Opening Range levels with configurable duration (default 15 min / 3 bars on 5m).
- Session HOD/LOD real-time tracking with dashboard position context.
- Bias trend tracking (IMPROVING / STABLE / FADING) via 3-bar SMA comparison.
- Expanded 18-row dashboard with session phase, squeeze state, TICK readings, OR position, and session context.
- 9 alert conditions including squeeze fired, TICK extremes, and adaptive strong bias thresholds.
- 4 `request.security` calls total — within headroom for 8+ simultaneous instances.

---

## v1.0 (2026-02-24) -- Market Monitor 1m

- General-purpose directional-bias overlay for multi-chart watchlist monitoring (6-8 charts per window).
- Timeframe-adaptive design: works from 1-minute through Daily without reconfiguration. VWAP auto-disables on Daily+ charts; bias engine swaps price anchor from VWAP to slow EMA accordingly.
- EMA Ribbon (9 / 21 / 50) with dynamic cloud fill — deliberately wider than the 0DTE scalper variants to provide meaningful trend context across timeframes.
- Session-anchored VWAP with configurable standard deviation bands and automatic intraday detection.
- Previous Day High / Low / Close reference levels via `request.security` on the Daily timeframe.
- Composite directional bias score (-5 to +5) from 5 equal-weighted binary conditions: EMA alignment, price vs VWAP/anchor, RSI bias, DI spread, and HTF EMA confirmation.
- HTF EMA confirmation layer with automatic timeframe mapping (1m→5m, 5m→15m, 15m→1H, etc.).
- Relative volume gauge (20-period SMA baseline) with SPIKE / ABOVE / BELOW classification.
- Optional background tint (94% transparency) triggered at configurable bias score threshold.
- Compact 12-row dashboard with three size options (Tiny / Small / Normal) and four corner positions.
- 6 alert conditions: strong bullish/bearish bias, bias crossed neutral, volume spike, RSI overbought/oversold.
- 3 `request.security` calls total — lightweight footprint for 8+ simultaneous instances.
- No signal generation — pure context and bias assessment. No loops, arrays, or maps; fully vectorized.

---

## v1.1 (2026-02-20) -- All Scalper Variants

- TTM Squeeze detection with three-state classification and momentum histogram.
- NYSE TICK Index integration with six-tier breadth classification.
- Expanded dashboard rows for squeeze and TICK status.
- New alert conditions for squeeze fired events.
- Enhanced dynamic alert messages with squeeze and TICK context.

**1-Minute specific**: Squeeze and TICK added as optional AND-gate filters (default OFF). VWAP cross markers added.

**5-Minute specific**: Squeeze recency and TICK breadth added as scoring conditions #8 and #9 in the 5+4 engine. Level proximity added as scoring condition #7. Expanded candle pattern detection (inside bar breakout, 3-bar momentum).

**15-Minute specific**: Integrated into scoring and directional bias system with timeframe-appropriate calibration.

---

## v1.0 (2026-02-18) -- Initial Release

- EMA Ribbon with dynamic cloud fill.
- Session-anchored VWAP with standard deviation bands.
- RSI, ADX/DMI, ATR calculations with dashboard display.
- Pre-market high/low, prior day H/L/C, opening range, session HOD/LOD levels.
- Five-mode regime classifier.
- Signal engine (AND-gate for 1-min, scoring for 5-min and 15-min).
- CALLS/PUTS labels with tooltips, arrow shapes, background flash.
- Real-time dashboard with color-coded status indicators.
- Dual alert system (alertcondition + dynamic alert).
- Market Monitor v1.0 with composite bias scoring (-5 to +5).
