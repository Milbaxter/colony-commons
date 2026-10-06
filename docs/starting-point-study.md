# Starting-point study

> Reviewed: 6 October 2026. Status: initial source review expanded; finalist selection and runtime trials remain open. No installations, inference runs, or performance benchmarks were performed for this study.

## Recommendation

Start with the task contract, shared evidence format, and evaluation harness. Review all 15 options in the [framework landscape](framework-landscape.md). Then select **two prototype configurations and one single-agent baseline** for the first runtime trial. A complete coding runtime can compete with a custom coordinator if it meets the same contract.

The earlier LangGraph–Omega shortlist was too narrow. PydanticAI, CrewAI, Agno, Google ADK, Strands, Mastra, OpenAI Agents SDK, CAMEL, Letta Code, and smolagents add relevant choices. Some supply explicit workflow control; others supply more of the team or coding runtime. No candidate has a reserved finalist place. The source review does not establish a winner.

Omega has a direct fit with the Hyperon ecosystem. Its symbolic features must show value on the chosen tasks, or reduce integration effort, to justify choosing it. Do not select it just because the long-term plan mentions Hyperon. A different coordinator can still use Hyperon components later.

Use OpenHands Software Agent SDK as the proposed coding baseline because it supplies an existing software-agent runtime. Letta Code and smolagents are also relevant to this choice; record the reason if the source screen changes the baseline. If one agent meets the requirement and added coordination gives no useful gain, retain the simpler system and publish that result. Avoid combining frameworks before the task requires it.

## Separate the choices

There are three decisions, not one:

1. **Coordination:** who acts next, what state persists, when work stops, and who can approve an action.
2. **Worker and reasoning:** which model, agent runtime, or symbolic engine performs a task.
3. **Deployment:** where tools run and how access, network use, and resource limits are enforced.

Using LangGraph for coordination does not prevent testing an Omega worker or a Hyperon reasoning service later. Using Omega does not supply every deployment control automatically. The first trial should compare complete, minimal configurations with equivalent external interfaces.

## Notes on the original five options

The full comparison is now in the [framework landscape](framework-landscape.md). These notes retain the more detailed review of the original five options. The gaps concern Colony's proposed hive; they are not claims that a project lacks all related capabilities.

| Candidate | Documented strengths | Work Colony still needs | Proposed role |
|---|---|---|---|
| **Omega** | Existing MeTTa agent loop; reasoning integrations; model-provider options; Docker and test support. | Hive coordination, shared typed evidence, persistent symbolic state as required by the task, and validated patch approval and recovery. | Candidate base or symbolic worker. |
| **LangGraph** | Graph-based control flow, checkpoints, cross-thread stores, subgraphs, and explicit interrupts. | Coding tools, isolated tool execution, semantic schema, budget enforcement, and application-specific approval checks. | Candidate coordinator. |
| **OpenHands Software Agent SDK** | Coding-agent tools, conversation persistence, subagent delegation, configurable action confirmation, and remote workspace options. | Colony evidence schema, independent release control, and any shared symbolic reasoning. | Single-agent baseline; can become the base if sufficient. |
| **Microsoft Agent Framework** | Python and .NET agents, typed workflows, checkpointing, human-input events, and multiple model providers. | Colony-specific tools, evidence schema, deployment controls, and evaluation. | Candidate coordinator, including for a .NET team. |
| **Hyperon directly** | MeTTa interpreter and atom/space interfaces; symbolic integration target. | Most of the agent runtime, coordination, and operations would need to be assembled. | Component experiment, not the first whole-hive base. |

Primary sources: [Omega repository][omega], [LangGraph overview][langgraph], [OpenHands SDK][openhands], [Microsoft overview][maf], [Hyperon interpreter][hyperon].

## What the research establishes

### Omega: real candidate, incomplete evidence for the target hive

Omega's reviewed memory documentation distinguishes volatile working memory, ChromaDB long-term memory, and a formal AtomSpace created for each inference invocation. This does **not** establish a persistent symbolic store shared by multiple agents. A shared chat history, vector database, and shared symbolic knowledge base are different things. The required integration must be demonstrated. [Memory internals][omega-memory]

Omega already has controls: owner authentication, a key proxy, filesystem policy configuration, and a startup policy call. The sample policy uses Landlock in `best_effort` mode. Validate behavior when enforcement is unavailable and when the process restarts. Do not describe the framework as having no security, or assume the current setup enforces Colony's whole policy. [Owner authentication][omega-auth], [configuration][omega-config], [sample policy][omega-policy], [startup code][omega-loop]

