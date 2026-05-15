<div align="center">

# Kabra Coin

### Landing page for the first memecoin from Punta Cana, Dominican Republic. Built on Solana.

Live Price · Trading Chart · Exchanges · Dynamic YouTube · AI Chat · Tokenomics

[![Live Site](https://img.shields.io/badge/Visit_Live-kabracoin.com-00D4C4?style=for-the-badge&logo=solana&logoColor=white)](https://kabracoin.com/)
[![Status](https://img.shields.io/badge/Status-Production-22c55e?style=for-the-badge)](https://kabracoin.com/)
[![Solana](https://img.shields.io/badge/Blockchain-Solana-9945FF?style=for-the-badge&logo=solana&logoColor=white)](https://solana.com/)

![Landing](screenshots/01-landing.jpg)

</div>

---

## What is this?

**Kabra Coin ($KABRA)** is the first community memecoin from Punta Cana, Dominican Republic, deployed on the Solana blockchain. This repository is the project's official landing page. A single-page site that informs, integrates real-time data, and connects the community with the exchanges where the token trades.

The site is not a static showcase. It has live prices, an embedded trading chart, a video gallery loaded dynamically from YouTube, and an AI chat widget built on n8n.

> 🌐 **Live:** [kabracoin.com](https://kabracoin.com/) · ⛓️ Solana · 🌴 Punta Cana, Dominican Republic

---

## Sections

### 📊 Price Ticker

Fixed bar at the top with real-time prices for $KABRA, BTC, ETH, and SOL. Updates every 30 seconds without reloading the page.

- **$KABRA:** price fetched from DexScreener API (`/latest/dex/tokens/{contract}`), the right source for tokens on Solana DEXs
- **BTC / ETH / SOL:** CoinGecko API with 24h change
- **Animation:** horizontal ticker with CSS `transform` and `requestAnimationFrame`, no animation libraries
- **Color indicators:** automatic green/red based on positive or negative 24h change

---

### 📈 Trading Chart

Live trading chart embedded directly from DexScreener. $KABRA/SOL pair on Solana mainnet.

![Trading Chart](screenshots/02-chart.jpg)

- **Auto-recovery:** automatically reloads when returning to the tab (Page Visibility API) and every 5 minutes to keep the WebSocket connection alive
- **Manual reload button** to force refresh without reloading the page

---

### 💱 Exchanges

Cards for the exchanges where $KABRA currently trades.

![Exchanges](screenshots/03-exchanges.jpg)

- DexScreener, Pump.fun, Gate.io, OKX Web3, Streamflow (vesting)

---

### 🎬 Video Gallery

Dynamic gallery loaded from the YouTube Data API v3. Shows the latest 6 videos from the official channel.

![Video Gallery](screenshots/04-videos.jpg)

- **Dynamic loading:** fetches the channel via API, no hardcoded videos
- **Main video:** clicking a thumbnail replaces the main embed without reloading
- **Fallback:** if the API fails, loads a manual set of known videos
- **Relative timestamps:** "3 days ago", "2 weeks ago", etc.

---

### 🔢 Tokenomics

Supply distribution with Streamflow stats (on-chain verifiable vesting contract).

![Tokenomics](screenshots/05-tokenomics.jpg)

---

### 💬 AI Chat (n8n)

Floating chat widget connected to an n8n workflow via webhook. The bot answers questions about $KABRA, the project, and how to buy.

![Chat](screenshots/06-chat.jpg)

- **Backend:** self-hosted n8n on Easypanel
- **UX:** floating button opens an overlay with an iframe, closes with Escape or the close button

---

## Tech Stack

<div align="center">

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript_ES6+-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![Solana](https://img.shields.io/badge/Solana-9945FF?style=for-the-badge&logo=solana&logoColor=white)
![n8n](https://img.shields.io/badge/n8n-EA4B71?style=for-the-badge&logo=n8n&logoColor=white)

</div>

- **HTML5 + CSS3 + Vanilla JS (ES6+):** no framework, no build step
- **APIs:** DexScreener, CoinGecko, YouTube Data API v3
- **Embeds:** DexScreener trading chart with auto-recovery
- **Automation:** self-hosted n8n (Easypanel) for the AI chat
- **Hosting:** Hostinger VPS with deploy via GitHub
- **Icons:** Font Awesome 6.4

---

## Engineering Decisions

### 🎯 No framework, on purpose

A memecoin landing page has a short lifecycle and high content volatility. There is no reason to introduce a framework with its dependency ecosystem for a site that might be rewritten in days. Vanilla HTML + CSS + JS deploys with a `git push`, has zero dependencies to update, and any developer can read it without onboarding.

### 📊 DexScreener over CoinGecko for $KABRA

CoinGecko does not reliably index recent or low market cap tokens. DexScreener tracks any active pair on Solana from the first trade. For $KABRA's price, DexScreener is the right source. It returns price, 24h volume, and real pair liquidity.

### 🔄 Chart auto-recovery

DexScreener embeds use WebSocket internally. When the tab goes to the background, the WebSocket drops and the chart gets stuck on "Loading pair..." without reconnecting. The fix uses the Page Visibility API to reload the iframe when returning to the tab, plus a 5-minute interval as an additional safety net.

### 🎬 Dynamic YouTube API

When the channel publishes a new video, the gallery shows it automatically without touching the code. The manual fallback ensures that if the API fails or hits its quota limit, the user still sees content.

### 🤖 n8n for the chat

The chat needed to answer specific questions about $KABRA. A direct LLM integration would have required a server to protect the API keys. Self-hosted n8n solves that. The workflow lives on the server and the frontend only fetches a webhook.

---

## About the project

Designed and developed by [@tokiopy](https://github.com/tokiopy) for the **Kabra Coin** team, the first community memecoin from Punta Cana, Dominican Republic.

**Status:** Production · [kabracoin.com](https://kabracoin.com/)

---

## Other projects

- **[BitcoinLab Bolivia](https://github.com/tokiopy/bitcoinlab-bolivia-showcase):** Bitcoin education platform with 7 integrated tools
- **[Satoshi's Playroom](https://github.com/tokiopy/satoshis-playroom-showcase):** Bitcoin gaming platform with Domino, Poker, and Chess on Lightning Network

---

## Connect

- 💬 **GitHub:** [@tokiopy](https://github.com/tokiopy)
- 📧 **Email:** info@tokiohub.com

---

<div align="center">

**From Tokio With ⚡**

</div>
