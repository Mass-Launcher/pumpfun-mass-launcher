# How the pump.fun mass launcher works

A technical look at how MassLauncher mass-launches meme coins on pump.fun.

## The basic flow

```
You → MassLauncher backend → Solana wallet pool → pump.fun
```

When you trigger a launch of N coins:

1. **Wallet pool checkout** — N pre-funded wallets are reserved from a shared pool. Each holds enough SOL to cover rent + the pump.fun bonding-curve seed.
2. **Metadata upload (parallel)** — Coin image + JSON metadata pushed to pump.fun's IPFS gateway. Done concurrently for all N coins.
3. **Transaction crafting** — N pump.fun `create_coin` transactions are built and signed by each pool wallet.
4. **Parallel submission** — All N transactions submitted to Solana RPC at once.
5. **Confirmation batch** — A single `getSignatureStatuses` RPC call confirms all N at once.
6. **Wallet pool checkin** — Used wallets return to the pool.

## Why pre-funded wallets matter

A naive approach would fund a fresh wallet for each launch. That means:

```
[fresh wallet] → [fund tx, wait 12s] → [launch tx, wait 12s] → done
```

Each launch takes ~24 seconds.

With a pre-funded pool:

```
[checkout pre-funded wallet] → [launch tx, wait 12s] → done
```

Each launch takes ~12 seconds. And in parallel, **N launches still take ~12 seconds total**.

## Why parallel matters

Sending N transactions sequentially: `N × 12s` wall-clock time.
Sending N transactions in parallel: `~12s` wall-clock time (limited by single-tx confirmation).

For a mass launch of 25 coins:
- Sequential: ~5 minutes
- Parallel: ~15 seconds

The parallel version means all 25 land in **the same Solana slot block** of each other — they appear simultaneously on pump.fun's new-pairs feed.

## Wallet pool size

MassLauncher operates with a pool of ~120 pre-funded wallets. Each one is reusable: after a launch, the wallet gets swept of residual SOL and put back in the pool for the next user.

Pool size is a balance between:
- Idle capital sitting in funded wallets (overhead)
- Concurrent launch capacity (more wallets = more parallel slots)

## Confirmation strategy

Solana's `getSignatureStatuses` RPC accepts up to 256 signatures per call. That means a single round-trip can confirm up to 256 launches at once — well above any realistic mass launch size.

The backend polls every 2 seconds with the full batch. As soon as a signature flips to `confirmed`, the user gets notified with the pump.fun link.

## RPC selection

Priority fees are tuned per-launch based on current Solana network conditions. We use Helius RPC for both submission and confirmation reads.

## Metadata upload

pump.fun expects coin metadata in a specific JSON shape, uploaded to their IPFS gateway:

```json
{
  "name": "...",
  "symbol": "...",
  "description": "...",
  "image": "https://ipfs.../coin.png",
  "twitter": "...",
  "telegram": "...",
  "website": "..."
}
```

MassLauncher uploads the image first (gets the IPFS URL), then uploads the metadata JSON referencing it. Both happen in parallel for all coins in a mass launch.

## Failure handling

If a launch transaction fails (RPC timeout, pump.fun program error, etc.):

- The credit is automatically refunded
- The wallet returns to the pool
- The user sees `failed` status in their History with the error

No support ticket needed.

---

📖 More:

- [`getting-started.md`](getting-started.md) — step-by-step user guide
- [`pricing.md`](pricing.md) — pricing details

🌐 Try it: **[masslauncher.fun](https://masslauncher.fun)**
