# pump.fun mass launcher — pricing

Pay-per-launch. No subscriptions. Volume discounts applied automatically.

## Per-launch pricing

| Launch # | Per-launch (SOL) |
|---|---|
| 1–10 | 0.0200 |
| 25 | 0.01925 |
| 50 | 0.0180 |
| 75 | 0.01675 |
| 100+ | 0.0150 (floor) |

The per-launch price slides linearly from 0.02 SOL at launch 10 to 0.015 SOL at launch 100. After 100, you stay at the floor rate.

## Example totals

| Launches | Total cost | Per-coin cost |
|---|---|---|
| 5 | 0.10 SOL | 0.020 SOL |
| 25 | ~0.47 SOL | ~0.019 SOL |
| 50 | ~0.88 SOL | ~0.018 SOL |
| 100 | 1.625 SOL | ~0.016 SOL |
| 200 | 3.125 SOL | ~0.016 SOL |

## What the fee covers

Every per-launch fee includes:

- Pre-funded wallet for the launch (rent + pump.fun bonding-curve seed)
- Solana RPC fees + tuned priority fee
- pump.fun `create_coin` transaction submission
- Metadata + image upload to pump.fun's IPFS
- Confirmation polling and pump.fun link delivery

No hidden fees, no metadata-upload surcharges, no priority fee markups.

## Refunds

Failed launches → automatic credit refund. Check **History** in the dashboard.

## Withdrawals

Unused credits convert back to SOL at the current per-launch floor rate and can be withdrawn to any Solana address. No KYC.

---

🌐 Start launching: **[masslauncher.fun](https://masslauncher.fun)**
