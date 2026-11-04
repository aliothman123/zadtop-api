# Quick start

Base URL: `https://api.zadtop.com`

1. Open [@ZadTopBot](https://t.me/ZadTopBot), top up USDT, choose a plan, and buy the HTTP API add-on.
2. Create an API key. A new key replaces the old one immediately.
3. Send the key on every call:

```http
X-API-Key: pk_YOUR_KEY
Content-Type: application/json
```

## Redeem

```bash
curl -sS -X POST https://api.zadtop.com/v1/jobs/instant-redeem \
  -H "X-API-Key: pk_YOUR_KEY" \
  -H "Content-Type: application/json" \
  -d '{"player_id":"2186053213","codes":["4233939008625064"],"game":"freefire"}'
```

The response includes a `job_id`. Redeem and bulk checks are asynchronous.

## Read the result

```bash
curl -sS "https://api.zadtop.com/v1/jobs/JOB_ID?wait=25" \
  -H "X-API-Key: pk_YOUR_KEY"
```

`status: done` means the job finished. Read `results[].success` and `results[].err_code` for each code.

## Check without redeeming

```bash
curl -sS -X POST https://api.zadtop.com/v1/codes/check \
  -H "X-API-Key: pk_YOUR_KEY" \
  -H "Content-Type: application/json" \
  -d '{"game":"freefire","with_value":true,"codes":["4233939008625064"]}'
```

Up to 20 codes on this route. Larger batches use `POST /v1/jobs/code-check` (up to 10,000) and are polled like a redeem.

## Player name

```bash
curl -sS "https://api.zadtop.com/v1/player/lookup?game=pubg&player_id=5123456789" \
  -H "X-API-Key: pk_YOUR_KEY"
```

Lookup is synchronous and costs 0.25 of a request when it succeeds.
