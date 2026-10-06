# First hive: software maintenance

> Proposed implementation milestone. No runtime or evaluation result is delivered by this document. See the [starting-point study](starting-point-study.md) and [project plan](../README.md).

## Objective

Given a small repository issue, produce a patch, test evidence, and a separate review within a fixed budget. The patch should be ready for an authorised operator to accept or reject. Establish whether a hive improves on one coding agent.

Start with small, licensed public repositories or purpose-built fixtures. Include bug fixes, tests, and small refactors with checks that can run independently of the worker. Avoid tasks that require private production access.

## Minimum system

| Part | Responsibility |
|---|---|
| Planner | Read the issue and approved task checks. Propose a bounded work plan. |
| Worker | Edit a disposable checkout and run permitted commands. Produce a patch and evidence references. |
| Reviewer | Review the patch against the original request and independently collected test results. Request changes or recommend acceptance. |
| Tool runner | Enforce workspace, network, tool, time, and resource limits outside agent-writable code. |
| Evidence store | Record task state, observations, artifacts, costs, and decisions with their source and version. |
| Release gate | Bind authorisation to the exact patch, repository revision, policy version, and test evidence. |

A reviewer agent is a separate workflow role. It does not replace independent grant evaluation, and agreement between agents is not a proof. External evaluators must be able to rerun the checks.

The initial output is a local patch and report. Credentials for pushing code or deploying services stay outside the worker. A controlled publisher can be added later. Operational approval implements the current policy; it is not a separate human voting track or an immutable constitutional rule.

## Shared evidence contract

Define a versioned schema before tying the system to a framework. The first implementation may use a small database and artifact directory. A full ontology is not required to test this workflow.

Each record includes:

- Task ID, run ID, role, timestamp, and schema version.
- Base repository commit, patch identity, and artifact hashes.
- Claim or observation, its source, supporting evidence, and status: proposed, observed, checked, rejected, or superseded.
- Model and runtime versions, configuration, tool calls, resource use, and failures.
- Constitution/policy version, relevant permissions, and approval or rejection record.

Preserve conflicting claims and their sources until an authorised rule resolves them. Validate writes, make retries safe, and keep an append-only history of decisions. Agents cannot rewrite the evaluator's results or their own permissions.

A shared transcript is not the evidence contract. Later MeTTa, AtomSpace, MORK, or Hyperseed adapters must preserve the same record identities and provenance so their effect can be compared.

## Trial protocol

### 1. Freeze the scope before spending

Complete the [framework source screen](framework-landscape.md#how-to-select-the-trial) before selecting prototypes. Publish evidence and a reason for advancing or deferring every option. Choose two minimal hive configurations and one single-agent baseline. No places are reserved for Omega, LangGraph, or any other project.

Publish a trial manifest with the task set, candidate versions, tool interface, model settings, hardware, total budget, engineering time allowance, and stop conditions. Name the funder, accountable project lead, independent evaluator, and approval permissions. Before token governance starts, these permissions apply only to that trial. Pin dependencies and container images. Record all configuration differences.

Proposed pilot size: 10 development tasks and 20 fresh evaluation tasks, with three repeated runs per evaluated configuration. Adjust this size to the approved budget before evaluation starts. This is an engineering pilot, not enough evidence for a broad claim about intelligence.

Pre-register the minimum useful improvement: an accepted-patch target, maximum cost per accepted patch, maximum reviewer time, and acceptable regression rate. Do not choose these thresholds after seeing results.

### 2. Check controls with scripted outputs

Before live inference, require each candidate configuration to demonstrate:

1. A run can restart with its task state and pending approval intact.
2. Retried messages do not create duplicate external actions.
3. Writes outside the permitted checkout and disallowed network access are denied.
4. A stopped or rejected task cannot continue through another role or tool path.
5. Time and total resource limits stop the whole hive, including its children.
6. Invalid or conflicting evidence writes are detected and recorded.
7. A worker cannot edit evaluation tests, approval records, or the release policy.
8. Approval for one patch does not authorise a changed patch or a different base revision.

Run the relevant checks on the actual deployment configuration, including unsupported enforcement features. A prompt instruction is not evidence that a boundary is enforced.

### 3. Compare the smallest useful configurations

- **Single-agent baseline:** one coding agent, with delegation disabled, behind the same external limits and evaluator. OpenHands is the proposed baseline; the source screen may justify another choice.
- **Candidate A:** a minimal planner/worker/reviewer configuration selected from the source screen.
- **Candidate B:** a second selected configuration that meets the same task and evidence contract.

Name all three configurations and justify the choices in the trial manifest. A complete coding runtime with native delegation can be a hive candidate. A reasoning component alone is not an equivalent full configuration.

Keep model, total budget, repository inputs, permitted tools, and acceptance tests equal where possible. If native tools or runtimes require a difference, record it and treat the result as a comparison of complete configurations. Do not claim the framework alone caused the result.

Use the development set for tuning. Freeze configurations before opening the evaluation set. Include timeouts, crashes, rejected patches, and overruns in the results. No selective reruns. Keep evaluation checks outside the worker's editable checkout and verify the final patch on a fresh copy.

If source review suggests that the baseline's native delegation can meet the hive contract, consider it for one of the two candidate places before evaluation. A later investigation belongs in a separate trial with fresh evaluation tasks. If a selected configuration fails a required control, record the failure. A replacement requires a published reason and must fit the trial budget; it receives the same checks. Select replacements before opening evaluation tasks. Do not add candidates or change success thresholds in response to evaluation scores.

### 4. Measure and reproduce

Report valid task completion, test regressions, total model and tool cost, elapsed time, operator interventions, review minutes, recovery failures, and setup/maintenance effort. Show per-task results and variation across runs. Charge all roles, retries, and failed work to the configuration's total budget.

For the selected configuration, compare the same worker alone with the added planner/reviewer roles. Then add memory or symbolic reasoning separately. This tests whether the hive structure and later components actually contribute. Predeclare these comparisons and their budget before evaluation, or run them as a later trial with fresh evaluation tasks.

A second evaluator reproduces a published subset from clean setup instructions. Document any restricted data or unreproducible dependencies. Publish logs and artifacts with credentials and personal data removed.

## Acceptance and next work

Complete the comparison milestone when it provides:

- A source and dependency manifest, reproducible setup, and operating cost report.
- The evidence schema and its validated task/review workflow.
- Results for every required control check, including failures and the limits of the checks.
- Complete comparison results, independent review, and a written runtime decision.
- A patch/release recovery procedure; a framework checkpoint alone does not undo filesystem or external changes.
- Proposed contributions to existing projects, with the original maintainers' review requirements respected.

A deployed configuration must pass every required control check. A hive must also meet the registered benefit threshold before it is promoted. A negative result can still complete a research grant whose acceptance terms require an honest comparison. If the hive cannot meet the benefit threshold, publish the result and keep or improve a single-agent system that passes the controls. Do not report a successful hive deployment simply because three agents exchanged messages.

The next milestone can add one measured capability: persistent symbolic state, a reasoning module, cross-run learning, or a second deployment node. Live self-upgrade, a decentralized network, and a verified microkernel port each need their own scope and acceptance evidence. They are not prerequisites for this first comparison.
