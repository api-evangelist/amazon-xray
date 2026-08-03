# Amazon X-Ray (amazon-xray)

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
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

AWS X-Ray is a distributed tracing service that helps developers analyze and debug production applications, providing end-to-end visibility into requests as they travel through the application. X-Ray provides service maps, trace analysis, sampling rules, group filtering, and AI-powered insights for identifying performance bottlenecks and errors across microservices and serverless architectures.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/amazon-xray/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/amazon-xray/refs/heads/main/apis.yml)

## Scope

- **Type:** Index

## Tags

- Application Performance
- AWS
- Debugging
- Distributed Tracing
- Monitoring
- Observability

## Timestamps

- **Created:** 2024-01-15
- **Modified:** 2026-05-19

## APIs

### Amazon X-Ray REST API

RESTful API for AWS X-Ray distributed tracing operations including trace retrieval, service map generation, sampling rule management, group management, and insights analysis for application performance monitoring. 30 operations for traces, service graphs, sampling, groups, and insights.

- **Human URL:** [https://aws.amazon.com/xray/](https://aws.amazon.com/xray/)
- **Base URL:** `https://xray.amazonaws.com`

#### Tags

- AWS
- Distributed Tracing
- Observability
- Tracing

#### Properties

- [Documentation](https://docs.aws.amazon.com/xray/latest/api/)
- [OpenAPI](openapi/amazon-xray-openapi-original.yaml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [JSON Schema](json-schema/xray-trace-summary-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON-LD](json-ld/amazon-xray-context.jsonld) — [JSON-LD](https://www.w3.org/TR/json-ld11/)
- [Pricing](https://aws.amazon.com/xray/pricing/)
- [Getting Started](https://aws.amazon.com/xray/getting-started/)
- [Authentication](https://docs.aws.amazon.com/xray/latest/api/CommonParameters.html)
- [SDK](https://aws.amazon.com/tools/)
- [Status Page](https://status.aws.amazon.com/)
- [F A Q](https://aws.amazon.com/xray/faqs/)
- [API Reference](https://docs.aws.amazon.com/xray/latest/api/Welcome.html)
- [Code Examples](https://docs.aws.amazon.com/xray/latest/devguide/xray-sdk-sample.html)
- [Security](https://docs.aws.amazon.com/xray/latest/devguide/security.html)

## Common Properties

- [Portal](https://aws.amazon.com/)
- [Website](https://aws.amazon.com/xray/)
- [Documentation](https://docs.aws.amazon.com/xray/)
- [Terms of Service](https://aws.amazon.com/service-terms/)
- [Privacy Policy](https://aws.amazon.com/privacy/)
- [Support](https://aws.amazon.com/premiumsupport/)
- [Blog](https://aws.amazon.com/blogs/developer/)
- [GitHub Organization](https://github.com/aws)
- [Console](https://console.aws.amazon.com/xray/)
- [Sign Up](https://signin.aws.amazon.com/signup?request_type=register)
- [Login](https://aws.amazon.com/console/)
- [Status Page](https://health.aws.amazon.com/health/status)
- [Knowledge Center](https://repost.aws/knowledge-center)
- [YouTube](https://www.youtube.com/user/AmazonWebServices)
- [Stack Overflow](https://stackoverflow.com/questions/tagged/aws-xray)
- [Contact](https://aws.amazon.com/contact-us/)
- [Spectral Rules](rules/amazon-xray-spectral-rules.yml)
- [Vocabulary](vocabulary/amazon-xray-vocabulary.yaml)
- [Features](undefined)
- [Use Cases](undefined)
- [Integrations](undefined)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
