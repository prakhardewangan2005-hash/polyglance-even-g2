# PolyGlance G2

**Polymarket odds and Hyperliquid paper positions on Even Realities G2, readable in one second.**

Live demo: https://prakhardewangan2005-hash.github.io/polyglance-even-g2/
Repo: https://github.com/prakhardewangan2005-hash/polyglance-even-g2

Built for *Heads Up: Even Realities Hackathon* (TVM Ventures x Daos Hub), Crypto & DeFi Track.

> Read-only live data. Paper trading only. No wallets, no keys, no real funds.

## G2 UX design (576x288 monochrome)

- Phosphor green (#00FF66) on pure black (#000) suits an optical waveguide display.
- One idea per screen, a monospace face, and no decoration.
- No camera and no speaker. Input is the R1 Ring, Temple Tap and the microphone only.

| Input | Action |
|---|---|
| R1 Ring Up / Down | Move through markets, positions or voice presets |
| R1 Ring Click | Cycle the option (YES/NO and $25/$50/$100, or Trim/Close) |
| Temple Tap | Confirm |
| Temple Long-Press | Back / cancel |
| Mic | Voice command |
| Left / Right | Switch view |

Keyboard: arrows, Enter, Esc, Space, and T for Temple Tap.

## Views

1. **Polymarket odds:** top markets by 24h volume, with YES/NO %, volume and a quick paper bet.
2. **Hyperliquid paper positions:** BTC, ETH and SOL perps with mark price, unrealized PnL and leverage. Trim 50% or Close, each behind a confirm card.
3. **Voice and quick confirm:** Web Speech API plus 4 presets. Commands become a 2-line card: `CONFIRM: $50 YES?` / `[TAP = YES | HOLD = NO]`. An activity log records every action.

## Integrations (read-only)

- Polymarket Gamma: `GET https://gamma-api.polymarket.com/markets?active=true&closed=false&limit=8&order=volume24hr&ascending=false`
- Hyperliquid info: `POST https://api.hyperliquid.xyz/info` with `{"type":"allMids"}`

If either call fails (for example because of CORS), the app uses curated sample data and shows a FALLBACK badge. The demo always works.

## Paper-trading safety rules

- No order, signing or wallet endpoints are ever called.
- Max $100 per paper bet. Max $300 total paper exposure. Starting paper balance is $1,000.
- Every trade needs an explicit Temple Tap. Long-press or Esc cancels.
- Voice commands are parsed locally. Invalid or over-limit requests are rejected and logged.

## Even Hub simulator architecture

A single `index.html` with no build step. The lens is a 576x288 DOM canvas. Every hardware event (ring, tap, long-press, mic, keyboard) maps to one `act()` function, so the same logic can run in the Even Hub WebView. The app.json preview in the page is illustrative, so verify it against the current SDK docs.

## Run locally

Open `index.html` in a browser, or serve it with `python3 -m http.server`.

## License

MIT
