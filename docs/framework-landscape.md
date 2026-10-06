# Framework landscape

> Source review: 6 October 2026. This is a wider set of options for the first hive, not a benchmark or a ranked shortlist. No frameworks were installed or run. See the [study](starting-point-study.md) and [trial protocol](first-hive.md).

## What we are choosing

Colony needs a small system that can plan work, produce a patch, review evidence, recover from failure, and obey external limits. It also needs a path to test shared symbolic knowledge later. A project need not supply every layer to be useful.

The first shortlist gave too much weight to LangGraph and Omega. The review now covers **15 options**: coordination frameworks, complete coding runtimes, and a symbolic component. These roles can overlap. A coding runtime can become the whole base; a coordinator can call an existing coding worker.

This is a bounded review for the maintenance task, not a list of every agent library. Add another option when it offers a relevant capability or lower integration cost that this set does not cover. GitHub stars, vendor affiliation, and the number of supported agents are not selection criteria.

## Coordination and team frameworks

Each row states why the option belongs in the review and the main work or uncertainty for Colony. A documented feature still needs a check in the selected deployment.

| Option | Why compare it | Main Colony work or check |
|---|---|---|
| **[LangGraph][langgraph]** | Explicit graph control, checkpoints, stores, and approval interrupts. Suits a workflow with fixed review steps. | Add coding tools and typed evidence. Check replay around approvals and external actions. |
| **[PydanticAI + Pydantic Graph][pydantic]** | Typed interfaces, graph state, agent delegation, deferred tool approval, and model-free test facilities. | Select a durable execution engine if needed; validate authority at the tool boundary. A stored conversation is not durable execution. |
| **[CrewAI Crews + Flows][crewai]** | Role/task teams, structured flow state, checkpoint restoration, and persisted human feedback. Could reduce team setup work. | Use explicit flows for release gates. Automatic checkpoint writes are best-effort; manual checkpoint calls raise on failure. Check recovery and replay. |
| **[Agno SDK + AgentOS][agno]** | Agents, teams, workflows, stored state, approvals, and an HTTP runtime. Could reduce service and operator-tool work. | Configure durable jobs when needed. Ordinary background tasks remain process-bound. Separate the open runtime from vendor control-plane features. |
| **[Google ADK][adk]** | Multi-agent delegation and workflow control, tools, evaluation support, and local deployment. Designed for multiple models, with Gemini integration. | Test the chosen model adapter, state backend, approval path, and recovery in a self-hosted configuration. |
| **[Strands Agents][strands]** | Agent harnesses, multi-agent patterns, model adapters, sessions, and lifecycle limits. Runs in process without a hosted control plane. | Verify durable recovery and external approval semantics. Add the evidence schema and isolated coding tools. |
| **[Mastra][mastra]** | TypeScript agents and workflows, memory, tracing, and persisted suspend/resume. Relevant if the implementation team uses TypeScript. | Check approval and restart behavior in the chosen workflow. Separate Apache-licensed code from the separately licensed `ee/` directories. |
| **[OpenAI Agents SDK][openai-sdk]** | Small agent loop with tools, handoffs, agents as tools, approval interruptions, and provider adapters. | Supply application storage and tool isolation. Check feature support for the chosen model provider; the SDK is separate from managed services. |
| **[Microsoft Agent Framework][maf]** | Python and .NET agents, typed workflows, checkpoints, human input, and model-provider options. | Add Colony tools, evidence, and deployment controls. Team experience may reduce implementation cost. |
| **[CAMEL][camel]** | Workforce task decomposition, worker assignment, parallel execution, shared-memory options, snapshots, and human-input tools. | Fix roles and permissions for the trial. Test snapshot recovery and prevent publishing through an unapproved tool path. |
| **[Omega][omega]** | MeTTa agent loop and direct access to the Hyperon research path. Could reduce symbolic integration work. | Demonstrate the full hive workflow and required persistent shared state. Symbolic integration is a reason to compare it, not an automatic selection. |

