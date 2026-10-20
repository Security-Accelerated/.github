# Security Accelerated

Domain and IP intelligence for security teams, delivered as one REST API.

Most of what an analyst does when a domain or address shows up in an alert is the same
dozen lookups, in the same order, by hand. The **Intelligence API** runs them concurrently
and returns one JSON document, so the answer to "what is this thing?" is a single request.

## Intelligence API

**[Source](https://github.com/Security-Accelerated/intelligence-api)** ·
**[Docs](https://api.securityaccelerated.com/docs)** ·
**[OpenAPI 3.1](https://api.securityaccelerated.com/docs/openapi.yaml)** ·
**[Release notes](https://api.securityaccelerated.com/docs/changelog)**

**Domains:** WHOIS, DNS, TLS certificate, HTTP headers, email security (SPF, DKIM, DMARC,
MTA-STS, TLS-RPT, BIMI), subdomains, certificate transparency, BGP/ASN, technology
fingerprinting, DNSSEC and CAA, reputation, threat intelligence, and an aggregate risk
score.

**IPs:** GeoIP, ASN, reverse DNS, abuse contact, threat intelligence.

```sh
curl -s https://api.securityaccelerated.com/v1/domain/lookup \
  -H 'X-API-Key: YOUR_KEY' -H 'Content-Type: application/json' \
  -d '{"domains":["example.com"],"lookups":["dns","ssl","email_security","risk"]}'
```

Every lookup in the response carries its own `cache_hit`, and a lookup that fails reports
why in a per-result `errors` array instead of failing the whole request. You always get
what worked.

### Plans

| | Free | Pro |
|---|---|---|
| Rate limit | 5 req/min | 120 req/min |
| Domains or IPs per request | 1 | 20 |
| Core and extended lookups, risk score | Yes | Yes |
| Reputation and threat intelligence | No | Yes |

Pro keys are self-service: subscribe from the [docs](https://api.securityaccelerated.com/docs),
get the key on the confirmation page, rotate it yourself with a grace window, and query
your own usage from the API.

### Why the source is public

The code is published so it can be read and evaluated before you send it anything. It is
source-available, all rights reserved, not open source. Outbound connections go through a
single SSRF-prevention layer, failures are never cached, and the production release
process is in the repo.

## Contact

Questions and support: support@securityaccelerated.com

Security reports: see [SECURITY.md](https://github.com/Security-Accelerated/intelligence-api/blob/main/SECURITY.md)