The build uses PeTTa, SWI-Prolog, Python, and embedding dependencies. The reviewed Dockerfile defaults one dependency to a moving branch. Pin all dependencies and image digests for the trial. The contribution guide provides test tiers and a Test provider, which can support checks without live inference. [Dockerfile][omega-docker], [contribution guide][omega-contrib]

### LangGraph: explicit coordination, separate execution boundary

LangGraph separates per-thread checkpoints from longer-term stores used across threads. Neither supplies Colony's ontology or its rules for conflicting statements; those remain application work. [Persistence][lg-persistence]

An interrupt can pause a workflow for input. On resume, the interrupted node starts again from its beginning. Approval and tool operations must therefore tolerate replay without performing an external action twice. Use a persistent checkpointer and authenticated approval records. A graph checkpoint alone is not a filesystem rollback. [Interrupts][lg-interrupts]

The framework is a coordinator, not a sandbox. A Colony configuration would need an external tool runner, enforced resource limits, and a review gate outside the worker's write access. Scripted model and tool outputs can test those transitions without paid inference. [Testing][lg-test]

### OpenHands: a serious baseline, not only a demo

The SDK documents saved conversations, specialised subagents, and action confirmation. Its documented TaskToolSet runs a child synchronously while the parent waits; this should not be mistaken for a concurrent shared-state hive. The optional persistent-memory feature uses Markdown files, not a typed symbolic store. [Persistence][oh-persistence], [delegation][oh-tasks], [memory][oh-memory]

Use its existing coding tools to establish the cost and quality a hive must improve upon. Select an isolated remote workspace for tool execution; the SDK also permits local workspaces. Confirmation policy and operating-system isolation are separate controls. [SDK][openhands], [action confirmation][oh-security]

### Microsoft Agent Framework and Hyperon

Microsoft Agent Framework is a credible alternate coordinator. Its workflow, checkpoint, and model-provider documentation is relevant if the team can implement it with less effort. Its shell documentation explicitly distinguishes local execution from isolation. [Workflows][maf-workflows], [checkpoints][maf-checkpoints], [providers][maf-providers], [shell tools][maf-shell]

Do not start a new comparison around old AutoGen examples: AutoGen's repository now recommends Microsoft Agent Framework for new users and describes AutoGen as being in maintenance mode. [AutoGen][autogen]

Hyperon's interpreter and Distributed AtomSpace integration are useful candidates for later symbolic experiments. They do not by themselves provide the full maintenance workflow. Investigate existing DAS interfaces before inventing another distributed store. The interpreter repository describes active pre-alpha development; runnable integration instructions do not establish deployment readiness. [Interpreter][hyperon], [DAS integration][das]

## Selection procedure

