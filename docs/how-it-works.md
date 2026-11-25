# Reading a Pump.fun batch result

A five-coin order is five separate creations. A shared name or ticker won’t tell you which one you’re looking at. Save the **mint address** from each successful row; use its transaction signature when you want to check what Solana confirmed.

| What you see | What to do |
| --- | --- |
| Confirmed, with a mint link | Open the link and compare the full mint address. That address identifies the coin. |
| Pending | Check the same order again later in History. Its credit is reserved; don’t repeat the launch while the outcome is unknown. |
| Definitively failed | Read the reason and check the returned credit. If you retry, request only the coins you still want. |

The web app accepts up to 25 coins per order, and Telegram accepts up to 100. The service processes larger orders in smaller groups, so different confirmation times within the same batch are expected. [See how to verify one mint on Solscan](https://masslauncher.fun/blog/verify-pump-fun-launch-solscan).

## If you are using the API

Create a key in the [signed-in API dashboard](https://masslauncher.fun/app/api-keys) and store it on your server. Start with a **read-only** check. With your own key set as an environment variable:

```sh
curl --fail --silent --show-error \
  -H "Authorization: Bearer ${MASSLAUNCHER_API_KEY}" \
  https://masslauncher.fun/api/v1/credits
```

This only reads the account balance; it does not spend credits. Submitting a launch creates a job. Save the job ID, then read `GET /api/v1/launches/{job_id}` for the per-coin results. If a submission times out, check recent jobs before retrying; a repeated submission can create extra coins. The [full API quickstart](https://masslauncher.fun/blog/pump-fun-launch-api) explains authentication, profiles and recovery. Never put an API key in browser code, a GitHub issue or a screenshot.
