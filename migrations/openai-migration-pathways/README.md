# OpenAI Migration Pathways

Version 0.4.2 packages this solution for the OpenAI Solutions on AWS marketplace and gives discovery and code assessments the same nine-section report, with linked routes, gaps/blockers, orchestration designs and Azure-to-AWS service mappings. It retains the nine-model compatibility catalog and official evidence reviewed October 14, 2026. See [installation](INSTALL.md), [the catalog](docs/compatibility-catalog.md), [release notes](docs/release-0.4.2.md), and [refresh procedure](docs/refreshing-evidence.md).

## Discovery without code

> Use $openai-migration-pathways. Help me migrate an Azure GPT-4.1 workload to Bedrock with geographic residency and prompt caching. Do not inspect code. Ask the questions needed to narrow the route and explain assumptions.

See [testing scenarios](docs/testing-scenarios.md), [discovery guidance](skills/openai-migration-pathways/references/discovery.md), and [compatibility rules](skills/openai-migration-pathways/references/route-compatibility.md). The refreshed workbook is in `assets/workbooks/`; the evaluator reads `data/capabilities.json`, not Excel. The target policy includes GPT-6 Astra, GPT-6.1 Sol, GPT-6 Sol, GPT-6 Luna, GPT-5.6 Sol/Terra/Luna, GPT-5.5 and GPT-5.4. GPT-OSS and Daybreak are excluded. Other source models remain valid migration inputs; they are not target candidates.

## Start a migration

After installing the plugin, start a new Codex task:

> Use $openai-migration-pathways for this repository: <GitHub URL>. Assess the entire repository and prepare the AWS deployment package, application changes, and one unified Azure-to-AWS architecture. Target Region: <AWS Region>. Do not deploy cloud resources.

A branch or tag is enough; Codex resolves the commit. No existing checkout is needed. Private repositories use the customer's configured access. With approval for a named Azure tenant/subscription, Codex uses available read-only discovery tools. Without that access, it continues with repository evidence and labels what is unverified.

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

## What runs where

The plugin contains instructions, artifact helpers, an optional customer-operated deployment runner, and reusable application/infrastructure source. Codex performs the analysis and implementation with the tools available in the customer's workspace.

Installing or using it does not require Docker, GitHub Actions, a custom signed runtime, root-owned trust keys, or the publisher's Mac. Python helpers use the standard library; renderers and evaluators make no cloud calls. The optional evidence refresher fetches official public documentation only. A container builder is needed only to verify container images. Customer dependencies and credentials are specific to the application, not plugin installation.

Preparing a package does not deploy it. Each workload is labeled source-only, statically checked, build-verified, or deployment-verified according to actual evidence. An arbitrary repository may still need application-specific migration work. Cloud changes require a separately authorized deployment.

## Source and verification

The portable manifest is `plugin.json`; `.codex-plugin/plugin.json` supplies matching compatibility metadata. [INSTALL.md](INSTALL.md) covers local installation and sharing a source archive. The release includes no publisher credentials or mandatory cloud connection.

Maintainer details: [implementation notes](docs/implementation-notes.md). Output contract: [deployment package](skills/openai-migration-pathways/references/deployment-package.md). Diagram contract: [architecture](skills/openai-migration-pathways/references/architecture.md).

The [Customer Assist reference wiring](assets/fargate-hosting/customer-assist.md) connects its ported frontend, session service and worker. Use it with the matching application patch; it is not a generic configuration for every repository.

Offline regression tests are included under `scripts/test_*.py`. Run `python3 -B scripts/package_plugin.py /path/to/new-release-directory --marketplace-name openai-solutions` to create a shareable marketplace folder and ZIP with file checksums. Python 3.10 or later is required for the helpers. Application build and deployment verification are still required for each migration.

## Licensing and publication

Original code follows MIT-0 and original documentation follows CC-BY-SA-4.0, matching the repository. Third-party artwork and captured provider documentation retain their own terms; see [LICENSING.md](LICENSING.md) and [THIRD-PARTY-NOTICES.md](THIRD-PARTY-NOTICES.md). Authors: Sudeesh and EB Khiyami.

See [publishing and release checks](docs/publishing.md) for the marketplace layout, CI, release tags and archive verification.