## Coding runtimes and lean workers

These are eligible as a single-agent baseline or as the base for a small hive. Do not require a custom coordinator if native delegation already meets the contract.

| Option | Why compare it | Main Colony work or check |
|---|---|---|
| **[OpenHands Software Agent SDK][openhands]** | Existing coding tools, saved conversations, delegation, action confirmation, and remote workspaces. Proposed single-agent baseline. | Use an isolated workspace. Add shared evidence and independent release control; delegation is not itself a shared-state hive. |
| **[Letta Code][letta]** | Coding runtime with subagents, headless/server operation, permissions, and persistent Git-backed memory. Local backend available. | Test the local deployment and recovery. Documented shared-memory repositories require cloud-hosted agents; local persistent memory alone does not establish shared hive state. |
| **[Hugging Face smolagents][smolagents]** | Small code/action-agent implementation, managed-agent composition, model choice, and local or remote execution options. | Add durable task state, approval records, and recovery. Agent export is not an execution checkpoint; isolate the whole tool path. |

## Symbolic component

| Option | Why compare it | Main Colony work or check |
|---|---|---|
| **[Hyperon directly][hyperon]** | MeTTa and atom/space interfaces for symbolic experiments. Can sit behind any selected coordinator. | It is not a complete coding hive. Compare the extra integration work and measured value before adding it. |

This separation keeps the long-term research path open. Choosing a general workflow framework does not rule out Omega workers, MeTTa reasoning, or AtomSpace adapters.

## Details that affect the choice

**PydanticAI:** durable execution integrates engines such as Temporal, DBOS, Prefect, and Restate. The selected engine adds setup and operating work. Deferred approval requires application-side caller checks. Its test models can support control tests without paid inference. [Durability][py-durable], [approval boundary][py-approval], [testing][py-tests]

**CrewAI and Agno:** both document recovery and approval support. Neither should be dismissed as a chat-only wrapper. CrewAI covers checkpoints and persisted human feedback. Agno distinguishes persisted sessions from a durable queue. Compare these features in the open deployment; do not assume paid management features are included. [CrewAI checkpoints][crew-checkpoints], [human feedback][crew-feedback], [Agno durability][agno-durable], [Agno runtime][agno-runtime]

**Letta:** the current `letta-ai/letta` repository points new work to Letta Code; the V1 server is retired. MemFS gives inspectable memory history, but it is not Colony's typed symbolic evidence store. The documented cloud requirement for shared-memory repositories matters to a reproducible self-hosted hive. [Project direction][letta-direction], [shared-memory limits][letta-shared]

**Mastra and OpenAI Agents SDK:** both provide ways to pause work for input or approval. The application must preserve state and authorize the caller. An approval API does not isolate shell commands or bind approval to Colony's patch identity by itself. OpenAI's SDK supports provider adapters, but some features depend on the OpenAI Responses path. [Mastra suspend/resume][mastra-resume], [SDK review flow][oa-review], [SDK providers][oa-providers]

**CAMEL and smolagents:** existing worker composition can reduce custom code. Check the actual pause/restart and tool-execution path. For smolagents, restrictions on generated code and isolation of the whole agent are distinct. [CAMEL Workforce][camel-workforce], [smolagents execution][smol-execution]

**Shared memory:** conversations, vector retrieval, saved workflow state, Git-backed notes, and symbolic knowledge serve different purposes. Every configuration must implement the same evidence schema, sources, conflict rules, and write permissions. None of these feature labels alone proves that it meets the contract.

**Project names change:** Strands' former Python SDK repository now redirects to its harness monorepo. Microsoft recommends Agent Framework for new users of AutoGen, which is in maintenance mode. Use current source and APIs when estimating effort. [Strands source][strands], [AutoGen status][autogen]

## How to select the trial

