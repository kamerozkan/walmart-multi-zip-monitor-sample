# Data Notice

## Purpose

This repository is a technical sample for the [Walmart Multi-Zip Monitor Actor](https://apify.com/kamerozkan/walmart-multi-zip-monitor). It demonstrates exact task inputs, live output shapes, validation status, selected-store context, and conservative downstream decisions.

It is not a nationwide inventory dataset, a continuous real-time feed, a physical shelf count, or a complete Walmart catalog.

## Audit snapshot

The following state was verified through the Apify API and public Store page on 2026-07-28:

| Item | Verified value |
|---|---|
| Actor | `kamerozkan/walmart-multi-zip-monitor` |
| Actor ID | `3cwqAqYVIVaObWGRE` |
| Public | `true` |
| Current latest build | `0.0.38`, build ID `grQanbey4Ku2ca9Ad`, build status `SUCCEEDED` |
| Public Store Example Tasks | 2 |
| Public five-ZIP task | `bf8K5citBpGdKx3wt` |
| Public price-and-restock task | `5BK6oCAFavoRVxdgS` |
| Latest successful Actor run | `vMIdkNEUObGusnug1`, build `0.0.37`, dataset `6TSxRMjjWnhhtRPO3`, 2 rows |
| Latest successful public five-ZIP run | `7x6IhPLO44mMXLUhD`, build `0.0.36`, dataset `JlisIcT1iGaHa3X0O`, 10 rows |
| Latest successful public price-and-restock run | `WgYXoRN3WgDfPgo8o`, build `0.0.36`, dataset `BarHFQsOSNnaVafYf`, 9 rows |

The current `0.0.38` build finished after the inspected runs. No successful runtime observation of `0.0.38` was present in the inspected history, so these files do not claim to validate that version's runtime behavior.

## Public, private, and replay boundaries

- [`01_compare_five_zip_codes.json`](01_compare_five_zip_codes.json) and [`02_price_restock_watch.json`](02_price_restock_watch.json) are exact public Store Example Task inputs.
- [`03_grocery_change_only_watch.json`](03_grocery_change_only_watch.json) is an exact existing private task configuration. That task had zero runs at audit time.
- All three output files are redacted excerpts from live datasets.
- No deterministic or hand-authored replay output is included.
- No output is represented as customer activity.

The legacy `monitorKey` value in input 02 was already exposed by the public Store Example Task. It is not an Apify API token, password, cookie, or Walmart account credential.

## Output provenance

### Outputs 01 and 03

[`01_live_validated_in_stock.json`](01_live_validated_in_stock.json) and [`03_live_blocked_diagnostic.json`](03_live_blocked_diagnostic.json) came from the latest successful run and dataset listed above.

That run requested and emitted two rows:

- 1 validated success row
- 1 blocked diagnostic row
- 1 chargeable validated check
- overall run health `DEGRADED`

The run succeeded because it preserved both the validated row and the explicit non-chargeable failure diagnostic.

### Output 02

[`02_live_digital_out_of_stock.json`](02_live_digital_out_of_stock.json) came from the latest successful public price-and-restock task run.

That dataset contained nine successful rows:

- 8 with digital `IN_STOCK`
- 1 with digital `OUT_OF_STOCK`
- all 9 with a non-null prior observation
- 0 with a typed change in that run

The sample is the single observed `OUT_OF_STOCK` row. It is not a claim about current or nationwide availability.

## Redactions

The original `combinationId` in each output sample was replaced with a clearly non-operational identifier. Public product IDs, generic references, requested ZIPs, resolved store context, product titles, prices, fulfillment signals, statuses, and timestamps were preserved because they are necessary to explain the row contract and contain no person-level data.

Values are historical observations. Do not treat sample prices or availability as current.

## Privacy boundary

The samples contain no:

- customer names
- email addresses
- phone numbers
- delivery addresses
- Walmart account data
- cookies
- payment data
- API tokens

The optional `reference` input becomes `inputRef`. Do not place personal data, secrets, or customer account identifiers in that field.

## Interpretation limits

- `locationApplied = true` indicates that the returned website context was accepted for the selected store. It does not confirm physical shelf inventory.
- `zipCodeRequested` and `zipCodeResolved` may differ because a requested ZIP can map to a nearby store.
- `availability`, pickup, delivery, and shipping are point-in-time digital signals.
- `status = success` applies to that product, selected-store context, and observation time only.
- Failure rows must not be converted into zero price or `OUT_OF_STOCK`.
- `previous` and `changes` compare stored observations. They do not observe every website change between runs.
- The requested matrix is not evidence of nationwide completeness.
- Polling does not provide exact real-time monitoring.
- Website changes, throttling, and access defenses can create partial, blocked, or failed observations.
- This independent Actor is not affiliated with, endorsed by, or sponsored by Walmart.
- No uptime, freshness, accuracy, or completeness SLA is provided by this repository.

Users are responsible for reviewing applicable law, platform terms, retention rules, and downstream use requirements.

## Listing update on September 30, 2026

The Store title, description and search metadata were checked against the owned Actor and synchronized with this repository. This documentation update does not alter executable code, input or output schemas, recorded test outputs, artifact hashes, billing or runtime builds. Existing examples retain their original dates and validation limits. A public listing is not evidence of successful output, network acceptance or an achieved search ranking.
