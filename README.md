# Colony Commons

> Status: research and build plan, updated 6 October 2026. No Colony hive, token, or deployment is implemented in this repository. The starting framework is not selected.

Colony Commons funds the integration, independent evaluation, and operation of open agent hives. It builds on existing projects, contributes reusable improvements to them, and publishes evidence for its deployment decisions.

The first objective is a small, useful hive that another team can reproduce. A larger colony follows only if the smaller system earns it through measured results.

- [Starting-point study: Omega and alternatives](docs/starting-point-study.md)
- [First hive: scope, comparison trial, and acceptance checks](docs/first-hive.md)

## Fit with existing projects

These are independent potential partners, not guilds under Colony's authority. No partnership or endorsement is implied.

| Existing effort | Work already under way | Colony's contribution |
|---|---|---|
| [OpenCog Hyperon](https://singularitynet.io/research/opencog-hyperon/) and [Omega](https://github.com/singnet/Omega) | Symbolic representation, reasoning, learning, and an agent framework that uses part of Hyperon. | Test and connect components; fund missing interfaces; send fixes to the original projects. Omega is a candidate, not a committed base. |
| [ASI Alliance](https://superintelligence.io/products/asi-chain/) | Agent platforms, compute, and decentralized infrastructure. ASI:Chain's public roadmap still includes unfinished shared-memory and Hyperon integration. | Run useful workloads, build deployment adapters, and publish reliability and cost data. Choose infrastructure by demonstrated readiness. |
| [BGI Commons](https://bgicommons.org/resources/bgi-commons-overview) | Community, learning resources, and build sprints around beneficial AGI. | Sponsor specific challenges and fund continued work, independent review, and maintenance after a sprint. |
| [DEEP / Deep Funding](https://deep-projects.ai/) and [Alliance support programmes](https://superintelligence.io/grants/) | Grants, milestone funding, startup support, and compute support. | Check existing awards before funding a gap. Seek joint funding where useful. |

Assurance is also an existing research direction. Goertzel describes specification work and proposed Genode/seL4 ports for parts of this stack; he distinguishes those plans from completed ports. Colony can help implement and independently check such work. See his [technical account](https://bengoertzel.substack.com/p/averting-the-cybersecurity-apocalypse).

Colony's useful role is delivery: one working integration, evidence others can check, and funded improvements. It does not need a new language, blockchain, general agent marketplace, or community portal to begin.

## Build the first hive

The first use case is software maintenance in a bounded repository workspace:

1. A planner turns an issue into a task and acceptance checks.
2. A worker proposes a patch and runs permitted tools.
3. A separate reviewer examines the patch and test evidence.
4. An authorised operator decides whether to submit or release it under the current policy.

The roles share a structured record of tasks, observations, artifacts, and decisions. Claims must point to evidence. Shared chat alone does not meet this requirement.

Start by comparing existing runtimes. Keep the task format, evidence format, evaluation suite, and tool permissions independent of the chosen runtime. The [starting-point study](docs/starting-point-study.md) gives a provisional recommendation and records what still needs a trial. No framework is selected by affiliation alone.

## Work groups

One treasury, five work groups, no sub-tokens. These describe responsibilities; one small team can cover several groups.

| Work group | First responsibility |
|---|---|
| Hive integration | Select and assemble existing components. Maintain interfaces and reproducible builds. |
| Motivation and constitution | Turn approved goals and rules into clear operating requirements. Treat stable motivation under broad self-modification as a research goal. |
| Ontology and evaluation | Maintain the shared evidence schema and independent comparisons. Test Hyperseed or other symbolic representations when a concrete task requires them. |
| Assurance | Check access limits, resource limits, update controls, and proof claims. Publish assumptions and failures. |
| Deployment and governance | Operate the reference hive, manage its releases, and administer treasury decisions. |

A super-colony is a later deployment of multiple hives with shared rules and defined state exchange. It is not a separate guild or a requirement for the first prototype.

## Evidence and release rules

Compare the hive with a single-agent baseline on the same tasks and resource limits. Report task success, regressions, reviewer effort, recovery from failure, and total cost. Use fixed development tasks and fresh evaluation tasks; publish evaluation methods and release completed test cases when rights permit.

Independent reviewers check metric gains and proof claims and certify acceptance before payment releases. Builders retain their token voting rights, but cannot serve as the independent acceptance reviewer for their own work. Fund replication, useful negative results, and maintenance as well as improvements. Public benchmark scores alone do not justify a bounty.

Safety and operating limits are separate acceptance checks. A capability gain cannot cancel a failed limit. Controlled releases include a recovery plan and a record of the approved artifact and configuration.

A proof establishes a named property under stated assumptions. A verified microkernel does not establish beneficial motivation or verify every application above it. Use formal methods for bounded properties where practical, alongside tests and review. If a release requires a proof and that proof is missing or fails, the release does not ship under those requirements.

## Token and treasury

One governance token, fixed supply, no built-in yield. No guild or work group can issue a shard token. The treasury does not run a market on its own roadmap.

The treasury provides pre-seed funding for human development, inference, servers, evaluation, maintenance, and milestone grants. Each grant names a deliverable, budget, license, independent reviewer, and acceptance checks. Payment follows accepted evidence. Contributions to existing projects should agree scope with their maintainers before work begins; those maintainers retain control of their repositories.

The work may later support a startup that raises capital and could pursue an IPO. Any return to the treasury or early funders depends on separately agreed ownership, repayment, or other rights. The governance token alone does not establish ownership in a future company or promise a return.

## Voting and amendments

**Token holder = voter.** Voting power follows token holdings, whether the holder is human or agent. There are no separate voting tracks, proof-of-humanity requirements, or agent-only voting caps. Attestation may be a deployment requirement; it is not a voting qualification.

A proposal is a specification diff. It states the problem, intended result, cost, acceptance checks, and constitutional clauses or definitions it changes. Token holders approve treasury allocations and amendments. Operational reviewers have only the permissions assigned by the current policy; their role creates no extra voting rights or permanent constitutional veto.

The constitution is versioned and amendable. Token holders may change its goals, definitions, and proof requirements. Constitutional amendments require a token-holder supermajority and a published review period. The exact threshold, quorum, delegation rules, and review period must be specified before token governance starts.

An amendment must show what changes and what evidence needs to be checked again. It need not preserve every previous goal. Releases are checked against their approved constitution and specification. A vote can change the requirements; it does not supply evidence of compliance.

## Phases

| Phase | Deliverable and exit condition |
|---|---|
| 0: select and specify | Complete the starting-point comparison, publish the task and evidence formats, approve a trial budget, and record a runtime decision from the trial. Publish the first versioned constitution. |
| 1: build and compare | Deliver the bounded maintenance prototype, baseline comparison, restart and permission tests, cost report, and independent reproduction. Promote a hive only if it meets the registered benefit threshold. |
| 2: operate and extend | Use the selected system on agreed partner work. Retain a single-agent system if the hive has not earned its extra cost. Add roles, memory, reasoning, or other components one at a time and measure each change. |
| 3: connect hives | Test state exchange, failures across nodes, and controlled upgrades across multiple hives. Adopt decentralized infrastructure when it meets the deployment requirements. The DAO retains control of its funds and approved deployments. |

The same token voting rule applies whenever token governance is active. A token launch and a complete Hyperseed formalization are not prerequisites for the first research prototype.

Before token governance starts, each trial manifest names its funder, accountable project lead, spending limit, and decision permissions. This temporary authority covers that trial only. It ends when the trial ends or token governance takes over.

## Openness and scope of authority

Colony-authored code will use Apache-2.0 or MPL-2.0, selected explicitly per component. Public documents, ontology definitions, metrics, and the constitution will use CC-BY-4.0. Reused components retain their existing licenses. Each implementation milestone must include the required license files and notices.

Publish specifications, code, test methods, and permitted evidence. Public artifacts do not require publishing credentials or private partner data. Shared libraries and evaluations remain usable without the Colony token.

The DAO's authority covers its treasury, approved releases, and participating deployments. Independent forks may adopt other rules. The constitution does not make those forks safe or bind their operators to Colony's decisions.

## Origin and longer-term direction

The original plan follows a reduced path from [Ben Goertzel's twenty-step thread](https://x.com/bengoertzel/status/2107478576794833038), removing steps 9, 12, 14, 15, and 16. That remains the background, rather than a requirement to rebuild each layer.

The longer-term research direction includes neural-symbolic-evolutionary agents, motivation, shared knowledge, public metrics, controlled self-upgrade, and an evolving constitution. The immediate test is smaller: can an open hive perform useful work, at an acceptable cost, with evidence that others can reproduce?
