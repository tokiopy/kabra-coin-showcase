<div align="center">

# Kabra Coin

### Landing page para la primera memecoin de Punta Cana, República Dominicana. Construida sobre Solana.

Precio en vivo · Trading Chart · Exchanges · YouTube dinámico · Chat IA · Tokenomics

[![Live Site](https://img.shields.io/badge/Visit_Live-kabracoin.com-00D4C4?style=for-the-badge&logo=solana&logoColor=white)](https://kabracoin.com/)
[![Status](https://img.shields.io/badge/Status-Production-22c55e?style=for-the-badge)](https://kabracoin.com/)
[![Solana](https://img.shields.io/badge/Blockchain-Solana-9945FF?style=for-the-badge&logo=solana&logoColor=white)](https://solana.com/)

</div>

---

## What is this?

**Kabra Coin ($KABRA)** es la primera memecoin comunitaria de Punta Cana, República Dominicana, desplegada en la blockchain de Solana. Este repositorio es la landing page oficial del proyecto: una web de una sola página que informa, integra datos en tiempo real y conecta a la comunidad con los exchanges donde opera el token.

El sitio no es una vitrina estática. Tiene precios en vivo, un chart de trading embebido, una galería de videos cargada dinámicamente desde YouTube, y un widget de chat con IA construido sobre n8n.

> 🌐 **Live:** [kabracoin.com](https://kabracoin.com/) · ⛓️ Solana · 🌴 Punta Cana, RD

---

## Secciones

### 📊 Price Ticker

Barra fija en la parte superior con precios en tiempo real de $KABRA, BTC, ETH y SOL. Se actualiza cada 30 segundos sin recargar la página.

- **$KABRA:** precio obtenido de DexScreener API (`/latest/dex/tokens/{contract}`) — la fuente correcta para tokens en DEXs de Solana
- **BTC / ETH / SOL:** CoinGecko API con variación 24h
- **Animación:** ticker horizontal con CSS `transform` y `requestAnimationFrame` — sin librerías de animación
- **Indicadores de color:** verde/rojo automático según variación 24h positiva o negativa

---

### 🦸 Hero

Video de fondo a pantalla completa con el branding del proyecto. CTA directo a Pump.fun para compra inmediata.

---

### 📖 About

Presentación del proyecto: origen en Punta Cana, visión comunitaria, contrato en Solana. Botón de copia del contract address con feedback visual (icono cambia a checkmark al copiar, usando Clipboard API con fallback a `execCommand`).

---

### 📈 Trading Chart

Chart de trading en vivo embebido directamente desde DexScreener. Par $KABRA/SOL en Solana mainnet. El embed incluye theme dark, sin panel de trades ni info lateral para una UX más limpia.

Links secundarios a DexScreener y Pump.fun para operaciones directas.

---

### 💱 Exchanges

Cards con los exchanges donde $KABRA opera actualmente:

- **DexScreener** — análisis y trading
- **Pump.fun** — plataforma de lanzamiento y trading
- **Gate.io** — exchange centralizado
- **OKX Web3** — wallet y DEX agregador
- **Streamflow** — vesting y contratos de distribución

---

### 🎬 Video Gallery

Galería dinámica cargada desde YouTube Data API v3. Muestra los últimos 6 videos del canal oficial, con miniaturas, títulos truncados y timestamps relativos ("hace 3 días").

- **Carga dinámica:** fetch al canal vía API, no videos hardcodeados
- **Video principal:** click en miniatura reemplaza el embed principal sin recargar
- **Fallback:** si la API falla, carga un set manual de videos conocidos
- **Timestamps relativos:** función custom que convierte fechas ISO a "hace X días/semanas/meses"

---

### 👥 Equipo

Presentación del equipo fundador con fotos, roles y redes sociales.

---

### 🔢 Tokenomics

Distribución del supply con stats de Streamflow (vesting contract verificable on-chain).

---

### 🌐 Comunidad

Links a todos los canales de la comunidad: X (Twitter), Instagram, YouTube, Telegram.

---

### 💬 Chat IA (n8n)

Widget flotante de chat conectado a un workflow de n8n vía webhook. El bot responde preguntas sobre $KABRA, el proyecto y cómo comprar. Se abre como overlay sin salir de la página.

- **Backend:** n8n self-hosted en Easypanel
- **UX:** botón flotante → overlay con iframe → cierre con Escape o botón ✕
- **Accesibilidad:** `role="dialog"`, `aria-modal`, `aria-label` correctos

---

## Stack

<div align="center">

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript_ES6+-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![Solana](https://img.shields.io/badge/Solana-9945FF?style=for-the-badge&logo=solana&logoColor=white)
![n8n](https://img.shields.io/badge/n8n-EA4B71?style=for-the-badge&logo=n8n&logoColor=white)

</div>

- **HTML5 + CSS3 + Vanilla JS (ES6+):** sin framework, sin build step
- **APIs:** DexScreener, CoinGecko, YouTube Data API v3
- **Embeds:** DexScreener trading chart
- **Automatización:** n8n self-hosted (Easypanel) para el chat IA
- **Hosting:** Hostinger (deploy por FTP)
- **Iconos:** Font Awesome 6.4

---

## Decisiones de ingeniería

### 🎯 Sin framework, a propósito

Una landing page de memecoin tiene un ciclo de vida corto y alta volatilidad de contenido. No tiene sentido introducir un framework con su ecosistema de dependencias para un sitio que en el peor caso se reescribe en semanas. HTML + CSS + JS nativo despliega con un upload, tiene cero dependencias que actualizar, y cualquier dev puede leerlo y modificarlo sin onboarding.

### 📊 DexScreener sobre CoinGecko para $KABRA

CoinGecko no indexa tokens recientes o de bajo market cap de forma confiable. DexScreener sí rastrea cualquier par activo en Solana desde el primer trade. Para el precio de $KABRA, DexScreener es la fuente correcta: da precio, volumen 24h y liquidez del par real.

### 🎬 YouTube API dinámica sobre videos hardcodeados

Si el canal sube un video nuevo, la galería lo muestra automáticamente sin tocar el código. El fallback manual asegura que si la API falla o llega al límite de cuota, el usuario igual ve contenido. Es el mismo trade-off que apliqué en otros proyectos: las UIs no deberían depender de que las APIs externas siempre funcionen.

### 🤖 n8n para el chat

El chat necesitaba responder preguntas específicas sobre $KABRA (precio, cómo comprar, tokenomics). Una integración directa con OpenAI/Claude requería un servidor propio para proteger las API keys. n8n self-hosted resuelve eso: el workflow vive en el servidor, el frontend solo hace fetch a un webhook. Cambiar el comportamiento del bot es editar el workflow de n8n, no tocar el código del sitio.

---

## Acerca del proyecto

Diseñado y desarrollado por [@tokiopy](https://github.com/tokiopy) para el equipo de **Kabra Coin**, la primera memecoin comunitaria de Punta Cana, República Dominicana.

**Estado:** Production · [kabracoin.com](https://kabracoin.com/)

---

## Otros proyectos

- **[BitcoinLab Bolivia](https://github.com/tokiopy/bitcoinlab-bolivia-showcase):** plataforma de educación Bitcoin con 7 herramientas integradas
- **[Satoshi's Playroom](https://github.com/tokiopy/satoshis-playroom-showcase):** plataforma de gaming Bitcoin con Dominó, Póker y Ajedrez sobre Lightning Network

---

## Contacto

- 💬 **GitHub:** [@tokiopy](https://github.com/tokiopy)
- 📧 **Email:** info@tokiohub.com

---

<div align="center">

**From Tokio With ⚡**

</div>
