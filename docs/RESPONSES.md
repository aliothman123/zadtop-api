# Responses

## HTTP

| Status | When |
| --- | --- |
| `401` | The key is missing, mistyped, or was replaced |
| `403` | No active plan with the API add-on |
| `403 CHECK_CODE_SUBSCRIPTION_ONLY` | This key can check codes and cannot redeem |
| `403 GAME_NOT_IN_PLAN` | Add this game to the plan |
| `400 INVALID_CODE` | Not a valid code for this game. Nothing was sent |
| `400 INVALID_PLAYER_ID` | Not a valid player ID. Nothing was sent |
| `400 INSUFFICIENT_BALANCE` | The USDT balance does not cover the price |
| `422 UNSUPPORTED_REGION` | Garena sells no vouchers in this player's country |
| `429 QUOTA_EXHAUSTED` | Not enough requests left today. They refill at midnight UTC |
| `429 RATE_LIMIT` | Wait for the `Retry-After` seconds |
| `503 SERVICE_DRAINING` | A short restart. Nothing was queued. Retry in a few seconds |

## One card inside a finished job

`done` is the job, not a promise that every card succeeded.

| `err_code` | Meaning | Charged? |
| --- | --- | --- |
| `CODE_ALREADY_USED` | Already redeemed | yes |
| `INVALID_CODE` | The shop does not recognise it | yes |
| `REGION_MISMATCH` | Wrong region | yes |
| `PLAYER_NOT_FOUND` | No such player. Cards were not used | yes, as the answer |
| `ACCOUNT_RESTRICTED` | The account does not accept top-ups | yes |
| `NETWORK` | The connection dropped, the shop refused the request, or no result came back | refunded |
| `SESSION_EXPIRED` | Try again | refunded |
| `VERIFICATION` · `VERIFICATION_FAILED` | Verification did not pass. The card was not spent | refunded |
| `RATE_LIMITED` · `SHOP_BLOCKED` · `SHOP_MAINTENANCE` | Try later | refunded |

Check statuses are `valid`, `used`, `invalid`, `expired`, `inactive`, `blocked`, `region_mismatch`, `unknown`, and `error`. Only `valid` means the card can be redeemed. `unknown` and `error` mean the answer is not known yet.

A Razer recharge uses `recharged` when the PIN was credited. `wallet_full` means the wallet had no room: the PIN was not credited and is not charged.

Do not read a pack value as a status. A used card can still carry the pack it was sold as.
