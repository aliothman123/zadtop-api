# Endpoints

Authentication: `X-API-Key` on every `/v1` route. The live field-by-field reference is [api.zadtop.com/docs](https://api.zadtop.com/docs). This page is the map.

| Method | Path | Notes |
| --- | --- | --- |
| `GET` | `/health` | Public health, when enabled |
| `GET` | `/v1/me` | Balance, plan, API add-on |
| `GET` | `/v1/quota` | Allowance left today |
| `GET` | `/v1/history` | Past orders |
| `GET` | `/v1/players` | Saved players |
| `GET` | `/v1/player/lookup` | Name and region. Query: `game`, `player_id` |
| `POST` | `/v1/jobs/instant-redeem` | `player_id`, `codes`, `game`. Ludo also needs `tier`. Razer recharge also needs `email` and `password` |
| `POST` | `/v1/jobs/stock-redeem` | Redeem reserved stock by pack |
| `POST` | `/v1/codes/check` | Up to 20 codes. Optional `with_value` |
| `POST` | `/v1/jobs/code-check` | Up to 10,000 codes |
| `GET` | `/v1/jobs/{id}` | Poll. `?wait=25` holds the request until the job finishes or 25 seconds pass |
| `GET` | `/v1/jobs` | Recent jobs |
| `GET` | `/v1/stock/summary` | Counts by game and pack |
| `POST` | `/v1/order/screenshot` | PNG of the shop confirmation |
| `POST` | `/v1/subscription/purchase` | Buy or extend a plan from the USDT balance |
| `POST` | `/v1/subscription/purchase-api-addon` | Buy the 15 USDT API add-on |
| `POST` | `/v1/subscription/purchase-check-code` | Buy a code-checking budget. Body: `{"plan_key":"cc1"}` or `cc2` |

## Games on the same routes

`freefire` · `pubg` · `ludo` · `ludogold` · `jawaker` · `itunes` · `razer` · `razer_recharge`

Details: [GAMES.md](./GAMES.md).

## Allowance

| Call | Requests |
| --- | --- |
| Redeem, per code | 1 |
| Check, per card | 1 |
| Razer Gold PIN, check or recharge | 5 |
| Player lookup | 0.25 |
| Account, history, stock, job poll, screenshot | 0 |

A Code checking subscription pays for checks first. It cannot redeem. Other routes then answer `403 CHECK_CODE_SUBSCRIPTION_ONLY`.

A plan that does not include the game answers `403 GAME_NOT_IN_PLAN`.
