# JOLT (jolt-charge)

JOLT is a Sydney-headquartered electric vehicle charging network operator that builds and runs free-to-start kerbside DC fast chargers across Australia, and has since extended the same model into New Zealand, Canada, the United Kingdom and the United States. Its charge points deliver the first 7kWh of each day's charging at no cost — around 45km of range in roughly 15 minutes over CCS2 or CHAdeMO — funded not by the driver but by the digital out-of-home advertising screens mounted on the charger itself, which makes JOLT simultaneously a charge point operator and a media network selling audience reach to advertisers. It sits in the energy value chain as a downstream infrastructure and demand-side player: it buys electricity (claiming 100% GreenPower green-certified wind and solar), owns and operates the charging assets on public and retail land in partnership with governments and hosts such as Transport for NSW, Ausgrid and major grocery retailers, and monetises the dwell time rather than the kilowatt-hour. Its API posture is honestly closed. JOLT publishes no developer programme, no API documentation, no OpenAPI or other machine-readable contract, and no open data feed; the only public HTTP surfaces on its domains are a marketing WordPress install (whose custom `jolt/v1` REST namespace exposes a single VAT form endpoint) and an `api.joltcharge.com` host that serves a static redirect to the mobile app rather than any API. It is not a designated data holder under the Australian Consumer Data Right for energy — it does not appear in the CDR Register's energy data holder brands — so the CDR energy mandate that compels Australian electricity retailers to expose standardised usage and tariff data does not reach it, and no OCPP, OCPI, ISO 15118 or Green Button/ESPI conformance is published. All customer charging data, session history and audience analytics are reachable only through the JOLT consumer app or a sales conversation.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/jolt-charge/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/jolt-charge/refs/heads/main/apis.yml)

## Tags

- Energy
- Australia
- EV Charging
- Electricity
- Utilities
- Renewables
- Advertising
- Mobility
- Carbon
- Infrastructure

## Timestamps

- **Created:** 2026-07-27
- **Modified:** 2026-07-27

## APIs

None. JOLT publishes no documented public API. See [review.yml](review.yml) for the full probe log, including the subdomains and paths tested and the HTTP status returned by each.

There is, however, a **private** API. A second enrichment round (2026-07-27) corrected round 1's reading of `api.joltcharge.com`: the host root is a static S3 app-deep-link page, but the `/v1/` prefix on that same host routes to an AWS API Gateway stage that answers `401 {"message":"Unauthorized"}` (`x-amzn-errortype: UnauthorizedException`) on every path and method probed anonymously. JOLT's own public website bundle calls one endpoint on it — `POST https://api.joltcharge.com/v1/au/web/user` for partner/user sign-up, authenticated with a static `x-api-key` header hardcoded into the JavaScript served to every visitor. That surface is undocumented, unversioned publicly, offered to nobody, and so is deliberately **not** listed as an API here; it is recorded in `review.yml` under `privateApiSurface`. The credential value is not reproduced in this repository.

Also note: `joltcharge.com` returns HTTP **200 with the homepage body** for unknown paths under a region prefix, so a 200 on `/au/anything` proves nothing. Use the Yoast page sitemap and the page `<title>` as the existence test.

## Artifacts

- [conformance/jolt-charge-conformance.yml](conformance/jolt-charge-conformance.yml) — standards assertions (OCPI, OCPP, ISO 15118, CDR energy, OAuth2, OIDC, OpenAPI, AsyncAPI, RFC 9457, RFC 9116), every one negative, every one with the evidence observed
- [well-known/jolt-charge-well-known.yml](well-known/jolt-charge-well-known.yml) — the `/.well-known/` probe record across all three hosts; nothing published
- [security/jolt-charge-domain-security.yml](security/jolt-charge-domain-security.yml) — TLS 1.3 everywhere, no HSTS, no DNSSEC, no CAA; SPF + DMARC quarantine on `joltcharge.com`, no SPF and DMARC `p=none` on the legacy `jolt.com.au`
- [llms/jolt-charge-llms.txt](llms/jolt-charge-llms.txt) — generated agent-facing summary of the closed posture

## Mandate Posture

- **Home market:** Australia
- **Mandate regime:** none
- **Mandate status:** not-applicable
- **Data standard:** no standard reference found (CCS2 and CHAdeMO are connector standards, not data standards)
- **Consumer data API:** no
- **Open market data:** no
- **Access gate:** none-published

The Australian Consumer Data Right was extended from banking into energy, designating electricity retailers as data holders with AEMO as the gateway. That designation reaches retailers and AEMO — not charge point operators. An anonymous query against the CDR Register's public energy data holder brands endpoint (`https://api.cdr.gov.au/cdr-register/v1/energy/data-holders/brands/summary`, `x-v: 1`, HTTP 200) returned 84 brands on 2026-07-27; none of them is JOLT.

## Common Properties

- [Website](https://joltcharge.com/au/)
- [Blog](https://joltcharge.com/au/news/)
- [Blog RSS](https://joltcharge.com/au/feed/)
- [LinkedIn](https://www.linkedin.com/company/jolt-charge)
- [GitHub Organization](https://github.com/jolt-charge)
- [Support](https://joltcharge.com/au/contact/) — the contact form is the published support route; the `/au/support/` path recorded in round 1 is a soft-404
- [Contact Form](https://joltcharge.com/au/contact/)
- [Sign Up](https://joltcharge.com/au/start/)
- [Pricing](https://joltcharge.com/au/jolt-plus/)
- [Careers](https://joltcharge.com/au/careers/)
- [Terms of Service](https://joltcharge.com/au/terms/)
- [Privacy Policy](https://joltcharge.com/au/privacy/)
- [Fair Use Policy](https://joltcharge.com/au/fair-use-policy/)

## Maintainers

- Kin Lane — kin@apievangelist.com
