# LIVE_LEDGER

As of 2026-09-16 UTC, this ledger is seeded from public `sale` issues only because live `/ledger/revenue` was not readable from this environment at authoring time.

## Summary table (publicly verifiable)

| period | gross USDC to payTo (on-chain + sale-watch issues) | unique paying wallets | settlement failures if known | top paid endpoints if known |
|---|---:|---:|---|---|
| trailing 7d | 0.00 | 0 | unknown (no public failure log visible here) | unknown |
| trailing 30d | 1.75 | 8 | unknown (no public failure log visible here) | unknown |

## Source notes

- The 30d total above is computed from public `sale` issues dated 2026-08-17 through 2026-09-06, including:
  - [#525](https://github.com/kwizzlesurp10-ctrl/x402-mcp/issues/525) — $0.0500 USDC, `0xc22c17fc…`, BaseScan tx `0x532cf2b13f9a54b7e55b2b1195d671a4c42fa2a1c4519e33b14d8d10c24f260f`
  - [#523](https://github.com/kwizzlesurp10-ctrl/x402-mcp/issues/523) — $0.0100 USDC, `0x6777e11f…`, BaseScan tx `0x8baaae5a1a1e07a0161ed5d4ad15e16a806f1e530a5ad07a652c8ec9ecc24201`
  - [#522](https://github.com/kwizzlesurp10-ctrl/x402-mcp/issues/522) — $0.0100 USDC, `0x54e163e9…`, BaseScan tx `0x636ae5b7b721ab1ca0693d41768b60459e30735b3f943771d4d16f594331bea9`
  - [#501](https://github.com/kwizzlesurp10-ctrl/x402-mcp/issues/501) — $1.5000 USDC, `0xc22c17fc…`, BaseScan tx `0xf0b4b4b442c17d5f8276347d3c8e14daf5d8266192313de182bc59d5beab4723`
  - [#526](https://github.com/kwizzlesurp10-ctrl/x402-mcp/issues/526) — $0.0100 USDC, `0x7ef12be6…`, BaseScan tx `0x87811a9be488a36e8334e309672e9792cc0086afe10fe370c89a374ed41cda97`
- The 2026-08-26 `0xc22c17fc…` `$0.01` payment transactions requested in the issue are included via `sale` issues [#488](https://github.com/kwizzlesurp10-ctrl/x402-mcp/issues/488), [#489](https://github.com/kwizzlesurp10-ctrl/x402-mcp/issues/489), [#490](https://github.com/kwizzlesurp10-ctrl/x402-mcp/issues/490), [#491](https://github.com/kwizzlesurp10-ctrl/x402-mcp/issues/491), [#492](https://github.com/kwizzlesurp10-ctrl/x402-mcp/issues/492), [#499](https://github.com/kwizzlesurp10-ctrl/x402-mcp/issues/499), [#500](https://github.com/kwizzlesurp10-ctrl/x402-mcp/issues/500), [#502](https://github.com/kwizzlesurp10-ctrl/x402-mcp/issues/502), and [#503](https://github.com/kwizzlesurp10-ctrl/x402-mcp/issues/503).
- If `/ledger/revenue` becomes readable, this file should be extended (add-only) with endpoint-level breakdown and explicit settlement-failure counts.

## Calculation detail (30d window)

Included issues in 30d window: #480, #481, #483, #484, #488, #489, #490, #491, #492, #499, #500, #501, #502, #503, #522, #523, #525, #526.

Gross total check:

- $1.50 (issue #501)
- $0.05 + $0.05 (issues #483, #525)
- $0.01 × 15 (issues #480, #481, #484, #488, #489, #490, #491, #492, #499, #500, #502, #503, #522, #523, #526)

Total: **$1.75 USDC**.
