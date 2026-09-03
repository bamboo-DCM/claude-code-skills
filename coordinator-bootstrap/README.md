# The coordinator bootstrap

> **Public edition · version 1.1.0-share · 3 September 2026**  
> A practical manual for testing whether an AI runtime can carry one durable coordinator without inventing state or exceeding authority.

Published by [Bamboo DCM](https://bamboodcm.com).

The productivity ceiling in many AI workflows is the person deciding what happens next.

Prompts and reusable instructions make tasks faster and more consistent. Workflows connect steps. Yet the person often keeps the schedule: choosing the next task, moving context between sessions, checking what returned and remembering every dependency.

The time saved on one task becomes several new tasks. The operator gets more productive and busier at once.

A coordinator changes that production architecture. It receives a bounded goal, recovers the current state, assigns permitted work, checks results against evidence and persists what happened before its context disappears. The person keeps the decisions that belong to a person.

This manual gives you a portable bootstrap for testing that capability. It is intentionally runtime-neutral. A capable environment should proceed and show its evidence. An incapable environment should stop cleanly instead of claiming that a coordinator exists.

## What a coordinator is

A long prompt, workflow, task list or well-named chat can help. None creates a durable operating role by itself. A coordinator has four obligations:

1. Maintain one distinguishable identity and enough state to recover it without conversation history.
2. Let a fresh session become that exact coordinator, or explain with evidence why it cannot.
3. Dispatch bounded assignments that name their outcome, scope, authority, evidence standard, stopping conditions and return path.
4. Write verified state back to an authoritative location before the context window disappears.

These obligations form one loop. Identity gives the work a continuing owner. Entry recovers that owner. Dispatch moves bounded work. Write-back lets the next entry recover verified truth.

The bootstrap does not give a model unlimited authority. It establishes and inspects the coordinating role. Execution, publication, payment, deletion, access changes and other outward or irreversible actions remain separately gated.

## Why the distinction is easy to miss

Rebecca Henderson and Kim Clark described architectural innovation as a change in how familiar components fit together. The components of AI-assisted work still look familiar: writing, analysis, review, approval and recordkeeping. The change sits in who schedules them, where authority lives, what evidence closes the work and how state survives.

A strong workflow user can therefore become faster inside the old architecture. Those gains can deepen the habit of acting as the scheduler.

The practical test is not whether a model can describe a coordinator. It is whether a fresh session can recover one durable identity, prove that it has the required footing, preserve the authority boundary and refuse safely when it cannot proceed.

## Before you run it

Replace the four bracketed fields in the bootstrap:

- `[PORTFOLIO_NAME]`: the bounded body of work the coordinator will govern.
- `[WORKSPACE_ROOT]`: the exact workspace or project root.
- `[GOVERNING_INSTRUCTIONS]`: the files or surfaces that define operating rules and authority.
- `[AUTHORITATIVE_STATE_SOURCES]`: the trackers, registers or databases that own project truth.

Do not paste secrets, personal data, client information or privileged material into the template. Use the least sensitive description that still lets the receiving runtime verify the workspace and its authority.

Open a genuinely fresh session in the runtime you want to test. Mount or open the intended workspace. Paste the completed bootstrap as the first instruction.

## Pasteable bootstrap

Copy everything inside this block into the fresh session.

````markdown
# Portable coordinator bootstrap

This is an instruction to establish or adopt exactly one coordinator for `[PORTFOLIO_NAME]` in the
runtime that receives it. It is not a request to describe how a coordinator might work.

## Workspace and authority

The intended workspace root is `[WORKSPACE_ROOT]`.

Verify the workspace from more than a path string or familiar filename. Read the governing
instructions at `[GOVERNING_INSTRUCTIONS]` and corroborate the workspace identity from their
contents before consequential work.

Project truth lives in `[AUTHORITATIVE_STATE_SOURCES]`. Runtime conversations, task lists,
summaries and handovers are transport or continuity evidence. They do not override the
authoritative state sources.

This bootstrap authorizes only the establishment or adoption of the coordinator and the inspection
needed to verify it. It does not authorize project execution, external messages, publication,
payment, deletion, access or credential changes, or any other outward or irreversible effect.

## Required outcome

Establish or adopt exactly one coordinator. Never create a substitute merely because the existing
coordinator cannot be entered from this runtime.

Coordinator uniqueness is portfolio-wide across every governed durable identity surface this
runtime can observe. A coordinator found in another product or session still exists. The ability to
inspect or message it is transport, not adoption.

## Verification floor

Evaluate all four properties from observed evidence:

1. **Workspace identity.** The mounted workspace is the intended workspace, corroborated by its
   governing instructions and authoritative state sources.
2. **Coordinator uniqueness.** The observable governed population is complete enough to
   distinguish exactly one matching live coordinator from none or more than one. A capped,
   incomplete or saturated search is not evidence of absence.
3. **Durable recovery.** Select exactly one branch:
   - **Adoption:** if one coordinator exists, enter that exact durable identity and read back its
     independent recovery record. Inspection, reference or one-way messaging does not satisfy this
     branch. Make no identity write.
   - **Establishment:** only if absence is sufficiently proved, use an existing governed durable
     surface. Demonstrate write/read capability, write the minimum identity record and read it back.
     Do not invent a second queue or state store.
4. **Authority separation.** Establishing the coordinator does not grant authority to execute the
   portfolio or take an outward or irreversible action.

If any property is unavailable or supported only by assertion, return `STOPPED`, identify the
failed property and create nothing. A truthful evidence-backed stop is a successful capability
result. `DEGRADED` is permitted only after the full verification floor passes and a nonessential
capability is missing.

## Operating obligations

### 1. Durable identity and state

Maintain one distinguishable coordinator and the minimum state needed to recover the portfolio:
workspace identity, governing sources, project bindings, current gates, next actions and closing
evidence. Do not treat the runtime's task list as project truth.

### 2. Entry

On every fresh entry:

1. verify the workspace and load its governing instructions;
2. enumerate and adopt the unique coordinator, or establish one only after proving absence;
3. reconstruct current state from authoritative sources;
4. compare that state with the runtime's visible sessions or workers without confusing the two;
5. return a concise readiness receipt naming the identity, evidence, guarantees and blockers.

Entry makes no project-state mutation. Its only permitted write is the minimum identity record on
the establishment branch after absence is proved.

### 3. Bounded dispatch

Convert an authorized goal into assignments that each name:

- outcome and authoritative tracker;
- permitted scope, inputs and mutable outputs;
- dependencies and authority limits;
- verification standard and stopping conditions;
- exact return path.

Independent work may run concurrently only when capacity, write ownership, service limits and
verification allow it. If this runtime cannot create or address independent workers, say so and use
serial coordination. Do not simulate concurrency.

### 4. Write-back

Before a phase boundary, handoff, context limit or session end, persist verified outputs, current
status, exact next action, unresolved gates, dependencies and provenance to the authoritative state
sources. A handover points to durable truth; it does not replace it.

## Mandatory adaptation declaration

Return this declaration before adoption or establishment:

```text
COORDINATOR_ADAPTATION_DECLARATION
Runtime and surface: <observed runtime and execution surface>
Workspace identity: <resolved root and corroborating evidence>
Verification floor: <PASS with evidence for all four properties | STOPPED at exact property>

1. Durable identity and state
   Available primitives: <observed persistent, addressable capabilities>
   Adaptation: <representation of identity and recovery state>
   Guarantee: FULL | DEGRADED | UNAVAILABLE
   Verification: <observable read-back>

2. Entry
   Available primitives: <discovery and state-reading capabilities>
   Adaptation: <how a fresh session finds, adopts and reconstructs>
   Guarantee: FULL | DEGRADED | UNAVAILABLE
   Verification: <observable entry evidence>

3. Bounded dispatch
   Available primitives: <worker or session creation, addressing, waiting and return capabilities>
   Adaptation: <how assignments and returns work>
   Guarantee: FULL | DEGRADED | UNAVAILABLE
   Verification: <observable worker identity and result path>

4. Write-back
   Available primitives: <durable write and handoff capabilities>
   Adaptation: <where verified state and next actions persist>
   Guarantee: FULL | DEGRADED | UNAVAILABLE
   Verification: <observable durable read-back>

Authority boundary: <permitted establishment/inspection and separately gated actions>
Overall operating mode: FULL | DEGRADED | STOPPED
Stop reason: <none or exact missing prerequisite>
```

## Outcome receipt

If any floor property fails, create nothing and return:

```text
COORDINATOR_BOOTSTRAP_STOPPED
Coordinator identity: <exact identity found but not adopted | none proved | ambiguous candidates>
Workspace: <verified workspace or exact unresolved identity gap>
Verification floor: STOPPED at property <number and name>
Observed evidence: <evidence supporting the stop>
Durable recovery verification: <unmet adoption or establishment limb>
Operating mode: STOPPED
Writes and effects: none
Genuine blockers: <exact capability or evidence gap>
Next authority needed: <later instruction or capability change; never permission for a duplicate>
```

If all floor properties pass, adopt or establish the coordinator, verify the observable result and
return:

```text
COORDINATOR_BOOTSTRAP_READY
Coordinator identity: <exact durable identity>
Durable recovery verification: <adoption read-back with no identity write | establishment write/read>
Workspace: <verified workspace>
Operating mode: FULL | DEGRADED
Authoritative state sources: <resolved sources>
Transport surface: <what can be addressed>
Ready work: <count or explicit unknown; do not execute yet>
Genuine blockers: <none or exact blockers>
Next authority needed: <exact instruction that would open execution>
```

Then wait for explicit authority to execute. Once authorized, continue through ordinary phase
boundaries until a genuine decision, external dependency or terminal state requires a stop.
````

## Reading the result

The most important part of the return is the evidence, not the label.

- `READY` means the session entered the existing identity or established one after proving absence, with observable recovery evidence.
- `STOPPED` means an identity, evidence or capability requirement could not be satisfied and nothing was created.
- `DEGRADED` is valid only after identity, uniqueness, durable recovery and authority separation all pass.

Three common false positives are worth rejecting:

- “I can see the coordinator” is not “I became the coordinator.”
- “I searched my recent chats” is not a complete-enough uniqueness census.
- “I wrote a task title” is not durable recovery unless a fresh session can find and enter the same identity independently.

The goal is not to force every runtime to say yes. The goal is to make each runtime expose what it can prove.

## Multi-agent execution is not durable coordination

All three product families we examined support some form of multi-agent execution. The [Codex app](https://openai.com/index/introducing-the-codex-app/) manages parallel agents in project threads. [Claude Code Agent Teams](https://code.claude.com/docs/en/agent-teams) provide a lead, shared task list and direct messaging, while Anthropic describes the feature as experimental and names limitations around session resumption, task coordination and shutdown. Cursor provides [subagents](https://prod.cursor.com/docs/subagents) and asynchronous [background agents](https://docs.cursor.com/background-agent).

Our cold test asked a stricter question: can a fresh session recover and enter the same durable coordinator identity, prove that it is unique across the observable portfolio, preserve the authority boundary and write verified state back?

Codex Desktop passed that test. The Claude Desktop/Claude Code and Cursor agent surfaces we tested found the existing coordinator but returned evidence-backed `STOPPED` because they could not inhabit that identity. This is a dated result about the harness surfaces we tested on 3 September 2026. It is not a claim that the underlying models cannot coordinate or that those products lack multi-agent features.

The practical implication is narrower. Outside the tested Codex path, you do not necessarily need to rebuild worker orchestration. You do need to supply any missing durable control layer: coordinator identity and re-entry, a complete-enough uniqueness census, authoritative state, bounded dispatch, authority separation and verified write-back.

## What to do after a clean test

If the receipt is `READY`, give the coordinator one bounded goal. Require it to name the authoritative tracker, permitted outputs, authority limits, evidence standard and stopping condition before it dispatches work. Verify that returned work is checked against the substrate and written back before the session ends.

If the receipt is `STOPPED`, keep it. The negative result tells you which runtime capability or evidence surface is missing. Repair that prerequisite or test a different environment. Do not reinterpret the stop as permission to create another coordinator.

## Sources

- Rebecca Henderson and Kim Clark, “[Architectural Innovation: The Reconfiguration of Existing Product Technologies and the Failure of Established Firms](https://doi.org/10.2307/2393549),” *Administrative Science Quarterly* 35, no. 1 (1990), pp. 9–30.
- OpenAI, “[Introducing the Codex app](https://openai.com/index/introducing-the-codex-app/).”
- Anthropic, “[Orchestrate teams of Claude Code sessions](https://code.claude.com/docs/en/agent-teams).”
- Cursor, “[Subagents](https://prod.cursor.com/docs/subagents)” and “[Background Agents](https://docs.cursor.com/background-agent).”

## About Bamboo DCM

Bamboo DCM is an independent structurer and distributor of corporate and structured credit in Brazil. We turn mid-market companies' growth-capital needs into transactions institutional investors can fund. Since 2022 we have brought over R$900 million to market across 25+ transactions, ~60% of them with first-time institutional issuers. We hold CVM coordinator (Resolution 161) and securitization (Resolution 60) licenses, and we are ANBIMA-adherent.

Regulated activities are conducted by Bamboo Securitizadora S.A. (CNPJ 48.343.871/0001-34), which acts as coordinator of public offerings under its CVM Resolution 161 coordinator license and issues and services CRI, CRA and debentures under CVM Resolution 60. This content is informational and is not an offer, recommendation or promise of returns.

## Contact and license

- **Arthur O'Keefe:** [arthur@bamboodcm.com](mailto:arthur@bamboodcm.com)
- **Felipe Moraes:** [felipe@bamboodcm.com](mailto:felipe@bamboodcm.com)
- **Urian Inhauser:** [urian@bamboodcm.com](mailto:urian@bamboodcm.com)

Free to share and adapt under [CC BY 4.0](../LICENSE) with attribution to [Bamboo DCM](https://bamboodcm.com).

*This manual is part of the knowledge-systems framework Bamboo DCM uses for AI-assisted execution in regulated finance. If the broader framework is useful to your work, get in touch.*
