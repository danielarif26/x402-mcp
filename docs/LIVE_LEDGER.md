# LIVE_LEDGER

As of 2026-09-16 UTC, this ledger is seeded from public `sale` issues only because live `/ledger/revenue` was not readable from this environment at authoring time. This snapshot uses issue `created_at` as a period proxy because BaseScan timestamps were not machine-read in this environment.

Update rule (add-only): append a new dated snapshot section for each future update, and keep one source per snapshot (do not mix issue-derived and ledger-derived totals within the same period row). Historical snapshots stay frozen (never recompute an older snapshot from a different source).

## Summary table (publicly verifiable)

| period | gross USDC to payTo (on-chain + sale-watch issues) | unique paying wallets | settlement failures if known | top paid endpoints if known |
|---|---:|---:|---|---|
| trailing 7d | 0.00 | 0 | unknown (no public failure log visible here) | unknown |
| trailing 30d | 1.75 | 8 | unknown (no public failure log visible here) | unknown |

## Source notes

- The 30d total above is computed from public `sale` issues dated 2026-08-17 through 2026-09-06, including:
  - [#480](https://github.com/kwizzlesurp10-ctrl/x402-mcp/issues/480) — $0.0100 USDC, `0xc533bf52…`, BaseScan tx `0xcdbce4500066fa4d8f0715709a5fcaf6b984e54c274972ee77e0b82fb7eb99b4`
  - [#481](https://github.com/kwizzlesurp10-ctrl/x402-mcp/issues/481) — $0.0100 USDC, `0x9138fea6…`, BaseScan tx `0x60f160658a5a8c18efdc800d396c92c9fdd40c590c43e2d4657de1f92d70029e`
  - [#483](https://github.com/kwizzlesurp10-ctrl/x402-mcp/issues/483) — $0.0500 USDC, `0xc59e74ed…`, BaseScan tx `0xc561420278c18f89831b2d34407ac9d3ad968b055b63cf62d68110c6e14ccca0`
  - [#484](https://github.com/kwizzlesurp10-ctrl/x402-mcp/issues/484) — $0.0100 USDC, `0x644678ad…`, BaseScan tx `0x071428674f7bdcd4a75571b5623563e55be16c9c2682a345efbabd5e51910324`
  - [#525](https://github.com/kwizzlesurp10-ctrl/x402-mcp/issues/525) — $0.0500 USDC, `0xc22c17fc…`, BaseScan tx `0x532cf2b13f9a54b7e55b2b1195d671a4c42fa2a1c4519e33b14d8d10c24f260f`
  - [#523](https://github.com/kwizzlesurp10-ctrl/x402-mcp/issues/523) — $0.0100 USDC, `0x6777e11f…`, BaseScan tx `0x8baaae5a1a1e07a0161ed5d4ad15e16a806f1e530a5ad07a652c8ec9ecc24201`
  - [#522](https://github.com/kwizzlesurp10-ctrl/x402-mcp/issues/522) — $0.0100 USDC, `0x54e163e9…`, BaseScan tx `0x636ae5b7b721ab1ca0693d41768b60459e30735b3f943771d4d16f594331bea9`
  - [#501](https://github.com/kwizzlesurp10-ctrl/x402-mcp/issues/501) — $1.5000 USDC, `0xc22c17fc…`, BaseScan tx `0xf0b4b4b442c17d5f8276347d3c8e14daf5d8266192313de182bc59d5beab4723`
  - [#526](https://github.com/kwizzlesurp10-ctrl/x402-mcp/issues/526) — $0.0100 USDC, `0x7ef12be6…`, BaseScan tx `0x87811a9be488a36e8334e309672e9792cc0086afe10fe370c89a374ed41cda97`
- Complete 18-issue set used for trailing-30d is listed in **Calculation detail (30d window)** below.
- The `$0.01 × 15` line item in trailing-30d consists of these 15 `sale` issues: [#480](https://github.com/kwizzlesurp10-ctrl/x402-mcp/issues/480), [#481](https://github.com/kwizzlesurp10-ctrl/x402-mcp/issues/481), [#484](https://github.com/kwizzlesurp10-ctrl/x402-mcp/issues/484), [#488](https://github.com/kwizzlesurp10-ctrl/x402-mcp/issues/488), [#489](https://github.com/kwizzlesurp10-ctrl/x402-mcp/issues/489), [#490](https://github.com/kwizzlesurp10-ctrl/x402-mcp/issues/490), [#491](https://github.com/kwizzlesurp10-ctrl/x402-mcp/issues/491), [#492](https://github.com/kwizzlesurp10-ctrl/x402-mcp/issues/492), [#499](https://github.com/kwizzlesurp10-ctrl/x402-mcp/issues/499), [#500](https://github.com/kwizzlesurp10-ctrl/x402-mcp/issues/500), [#502](https://github.com/kwizzlesurp10-ctrl/x402-mcp/issues/502), [#503](https://github.com/kwizzlesurp10-ctrl/x402-mcp/issues/503), [#522](https://github.com/kwizzlesurp10-ctrl/x402-mcp/issues/522), [#523](https://github.com/kwizzlesurp10-ctrl/x402-mcp/issues/523), and [#526](https://github.com/kwizzlesurp10-ctrl/x402-mcp/issues/526).
- If `/ledger/revenue` becomes readable, this file should be extended (add-only) with a new snapshot and endpoint-level breakdown plus explicit settlement-failure counts.
- Unique-wallet count for trailing 30d is from these eight payer addresses in included issues: `0xc533bf52…`, `0x9138fea6…`, `0xc59e74ed…`, `0x644678ad…`, `0xc22c17fc…`, `0x54e163e9…`, `0x6777e11f…`, `0x7ef12be6…`.

## Reproducible retrieval steps

Use public issue data only (no wallet spend required):

```bash
curl -s "https://api.github.com/repos/kwizzlesurp10-ctrl/x402-mcp/issues?state=all&labels=sale&per_page=100" > /tmp/sale_issues.json
jq -r '.[] | [.number, .created_at, .title] | @tsv' /tmp/sale_issues.json
```

Then:

1. For future snapshots, determine period membership from settlement time: use the BaseScan timestamp for each tx hash in the issue body (preferred). This 2026-09-16 snapshot used `created_at` fallback. If a tx timestamp cannot be read, fallback to `created_at` and mark that period cell as `trailing Nd (approx)`.
2. Read `Amount` and `From` fields from each issue body.
3. Sum amounts for `gross USDC`, count distinct `From` wallets for `unique paying wallets`.
4. If settlement-failure or endpoint-attribution fields are absent in public issue bodies, report `unknown`.

## Calculation detail (30d window)

Included issues in 30d window: #480, #481, #483, #484, #488, #489, #490, #491, #492, #499, #500, #501, #502, #503, #522, #523, #525, #526.

Gross total check:

- $1.50 (issue #501)
- $0.05 + $0.05 (issues #483, #525)
- $0.01 × 15 (issues #480, #481, #484, #488, #489, #490, #491, #492, #499, #500, #502, #503, #522, #523, #526)

Total: **$1.75 USDC**.