Use the [landscape screen](framework-landscape.md#how-to-select-the-trial) to record source evidence, gaps, licenses, team fit, and estimated integration work for every option. Publish the reasons for selecting two prototype configurations and the baseline. The broader review is inexpensive compared with building and benchmarking every option.

Then use the [first-hive protocol](first-hive.md). Check the selected configurations with scripted control tests before inference. Replace a failing configuration from the source-screened candidates if the trial budget permits; publish the failure. Compare equivalent task inputs, tools, models, time limits, and total inference budgets. Record differences that cannot be held constant.

Keep two comparisons separate:

- **Practical choice:** which complete configuration produces accepted patches with the least cost and review effort?
- **Contribution of each component:** with the same worker and model, does another role, shared memory, or symbolic reasoning improve the result?

The first comparison cannot by itself attribute a gain to a framework. The second requires controlled additions or removals of components.

Reject configurations that fail a required permission, recovery, or evidence check. Among those that pass, choose the smallest maintainable setup that meets the task target. Publish failures and setup effort as well as task scores. A small pilot supports a local engineering decision, not a claim of general intelligence.

**Decision remains open:** there is no measured winner yet. The result must include the chosen versions, the rejected alternatives, the reason for selection, and the conditions that would justify changing the base.

## Version and license snapshots

These identify reviewed source, not tested installation pins. Create resolved dependency locks and image digests during implementation. Web documentation can move after this review.

| Project | Source snapshot | Core license |
|---|---|---|
| Omega | [v0.1.20 / 19e94bb, 6 Oct 2026][omega] | [Apache-2.0][omega-license] |
| LangGraph | [1.2.13 release / 2d94208, 5 Oct 2026][lg-release]; [1.2.14 version-bump commit, 6 Oct][lg-head] was also visible during review | [MIT][lg-license] |
| OpenHands Software Agent SDK | [1.50.0 / dcf401a, 29 Sep 2026][oh-release] | [MIT][oh-license] |
| Microsoft Agent Framework | [Python 1.20.0 / cb77f68, 2 Oct 2026][maf-release] | [MIT][maf-license] |
| Hyperon experimental interpreter | [v0.2.10 / 3f76dc4, 11 Feb 2026][hyperon] | [MIT][hyperon-license] |

These license observations apply to the named code. They do not cover every model, dataset, hosted service, or optional package.

[omega]: https://github.com/singnet/Omega/tree/19e94bb336378eebb66e8e689d0d3ff0e1bf5f77
[omega-memory]: https://github.com/singnet/Omega/blob/19e94bb336378eebb66e8e689d0d3ff0e1bf5f77/docs/reference-internals-memory-store.md
[omega-auth]: https://github.com/singnet/Omega/blob/19e94bb336378eebb66e8e689d0d3ff0e1bf5f77/README.md#L129-L133
[omega-config]: https://github.com/singnet/Omega/blob/19e94bb336378eebb66e8e689d0d3ff0e1bf5f77/config/config.yaml
[omega-policy]: https://github.com/singnet/Omega/blob/19e94bb336378eebb66e8e689d0d3ff0e1bf5f77/profile/policy.yaml
[omega-loop]: https://github.com/singnet/Omega/blob/19e94bb336378eebb66e8e689d0d3ff0e1bf5f77/src/loop.metta
[omega-docker]: https://github.com/singnet/Omega/blob/19e94bb336378eebb66e8e689d0d3ff0e1bf5f77/Dockerfile
[omega-contrib]: https://github.com/singnet/Omega/blob/19e94bb336378eebb66e8e689d0d3ff0e1bf5f77/CONTRIBUTING.md
[omega-license]: https://github.com/singnet/Omega/blob/19e94bb336378eebb66e8e689d0d3ff0e1bf5f77/LICENSE
[langgraph]: https://docs.langchain.com/oss/python/langgraph/overview
[lg-persistence]: https://docs.langchain.com/oss/python/langgraph/persistence
[lg-interrupts]: https://docs.langchain.com/oss/python/langgraph/interrupts
[lg-test]: https://docs.langchain.com/oss/python/langgraph/test
[lg-release]: https://github.com/langchain-ai/langgraph/commit/2d942085e214ef6b99b6f54ed4d544a7c7c5ac56
[lg-head]: https://github.com/langchain-ai/langgraph/commit/70dd64065bffaa3b6ab61a33f1f020fb54db8efa
[lg-license]: https://github.com/langchain-ai/langgraph/blob/2d942085e214ef6b99b6f54ed4d544a7c7c5ac56/LICENSE
[openhands]: https://github.com/OpenHands/software-agent-sdk/tree/dcf401af7a9a302ef92cb7d092e1df9bb659daa5
[oh-persistence]: https://docs.openhands.dev/sdk/guides/convo-persistence
[oh-tasks]: https://docs.openhands.dev/sdk/guides/task-tool-set
[oh-memory]: https://docs.openhands.dev/sdk/guides/persistent-memory
[oh-security]: https://docs.openhands.dev/sdk/guides/security
[oh-release]: https://github.com/OpenHands/software-agent-sdk/commit/dcf401af7a9a302ef92cb7d092e1df9bb659daa5
[oh-license]: https://github.com/OpenHands/software-agent-sdk/blob/dcf401af7a9a302ef92cb7d092e1df9bb659daa5/LICENSE
[maf]: https://learn.microsoft.com/en-us/agent-framework/overview/
[maf-workflows]: https://learn.microsoft.com/en-us/agent-framework/journey/workflows
[maf-checkpoints]: https://learn.microsoft.com/en-us/agent-framework/workflows/checkpoints
[maf-providers]: https://learn.microsoft.com/en-us/agent-framework/agents/providers/
[maf-shell]: https://learn.microsoft.com/en-us/agent-framework/integrations/by-component/tools/shell-tools
[maf-release]: https://github.com/microsoft/agent-framework/commit/cb77f68f005f40e0b844392f778c4cb6b91cee1b
[maf-license]: https://github.com/microsoft/agent-framework/blob/cb77f68f005f40e0b844392f778c4cb6b91cee1b/LICENSE
[autogen]: https://github.com/microsoft/autogen
[hyperon]: https://github.com/trueagi-io/hyperon-experimental/tree/3f76dc460da6961f57f69f6c3e550c59c74ada83
[das]: https://github.com/trueagi-io/hyperon-experimental/blob/3f76dc460da6961f57f69f6c3e550c59c74ada83/docs/das_setup.md
[hyperon-license]: https://github.com/trueagi-io/hyperon-experimental/blob/3f76dc460da6961f57f69f6c3e550c59c74ada83/LICENSE
