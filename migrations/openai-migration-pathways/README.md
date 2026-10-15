# OpenAI Migration Pathways

OpenAI Migration Pathways is a Codex plugin that helps teams assess and plan migrations from Azure OpenAI or direct OpenAI integrations to Amazon Bedrock. Starting from customer requirements or a code repository, it identifies workloads and dependencies, evaluates model, API, and Region combinations against an evidence-based compatibility catalog, and checks requirements such as residency, caching, streaming, structured outputs, and tool use. It generates a standardized migration report with route recommendations, gaps and blockers, proposed orchestration, Azure-to-AWS service mappings, and validation steps. When requested, it also prepares architecture diagrams, application changes, and deployment artifacts, while recording assumptions, implementation status, and readiness for deployment.

See [installation](INSTALL.md), [the catalog](docs/compatibility-catalog.md), [release notes](docs/release-0.4.2.md), and [refresh procedure](docs/refreshing-evidence.md).

## Discovery without code

> Use $openai-migration-pathways. Help me migrate an Azure GPT-4.1 workload to Bedrock with geographic residency and prompt caching. Do not inspect code. Ask the questions needed to narrow the route and explain assumptions.

See [testing scenarios](docs/testing-scenarios.md), [discovery guidance](skills/openai-migration-pathways/references/discovery.md), and [compatibility rules](skills/openai-migration-pathways/references/route-compatibility.md). The refreshed workbook is in `assets/workbooks/`; the evaluator reads `data/capabilities.json`, not Excel. The target policy includes GPT-6 Astra, GPT-6.1 Sol, GPT-6 Sol, GPT-6 Luna, GPT-5.6 Sol/Terra/Luna, GPT-5.5 and GPT-5.4. GPT-OSS and Daybreak are excluded. Other source models remain valid migration inputs; they are not target candidates.

## Start a migration (with code assessments)

After installing the plugin, start a new Codex task:

> Use $openai-migration-pathways for this repository: <GitHub URL>. Assess the entire repository and prepare the AWS deployment package, application changes, and one unified Azure-to-AWS architecture. Target Region: <AWS Region>. Do not deploy cloud resources.

## What the customer receives

Every full saved assessment includes readable Markdown and a shared JSON contract:

1. Decision and target-model recommendations.

2. Scope, evidence and execution provenance.

3. Workload and route inventory.

4. Source AI contracts.

5. Bedrock feature mapping and API migration, including orchestration designs.

6. Azure-to-AWS service mapping.

7. Unified architecture and data flows.

8. Deployment implementation and gaps, including the central gap and blocker register.

9. Validation, readiness and next actions.

Discovery records supplied requirements and assumptions. Code assessment adds repository evidence, source-call contracts and coverage. Every gap identifies affected routes/services, impact, owner, resolution, tests and any stage it blocks. Orchestration acceptance, implementation and verification are separate states. See the [shared report contract](skills/openai-migration-pathways/references/shared-report.md) and [fictional discovery example](examples/discovery-report/assessment.md).

When application changes or a deployment package are requested, additional outputs include a canonical service matrix, application and infrastructure source, one architecture in Draw.io/SVG/JSON, migration waves, validation evidence and checksums. These require workload-specific implementation.

The optional [deployment page](docs/deployment-page.md) supports preparation and authorized deployment workflows. **Its current account-availability check cannot verify the approved catalog's inference-profile or Mantle routes. Live deployment stays blocked until a suitable account-specific verifier is supplied.** Catalog compatibility and a passing report validator do not establish account access or deployment readiness.

The architecture shows Azure placement, migration connections, and the AWS target. The bundle includes 36 pinned official Azure/AWS icons; services without a matching icon use labeled shapes. Approved OpenAI model choices use `bedrock-runtime` or `bedrock-mantle` when available. GPT-OSS and Daybreak are not target candidates.

## Examples scenarios - copy the following examples in the prompt to try the plugin

Paste any of these into the OpenAI Migration Pathways agent to exercise discovery mode. Each is written the same way a field rep would describe a customer — no pre-filled answers, so the engine runs its own discovery and route evaluation. They deliberately cover three different outcomes: a residency conflict, a clean structured-output case, and a zero-retention conflict.

### Scenario 1 — EU residency vs. US-only model

A geography conflict: the workload demands EU processing, which forces the engine to confront entry-Region-vs-processing-Region and reject US/global profiles.

> Migrate our Azure OpenAI customer-support assistant to Bedrock. It uses streaming and client-side tools, and we rely on prompt caching for a long shared system prompt. Hard requirement: all inference and cached data must stay within the EU — this is a regulated banking customer. Which Bedrock pathway supports this, and if none does, what are our options?

### Scenario 2 — Structured outputs for a data-extraction pipeline

A cleaner case that should surface a qualifying or verify-level pathway, and exercises the structured-output nuance (native strict schema vs. VERIFY across APIs).

> We have a direct OpenAI document-extraction service moving to Bedrock. It needs strict structured JSON outputs (a fixed schema), plus streaming and client tools. No prompt caching, no guardrails. US geography is fine, any US Region works. Which model and API should we use, and is strict structured output actually native or does it need verification?

### Scenario 3 — Zero-retention vs. background + stored state

A retention conflict: ZDR collides with background execution and stored conversation state, and should trip the engine's "store=false is not full ZDR" and retention-conflict logic.

> Our Azure OpenAI agent runs long background jobs and keeps stored conversation state across turns. We're migrating to Bedrock under a strict zero-data-retention policy for a healthcare client. We also want streaming. Can we keep background execution and stored state under ZDR, and what exactly has to change if not?

## Licensing and publication

Original code follows MIT-0 and original documentation follows CC-BY-SA-4.0, matching the repository. Third-party artwork and captured provider documentation retain their own terms; see [LICENSING.md](LICENSING.md) and [THIRD-PARTY-NOTICES.md](THIRD-PARTY-NOTICES.md). Authors: EB Khiyami.

See [publishing and release checks](docs/publishing.md) for the marketplace layout, CI, release tags and archive verification.