Complete one source-screen record for **every option above**. Mark each requirement as documented, unknown, needs an adapter, or unsuitable for the proposed role. Include source links, the version checked, and a reason to advance or defer it. The tables above begin this review; they do not certify all requirements.

Use the same questions:

1. Can the required runtime and evidence store run under Colony's control with an acceptable license? Which optional services would be used?
2. Can the chosen models and tools use the common task interface? Record provider-specific features and costs.
3. How are role transitions, typed state, conflicting evidence, and access rights represented?
4. What survives a crash? Can approval and external actions resume without repeating a side effect?
5. Where are tool isolation, caller authorization, cancellation, and the total budget enforced?
6. How much code, dependency management, and operating work must Colony add? Does the team know the language and runtime?
7. Can evaluators inspect logs, replace components, and reproduce a run without a required proprietary control plane?

Do not assign numerical performance scores from documentation. Record uncertainty. Agree any preference weights before runtime results are available. A full runtime may need less work than a smaller library; a smaller library may make the controls easier to inspect.

Select **two complete prototype configurations and one single-agent baseline** within a published engineering and inference budget. Keep OpenHands as the proposed baseline unless the screen gives a clear reason to change it. Select finalists by fit and estimated integration work, not to preserve the earlier shortlist.

Then run the [same scripted controls and task trial](first-hive.md) on those configurations. If a finalist fails controls, report it and consider a replacement within the agreed budget. Do not build and benchmark all 15 options by default. Publish the selection record, including why each other option was deferred.

No framework is selected yet. Colony's common evidence contract, evaluation suite, deployment controls, and upstream fixes remain useful whichever base wins.

## Source and license snapshots for added options

