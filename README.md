# pumpfun-mass-launcher

> **The pump.fun mass launcher.** Everything you need to know about mass-launching meme coins on pump.fun — how it works, what it costs, and where to start.

[![Try MassLauncher](https://img.shields.io/badge/Try%20it-masslauncher.fun-4ade80?style=for-the-badge)](https://masslauncher.fun)
[![Telegram Bot](https://img.shields.io/badge/Bot-@MassLauncherBot-26A5E4?style=for-the-badge&logo=telegram&logoColor=white)](https://t.me/MassLauncherBot)
[![Main Repo](https://img.shields.io/badge/Main%20Repo-MassLauncher-181717?style=for-the-badge&logo=github)](https://github.com/Mass-Launcher/MassLauncher)

---

## What is a pump.fun mass launcher?

A **pump.fun mass launcher** fires many meme coin launches on [pump.fun](https://pump.fun) in rapid succession. Every coin you launch hits pump.fun's new-pairs feed, so launching 25–100 coins at once **floods that feed** with your project's tokens.

This is one of the cheapest ways to get organic visibility on Solana memecoin land — no ad spend, no influencer fees, just raw new-pairs saturation.

**[MassLauncher](https://masslauncher.fun)** is a hosted pump.fun mass launcher. Sign in (Telegram / Google / email), deposit SOL, fire as many parallel launches as you want.

## Why mass launch on pump.fun?

| Use case | Goal |
|---|---|
| **Project promotion** | Spam-launch coins that reference your main token. Free eyeballs from the new-pairs feed. |
| **Dead coin revival** | Mass-launch derivatives that point back to an existing dead coin. The chart often notices. |
| **Volume probing** | Generate consistent on-chain activity around a project. |
| **Pure degen** | Launch 100 coins, see which sticks. |

## How fast is it?

- **Individual launch**: under 10 seconds on pump.fun
- **25 coins in parallel**: minted within a single Solana slot (~400ms apart on-chain)
- **100 coins**: wall-clock under 15 seconds

Speed comes from a pre-funded wallet pool — no waiting for fresh wallets to get bootstrapped before each launch.

## How much does mass launching cost?

| Launches | Per-launch price | Total |
|---|---|---|
| 10 | 0.02 SOL | 0.20 SOL |
| 25 | 0.01925 SOL | ~0.47 SOL |
| 50 | 0.0175 SOL | ~0.88 SOL |
| 100 | 0.015 SOL | 1.50 SOL |

Volume discount kicks in after launch 10. Price slides linearly down to 0.015 SOL at 100 launches.

📖 Full pricing: [`docs/pricing.md`](docs/pricing.md)

## Getting started

1. Go to **[masslauncher.fun](https://masslauncher.fun)** (or message [@MassLauncherBot](https://t.me/MassLauncherBot) on Telegram)
2. Sign up with Telegram, Google, or email — no Solana wallet required
3. Send SOL to your personal deposit address (credits land in ~30s)
4. Set up a coin profile (name, ticker, image, socials)
5. Pick a quantity and mass launch on pump.fun

📖 Step-by-step: [`docs/getting-started.md`](docs/getting-started.md)

## How a pump.fun mass launch works (technical)

When you fire a mass launch of N coins:

1. N pre-funded wallets are reserved from a shared pool
2. Coin metadata is uploaded to pump.fun's IPFS in parallel
3. N pump.fun create-coin transactions are built and signed
4. All transactions go out to Solana RPC at once
5. Confirmations polled in a single batch RPC call
6. Used wallets returned to the pool

📖 Deeper dive: [`docs/how-it-works.md`](docs/how-it-works.md)

## Do I need a Solana wallet?

**No.** MassLauncher generates a Solana deposit wallet for your account on sign-up. You can sign in with Telegram, Google, or email — no browser wallet extension needed.

If you want to link a Solana wallet later (for withdrawals), that's a one-click option in Account settings.

## Why use a hosted pump.fun mass launcher vs. running your own script?

You could write a Solana script that fires pump.fun create-coin instructions yourself. Most people don't because:

- Every fresh wallet needs ~0.012 SOL bootstrapped first (rent + bonding-curve seed)
- RPC selection, retry logic, and priority fee tuning are all non-trivial
- pump.fun expects metadata in a specific IPFS shape
- Residual SOL needs to be swept back after launches finish

MassLauncher handles all of that. You pay a flat per-launch fee.

## Links

- 🌐 **Web app**: https://masslauncher.fun
- 🤖 **Telegram bot**: https://t.me/MassLauncherBot
- 🐦 **Twitter**: https://x.com/masslauncher
- 📦 **Main repo (docs + branding)**: https://github.com/Mass-Launcher/MassLauncher
- 🎯 **pump.fun**: https://pump.fun

## License

Documentation only. The MassLauncher service itself is closed-source SaaS. See [`LICENSE`](LICENSE).

---

<sub>**Keywords:** pump.fun mass launcher, pumpfun mass launcher, pump fun launcher, mass launch on pump.fun, pump.fun spam launcher, solana memecoin mass launch, meme coin mass launcher, pump.fun bot, memecoin launcher solana, spam launch tokens solana.</sub>
