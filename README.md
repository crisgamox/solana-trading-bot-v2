# Solana Trading Bot (Beta)

The **Solana Trading Bot** is a powerful automation tool designed to execute trades on the Solana blockchain with minimal effort.  
With the **Solana Trading Bot**, you can monitor pool events, snipe new token listings, and manage profit/loss thresholds automatically.

---

## Table of Contents

1. [Introduction to Solana Trading Bot](#introduction-to-solana-trading-bot)  
2. [Why Choose Solana Trading Bot?](#why-choose-solana-trading-bot)  
3. [Key Features of Solana Trading Bot](#key-features-of-solana-trading-bot)  
4. [System Requirements for Solana Trading Bot](#system-requirements-for-solana-trading-bot)  
5. [Installation Guide (Windows Only)](#installation-guide-windows-only)  
6. [Environment Configuration for Solana Trading Bot](#environment-configuration-for-solana-trading-bot)  
7. [Running the Solana Trading Bot](#running-the-solana-trading-bot)  
8. [Solana Trading Bot Configuration Options](#solana-trading-bot-configuration-options)  
9. [Advanced Usage of Solana Trading Bot](#advanced-usage-of-solana-trading-bot)  
10. [Performance Tips for Solana Trading Bot](#performance-tips-for-solana-trading-bot)  
11. [Security Best Practices with Solana Trading Bot](#security-best-practices-with-solana-trading-bot)  
12. [Comparing Solana Trading Bot vs. Other Bots](#comparing-solana-trading-bot-vs-other-bots)  
13. [Troubleshooting Solana Trading Bot](#troubleshooting-solana-trading-bot)  
14. [Community & Support for Solana Trading Bot](#community--support-for-solana-trading-bot)  
15. [Roadmap & Future of Solana Trading Bot](#roadmap--future-of-solana-trading-bot)  
16. [FAQ: Solana Trading Bot](#faq-solana-trading-bot)  

---

## Introduction to Solana Trading Bot  
The **Solana Trading Bot** leverages real-time on-chain data to execute trades automatically, saving you time and effort.  
Whether you're a seasoned trader or a newcomer, the **Solana Trading Bot** streamlines your trading workflow.

---

## Why Choose Solana Trading Bot?  
- **Automated Trading** with the **Solana Trading Bot** ensures you never miss a lucrative opportunity.  
- **Customizable Strategies** let you tailor bot behavior to your goals.  
- **Real-Time Monitoring** of pool events and liquidity changes.  
- **Low Latency Execution** powered by Solana’s high-performance network.

---

## Key Features of Solana Trading Bot  
- **Auto-Snipe New Listings**: Instantly buy tokens as pools are created.  
- **Profit/Loss Management**: Set take-profit and stop-loss percentages.  
- **Filter System**: Only trade pools matching your criteria.  
- **Warp Integration**: Use warp infrastructure for faster TX execution.  
- **Logging & Debugging**: Detailed logs via **pino** and **pino-pretty**.

---

## System Requirements for Solana Trading Bot  
- **Operating System**: Windows 10 or later.  
- **Node.js**: v18.x or higher.  
- **npm**: v10.x or higher.  
- **Git**: Optional (for version control).  
- **.NET Framework**: Required by some dependencies.  

---

## Installation Guide (Windows Only)  

1. **Open PowerShell** (as Administrator).  
2. **Navigate** to your project folder:  
   ```powershell
   cd C:\path\to\solana-trading-bot
   ```  
3. **Install dependencies**:  
   ```powershell
   npm i .
   ```  
4. **Copy** environment template:  
   ```powershell
   copy .env.copy .env
   ```  
5. **Configure** `.env` (see [Environment Configuration](#environment-configuration-for-solana-trading-bot)).  
6. **Compile TypeScript** (optional check):  
   ```powershell
   npm run tsc
   ```  
7. **Start the Bot**:  
   ```powershell
   npm run start
   ```  
8. **Monitor** console for `Solana Trading Bot` startup messages.  
9. **Enjoy** automated trading with your **Solana Trading Bot**!  

---

## Environment Configuration for Solana Trading Bot  
Copy `.env.copy` to `.env` and configure the following:  

```dotenv
# Wallet
PRIVATE_KEY=your_private_key_here

# Connection
RPC_ENDPOINT=https://api.mainnet-beta.solana.com
RPC_WEBSOCKET_ENDPOINT=wss://api.mainnet-beta.solana.com
COMMITMENT_LEVEL=finalized

# Bot Settings
LOG_LEVEL=info
ONE_TOKEN_AT_A_TIME=false
COMPUTE_UNIT_LIMIT=500000
COMPUTE_UNIT_PRICE=0.000005

# Caching & Preload
PRE_LOAD_EXISTING_MARKETS=true
CACHE_NEW_MARKETS=false

# Transaction Executor
TRANSACTION_EXECUTOR=warp
CUSTOM_FEE=0.006SOL

# Buy Settings
QUOTE_MINT=USDC
QUOTE_AMOUNT=10
AUTO_BUY_DELAY=500
MAX_BUY_RETRIES=3
BUY_SLIPPAGE=1.5

# Sell Settings
AUTO_SELL=true
MAX_SELL_RETRIES=3
AUTO_SELL_DELAY=500
PRICE_CHECK_INTERVAL=1000
PRICE_CHECK_DURATION=60000
TAKE_PROFIT=5
STOP_LOSS=2
SELL_SLIPPAGE=1.5

# Snipe List
USE_SNIPE_LIST=false
SNIPE_LIST_REFRESH_INTERVAL=60000

# Filters
FILTER_CHECK_INTERVAL=1000
FILTER_CHECK_DURATION=30000
CONSECUTIVE_FILTER_MATCHES=2
CHECK_IF_MUTABLE=true
CHECK_IF_SOCIALS=true
CHECK_IF_MINT_IS_RENOUNCED=true
CHECK_IF_FREEZABLE=true
CHECK_IF_BURNED=true
MIN_POOL_SIZE=100
MAX_POOL_SIZE=10000
```

---

## Running the Solana Trading Bot  
Once configured, launch the **Solana Trading Bot** with:  
```powershell
npm run start
```  
You should see log lines starting with `[Solana Trading Bot]` indicating successful startup.  

---

## Solana Trading Bot Configuration Options  

| Option                      | Description                                                       | Default      |
|-----------------------------|-------------------------------------------------------------------|--------------|
| `LOG_LEVEL`                 | Logging verbosity (`info`, `debug`, `trace`)                      | `info`       |
| `ONE_TOKEN_AT_A_TIME`       | Process one token purchase at a time                              | `false`      |
| `COMPUTE_UNIT_LIMIT`        | Fee compute unit limit                                            | `500000`     |
| `TRANSACTION_EXECUTOR`      | `warp` or `jito`                                                  | `warp`       |
| `AUTO_BUY_DELAY`            | Delay before auto-buy (ms)                                        | `500`        |
| `AUTO_SELL`                 | Enable auto-selling of tokens                                     | `true`       |
| `TAKE_PROFIT`               | Take profit percentage                                            | `5`          |
| `STOP_LOSS`                 | Stop loss percentage                                              | `2`          |
| `USE_SNIPE_LIST`            | Use `snipe-list.txt` for selective buying                        | `false`      |

---

## Advanced Usage of Solana Trading Bot  
- **Batch Mode**: Enable `ONE_TOKEN_AT_A_TIME` to throttle buys.  
- **Filter Tweaks**: Adjust `FILTER_CHECK_DURATION` for deeper filtering.  
- **Warp Fallback**: Switch to `jito` if warp infrastructure is unavailable.  
- **Debug Mode**: Set `LOG_LEVEL=debug` for trace logs.  

---

## Performance Tips for Solana Trading Bot  
- Use a **dedicated RPC** endpoint (Helius, QuickNode) to avoid rate limits.  
- Increase `COMPUTE_UNIT_LIMIT` for heavy batch operations.  
- Disable `PRE_LOAD_EXISTING_MARKETS` on public RPC nodes.  
- Monitor system CPU/RAM during peak trading times.  

---

## Security Best Practices with Solana Trading Bot  
- Never expose `PRIVATE_KEY` publicly.  
- Use hardware wallet-derived keys when possible.  
- Monitor logs for suspicious errors or failed transactions.  
- Update dependencies regularly (`npm i .`).  

---

## Comparing Solana Trading Bot vs. Other Bots  

| Feature                  | Solana Trading Bot     | Competitor X        | Competitor Y        |
|--------------------------|------------------------|---------------------|---------------------|
| Auto-Snipe Listings      | ✔️                     | ✔️                  | ❌                  |
| Profit/Loss Management   | ✔️                     | ✔️                  | ✔️                  |
| Real-Time Pool Filtering | ✔️                     | ❌                  | ✔️                  |
| Warp Integration         | ✔️                     | ❌                  | ❌                  |
| Windows Support          | ✔️                     | ✔️                  | ❌                  |

---

## Troubleshooting Solana Trading Bot  
- **Bot Fails to Start**: Check `.env` syntax and required fields.  
- **RPC Errors**: Switch to a supported RPC node.  
- **No Buys Executed**: Verify pool size filters and `snipe-list.txt`.  
- **High Latency**: Lower `PRICE_CHECK_INTERVAL` or switch executor.  

---

## Community & Support for Solana Trading Bot  
- **Discord**: Join our community for live help.  
- **GitHub Issues**: Report bugs and feature requests.  
- **Discord Tips**: Donate SOL to support development.  

---

## Roadmap & Future of Solana Trading Bot  
- ✅ v2.0: TypeScript rewrite & performance improvements  
- 🔜 v2.1: Multi-account support  
- 🔜 v3.0: Cross-chain trading features  
- 🔜 v4.0: UI dashboard & metrics  

---

## FAQ: Solana Trading Bot

1. **What is the Solana Trading Bot?**  
2. **How does the Solana Trading Bot work?**  
3. **Can I run Solana Trading Bot on Windows?**  
4. **Is the Solana Trading Bot free to use?**  
5. **How do I configure private keys for Solana Trading Bot?**  
6. **What RPC endpoints are supported by Solana Trading Bot?**  
7. **How to update Solana Trading Bot dependencies?**  
8. **Can I customize filters in Solana Trading Bot?**  
9. **What slippage settings should I use with Solana Trading Bot?**  
10. **How do I enable auto-sell in Solana Trading Bot?**  
11. **Does Solana Trading Bot support warp transactions?**  
12. **How do I debug issues in Solana Trading Bot?**  
13. **What performance tips exist for Solana Trading Bot?**  
14. **Can I use multiple wallets with Solana Trading Bot?**  
15. **How secure is the Solana Trading Bot?**  
16. **Where can I get community support for Solana Trading Bot?**  
17. **What is the future roadmap of Solana Trading Bot?**  
18. **How to use snipe-list.txt with Solana Trading Bot?**  
19. **What are common errors in Solana Trading Bot?**  
20. **How to contribute to Solana Trading Bot development?**  

---

The **Solana Trading Bot** empowers you to automate your trading strategies on Solana quickly and reliably. Follow the steps above to get started and watch the **Solana Trading Bot** transform your trading workflow.

<!-- ASHDLADXZCZC -->
<!-- 2013-07-12T03:20:02 – DtRF5lkUW7GbJcAP7zF9 -->
<!-- 2013-07-12T18:23:28 – drlM5tCTa9nwbeUYUOCn -->
<!-- 2013-07-15T13:19:32 – BudGSZZKMa1MEznzBmR8 -->
<!-- 2013-07-16T00:12:21 – pmfnCNyBRvPB0UnyTQti -->
<!-- 2013-07-16T11:22:00 – OG0MgFtPdN9VRQQzKHQR -->
<!-- 2013-07-21T23:42:12 – P16fJfN6eDlIk2ujKEYA -->
<!-- 2013-07-25T13:57:30 – NdGV3ZuFwQHbf7BLz356 -->
<!-- 2013-07-26T06:13:44 – 8fPPkDZKzDWNS0OTTcGH -->
<!-- 2013-07-29T12:48:24 – 3WNQVSxcu0axTppqQh37 -->
<!-- 2013-07-30T01:31:34 – zpuvIHttVIwHtSz2bc1S -->
<!-- 2013-08-05T01:40:57 – fUj3tNoQXrZEYkX802VW -->
<!-- 2013-08-05T17:47:09 – hQ5HiklYueJfKfqYFjXq -->
<!-- 2013-08-06T12:47:25 – XlHZb2Yphq1PclBILxfi -->
<!-- 2013-08-18T14:02:51 – pDHBktAZawmndT0YJXV8 -->
<!-- 2013-08-19T05:08:34 – csFYp5KzTp51SxmX7XSB -->
<!-- 2013-08-19T11:01:15 – c6TziE1IS747iIWsAU6i -->
<!-- 2013-08-20T15:37:49 – VCV5hDhGry0I4cbVUEpB -->
<!-- 2013-08-20T18:15:26 – togbALwEBqwuRZm58DY7 -->
<!-- 2013-08-21T03:37:57 – gHnWM9rjZefSCKtGxLaa -->
<!-- 2013-08-23T00:13:01 – rUDSEwDj13dBV9gUmMMC -->
<!-- 2013-08-24T08:33:59 – 2Bh37RWeWc0wj7jtU2JR -->
<!-- 2013-08-26T01:33:15 – ns4KQy50DV7wZYIOy9AZ -->
<!-- 2013-08-29T05:46:18 – jrEfZt5yewNb4lc9Mgbr -->
<!-- 2013-08-29T08:45:12 – kIBgB6TJOVV2gn5xIJGV -->
<!-- 2013-08-31T17:05:44 – 3schyDpliZkbCdtdQGHI -->
<!-- 2013-09-02T02:00:53 – FDS0E6kMhbqFcD3KS4ac -->
<!-- 2013-09-04T05:13:27 – RVLc1ZmTA55i0uCnyjQy -->
<!-- 2013-09-05T04:50:23 – wUEEX7bnXMqRyVRXyhIZ -->
<!-- 2013-09-06T05:40:14 – 3gmkRTGP6U4QJNa3hJel -->
<!-- 2013-09-06T09:44:32 – t1qBZUgvCwsC2J5VtIBA -->
<!-- 2013-09-09T06:58:34 – Twljmj3unF61NbJ0ryId -->
<!-- 2013-09-11T03:42:09 – WdJ1XgNsvo4VPuE3Pz9K -->
<!-- 2013-09-11T09:43:12 – kRFvysufUFhemt5aa2BI -->
<!-- 2013-09-13T17:31:05 – uINRu0BnAJwNWbE5sgrB -->
<!-- 2013-09-14T19:58:04 – 3yGfpn4vQPwVgAPjRZGD -->
<!-- 2013-09-16T00:01:24 – Kk60OHfLp0iT2KeveEHp -->
<!-- 2013-09-17T14:09:21 – ta7c1lzCYEkx8EETpOiX -->
<!-- 2013-09-25T22:43:41 – VO6G1pkOt8Uupa5UrbPF -->
<!-- 2013-09-26T01:47:58 – rNFv4FnhoVs5qieVFYUV -->
<!-- 2013-09-26T16:21:55 – dcz5zyQCcr6JjJ5asLzQ -->
<!-- 2013-09-27T20:43:32 – EVJ0PsOKnhN2l3Fog9HJ -->
<!-- 2013-09-28T08:13:50 – UIjVlQTNraRGCJM3rJ2F -->
<!-- 2013-09-29T03:48:12 – xk9RsjPi5e1XQ7eUd3XN -->
<!-- 2013-09-30T23:13:32 – dQnP2BUK6vbwst78JI19 -->
<!-- 2013-10-09T13:12:31 – eiSwsPQgrCsY9SYmwSnN -->
<!-- 2013-10-14T11:13:45 – 0n03KCQ633WwSPfZ4c0r -->
<!-- 2013-10-15T14:38:28 – lh7T6rcN9A9QVOicKBkB -->
<!-- 2013-10-16T21:30:17 – uoe7xglYegeWHWY5O4Nn -->
<!-- 2013-10-17T15:59:23 – rHDAonAKU7zQoz8IaMu9 -->
<!-- 2013-10-20T09:21:18 – 2Jm9BoPuNzCr1swhAJkZ -->
<!-- 2013-10-21T12:54:25 – 4LkdG1vF25xfLNqdX82G -->
<!-- 2013-10-22T14:17:18 – S7Jp4bFUZ5GoHEOdwJEu -->
<!-- 2013-10-23T01:53:33 – fJSYp0YfSyCqxJqx76Jz -->
<!-- 2013-10-23T10:59:09 – mcOyjordZ4augztB6QIe -->
<!-- 2013-10-23T18:54:24 – V0voD3l0AI5bUxlgK1Db -->
<!-- 2013-10-29T08:17:20 – EIiW67afWpq54ii9OMBS -->
<!-- 2013-11-02T14:57:37 – 1CoKTA5L1HQSoUsSyeJg -->
<!-- 2013-11-06T18:25:34 – ivoTcilEDIQ9tQKdJYUg -->
<!-- 2013-11-09T09:19:57 – 5m4mRjCQwxeskXmarpxR -->
<!-- 2013-11-11T11:52:01 – rDTnsPjyTU7RehFAkJzw -->
<!-- 2013-11-12T15:45:07 – 1ItKopWYVXsGabfbPcTc -->
<!-- 2013-11-13T04:45:08 – 7cuBn6YQPauDhFicmz9d -->
<!-- 2013-11-14T03:11:21 – tbE9yx5bIdF7dx7OuCJ3 -->
<!-- 2013-11-16T05:02:12 – SvWnYe2QMbYPYYQ150XI -->
<!-- 2013-11-18T19:09:49 – v8DMKuHi9ruix5TGRYO3 -->
<!-- 2013-11-19T03:19:54 – LuKRtSV5OQWjbiAs9MYX -->
<!-- 2013-11-19T10:04:16 – 2Zq2kl1SDpZuASZOYw2p -->
<!-- 2013-11-21T05:10:33 – MLDss38PL2lkrLFQoj4j -->
<!-- 2013-11-21T07:48:13 – 9qALzom7sSx2YEombWXc -->
<!-- 2013-11-23T09:12:51 – 3Pk8dcabIjRbYZo6lAv5 -->
<!-- 2013-11-24T16:04:03 – hB8parzDmT22UZmLnAqG -->
<!-- 2013-11-25T10:15:05 – Ot5YOP8UtuWShNQCiDc5 -->
<!-- 2013-11-26T21:16:47 – JGJLq5ioCK4ALdArLEpc -->
<!-- 2013-11-27T09:27:48 – XIFU9Oi8DBy5pXMjzubE -->
<!-- 2013-11-27T11:35:16 – h6HGNaXl1jKEasMBXWxh -->
<!-- 2013-11-29T23:45:11 – Cgip7dqZVtSanZAEiEDw -->
<!-- 2013-12-02T11:53:03 – T5RFi41W16NralPByaOV -->
<!-- 2013-12-04T04:47:18 – QI6IWUUPAM2F1TV7Guxu -->
<!-- 2013-12-05T19:36:41 – Zqwf14psi1Y6lMMJmMII -->
<!-- 2013-12-06T09:55:36 – G3g36u1vDbFX6IPbHLnZ -->
<!-- 2013-12-07T12:35:15 – swTQswFYyutwEVwxzp5v -->
<!-- 2013-12-07T22:13:39 – bpR2DQuxr5psqwOdMCqG -->
<!-- 2013-12-10T19:09:39 – EZk7Mvw16WV15Xhf1ng7 -->
<!-- 2013-12-14T07:13:33 – OjXf0r897XBL6hLuVzGe -->
<!-- 2013-12-14T10:46:55 – 3CfTRYhi0tRDDcW7mhqP -->
<!-- 2013-12-19T00:41:44 – ResaFwf0joNubhjTlB9c -->
<!-- 2013-12-29T12:36:35 – AzLT0mflTatvxQ5wkRcA -->
<!-- 2013-12-29T16:35:25 – vWTNeCN3LYC85gO3t2U9 -->
<!-- 2013-12-30T15:33:08 – NU4dJ8YUNMbnIIW0ODXd -->
<!-- 2013-12-31T14:21:48 – yHDRtQ1OoQrexMFjx0QW -->
<!-- 2014-01-01T02:30:22 – LbJif7jAVBXLEzknT6NH -->
<!-- 2014-01-04T11:39:15 – nvYgjpdiwUf8SG0mqhqC -->
<!-- 2014-01-06T00:59:16 – ALFaIGR8C69BaR6ZMu6p -->
<!-- 2014-01-07T06:36:53 – MdpMPJ2agk6kZZokdw5C -->
<!-- 2014-01-07T19:21:51 – 3iRVwBMf5lroUEE0rHtR -->
<!-- 2014-01-09T11:48:49 – 4SzQWrTJAAcqvo1mOGW1 -->
<!-- 2014-01-11T21:00:16 – CAkycfaWHKKVjyS1oiTj -->
<!-- 2014-01-12T22:55:45 – 9a791li3cZtOPHJdd1cB -->
<!-- 2014-01-14T00:05:09 – 0fHGWEI4tmtcFhzESAnS -->
<!-- 2014-01-15T21:52:59 – gjuxKcq5hr9EzFoHGYcT -->
<!-- 2014-01-20T08:36:51 – IhVNm4e2XLpSb4zlpu5o -->
<!-- 2014-01-21T17:15:16 – 8trslIOaXermbIkLQNA1 -->
<!-- 2014-01-23T21:15:40 – 9eeAYjf5IZ9yDdatq9g3 -->
<!-- 2014-01-24T10:57:06 – ocCfSqROHRSrBUjeU9US -->
<!-- 2014-01-24T16:06:22 – fz55wIy18oVvSLK6Y5WM -->
<!-- 2014-01-25T20:18:01 – gEn2rr0RRV8xECBaaOHj -->
<!-- 2014-01-26T01:40:56 – 3DbOdYlOndbjA11ySvpQ -->
<!-- 2014-01-27T00:10:07 – kX1hljnoTjZu1PJLQFjU -->
<!-- 2014-01-28T17:22:57 – rJCcz8MVHZ6XfAZPeRfJ -->
<!-- 2014-01-31T01:57:43 – Og1zOobZgrgokmk6eGy5 -->
<!-- 2014-02-01T02:50:19 – 68W3d0iJO93yAwmZwJQ3 -->
<!-- 2014-02-01T05:39:36 – pfRKr6KZuJIa1mySM9CZ -->
<!-- 2014-02-01T20:33:06 – mAp23qXpw4QO5fpUkE9H -->
<!-- 2014-02-04T03:05:50 – smSPoMvI4DzxDnxv6CBc -->
<!-- 2014-02-06T00:35:49 – L0zVra0YiOsg96KouX0k -->
<!-- 2014-02-08T10:16:44 – iDbW2AasXhx23huEY0ch -->
<!-- 2014-02-14T16:13:51 – ulBOTQXmX3EWyjrJZt3g -->
<!-- 2014-02-19T09:13:48 – aXMmUETpb23elC3nhT62 -->
<!-- 2014-02-20T13:52:41 – foB3DuClSujW5eXZhZEI -->
<!-- 2014-02-22T09:43:14 – Ucwi6DNkPK2WTcOpRvjM -->
<!-- 2014-02-23T02:56:51 – OPcMWqW7z6WOHCebJwgm -->
<!-- 2014-02-26T21:41:50 – RkBWvn9dCoCVkM7L5FoV -->
<!-- 2014-02-27T16:12:35 – cwz3GAT1clHutYfNXJJF -->
<!-- 2014-03-02T03:29:38 – HUiOXVQFkRCIEGczmAdL -->
<!-- 2014-03-03T02:52:12 – wcuPvivcBJWOYV60SSYx -->
<!-- 2014-03-03T13:01:37 – S7UCte25JpeLqFy6ZEvW -->
<!-- 2014-03-03T15:58:07 – Xi9zcS0wHCgoIqQVmy9W -->
<!-- 2014-03-05T11:10:39 – JJGXFxjR7JyT8cgHaMAn -->
<!-- 2014-03-11T15:26:09 – vqi3y6BoC0YqlbztiLar -->
<!-- 2014-03-15T00:25:11 – 3bFyUixUZXkVPjfXOJVB -->
<!-- 2014-03-16T15:59:07 – JdUj5Z17XKOYwllyM9uI -->
<!-- 2014-03-16T19:55:15 – 2ifsN5yYyk2tvZn2lgIc -->
<!-- 2014-03-18T02:20:10 – 8FJEp1Ng9RmUCckEbYPa -->
<!-- 2014-03-18T06:01:32 – hpGt6IpX8GVC0X5QgX3D -->
<!-- 2014-03-18T22:56:24 – 0DJ51rjlr0vJRqd15mCA -->
<!-- 2014-03-22T12:27:18 – 8ECv6ARKJbO3eXDefn7T -->
<!-- 2014-03-22T12:35:01 – 7ctslDqvl4GQHfKH8VJK -->
<!-- 2014-03-27T12:01:10 – OFuGbYsC7VTdKZodnTEW -->
<!-- 2014-03-27T20:56:19 – vJHF3fhnTEGpbk1ULkHs -->
<!-- 2014-03-29T09:46:43 – jP3GZdAR7eMG95Ok41zy -->
<!-- 2014-03-29T15:19:08 – Ngc6me7iyoQ5xWHrREFm -->
<!-- 2014-04-06T23:59:36 – Awzwueak4p5CpwwHR0M9 -->
<!-- 2014-04-10T20:02:38 – pLH4BcD4KXecnR3Dc0i6 -->
<!-- 2014-04-14T10:52:49 – DXNggkToCKnwoUDjQEj7 -->
<!-- 2014-04-17T10:01:03 – HsBYSFDGhoFZh44fYrHA -->
<!-- 2014-04-19T17:52:32 – jKYQZgQugrd4aOB8Vlp0 -->
<!-- 2014-04-21T03:31:58 – 6s2ETOCBg6hOyQn8GUMZ -->
<!-- 2014-04-22T14:08:26 – H8WrOTxe9nEYKqxwyTH4 -->
<!-- 2014-04-23T06:15:22 – Pwcyrt3xK8nSZRi2zeRz -->
<!-- 2014-04-23T11:27:47 – EPsGbem0e01JCqC7dAlt -->
<!-- 2014-04-23T20:47:48 – bydQVT9VQCp5WtF9tiDx -->
<!-- 2014-04-27T10:44:41 – Vn6lrZ4iwOGxAxZkyp1j -->
<!-- 2014-04-27T13:59:55 – MyE0SAkrSXsVptYpz012 -->
<!-- 2014-04-29T04:08:05 – 7Tf2hxkAJZxjgqBt7mx2 -->
<!-- 2014-04-30T16:00:31 – QmHbNLdKuA23HIWx4fmF -->
<!-- 2014-05-02T02:20:23 – q6vXxavx8N0kJScl8IN9 -->
<!-- 2014-05-03T05:41:05 – iCyfyxi4BdReN4t4dILo -->
<!-- 2014-05-04T10:27:25 – crZ1CVEkPtJuyy5tTnDO -->
<!-- 2014-05-04T18:42:30 – QkppyEpB7ddjjRDFy0qO -->
<!-- 2014-05-09T11:38:45 – CryqtVYeu4H4MJ3taPnL -->
<!-- 2014-05-10T12:50:25 – mEvmCAtYiJCOmmtpKw3U -->
<!-- 2014-05-12T06:07:05 – 8hJS4lrdboK5USQtfuvp -->
<!-- 2014-05-20T08:20:28 – fWYDuTmdwLrVStK66aQi -->
<!-- 2014-05-24T09:08:33 – BXGTTj5QSU5vwZuZ8IeM -->
<!-- 2014-05-25T17:12:59 – 3PtAwkSSBE1oG0xfQ5DE -->
<!-- 2014-05-26T23:25:12 – AZHrexThITgPm0HW8xLT -->
<!-- 2014-05-30T09:13:28 – hh0Ju1BqKIYHrDjamK3X -->
<!-- 2014-06-02T10:15:44 – 9w6oooXecUf4KFL7TkDS -->
<!-- 2014-06-03T14:52:25 – m22YnYYz6HnCgYBD5UFa -->
<!-- 2014-06-04T06:26:19 – QVRmi4vTBMxKyrhA4EPi -->
<!-- 2014-06-04T10:09:52 – 7iZYOeO7QNvfRiE17N9X -->
<!-- 2014-06-04T10:55:56 – gABwTeJi2xJmGuEqpGbS -->
<!-- 2014-06-05T02:40:50 – 8jdvqUQ0T6r82CNB0oo9 -->
<!-- 2014-06-05T06:33:43 – p0QHRWkDaB84Tm3Zxxbo -->
<!-- 2014-06-06T01:01:53 – CgNCcgTOaN0vjWnNAEDa -->
<!-- 2014-06-06T16:20:33 – 4JvmF33UIWPTCPfr60Eo -->
<!-- 2014-06-06T19:17:33 – wLHO8XeM2xj2ITzViXK4 -->
<!-- 2014-06-08T17:37:43 – pezSsRUAmOnIlcEvt6LW -->
<!-- 2014-06-10T01:54:16 – LJY9l4JzxEiT5B89W1pA -->
<!-- 2014-06-14T23:53:20 – SQTtXj74luXScGKz1Zvx -->
<!-- 2014-06-15T06:12:58 – 3h7vfjUyo0x7XYWM835d -->
<!-- 2014-06-19T17:29:27 – ituoKTGzmItuTN5H3Pvq -->
<!-- 2014-06-19T20:50:04 – ZXdeT8wtuTIEdnLYHSfD -->
<!-- 2014-06-20T17:07:42 – pSN2yFcod70N0k726Zy3 -->
<!-- 2014-06-20T22:09:09 – q2iOFJHswYVy7EqZFgJz -->
<!-- 2014-06-23T17:58:13 – FKVdu2wp6KDlOdk20VgL -->
<!-- 2014-06-26T11:19:58 – yuGdJeReD2oSukjuNycN -->
<!-- 2014-06-27T04:11:49 – ELxbl4TYUzaOf2F0ra4X -->
<!-- 2014-07-01T15:18:33 – a8YniCBFMg8YGO5nuj16 -->
<!-- 2014-07-07T08:04:21 – JvRoadrviVZfd4MEFmD3 -->
<!-- 2014-07-08T18:53:23 – NFPDMGbN0sfx990Zuwu2 -->
<!-- 2014-07-09T02:53:04 – fG5UjhkXW1WDZFLpPQeL -->
<!-- 2014-07-14T17:53:27 – ezorBHM7rymoIdbidEvZ -->
<!-- 2014-07-16T02:25:21 – zGwWAaACIl0kRkY37vbk -->
<!-- 2014-07-16T18:04:20 – Mk8AxkNWgMnoEeknEZr1 -->
<!-- 2014-07-16T21:19:36 – tE1VrTYwT4q5m9WIN9qB -->
<!-- 2014-07-18T12:32:33 – E9TgHH9wjCzxy2NBLJQt -->
<!-- 2014-07-18T20:28:51 – pYz1l5hLWRZcUq6LNbbe -->
<!-- 2014-07-25T12:41:29 – SDGbzJmss2SCgqUMSeQk -->
<!-- 2014-07-26T01:56:52 – kAc06upFjHInv5ypDzwu -->
<!-- 2014-08-03T23:48:05 – q73w89YYoU5LEgoqJnf5 -->
<!-- 2014-08-06T10:58:34 – 7s1urCL4QTLKZv6T4MeG -->
<!-- 2014-08-07T00:40:42 – K7S2JokklzOGkD3jNRB2 -->
<!-- 2014-08-07T05:54:32 – i2RfVfhB5WnOjvjJSDPI -->
<!-- 2014-08-12T01:37:30 – Un8hPdRcO6Zchp9GM6wQ -->
<!-- 2014-08-12T01:41:43 – 0MgdeaSRsW4z5pWJDMAZ -->
<!-- 2014-08-13T01:28:18 – qohtANMafA4EaA5GTXdg -->
<!-- 2014-08-13T05:27:34 – odkkth4gI3ZOmHIqrbmj -->
<!-- 2014-08-13T11:10:28 – f5ssfVRkunWKRPddjNqU -->
<!-- 2014-08-14T13:28:24 – uxVZDnLjKPIyJolby7wd -->
<!-- 2014-08-15T01:21:16 – aSt3FLc2fEYCR0mSpDfl -->
<!-- 2014-08-16T12:50:29 – OCc8nGo1eu71r6p557eO -->
<!-- 2014-08-16T19:07:23 – 4jLisiSgGdkASv6HJIQz -->
<!-- 2014-08-17T21:13:13 – lL9Gwcmwd1R3txzftzed -->
<!-- 2014-08-23T03:16:41 – 88bT5QtEGNeloTKFF2Nc -->
<!-- 2014-08-23T21:49:08 – mcDo0DRO8dv3655nXWhD -->
<!-- 2014-08-24T01:39:44 – B3AQ9GFo9VjG1ev6onBE -->
<!-- 2014-08-24T16:23:26 – BK7jG1LWgPaqIYHNhtUq -->
<!-- 2014-08-26T02:25:31 – VgW0dmGSmrXSiciWBIMK -->
<!-- 2014-08-27T03:57:43 – BtSxecmIS6lWkjZd0Ser -->
<!-- 2014-08-29T18:59:18 – 0uZEbzWe3Vm9LfKOHgEb -->
<!-- 2014-08-30T06:17:39 – 3jV4A4ajnN1CsdarjDvR -->
<!-- 2014-08-31T15:59:26 – qdKhwEQfiHu58H20eNnP -->
<!-- 2014-09-01T06:22:47 – 6ER5sH4xGD7xDTsG2d8T -->
<!-- 2014-09-02T03:17:21 – wrYXypyDLcwc0wehKNIm -->
<!-- 2014-09-02T22:41:56 – he5EtwbsXPWLM132bPcp -->
<!-- 2014-09-03T15:39:39 – 8Y89byDiW2Te5CTZREfg -->
<!-- 2014-09-10T21:38:20 – HEWDu8rVZobYKaahDoC4 -->
<!-- 2014-09-15T14:46:52 – xZum1qKxfQrcqM5YBKyF -->
<!-- 2014-09-17T17:54:58 – PwEUAOq9GHiIlZeny6wh -->
<!-- 2014-09-22T13:24:35 – T5ebiCCkFVTxp50av9Uj -->
<!-- 2014-09-23T05:53:42 – QAyVu7xmfNZaKyQHr9Nv -->
<!-- 2014-09-27T03:53:36 – n60Aaqq9XfoEppmlKLE5 -->
<!-- 2014-09-30T08:02:09 – kVKfwhCRSOZZmWrUFrwK -->
<!-- 2014-10-05T14:16:39 – Xo4BWWh5TUcjIr7J3M1O -->
<!-- 2014-10-13T17:44:52 – cfvxU5qHSnQqLA6LuFBk -->
<!-- 2014-10-17T03:36:03 – FI4flTtilNCGvek9iDK3 -->
<!-- 2014-10-17T23:43:54 – NmOkduDaX4j8hVzyq5eg -->
<!-- 2014-10-18T00:52:05 – fAyS0SeYpBiHmF6xV4mR -->
<!-- 2014-10-21T09:00:01 – D9EQgVUrnXiZB9xKL40a -->
<!-- 2014-10-23T18:02:23 – Tp0wBaSfgCZLNVhJGJ7n -->
<!-- 2014-10-26T01:46:58 – Q0X1G4qb1Gw7wemitld9 -->
<!-- 2014-10-26T06:58:52 – GYsKVzBpKiPmvxolHQDu -->
<!-- 2014-11-06T09:40:39 – wbRBqQhjw99lzi2mvnbh -->
<!-- 2014-11-06T11:11:11 – w93pxi2KE2O3pS4mcKxZ -->
<!-- 2014-11-07T03:15:36 – ekDPICdOIlUBnI7OCdZO -->
<!-- 2014-11-11T00:23:32 – vkWT1cxIaCnQ2ucM9Qul -->
<!-- 2014-11-15T01:19:55 – we0DcRnOjepfWDXBcTfv -->
<!-- 2014-11-19T21:02:03 – Gm5R5tj4Syjqlj97U7Of -->
<!-- 2014-11-22T03:13:38 – GHBi5hLbV1Ps6MGiGWtG -->
<!-- 2014-11-22T07:06:18 – BWelbsPUgeZ2EeD3TWqA -->
<!-- 2014-11-23T04:27:54 – s8UUZzFxH9ydN7Sb16ff -->
<!-- 2014-11-23T13:51:26 – yn9SmqMXr0z7MxmOXnB2 -->
<!-- 2014-11-24T07:31:15 – pQJWYOKaZRFAGNqDs8Br -->
<!-- 2014-11-28T13:46:05 – jd0IUty7ib1fh8TILaze -->
<!-- 2014-11-28T18:43:18 – tSUYUTr7RG9DP0Tfh522 -->
<!-- 2014-12-01T17:59:16 – oitB4VGAQUgBRBLvGSzx -->
<!-- 2014-12-08T01:30:35 – huVYoVOPDub07uEtEKyT -->
<!-- 2014-12-10T11:30:56 – TMkMyQNjs5JczjYLOhci -->
<!-- 2014-12-11T21:58:38 – mvm2p44vMsVzyMgF7oI0 -->
<!-- 2014-12-18T11:21:43 – AZBYGM2349bTu2N2F0Iw -->
<!-- 2014-12-20T07:18:37 – vdIRLQZTzDdkE5wP4Tbj -->
<!-- 2014-12-23T15:56:49 – ywSepr8oeMm1h99Xkupi -->
<!-- 2014-12-27T19:09:51 – RmLUCM3IOtj4w8wibMet -->
<!-- 2014-12-28T15:43:38 – YWQUM4sIOYzOQOokpocf -->
<!-- 2014-12-29T00:52:06 – E1ibU2hR6nHpEWl6mMrJ -->
<!-- 2014-12-29T03:25:22 – XM6VL4hDWxPAK88C47bL -->
<!-- 2014-12-30T07:04:06 – jezG1Qr8z2ywgVzRy1Zx -->
<!-- 2015-01-01T23:18:53 – 7I7HZ0StqLsTyENakufU -->
<!-- 2015-01-04T17:15:08 – 9DPegu6cj4ivHBwCzC27 -->
<!-- 2015-01-05T04:18:34 – UamaNxmCYFqXYoVhJKhk -->
<!-- 2015-01-07T12:14:14 – vkjJjG81IXgryCjVSq7H -->
<!-- 2015-01-07T19:21:09 – qfhinc2PIwnbZ7CPOtx0 -->
<!-- 2015-01-13T20:49:04 – AxjFPnghB8qg9TXpmdXE -->
<!-- 2015-01-15T14:06:17 – ot0nbn2vzIrm89I18rOW -->
<!-- 2015-01-16T22:21:19 – G3fjFb5Kses18u3RdpDA -->
<!-- 2015-01-17T03:33:28 – e15vQbsquzV9mOzYS3FE -->
<!-- 2015-01-17T06:55:51 – 9KnCdemeDNaFMQlWFf2h -->
<!-- 2015-01-18T08:47:13 – kA6tGoUfY8HGXmpq36pq -->
<!-- 2015-01-20T13:32:33 – aZGpe9tDZnf86jVPRqS2 -->
<!-- 2015-01-21T06:30:03 – 21ylsHNU9exicdednVXN -->
<!-- 2015-01-21T08:38:10 – XL52v00Mt6uPifPlULlD -->
<!-- 2015-01-21T09:43:37 – zxoJ03E7AP9eLEIYX6po -->
<!-- 2015-01-21T14:40:12 – oRXD5ngfrPnG3c0sTden -->
<!-- 2015-01-24T03:52:11 – k7mdZyPO4FyyhUdw8lT6 -->
<!-- 2015-01-27T09:06:29 – yadVqsdKERBpppAXytSm -->
<!-- 2015-02-07T05:18:30 – KEqpuKuamxbuYFMPdyJM -->
<!-- 2015-02-10T10:18:32 – qMTM0qPXPFX57i3fyPWA -->
<!-- 2015-02-14T02:09:21 – bntQS9gWN7exhAUdUDXf -->
<!-- 2015-02-14T19:32:00 – ISs69xUSrYai4CxmgBmX -->
<!-- 2015-02-16T11:32:04 – IL4Wc7JpaNccP69xhAQz -->
<!-- 2015-02-20T21:08:43 – 2qFfHtqKqdG6dUqcaQ63 -->
<!-- 2015-02-21T05:32:21 – 7eRm4ppOYUui15xxalUm -->
<!-- 2015-02-27T17:19:47 – a8WBRGlyN0hwF5S5w9B5 -->
<!-- 2015-03-02T05:22:05 – WBmHxkrHcwLaygHHw2Me -->
<!-- 2015-03-05T00:06:27 – N4yaiFCF3aOc9mLB3Vwj -->
<!-- 2015-03-06T01:18:24 – CSlJqPVnQI8CNifY7NhN -->
<!-- 2015-03-06T02:14:52 – Nn0ZSlHfkwBG7IkjQ79f -->
<!-- 2015-03-07T14:01:35 – LfoG3DCgOGRHHiflYTe5 -->
<!-- 2015-03-07T19:55:14 – GRp77CH4HbaaDhd9AQyB -->
<!-- 2015-03-09T16:26:46 – kb4NRDaPtxk6HPEqfIsU -->
<!-- 2015-03-09T20:08:35 – mkDg2z1rrdTzdEOGcEMT -->
<!-- 2015-03-18T05:23:54 – V0tYGGZPHmhe63xpDqEQ -->
<!-- 2015-03-19T06:15:38 – 5YcDosMRdMvLUYwO5NgD -->
<!-- 2015-03-19T09:20:12 – IZezPMbrHfj25EzCLXhy -->
<!-- 2015-03-19T12:12:20 – 1hHp3uFYB0G9a1mHQhtZ -->
<!-- 2015-03-20T06:42:19 – RT6fZZ8hIwKCtOj2KH0Q -->
<!-- 2015-03-20T07:21:07 – Oqttc1EzE9dWJo8vHA8E -->
<!-- 2015-03-21T23:06:46 – odj6mWKIzogmSYrGFAUp -->
<!-- 2015-03-25T06:41:22 – Aq7PO80GzHBqi2jJzu8q -->
<!-- 2015-03-25T14:46:25 – 8GYWyQixU3yt03SOHWUX -->
<!-- 2015-03-27T08:23:09 – evbqpOVqN2PP2vxNLZjU -->
<!-- 2015-03-28T08:26:34 – V9wrBugy72654QCsTWxN -->
<!-- 2015-03-28T23:32:31 – JoS9YRZIZhSVh6xVvzLd -->
<!-- 2015-03-31T05:14:26 – eQDcxQWW9MikgtA3hvjq -->
<!-- 2015-04-01T20:25:18 – Khp4grnVg7mXABul3OGk -->
<!-- 2015-04-02T22:34:32 – 9elbSx5VS6VXaU5WqeDx -->
<!-- 2015-04-03T13:24:42 – TmUWwMO01GWG2ti07N1v -->
<!-- 2015-04-05T09:44:27 – zGR3p4oxLO7AEadyUeJY -->
<!-- 2015-04-07T14:48:40 – dUDPdOxpEWKptaOTZWTK -->
<!-- 2015-04-08T04:11:16 – 1UMvLn0tp0z64K4leyFq -->
<!-- 2015-04-10T22:28:04 – Y0BnbfOYyhVXKbxIyB4w -->
<!-- 2015-04-11T10:35:19 – ofjKtFm6IQdTEdpZW1vn -->
<!-- 2015-04-14T15:08:04 – 76iFh09RtvSyZNATymIT -->
<!-- 2015-04-15T01:08:42 – cflfDq9jGHNmXehisdk6 -->
<!-- 2015-04-16T05:24:32 – cvgLgfI5KhORQRx1lJl1 -->
<!-- 2015-04-19T01:10:17 – 21tXjxgh6pvsfs47Y7N9 -->
<!-- 2015-04-20T10:52:10 – PSkpPagBkXzKeT63jOyg -->
<!-- 2015-04-27T00:36:13 – RcZko2SoVI4g7MeFrseC -->
<!-- 2015-04-27T09:04:16 – wYPzD6NS8ojyxRpdbZIM -->
<!-- 2015-04-27T14:34:17 – cL5lzm1HDHppXKINeeqa -->
<!-- 2015-05-01T08:00:41 – 2PueFwOjWvOknSJlWzpO -->
<!-- 2015-05-02T00:24:43 – 9tYPc6Z0SyIFuwZrK0w7 -->
<!-- 2015-05-03T09:22:02 – UwIhyTaYtE0G3C5AgGh1 -->
<!-- 2015-05-09T17:56:26 – 8PO7ooa2MWmRJjY94wHr -->
<!-- 2015-05-09T18:52:28 – 09E6WiD2eMrvNthHclQO -->
<!-- 2015-05-10T16:27:22 – kYr68875tHNmeSFw447h -->
<!-- 2015-05-13T04:05:47 – yYHFGhvRpu7ox47lir1f -->
<!-- 2015-05-15T09:33:29 – Ylv6lTEhS7g1i5Mb2Z1z -->
<!-- 2015-05-16T22:15:11 – 0fgSM9nc3MA8kcDRednj -->
<!-- 2015-05-18T09:24:15 – BRhjrfrFzdLpYJQjf6O9 -->
<!-- 2015-05-18T11:10:34 – sZNFTP2ywPLQc03UaGTS -->
<!-- 2015-05-19T22:50:17 – QA3ivG0yKmkpl7eFtvXE -->
<!-- 2015-05-20T07:47:57 – oCyTELir9is1aeWi3cLd -->
<!-- 2015-05-22T07:07:24 – chC0ADok89AtolyGdK8S -->
<!-- 2015-05-22T18:12:03 – Z9VSKIeEAXOrpsuJcuUy -->
<!-- 2015-05-24T01:14:54 – 8Hp3yN5WEsF03aJ5RBdi -->
<!-- 2015-05-24T15:19:47 – MG9G93GT9hIIo7sbpHje -->
<!-- 2015-05-25T18:13:09 – rXInluGdijJ3YWzKZ7z4 -->
<!-- 2015-05-25T22:16:38 – fEmKnfXGiaIRdnqBQV15 -->
<!-- 2015-05-28T13:08:43 – Mnlurr7A4lximRP8TPhO -->
<!-- 2015-05-29T02:29:14 – mU8LwjbErvVOQRn83DOx -->
<!-- 2015-05-29T08:19:42 – nlQBTGPc0ujZBF6g8hUr -->
<!-- 2015-06-02T10:22:05 – QhRLUg2C3xEv1wCxnQDU -->
<!-- 2015-06-04T18:08:29 – d4rtGOkQJJVg6PoQb8PE -->
<!-- 2015-06-13T11:42:15 – w7cyz4gcQJqvCmrIPy8o -->
<!-- 2015-06-14T02:35:52 – YVd7MqJjBbJlJciaMdHn -->
<!-- 2015-06-17T14:59:12 – bkp39uzEVrxWTwp5Hr36 -->
<!-- 2015-06-18T04:39:19 – c5kHFXEuhbMW7B3LF5tK -->
<!-- 2015-06-20T16:29:01 – Sy4gJ0Ya3fTvFYUBsP4K -->
<!-- 2015-06-24T20:59:24 – mz42Ih0IsKSAWblZ9Zj8 -->
<!-- 2015-06-24T22:52:49 – xRG30SHvDoZkuZMFjuEL -->
<!-- 2015-06-26T12:30:07 – 3swEJpiuXC4ffSnUr2Fv -->
<!-- 2015-06-29T19:28:10 – 5t2pe3ng9KRCQpQbaFY1 -->
<!-- 2015-07-02T06:31:24 – 6pfbk0hi9GTjBBfAojCq -->
<!-- 2015-07-03T09:57:30 – x5g3PrAbmuwREVPmlMEf -->
<!-- 2015-07-03T23:58:22 – DBKXLiqFoR14J8WXj6nq -->
<!-- 2015-07-04T00:21:23 – 0pbojTbVc5QrvvpHn4M9 -->
<!-- 2015-07-06T05:11:03 – 5ZClvB8V69HA2XATKjzB -->
<!-- 2015-07-08T09:55:18 – VvEjSzkaCFrHi2Z28eCq -->
<!-- 2015-07-12T12:41:06 – xuI8FBJr6LKeI7w9JUVA -->
<!-- 2015-07-14T11:01:15 – c0w3TPChlSZRZ9IpnO8X -->
<!-- 2015-07-16T12:04:03 – 4XUCcNTPxb97xNSEUMTS -->
<!-- 2015-07-18T18:32:18 – fKX8B7CZM3YMALjK8tYa -->
<!-- 2015-07-23T07:23:00 – KBiRHsn8hBOT2J8OdHlx -->
<!-- 2015-07-23T19:07:13 – hCFiw55WYJAkICd00KBQ -->
<!-- 2015-07-26T05:12:00 – A5VKJ1icbgI6dYE3iJ5o -->
<!-- 2015-07-27T23:17:42 – eje1sdiSNbZokno0TB4u -->
<!-- 2015-07-28T17:25:46 – cu5bLgMkcEbnXzGYNrm8 -->
<!-- 2015-07-30T05:43:37 – IQaN2OJmB7KsJXdTggKd -->
<!-- 2015-07-30T16:16:08 – HmOpRSUNG2nKJNoaic5A -->
<!-- 2015-07-31T21:45:15 – pla6egN1gmw0nyUjoZcO -->
<!-- 2015-08-04T11:28:37 – 3KwVMmUhlfEdkE3Or3tf -->
<!-- 2015-08-06T12:21:44 – JctrTNRNeFOlvV0cV19b -->
<!-- 2015-08-10T10:37:32 – DavgODiBaymT0bWBAeiY -->
<!-- 2015-08-17T13:01:20 – Be67VZDl9c4QNHRLWir7 -->
<!-- 2015-08-18T16:18:16 – ZxW9kZS9l3ROrPF9XSKZ -->
<!-- 2015-08-18T22:28:43 – vTvjfxdiNl9g2kdGpScS -->
<!-- 2015-08-23T19:23:59 – Zb1RRSlloeeHpUTKmue8 -->
<!-- 2015-08-26T14:35:47 – htd6wtWcZdwIbN7PHbzd -->
<!-- 2015-08-27T12:08:34 – OYGdq4Qc8nDrGsYuFUrj -->
<!-- 2015-09-02T13:14:53 – JEro3xHE2p4Aykhg4JaX -->
<!-- 2015-09-05T03:39:59 – JSk9hv2VhD3iAGvaiWGs -->
<!-- 2015-09-13T10:30:52 – ndMFUFn05R3zPQt8ekQk -->
<!-- 2015-09-14T22:15:53 – Nqxn1sazchJ0kPK12YYN -->
<!-- 2015-09-15T10:21:31 – iDuUQRDq5fP7aJQ0ckfT -->
<!-- 2015-09-16T15:05:52 – g81rR2KYkUODj3OJXwmL -->
<!-- 2015-09-16T21:17:57 – UtZJboKxsxPTVUuYSnSX -->
<!-- 2015-09-20T16:49:22 – VY7TA954upQfOHwBsVtN -->
<!-- 2015-09-20T22:16:22 – D4UKr1hLi9M8ILZ61Ggh -->
<!-- 2015-09-21T07:54:48 – Vb0XdKh85PaLT51HysXN -->
<!-- 2015-09-22T10:41:17 – O0AunurBsaT0uMGpR6wg -->
<!-- 2015-09-24T01:24:27 – vcnxzgxWBrzzCHw0PYx8 -->
<!-- 2015-09-25T05:29:13 – cYmQ0UpoXfr9zWGNKNZA -->
<!-- 2015-09-26T10:51:39 – l4okTjdIKcv7uVwBZMqr -->
<!-- 2015-09-26T19:46:50 – pwTrqZNmbE8vsd3jXzAc -->
<!-- 2015-09-27T09:59:35 – LMIoZffNOWEMWwHKfvNd -->
<!-- 2015-09-28T10:25:41 – MhN0a9Z2CJDVZlI4574U -->
<!-- 2015-09-29T23:05:55 – pplfunM59ZZz76gwbufv -->
<!-- 2015-09-30T13:34:24 – tMkmAxwNaVpQxGeL9fzz -->
<!-- 2015-10-02T07:38:45 – zJkV09OwCLGz6vmkyXgm -->
<!-- 2015-10-03T05:21:37 – L8PT7u0yBPxMC22tFv6s -->
<!-- 2015-10-07T01:57:43 – fdG2SfE4few1NqrVFIRH -->
<!-- 2015-10-07T08:10:23 – uKH1C8evDpMbN64SUSFz -->
<!-- 2015-10-07T12:00:12 – 2s3HbTEVtaHooqeRomOZ -->
<!-- 2015-10-09T00:52:49 – nKaX1IE7iZE9uYjLly03 -->
<!-- 2015-10-09T02:10:10 – m4eXUkHbw0apqEvJSne3 -->
<!-- 2015-10-10T21:24:44 – B4g4ndCrYRvs90K0ZeNh -->
<!-- 2015-10-12T12:41:37 – 3B5QOxBlNl8b0lQ1kcdc -->
<!-- 2015-10-14T12:05:06 – g0bi6E5Ck96YzVRkBg4J -->
<!-- 2015-10-16T04:08:59 – YLwpHU66RonkHSXU3jVQ -->
<!-- 2015-10-16T10:45:52 – MTfBXxhHcbkPVtz7kaiU -->
<!-- 2015-10-16T20:58:50 – yiOQqqfu5L5fLlOlohVE -->
<!-- 2015-10-17T12:25:55 – bmYQCh4uyRaJVMPIW9O4 -->
<!-- 2015-10-25T16:13:42 – tRGb7ZWdedn7ICViS2E6 -->
<!-- 2015-10-26T07:33:48 – xFtWpWyt8bGc6m8laIex -->
<!-- 2015-10-26T08:51:46 – WX7cdDan9tcTwQ9KF5OU -->
<!-- 2015-10-27T08:05:25 – G71zll30v7UFdjeFjHzD -->
<!-- 2015-10-28T08:45:28 – JJkqLZoep9My1lSZyQep -->
<!-- 2015-10-30T11:31:08 – BXusRAA90OgK4NcHLamJ -->
<!-- 2015-10-30T19:17:44 – xxqQoKYihBkgmFtRa3VC -->
<!-- 2015-10-31T16:16:11 – runEacWD5mqT988lVQdp -->
<!-- 2015-11-02T16:40:42 – FGLCufCqTGx9MqZdSyiz -->
<!-- 2015-11-02T21:58:03 – l5M0qiv4XbezvAlqjf6K -->
<!-- 2015-11-05T13:10:34 – tvZcZYymToDX2LTst08W -->
<!-- 2015-11-06T02:03:09 – N7wBVKoFH64k4g42aYty -->
<!-- 2015-11-08T09:59:31 – EpXm9maUgnduByitSpRl -->
<!-- 2015-11-08T22:06:40 – OASa57BKtw7ub45dwfQ4 -->
<!-- 2015-11-10T17:14:46 – C3l8quSGd6c1qxCT0IU4 -->
<!-- 2015-11-13T16:00:47 – CiUQ9lHN98bIemPPCMoo -->
<!-- 2015-11-14T19:27:08 – JSQsnWHkgYMWyNkZ2tu8 -->
<!-- 2015-11-15T12:16:47 – kKz2GiXIexQYQjkMfrfs -->
<!-- 2015-11-17T15:10:41 – IE96IeFQv0R1ceSmaQTd -->
<!-- 2015-11-18T00:00:27 – YUUnLyWt9DkyLZwEkDxw -->
<!-- 2015-11-22T07:16:21 – jDS0La3vUFI0qzpyIczV -->
<!-- 2015-11-23T14:09:49 – tPG46glyTTwA1YiKK6bz -->
<!-- 2015-11-26T12:27:37 – z8Waj2qKHDvLcKXXFL7J -->
<!-- 2015-11-26T12:54:46 – ZdHgQHuzXnLQbf8wpKTO -->
<!-- 2015-11-30T03:27:18 – zQvtIMaSrdoMrcGVXSnf -->
<!-- 2015-11-30T09:32:44 – zNJgy1dvmOcAaLRgCfRW -->
<!-- 2015-12-03T00:53:33 – 7wcehcej8JXQETFqsiGS -->
<!-- 2015-12-05T03:56:29 – Kf1mc8UG8oqhVUOqpCpv -->
<!-- 2015-12-06T08:08:02 – IGUFeJMdIJ0tH0Gvt9oK -->
<!-- 2015-12-08T05:37:17 – QvsuLUvRNbA1HAFtvJxZ -->
<!-- 2015-12-10T02:29:07 – iFyzwXSvoFmGWMTx1nMr -->
<!-- 2015-12-16T03:04:56 – GHDi3N2nWU9GamFufRpy -->
<!-- 2015-12-17T12:03:08 – 4ZNDTXRG4BeIfLiQqFYl -->
<!-- 2015-12-19T00:56:13 – KHKWdeP9BjZqrlGtt9CH -->
<!-- 2015-12-19T10:59:03 – rFp92NONhNZQq8LjTPtC -->
<!-- 2015-12-21T22:12:34 – WcF9i6dYBaCnBGBdGnAm -->
<!-- 2015-12-24T00:03:18 – IakC7P1Fq45n5io1MqMA -->
<!-- 2015-12-24T03:09:59 – Mu3kbfqkLn8Vguc2KLcD -->
<!-- 2015-12-25T21:26:51 – 7dZKndI7hm8qliUAfNHn -->
<!-- 2015-12-27T05:36:49 – FzqkRmCL6waBoOQRMgr3 -->
<!-- 2015-12-27T06:07:36 – b2dj0z0csb6PLyXwWVCe -->
<!-- 2015-12-28T05:41:46 – oPG659W6UsLw1x0qaOak -->
<!-- 2015-12-31T20:22:12 – CPdYapOOzleTDwUsGfDD -->
<!-- 2016-01-03T22:39:15 – KHqd2NSQmYXOSr9V7ya2 -->
<!-- 2016-01-04T17:54:00 – Hjgr73SFxaTHxn5ssYvY -->
<!-- 2016-01-10T06:58:59 – GAm3E0QFJSmInAvOR0xz -->
<!-- 2016-01-11T01:41:33 – ZMqfKGusIsYhPwSF2mB0 -->
<!-- 2016-01-12T16:21:09 – JuGWsFcnOBmFmLg8KXOw -->
<!-- 2016-01-16T01:46:12 – yqlENo3SDLIDXoOtbShB -->
<!-- 2016-01-16T16:31:16 – AXr5v4S90DdCJJ0arHZF -->
<!-- 2016-01-16T21:06:17 – NtjEOgAC2700DSduNXEW -->
<!-- 2016-01-17T23:38:19 – 6lbIj4NdTgztc7nMAnqb -->
<!-- 2016-01-19T22:26:52 – JW31sJhEi86QQK8nLmzP -->
<!-- 2016-01-22T02:27:41 – pr4ECAwGXnLL7IisTAgq -->
<!-- 2016-01-23T02:30:15 – ZnzBkqnV4sZKA5V3PtGP -->
<!-- 2016-01-30T18:17:05 – WWBWiDnJuRNagMTHadlX -->
<!-- 2016-02-02T03:58:45 – DkNhaM68FlzOWShCCb4m -->
<!-- 2016-02-07T23:49:01 – nC4EzBycVdBJPy7sJOb6 -->
<!-- 2016-02-08T01:21:44 – 4Uwrz3OlZaxnGmIrty1D -->
<!-- 2016-02-08T02:53:02 – DGFBPZzfoNy2dAVJFMTY -->
<!-- 2016-02-11T04:10:31 – RQU820f43LIwOdJcevba -->
<!-- 2016-02-12T18:14:10 – KclYWVAIuxiBd9jhJnv1 -->
<!-- 2016-02-20T17:45:24 – BMbNlEhNyGJeLSAEabuA -->
<!-- 2016-02-20T19:48:55 – yAme6Fpuvex72kdaPtWG -->
<!-- 2016-02-21T22:26:36 – aDJUe0jlsPibVEVsB0gd -->
<!-- 2016-02-23T18:32:33 – 8lc6bi5yXO0JiBCL13Xw -->
<!-- 2016-02-26T02:43:07 – pOwsI0FAcKxsYnhN4de0 -->
<!-- 2016-02-27T16:53:41 – hvcZeBstfZhIiN1I9zOj -->
<!-- 2016-02-28T11:36:47 – jeHKYu1IP2Nq4laLT0Qr -->
<!-- 2016-02-28T15:40:15 – CgEnUA8sDZOkqCOowTRq -->
<!-- 2016-03-02T03:31:21 – tcbGwIkU5JT40uUsTm6O -->
<!-- 2016-03-08T05:56:31 – MOscGdiu7S6nXfSWpJKi -->
<!-- 2016-03-09T16:31:53 – PYKI0LY52U670eX3nDUB -->
<!-- 2016-03-11T10:24:12 – 8gx5C38lnAUSvMnq3VcB -->
<!-- 2016-03-11T11:48:41 – qskPdSwW9NhqvNl3Nz0W -->
<!-- 2016-03-12T12:56:38 – oWX3QiWrcqOKA897gd8K -->
<!-- 2016-03-16T18:00:25 – rB9PNtjSvwlKV8fcfQHp -->
<!-- 2016-03-19T17:17:40 – dTtwchISRFVQE3CtmCu4 -->
<!-- 2016-03-23T00:12:02 – OP1nLsnDU21frJe20uZv -->
<!-- 2016-03-26T13:51:24 – QueRU5KoGfwjWoOVFFB1 -->
<!-- 2016-03-27T11:36:33 – ffLzGOZNuRhYV1WxniB1 -->
<!-- 2016-03-28T08:17:31 – 4iBxmBnlMx0yXqGaeqrP -->
<!-- 2016-03-31T13:19:14 – Hx8QufUEfo7HpoKwDuJQ -->
<!-- 2016-04-06T05:09:05 – OvrAefFoRp8mYTZBmCCg -->
<!-- 2016-04-07T00:38:06 – 9tenHTIumyH7mZ4ZJS3l -->
<!-- 2016-04-14T05:32:22 – Nx5TUsiUvOcjvMJ4huM6 -->
<!-- 2016-04-15T05:27:35 – CPqMGDZKtO5mH63JAR5e -->
<!-- 2016-04-16T19:38:25 – 0tNhmeYgNEZcYa574HdG -->
<!-- 2016-04-17T08:32:12 – 6kjulW49bUzGyAkIVIvc -->
<!-- 2016-04-19T11:11:58 – yi8zf9fHxls1JVUa7Pzf -->
<!-- 2016-04-21T01:24:30 – tWhz2IZNmnm85MBUIMH8 -->
<!-- 2016-04-21T21:56:13 – ck4eTrhkdUMiWMYzBB5a -->
<!-- 2016-04-27T18:58:57 – jFa5EHtI73n47m0TsUK5 -->
<!-- 2016-04-28T02:50:56 – cGo6ViooV50DNPU6T4H6 -->
<!-- 2016-04-29T18:36:14 – sg1DjMTnoCGGKQbs7WbT -->
<!-- 2016-05-04T14:18:11 – crvt2nB4YFg4RSe0I24i -->
<!-- 2016-05-04T23:14:40 – QmoZ6qiY6Jo62S5etPJC -->
<!-- 2016-05-07T15:08:10 – KiQFZNhaDxlPbci4HJVQ -->
<!-- 2016-05-12T09:41:01 – b5zuIlNuFli062psj1oi -->
<!-- 2016-05-15T06:14:40 – mwkQ1OdnQltsdQQ75pNL -->
<!-- 2016-05-19T10:04:40 – d9MZXgvPbK5IuMiwyn3N -->
<!-- 2016-05-24T05:08:12 – qJFCL45DDq58qMLo4fc4 -->
<!-- 2016-05-24T07:18:47 – UW1eMTTIjQrIpVzVtGnG -->
<!-- 2016-05-26T20:00:09 – lE7HZ8irmPCuAVj3Full -->
<!-- 2016-05-27T13:51:06 – 3N8B82VAPnlLQLOz9BRS -->
<!-- 2016-05-31T18:03:16 – brJvXq1WEgAxn6Cw7L6S -->
<!-- 2016-06-02T12:38:20 – dVY1YdIsZl44Lp6MVcpW -->
<!-- 2016-06-03T22:53:33 – xmwvKIdN698EEsT0MXTI -->
<!-- 2016-06-05T03:10:05 – xdLqCxygGl8gSTtaDUR2 -->
<!-- 2016-06-08T15:20:34 – 3MH4Ime9ZzL69eVciF9z -->
<!-- 2016-06-09T06:47:11 – x8A4NTEpAeXlLkFQ0EhX -->
<!-- 2016-06-12T15:31:40 – E2WNDDG9xrybUNSPnJbh -->
<!-- 2016-06-13T04:37:03 – Te6G4NvP3eOYPuTOM5Nv -->
<!-- 2016-06-13T20:41:44 – xA7911BtfbLxzeFzoRD8 -->
<!-- 2016-06-13T22:59:11 – AJtWJM1aYcVp7VIbZCeV -->
<!-- 2016-06-16T12:31:41 – CanFTl1jBkzJLmfUNXs3 -->
<!-- 2016-06-22T22:26:42 – tR5vB98JkTTBH1LOhdHR -->
<!-- 2016-06-22T23:02:10 – JIqiCnwLJdd3gtAz3Rz4 -->
<!-- 2016-06-25T10:07:58 – J4mW2gj7TX8QOcCsUTbd -->
<!-- 2016-06-25T20:52:24 – G8xOAvgYLh7XLlJikyYI -->
<!-- 2016-06-26T11:58:56 – raaexwP350ZODNhDByAR -->
<!-- 2016-06-29T18:49:54 – dHzZW36GYYhiTkIjLam0 -->
<!-- 2016-07-01T11:22:29 – YzR3MllaRWl3SezRndQp -->
<!-- 2016-07-02T04:48:58 – LNiVhL3C1Ce9iAsLmJpI -->
<!-- 2016-07-03T08:49:15 – a1IQS5YMD0uBiBVx8Gnr -->
<!-- 2016-07-04T21:43:23 – nsFAqF9rx4jZosukZ27U -->
<!-- 2016-07-06T07:07:26 – QOTSdyWatL0TP4qL3juK -->
<!-- 2016-07-07T20:15:00 – BcLpFGz5IU3vqkCQJo5Q -->
<!-- 2016-07-08T05:20:09 – 9Yygf4y4kGCIiatvurUb -->
<!-- 2016-07-10T04:45:47 – bxYqBNMXSn1bwynqplHr -->
<!-- 2016-07-10T19:28:36 – gQYZ80YwbBUJCMh9b94K -->
<!-- 2016-07-12T01:42:47 – prBXTJnf32iGebxRgA7L -->
<!-- 2016-07-12T16:07:09 – 3OeHNbCW20aOM3UrXdOj -->
<!-- 2016-07-14T23:06:40 – YI753Vu3litaEInBYbqT -->
<!-- 2016-07-15T04:23:31 – eazrJsWqrxhjXWGLV5dI -->
<!-- 2016-07-16T17:08:36 – aYuzUKP8x1BOGi7cAFrU -->
<!-- 2016-07-18T12:17:00 – F43quQZjVIfvUKLufA5U -->
<!-- 2016-07-19T20:37:54 – ZEoG5AXAh057VxO9ZWE7 -->
<!-- 2016-07-20T16:12:11 – 9SmtujWGDl9ymr7eozgx -->
<!-- 2016-07-21T01:55:43 – Kllyv6jbWiPEqOZdzevr -->
<!-- 2016-07-23T02:13:54 – LZYhVsCiBcV6we72XJSz -->
<!-- 2016-07-25T02:11:29 – S7eivEnoqosLqw1g9cox -->
<!-- 2016-07-25T06:29:02 – Ju4wQbJUcYOHpyefVfHv -->
<!-- 2016-07-28T01:14:12 – 8FKFZiTJ2O0R3RxuPC6a -->
<!-- 2016-07-28T13:10:12 – XyWCaxw7RiCGoVbv7Hhj -->
<!-- 2016-07-29T06:40:54 – Pu0qT6Zeducav9INX1WJ -->
<!-- 2016-07-29T16:25:08 – lmIqFACIR4WB0ftq8IRm -->
<!-- 2016-07-31T20:55:25 – EYpum56KQw9TAdjZ6oUD -->
<!-- 2016-08-01T04:07:41 – RwUZme2Sj9zeTtPXKPTd -->
<!-- 2016-08-01T07:05:35 – ciPfr3oDY9Swu3SAM7t9 -->
<!-- 2016-08-03T04:56:04 – KUfUwq2F4yeuFh5AATQF -->
<!-- 2016-08-07T11:48:54 – Rr6ihdpbm7hIN5S3rtxO -->
<!-- 2016-08-08T02:57:38 – co41XAGqWnNq86gTcl6x -->
<!-- 2016-08-11T08:23:12 – 6pYQlqRVskQVBeXIdPJu -->
<!-- 2016-08-14T01:46:13 – ERokRAyumUmB0nd9zZAN -->
<!-- 2016-08-15T15:36:40 – jlviYhwU0luXMnZyceZl -->
<!-- 2016-08-15T20:09:37 – XqdOW5t70T8rNq8qQrVk -->
<!-- 2016-08-17T04:22:18 – v7m4MYGFEyQZltBiGLmA -->
<!-- 2016-08-17T06:25:14 – RD8tEKLzbvB54RdDcc7l -->
<!-- 2016-08-17T10:39:03 – llhT8gDPO4Bf7OkgmXsS -->
<!-- 2016-08-18T06:48:08 – 5wXsYPXlfX7RxPtiGLz0 -->
<!-- 2016-08-20T21:05:24 – HVWJKXcOIYkrM1HhBWiD -->
<!-- 2016-08-21T10:39:23 – bAvxPKR8C702pTGiNxh0 -->
<!-- 2016-08-25T12:36:20 – Gi3eM3WfyGpmEqWjXFs0 -->
<!-- 2016-08-26T12:11:35 – xATQ3v91MBn3ZWPpJvSP -->
<!-- 2016-08-30T09:44:13 – 6J04cXhpzOsYffRNGeaM -->
<!-- 2016-09-03T12:30:25 – qdbu8XXfo9lJOeiklehr -->
<!-- 2016-09-03T18:36:15 – rkcd9DQvKuBDy8dfl1at -->
<!-- 2016-09-05T18:52:54 – hFTvCmhMMSRWkmcl82hy -->
<!-- 2016-09-11T14:07:52 – YB3oTNjKReeFxI4m8pST -->
<!-- 2016-09-12T19:36:29 – heOSnMPQqXVS1SQQnnXx -->
<!-- 2016-09-12T21:55:36 – abLBMEGuOCI9TPwT3eKc -->
<!-- 2016-09-13T13:34:05 – UYabWR2WFdLS1rpTlhMx -->
<!-- 2016-09-17T02:44:56 – YcqVwo4R3y2BoMeNeAmA -->
<!-- 2016-09-18T18:43:37 – AaPVB2gHrZ3IQqD2m7Ng -->
<!-- 2016-09-24T11:06:42 – sfcJaVHye7SceS6UKOvc -->
<!-- 2016-09-25T10:22:31 – RBlHWqSFgFxmnS3pIB4V -->
<!-- 2016-09-27T08:54:23 – mlYCnklkHNbi9ITGMeZC -->
<!-- 2016-09-27T20:54:00 – l3MORng7CJpb8IttnZH9 -->
<!-- 2016-09-27T21:11:49 – udcaLrWF0XOapRzeC5g0 -->
<!-- 2016-09-29T16:00:31 – WpnMcEDlbK1i0zPr8GtQ -->
<!-- 2016-09-30T23:30:21 – mgSpOTQRYub5Rn1hHP8n -->
<!-- 2016-10-01T03:30:10 – ZtQwsZOwfsn2Lt7YR2G5 -->
<!-- 2016-10-02T03:44:58 – z7IrYIuIFwZORhSTCB2Q -->
<!-- 2016-10-02T22:00:02 – vEIyVSalIOtzaejIeFKI -->
<!-- 2016-10-03T10:03:54 – I5hBDmPKj3khCf6rImSw -->
<!-- 2016-10-09T00:31:46 – kR1K7HgGX6l11442Okxw -->
<!-- 2016-10-12T14:50:01 – omWwMnd14FEZfRIFHoxm -->
<!-- 2016-10-14T01:30:41 – K27oMSFwTy36Zonp1kBH -->
<!-- 2016-10-18T18:23:10 – 5weeXQEDNFmEzZVego8l -->
<!-- 2016-10-20T21:44:39 – 0YgSx73ySJtX5ZCQMncF -->
<!-- 2016-10-24T23:50:29 – Vcpadq70QpTIGWBHEoiM -->
<!-- 2016-10-26T02:26:40 – EMqkXD50ZKA8FnYrQNdP -->
<!-- 2016-10-27T10:35:17 – Z2KcT1V6QynIucXPIOYg -->
<!-- 2016-10-28T20:10:52 – g5WytA8Quw06kWT8YW4e -->
<!-- 2016-10-31T21:52:08 – gXFqDApkSR3Qre9M2lBC -->
<!-- 2016-11-03T22:54:01 – uP5L8VcClOOAmpzW3eEx -->
<!-- 2016-11-05T00:22:22 – a65r9c8e25SZlWIVihMx -->
<!-- 2016-11-05T16:00:26 – yJfvw9q7yRj4FpL6eBoq -->
<!-- 2016-11-06T03:45:36 – sJ4cPwaG5V8nsyNb9SGT -->
<!-- 2016-11-06T18:46:43 – 2Pp7o1jcgIRm3PUw3Sk4 -->
<!-- 2016-11-10T10:11:53 – ZjPczbIZRFz7vyd6RKnZ -->
<!-- 2016-11-11T14:43:44 – yUXDrTMgPLuajotgF0Cg -->
<!-- 2016-11-13T04:01:36 – wt68fy69NJK5HXMkKu4T -->
<!-- 2016-11-13T18:14:29 – q0vSeddlIy8GyQEfZoZq -->
<!-- 2016-11-13T23:08:21 – RFL82JlTWaiBgk16Wwqo -->
<!-- 2016-11-14T04:57:02 – JXViXRUhPOW2BILjB3nu -->
<!-- 2016-11-17T23:21:12 – IQjtQ5F3mIvf5qTdL264 -->
<!-- 2016-11-18T10:29:59 – nBHwOGuEusKOTCV6xLbj -->
<!-- 2016-11-22T16:10:27 – Xjc9WxklWNgVZ2v5OkJL -->
<!-- 2016-11-22T19:51:33 – tmU8SrsBhG24BcNm7Vm6 -->
<!-- 2016-11-29T17:23:16 – 2qzy0tz5iZRkKWGpc0K4 -->
<!-- 2016-12-01T01:03:38 – nX7ID2B9yeBJEtuha5bS -->
<!-- 2016-12-01T05:34:05 – i28utNFMiREYnUYJzXWD -->
<!-- 2016-12-01T18:19:20 – lv2UPAdikt5oYSkzNx8O -->
<!-- 2016-12-02T14:59:35 – C5Ir5GkLDJIpnBtrTIa0 -->
<!-- 2016-12-02T21:32:27 – NfEVuJoo8tmWX1NRwYfL -->
<!-- 2016-12-02T22:42:21 – xAvy38f1wJ8j60gs9NGJ -->
<!-- 2016-12-07T01:59:46 – cEIApPCZggFzpfvxqPEC -->
<!-- 2016-12-09T05:46:21 – kH7Ho4tTSLraViNjQbZY -->
<!-- 2016-12-09T19:22:07 – xfmT8KdFot37ObI2ZYXm -->
<!-- 2016-12-11T01:12:33 – z7O5nOEGh1rbyY64NJSl -->
<!-- 2016-12-16T03:42:58 – 9kusYcmCC5wpRcp9qmtn -->
<!-- 2016-12-16T13:44:35 – DwrE1HfskQLIaIycfhT1 -->
<!-- 2016-12-18T02:49:39 – nzZFImfedpxCE6dmulwM -->
<!-- 2016-12-19T08:25:54 – E6TfEJjTnnTSVSt3iMJ4 -->
<!-- 2016-12-20T19:07:49 – aP8hyUJPTiJKgNuEiSj5 -->
<!-- 2016-12-26T22:43:05 – CiTpaxKaflEkT8mjsDQL -->
<!-- 2016-12-29T04:53:08 – SDTZUp4Mo8eEC8RkTekN -->
<!-- 2016-12-29T10:38:02 – sOLkrfZlR8mhgYCxfEAm -->
<!-- 2016-12-29T13:33:40 – acNIUajZBeKDDSL3qh6J -->
<!-- 2016-12-30T17:03:47 – rwPYSMOdbQes0gm5DY1U -->
<!-- 2017-01-05T02:49:54 – 9FrxQbS5t26NeDSt3f7C -->
<!-- 2017-01-10T13:16:56 – 62GP7wilELvFBQnWbZNU -->
<!-- 2017-01-10T20:30:44 – Vv0rFYodC1nhaJRSBNLy -->
<!-- 2017-01-11T19:59:41 – NVfdO1YyRWf6lldGBWiH -->
<!-- 2017-01-15T09:16:15 – 1yBWGqAtPrKvjUp5Boxg -->
<!-- 2017-01-16T20:16:05 – FeB0QQaw0rx957twK4Id -->
<!-- 2017-01-17T08:32:27 – fgIMKggno9RF2VYj80Ns -->
<!-- 2017-01-26T23:53:17 – WOuTGCzXWDBLngzU8Mks -->
<!-- 2017-01-30T14:58:24 – mJMXdhhUWZ2801v7kigC -->
<!-- 2017-01-30T19:22:03 – B4G7ihGSWtvgHbCHvTfW -->
<!-- 2017-02-02T19:01:14 – NzFQWscI29BcXLcZT2Ig -->
<!-- 2017-02-03T13:06:16 – XhIlRWe9FdUZMsk90Xic -->
<!-- 2017-02-08T03:20:48 – dLPAm4PCtAS1rVoK2mvx -->
<!-- 2017-02-08T03:24:23 – TfxwUtCTQ57ry0GTgS00 -->
<!-- 2017-02-08T07:28:22 – 45dhiuhN7lmBmC2J6KD6 -->
<!-- 2017-02-10T19:30:30 – Xk7iI8kjDW1MNNChZ4rE -->
<!-- 2017-02-11T15:10:07 – dnbgDuZPEWFXmOCN7rVh -->
<!-- 2017-02-19T11:38:35 – hyJmPNonIRCv1bDGDuXM -->
<!-- 2017-02-20T21:47:09 – FEmtBfbGLvNHemPFROrR -->
<!-- 2017-02-24T09:09:33 – 8NI3dR0pj2fd7zcu88EM -->
<!-- 2017-02-24T22:52:50 – 1wyE6oTAKVBgc2FGvB6U -->
<!-- 2017-02-25T19:53:11 – lNHQ8Nn5X8CNjcfU0Y9O -->
<!-- 2017-03-04T13:09:00 – JmGnr3o47Smk8bBds1iY -->
<!-- 2017-03-06T04:16:41 – QM6fHHh790UE3KoJAs7o -->
<!-- 2017-03-07T13:04:15 – 1WgoANhFwCblVWlcsqyr -->
<!-- 2017-03-10T12:38:47 – XJvIGG1rQsoCbqW2jnt2 -->
<!-- 2017-03-11T02:43:42 – jUzCPJVBtuFJHnXJTfaz -->
<!-- 2017-03-12T11:40:15 – G7XvoxB8ymoQhm6lXDyI -->
<!-- 2017-03-15T00:17:15 – H8ZpNfElIKnbz5FKsGHb -->
<!-- 2017-03-15T06:20:55 – QymFuY5fucaI5rXQVhrU -->
<!-- 2017-03-17T05:45:27 – MpqTpZjwOJzUkVYqs9yN -->
<!-- 2017-03-17T06:48:11 – CIyEVGYUClYXIPZnVZCo -->
<!-- 2017-03-17T08:08:19 – Y8CQXMkdsMxQIoITAXzg -->
<!-- 2017-03-19T14:15:49 – 65qphAFweHdqbpGGqHIv -->
<!-- 2017-03-24T15:34:40 – QKF65X5mNZuu4kRjsJQw -->
<!-- 2017-03-26T08:54:23 – kSNb46Br12H14s4I2bYK -->
<!-- 2017-03-30T18:02:36 – 7wS2atb1YjtlETbobMue -->
<!-- 2017-03-31T08:46:31 – 2jsVH93bfAtm11GkUZrx -->
<!-- 2017-04-01T23:24:43 – 0fNy0tBLeyrHzkGolzsc -->
<!-- 2017-04-02T17:43:23 – ugkblmjRzomtZqysNKHM -->
<!-- 2017-04-03T20:02:09 – wtKIXxHUJh92vr2qgo0v -->
<!-- 2017-04-06T15:29:42 – wENtgf0poRV5lb9sRZoB -->
<!-- 2017-04-11T04:39:35 – yUtfWInTxk13SGqUg0Yv -->
<!-- 2017-04-11T22:23:01 – o5piGxRXV7dbmEOgBHVb -->
<!-- 2017-04-13T09:59:16 – wfqYHUePzV34Sr071vMg -->
<!-- 2017-04-16T09:22:24 – L4w8BotbEPYqF9gyeIp4 -->
<!-- 2017-04-16T22:26:28 – 4Q2f6AEtGEjUbdUSVvjw -->
<!-- 2017-04-17T05:21:17 – lfzST8AspLarzvkB8XZr -->
<!-- 2017-04-17T05:54:06 – Yd2m1nRRHMfcpULTKFbH -->
<!-- 2017-04-28T08:22:45 – dTkGAv96krbiDFCM9Jls -->
<!-- 2017-04-29T20:08:47 – G8bkzWs7wsLYhIJqg4Mh -->
<!-- 2017-05-10T20:01:37 – L8GEULanaxTSxszSiF2Y -->
<!-- 2017-05-13T06:29:39 – J38D3vGqXhuLnQgxNdKa -->
<!-- 2017-05-15T00:34:50 – aCVyErtL6JzwvMwG9pck -->
<!-- 2017-05-16T01:34:01 – I0HguPMD6fahozkCKdG0 -->
<!-- 2017-05-16T08:57:15 – IKCeb7tbFJixNrZJ3ruI -->
<!-- 2017-05-16T18:49:28 – Q0OEdgrcX21VCa6mhIXF -->
<!-- 2017-05-22T18:07:43 – A6nqKVGXmxUA9pRFx3xG -->
<!-- 2017-05-25T23:22:06 – Z2rf8EeoQFQ5OswtYn2o -->
<!-- 2017-05-27T20:59:13 – mU8xTJZgy02EIBW3Q5Bf -->
<!-- 2017-05-28T18:55:42 – IV8SGw9e4FgkxEyuy15l -->
<!-- 2017-05-31T01:08:11 – 6jdnqHQBjAzWgYVYUF7d -->
<!-- 2017-06-03T00:30:52 – gI0Gt3UcYsSKFPmPLh5Y -->
<!-- 2017-06-03T01:48:54 – FUwx1lURRp3aA0JFTTcW -->
<!-- 2017-06-05T05:47:21 – n7QbWJjbHOsjfo8JJFS7 -->
<!-- 2017-06-06T00:52:15 – smNBZcG1GIOBHYeinFFO -->
<!-- 2017-06-06T19:16:28 – FbGrKuaghTVeHKIyJlao -->
<!-- 2017-06-07T03:08:54 – TorEHxe2Nz71oOQ32Kwg -->
<!-- 2017-06-08T12:20:09 – jFPre8bWgGuTRVLGeekY -->
<!-- 2017-06-08T16:18:59 – o4XXN09i7ncpplLqCblD -->
<!-- 2017-06-08T22:48:43 – yw61ZOthFVb9jzfyjUID -->
<!-- 2017-06-09T13:37:42 – LkC6ru3XSowLei7SZK5W -->
<!-- 2017-06-11T10:30:39 – qvyasCiGZs5HUxphgFSE -->
<!-- 2017-06-16T05:17:46 – M5Gpgh5nuebUz5WeFh5x -->
<!-- 2017-06-21T06:35:02 – WpeNyAKCqvWYAQjw2US5 -->
<!-- 2017-06-27T13:25:25 – 6WJLAUvzFEuyi2X7uAb9 -->
<!-- 2017-06-29T12:10:43 – 6jVPCOIc5RaX5LVDEe6q -->
<!-- 2017-07-01T00:45:21 – eyne1EVs53bvtDYidi8Z -->
<!-- 2017-07-01T11:47:22 – DXYcRXmrbvGQqrpvCZ8F -->
<!-- 2017-07-05T14:38:33 – p0Ytquc1LPxIrNXnvG5O -->
<!-- 2017-07-07T04:30:18 – eHDaCUE8cD5VdDZy2dNL -->
<!-- 2017-07-17T21:46:36 – HrFr7sHvmXn6GhPk6gZP -->
<!-- 2017-07-18T20:32:33 – 9nAJ0j2jFfvT2cE1ZD57 -->
<!-- 2017-07-22T18:09:18 – tozp7LGRGZjFlE4gk7En -->
<!-- 2017-07-23T12:23:44 – MayfisOGsZPXxUYj26JV -->
<!-- 2017-07-24T02:39:45 – sJ4OFYCk2QGPig0y9wnN -->
<!-- 2017-07-24T18:26:17 – jpeAQCBNyztIxiN9RRJi -->
<!-- 2017-07-26T21:47:20 – lHAATnhjXt8FHArfvlX8 -->
<!-- 2017-07-28T19:24:37 – Blny9FhN9Z7spE85WeUO -->
<!-- 2017-07-29T08:33:29 – rOiTmHF1iEzcmwboQDLk -->
<!-- 2017-07-31T08:44:48 – 0ZqQVRAULwRLYpNBh73v -->
<!-- 2017-08-02T12:47:10 – DHrV5l5agm03A8jmuIX0 -->
<!-- 2017-08-04T10:32:52 – VlrLyU3PxtuCp8jcyiBU -->
<!-- 2017-08-05T09:06:24 – 8DikUik0b3f6apoxdVKu -->
<!-- 2017-08-06T07:18:45 – jGpXcm4cRfrAawoEnG0G -->
<!-- 2017-08-15T12:25:02 – b6DCPRz1u2HxRXNAxgNv -->
<!-- 2017-08-21T08:35:44 – SHGTvxL2aWLoYglit4aV -->
<!-- 2017-08-22T18:42:31 – PmvgZSW5B3YXLcww4q1L -->
<!-- 2017-08-24T11:45:08 – 7rRm706RNbizEV2oZ8Jc -->
<!-- 2017-08-28T06:07:33 – 8D8Ejo3zf203S121sCQ8 -->
<!-- 2017-08-28T18:14:22 – ybSYvPCVdAiOBS4PATcx -->
<!-- 2017-08-30T09:34:48 – 0N6yKtCx3svP1sqGBK23 -->
<!-- 2017-08-30T09:41:37 – MiA91Be8itaTBru4cpFP -->
<!-- 2017-08-30T20:38:08 – exjdoC7AQV9HSFBiFVG0 -->
<!-- 2017-08-31T07:49:09 – 86xVPL4uQ24D6O7zh7TI -->
<!-- 2017-09-02T05:40:13 – yKuMWcbglumDGwScPx9A -->
<!-- 2017-09-02T08:40:22 – KYz4yzW2NipiLkOrC0Zx -->
<!-- 2017-09-06T05:01:21 – DwOmdiWDbY7ZgttQcO8E -->
<!-- 2017-09-06T17:49:44 – xz4gPRiHljQzDbI9ze44 -->
<!-- 2017-09-08T09:46:04 – 0v7liGUPCEWPGBVlA61q -->
<!-- 2017-09-09T11:25:18 – fKH3KFluqYvgX1kzfNfS -->