These identify reviewed code, not verified installation pins. The [study](starting-point-study.md#version-and-license-snapshots) records the original five. Resolve dependency locks and inspect the selected release before implementation; web documentation may describe newer features.

| Added option | Reviewed source | Core license |
|---|---|---|
| PydanticAI / Pydantic Graph | [v2.54.0 / 6695132][pydantic] | [MIT][py-license] |
| CrewAI | [1.15.23 / deaa71e][crewai] | [MIT][crew-license] |
| Agno | [v3.1.1 / 3ca74c2][agno] | [Apache-2.0][agno-license] |
| Google ADK Python | [fac77be, 6 Oct 2026][adk] | [Apache-2.0][adk-license] |
| Strands harness monorepo | [356ca49, 6 Oct 2026][strands] | [Apache-2.0][strands-license] |
| Mastra | [9fc60a1, 6 Oct 2026][mastra] | [Apache-2.0 outside separately licensed areas][mastra-license] |
| OpenAI Agents SDK Python | [66504e9, 6 Oct 2026][openai-sdk] | [MIT][oa-license] |
| CAMEL | [0.2.91a7 source / 24fde60, 5 Oct 2026][camel] | [Apache-2.0][camel-license] |
| Letta Code | [0.34.4 source / 4b028fa, 6 Oct 2026][letta] | [Apache-2.0][letta-license] |
| smolagents | [1.27.0.dev0 source / 96f33fa, 6 Oct 2026][smolagents] | [Apache-2.0][smol-license] |

Licenses here cover the named code, not every model, dataset, tool, hosted service, or enterprise extension. The source versions labelled alpha or development are not claims of a stable release.

[langgraph]: https://docs.langchain.com/oss/python/langgraph/overview
[pydantic]: https://github.com/pydantic/pydantic-ai/tree/66951321b89587235f432281eba909a30a585ffd
[crewai]: https://github.com/crewAIInc/crewAI/tree/deaa71e168069a1d5307340172875def4330e75b
[agno]: https://github.com/agno-agi/agno/tree/3ca74c272fa5017fae4fab234e988378c8f14c63
[adk]: https://github.com/google/adk-python/tree/fac77be5d32cf8b07db0162fdd73f5f9155f60bf
[strands]: https://github.com/strands-agents/harness-sdk/tree/356ca49454d8d9219596216576b1fb3009921982
[mastra]: https://github.com/mastra-ai/mastra/tree/9fc60a17488d1b4ae46c3a7316cdf988da9e4d41
[openai-sdk]: https://github.com/openai/openai-agents-python/tree/66504e953ae49b9d884c638e7bd32b9fa1157fe0
[maf]: https://learn.microsoft.com/en-us/agent-framework/overview/
[camel]: https://github.com/camel-ai/camel/tree/24fde60ad739b4be8f8f533fea9ba54256fbc4a2
[omega]: https://github.com/singnet/Omega/tree/19e94bb336378eebb66e8e689d0d3ff0e1bf5f77
[openhands]: https://github.com/OpenHands/software-agent-sdk/tree/dcf401af7a9a302ef92cb7d092e1df9bb659daa5
[letta]: https://github.com/letta-ai/letta-code/tree/4b028fab07c69edaac2ddb4f7b9a43573ff20d81
[smolagents]: https://github.com/huggingface/smolagents/tree/96f33faaf028479119ec8d34507b47694cf14e34
[hyperon]: https://github.com/trueagi-io/hyperon-experimental/tree/3f76dc460da6961f57f69f6c3e550c59c74ada83
[py-durable]: https://pydantic.dev/docs/ai/capabilities/durable_execution/overview/
[py-approval]: https://pydantic.dev/docs/ai/tools-toolsets/deferred-tools/
[py-tests]: https://pydantic.dev/docs/ai/guides/testing/
[crew-checkpoints]: https://docs.crewai.com/v1.15.23/en/concepts/checkpointing
[crew-feedback]: https://docs.crewai.com/v1.15.23/en/learn/human-feedback-in-flows
[agno-durable]: https://docs.agno.com/use-cases/document-processing/batch-and-durability
[agno-runtime]: https://docs.agno.com/features/runtime
[letta-direction]: https://github.com/letta-ai/letta
[letta-shared]: https://docs.letta.com/concepts/shared-memory
[mastra-resume]: https://mastra.ai/docs/workflows/suspend-and-resume
[oa-review]: https://developers.openai.com/api/docs/guides/agents/guardrails-approvals
[oa-providers]: https://developers.openai.com/api/docs/guides/agents/models
[camel-workforce]: https://docs.camel-ai.org/key_modules/workforce
[smol-execution]: https://huggingface.co/docs/smolagents/en/tutorials/secure_code_execution
[autogen]: https://github.com/microsoft/autogen
[py-license]: https://github.com/pydantic/pydantic-ai/blob/66951321b89587235f432281eba909a30a585ffd/LICENSE
[crew-license]: https://github.com/crewAIInc/crewAI/blob/deaa71e168069a1d5307340172875def4330e75b/LICENSE
[agno-license]: https://github.com/agno-agi/agno/blob/3ca74c272fa5017fae4fab234e988378c8f14c63/LICENSE
[adk-license]: https://github.com/google/adk-python/blob/fac77be5d32cf8b07db0162fdd73f5f9155f60bf/LICENSE
[strands-license]: https://github.com/strands-agents/harness-sdk/blob/356ca49454d8d9219596216576b1fb3009921982/LICENSE.APACHE
[mastra-license]: https://github.com/mastra-ai/mastra/blob/9fc60a17488d1b4ae46c3a7316cdf988da9e4d41/LICENSE.md
[oa-license]: https://github.com/openai/openai-agents-python/blob/66504e953ae49b9d884c638e7bd32b9fa1157fe0/LICENSE
[camel-license]: https://github.com/camel-ai/camel/blob/24fde60ad739b4be8f8f533fea9ba54256fbc4a2/LICENSE
[letta-license]: https://github.com/letta-ai/letta-code/blob/4b028fab07c69edaac2ddb4f7b9a43573ff20d81/LICENSE
[smol-license]: https://github.com/huggingface/smolagents/blob/96f33faaf028479119ec8d34507b47694cf14e34/LICENSE
