# JOLT (jolt-charge)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
