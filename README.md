# Amazon X-Ray (amazon-xray)
AWS X-Ray is a distributed tracing service that helps developers analyze and debug production applications, providing end-to-end visibility into requests as they travel through the application. X-Ray provides service maps, trace analysis, sampling rules, group filtering, and AI-powered insights for identifying performance bottlenecks and errors across microservices and serverless architectures.

**URL:** [https://raw.githubusercontent.com/api-evangelist/amazon-xray/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/amazon-xray/refs/heads/main/apis.yml)

**Run:** [Capabilities Using Naftiko](https://github.com/naftiko/fleet?utm_source=api-evangelist&utm_medium=readme&utm_campaign=company-api-evangelist&utm_content=repo)

## Tags:

 - Application Performance, AWS, Debugging, Distributed Tracing, Monitoring, Observability

## Timestamps

- **Created:** 2024-01-15
- **Modified:** 2026-04-19

## APIs

### Amazon X-Ray REST API
RESTful API for AWS X-Ray distributed tracing operations including trace retrieval, service map generation, sampling rule management, group management, and insights analysis for application performance monitoring. 30 operations for traces, service graphs, sampling, groups, and insights.

**Human URL:** [https://aws.amazon.com/xray/](https://aws.amazon.com/xray/)

#### Tags:

 - AWS, Distributed Tracing, Observability, Tracing

#### Properties

- [Documentation](https://docs.aws.amazon.com/xray/latest/api/)
- [OpenAPI](openapi/amazon-xray-openapi-original.yaml)
- [JSONSchema](json-schema/xray-trace-summary-schema.json)
- [JSONLD](json-ld/amazon-xray-context.jsonld)
- [Pricing](https://aws.amazon.com/xray/pricing/)
- [GettingStarted](https://aws.amazon.com/xray/getting-started/)
- [Authentication](https://docs.aws.amazon.com/xray/latest/api/CommonParameters.html)
- [SDK](https://aws.amazon.com/tools/)
- [FAQ](https://aws.amazon.com/xray/faqs/)
- [APIReference](https://docs.aws.amazon.com/xray/latest/api/Welcome.html)
- [CodeExamples](https://docs.aws.amazon.com/xray/latest/devguide/xray-sdk-sample.html)

## Common Properties

- [Portal](https://aws.amazon.com/)
- [Website](https://aws.amazon.com/xray/)
- [Documentation](https://docs.aws.amazon.com/xray/)
- [TermsOfService](https://aws.amazon.com/service-terms/)
- [PrivacyPolicy](https://aws.amazon.com/privacy/)
- [Support](https://aws.amazon.com/premiumsupport/)
- [Blog](https://aws.amazon.com/blogs/developer/)
- [GitHubOrganization](https://github.com/aws)
- [Console](https://console.aws.amazon.com/xray/)
- [SignUp](https://signin.aws.amazon.com/signup?request_type=register)
- [Login](https://aws.amazon.com/console/)
- [StatusPage](https://health.aws.amazon.com/health/status)
- [KnowledgeCenter](https://repost.aws/knowledge-center)
- [YouTube](https://www.youtube.com/user/AmazonWebServices)
- [StackOverflow](https://stackoverflow.com/questions/tagged/aws-xray)
- [Contact](https://aws.amazon.com/contact-us/)

## Features

| Name | Description |
|------|-------------|
| End-to-End Distributed Tracing | Trace requests as they travel across services, microservices, and serverless functions to identify bottlenecks and errors. |
| Service Map Visualization | Automatically generate visual service maps showing all connected services and their health status and latency. |
| Trace Filtering and Groups | Create groups with filter expressions to organize and analyze subsets of traces based on service names, URLs, or annotations. |
| Adaptive Sampling | Configurable sampling rules to control the percentage of requests traced, balancing coverage with cost. |
| X-Ray Insights | AI-powered automatic detection of anomalies and performance issues with root cause analysis across the service map. |
| AWS Service Integration | Native tracing support across Lambda, EC2, ECS, EKS, API Gateway, SNS, SQS, and 200+ other AWS services. |
| SDK and Agent Support | X-Ray SDKs for Java, Node.js, Python, Go, Ruby, and .NET for custom application instrumentation. |
| CloudWatch Integration | Deep integration with Amazon CloudWatch for correlating traces with metrics, logs, and alarms. |

## Use Cases

| Name | Description |
|------|-------------|
| Microservices Debugging | Trace requests across microservices to identify which service is causing latency or errors in distributed applications. |
| Serverless Application Monitoring | Monitor Lambda function execution chains and identify cold start impacts and downstream service bottlenecks. |
| Performance Optimization | Use trace data and service maps to identify and eliminate performance bottlenecks in production applications. |
| Root Cause Analysis | Drill into traces to understand the exact call chain that caused an error or latency spike. |
| SLA Compliance Monitoring | Track end-to-end latency and error rates across services to ensure application SLAs are being met. |

## Integrations

| Name | Description |
|------|-------------|
| AWS Lambda | Automatic tracing of Lambda function invocations and downstream calls. |
| Amazon API Gateway | Native tracing of API Gateway requests through backend services. |
| Amazon CloudWatch | Correlation of traces with CloudWatch metrics, logs, and alarms. |
| AWS App Mesh | Service mesh integration for automatic tracing of Envoy-based microservices. |
| OpenTelemetry | X-Ray supports the OpenTelemetry standard via the AWS Distro for OpenTelemetry. |

## Artifacts

Machine-readable API specifications organized by format.

### OpenAPI

- [Amazon X-Ray OpenAPI (Original)](openapi/amazon-xray-openapi.yml)
- [Amazon X-Ray OpenAPI (APIs-guru)](openapi/amazon-xray-openapi-original.yaml)

### JSON Schema

232 JSON Schema files extracted from the OpenAPI specification.

### JSON Structure

232 JSON Structure files converted from JSON Schema definitions.

### JSON-LD

- [Amazon X-Ray Context](json-ld/amazon-xray-context.jsonld)

### Examples

109 example JSON files generated from JSON Schema definitions.

## Capabilities

Naftiko capabilities organized as shared per-API definitions composed into customer-facing workflows.

### Shared Per-API Definitions

- [Amazon X-Ray API](capabilities/shared/xray.yaml) — 6 operations for trace retrieval, service graph, sampling, groups, and insights

### Workflow Capabilities

| Workflow | APIs Combined | Tools | Persona |
|----------|--------------|-------|---------|
| [Distributed Tracing](capabilities/distributed-tracing.yaml) | Amazon X-Ray | 6 | Developer, Site Reliability Engineer |

## Vocabulary

- [Amazon X-Ray Vocabulary](vocabulary/amazon-xray-vocabulary.yaml) — Unified taxonomy mapping 7 resources, 5 actions, 1 workflow, and 2 personas across operational (OpenAPI) and capability (Naftiko) dimensions

## Rules

- [Amazon X-Ray Spectral Rules](rules/amazon-xray-spectral-rules.yml) — 15 rules across 8 categories enforcing Amazon X-Ray API conventions

## Maintainers

**FN:** Kin Lane

**Email:** kin@apievangelist.com
