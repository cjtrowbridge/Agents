# Agents
Me learning how to build a self-hosted agentic pipeline using ollama, jupyter, and autogen.

## Projects

basic-diy.ipynb is me starting completely from scratch and figuring out how to get autogen to work and actually have a bunch of agents collaborate to do something, completely from scratch without reading the documentation first.

## What, How, Why?

I’ll conduct research on agent frameworks that can solve a broad range of tasks such as research, coding, and brainstorming. I’ll look for leading papers, comparing approaches from academic labs and open source groups to provide a comprehensive overview. I will provide relevant citations and references to ensure credibility.


A world‑class agent framework is not a single “model,” but rather an ecosystem of components that together enable a language‑model‑driven agent to remember, plan, act and learn.  Recent research and open‑source projects illustrate a unifying taxonomy: agent construction (profile definition, memory, planning and action), collaboration, evolution and evaluation.  Below are the core qualities and illustrative examples drawn from leading papers and frameworks.

### 1. Rich memory mechanisms

Agents need to maintain context across steps and interactions.  The survey of LLM agents describes **short‑term memory** (transient context), **long‑term memory** (experience repositories, skill libraries) and **knowledge retrieval** from external systems.  Leading frameworks implement this through:

* **Stateful agents and persistent memory.**  Letta provides structured memory blocks that persist across interactions, uses techniques inspired by MemGPT to bypass context limits, and retains long‑term memory across different language‑model providers.
* **Memory‑enabled RAG (retrieval‑augmented generation).**  LlamaIndex integrates document parsing (LlamaParse) and a dynamic context engine to extract relevant information and supply it to agents.  This supports document‑aware agents that can fill forms or trigger downstream processes.
* **Episodic memory buffers.**  Reflexion stores reflective feedback in an episodic memory buffer and uses it to improve future decision making.

### 2. Explicit planning and reasoning

High‑performing agents plan multi‑step actions rather than produce a single response.  Research suggests two complementary approaches:

* **Chain‑of‑thought and ReAct.**  The ReAct framework interleaves chain‑of‑thought reasoning with action generation, using reasoning traces to update action plans and actions to gather external information.  It reduces hallucination in question answering and outperforms imitation and reinforcement‑learning baselines on interactive tasks by 34–10 percentage points.
* **Tree‑of‑Thought (ToT) and graph‑based planning.**  ToT generalizes chain‑of‑thought prompting by maintaining a **tree of thoughts**, exploring multiple reasoning paths and using search algorithms like breadth‑first or depth‑first search to backtrack or look ahead.  Experiments show that GPT‑4 with chain‑of‑thought solved only 4 % of Game‑of‑24 tasks, whereas ToT achieved 74 %.  LangGraph embodies these ideas in software, allowing developers to build graph‑structured workflows with customizable decision nodes and persistent state.

### 3. Tool use and action execution

Effective agents must interact with environments by calling tools or APIs, executing code or performing physical actions.  The survey notes that action execution comprises tool utilization (e.g., Python interpreters, web browsers, APIs) and physical interaction for embodied agents.  Modern frameworks enable this:

* **Function calling and agent tools.**  AutoGen uses an event‑driven architecture where agents communicate asynchronously, call Python functions or external services, and support cross‑language tool integration.
* **Built‑in tool ecosystems.**  DSPy modularizes agent behavior into declarative modules with input/output signatures and includes built‑in optimizers (e.g., MIPROv2, BootstrapRS) to automatically tune prompts and models.
* **Multimodal and multimodal tool support.**  Phidata (Agno) allows agents to handle text, images, audio and video with minimal configuration and provides retrieval‑augmented generation pipelines.

### 4. Multi‑agent collaboration

Complex tasks often require multiple specialist agents to work together.  The survey outlines **centralized control** (controllers that manage workers) and **decentralized collaboration** (agents communicate and revise each other’s work).  Several frameworks implement collaborative patterns:

* **Role‑based crews.**  CrewAI organizes agents into crews with specialized roles (planner, researcher, writer) and offers both no‑code and code‑first interfaces; it supports deployment on cloud or self‑hosted infrastructure and provides human‑in‑the‑loop monitoring.
* **Event‑driven multi‑agent systems.**  AutoGen’s asynchronous messaging allows teams of agents to exchange messages, enabling parallel reasoning and cross‑language coordination.
* **Graph‑based multi‑agent workflows.**  LangGraph enables teams of agents with defined roles and includes quality gates, approvals and streaming output for real‑time monitoring.

### 5. Self‑improvement and adaptation

Agents benefit from the ability to critique and refine their own outputs.  Research emphasises self‑supervised evolution via self-reflection and self-correction.  Key methods include:

* **Self‑Refine.**  This approach generates an initial output, uses the same model to provide feedback and refine the output iteratively, improving task performance by \~20 % across tasks.
* **Reflexion.**  Agents reflect on feedback signals (binary or textual), store reflections, and incorporate them into subsequent episodes; this verbal reinforcement paradigm achieved 91 % pass\@1 on HumanEval (vs. GPT‑4’s 80 %) and improved sequential decision‑making, reasoning and programming tasks.
* **RISE (Recursive Introspection).**  Fine‑tunes models to introspect on mistakes and iteratively improve over multiple turns; experiments show Llama2, Llama3 and Mistral models improve math reasoning over multiple turns.

### 6. Evaluation, observability and safety

To build reliable agents, frameworks must provide evaluation suites and robust monitoring:

* **AgentBench, Mind2Web, BLADE etc.**  The survey lists benchmarks for general and domain‑specific evaluation, ensuring agents are tested across diverse tasks.
* **Observability and debugging tools.**  AutoGen integrates OpenTelemetry to trace events and debug multi‑agent conversations; LangGraph provides streaming and human‑in‑the‑loop controls; CrewAI offers ROI analytics and approval gates.
* **Security and ethical considerations.**  Real‑world deployment raises security, privacy and societal risks; the survey highlights agent‑centric and data‑centric attacks and calls for security evaluations.

### 7. Modularity, extensibility and community support

An excellent framework should be modular, allowing developers to plug in different LLMs, memory backends, and tools without rewriting code.  DSPy’s declarative modules and optimizer ecosystem exemplify this.  LlamaIndex’s connectors, LlamaHub community and 300+ document formats make it adaptable to varied enterprises.  Letta provides an agent development environment (ADE) to inspect and edit memory and reasoning and is built on research from UC Berkeley’s MemGPT.

### 8. Use‑case fit and complementary frameworks

No single framework suits all situations.  For instance, AutoGen excels in research and multi‑agent prototyping; LangGraph is ideal for production systems requiring control and moderation; CrewAI works well for enterprises wanting a user‑friendly, role‑based platform; LlamaIndex shines in document‑centric intelligence; DSPy is suited for modular programming and optimization; Letta provides persistent memory and stateful agents; Phidata/Agno emphasises multimodal agents.  Selecting the right framework depends on the task domain, the need for memory or multi‑agent coordination, deployment constraints and cost considerations.

### Bringing It Together, and Diving Deeper

An **excellent agent framework** therefore combines: (1) robust memory and retrieval mechanisms to provide context and persistence; (2) advanced planning such as ReAct and Tree‑of‑Thought to explore reasoning paths; (3) tool integration to act on the world; (4) multi‑agent collaboration patterns; (5) self‑improvement via reflection and iterative refinement; (6) evaluation tools and safety controls; (7) modular, extensible architectures supported by active communities; and (8) a fit between the framework’s strengths and the intended use case.  By drawing on both foundational research (ReAct, Tree‑of‑Thought, Self‑Refine, Reflexion) and practical systems (AutoGen, LangGraph, CrewAI, LlamaIndex, DSPy, Letta, Phidata), one can design agents capable of research, coding, brainstorming and other complex tasks.

Below is a concrete, end-to-end pipeline that “turns a raw user input into the right mix of agents, tools, memory lookups, plans, and self-improvement loops,” while staying compatible with the research patterns (ReAct, ToT, Reflexion, Self-Refine, RISE) and the OSS frameworks (LangGraph, AutoGen, CrewAI, DSPy, Letta, LlamaIndex/“document RAG”, Phidata/Agno, etc.).
I’m describing **what each stage does, what it needs in/out, and how it decides what to spawn**. Use it as a reference design; you can collapse or expand pieces to fit your stack.

---

## 0. Mental model: Two planes + an event bus

* **Control plane (orchestrator):** Interprets the request, chooses strategies, spawns/coordinates agents, enforces safety/HITL gates, monitors metrics.
* **Data plane (agents + tools):** Agents reason, call tools, read/write memory, produce intermediate artifacts.
* **Event bus / message layer:** Async pub/sub or directed graph edges (LangGraph/AutoGen style). Every agent/tool step emits structured events (state deltas, traces).

---

## 1. Ingress & Normalization Layer

**Purpose:** Capture the raw request + context and turn it into a normalized, typed “TaskSpec”.

**Steps:**

1. **Input collector:** Text, voice, code diff, doc upload, etc.
2. **Sanitizers / guardrails:** PII scrubbing, prompt-injection filters, jail-break scans.
3. **Metadata enrichment:**

   * User identity, permissions, org/team context
   * Session/task IDs, urgency/deadline, cost/latency budget
   * Domain hints from prior sessions (e.g., “coding”, “policy research”)
4. **Normalization:** Convert to a canonical JSON:

```json
{
  "task_id": "uuid",
  "user": {"id":"cj", "roles":["dev","research"]},
  "raw_input": "...",
  "modalities": ["text"],
  "attachments": [{"type":"pdf","path":"..."}],
  "constraints": {"max_cost":"$2", "deadline":"5m"},
  "safety": {"pii":false, "risk_level":"low"}
}
```

---

## 2. Task Understanding & Routing

**Goal:** Decide *what kind of problem this is, how hard it is, and which pipeline template to use*.

### 2.1 Classifiers / routers

* **Task-type classifier(s):** Research vs coding vs brainstorming vs data extraction vs multi.

  * Could be a light model (fast LLM, small transformer) or rule-based (regex on “code”, “write”, “summarize”).
* **Complexity estimator:** Single-shot vs multi-step reasoning vs multi-agent collab.
* **Risk/compliance classifier:** Does it need human approval checkpoints? (LangGraph HITL gates)
* **Modality needs:** Does it require doc parsing (LlamaIndex), code execution, browser/tools, multimodal perception?

### 2.2 Template selection

Map classifiers → **Pipeline Template** (YAML/JSON or a graph definition):

```yaml
template: "research_coding_hybrid"
strategy:
  planner: "ToT+ReAct"
  reflection: "Reflexion+SelfRefine"
  evaluation: ["factuality_check","unit_tests"]
agents:
  - role: "planner"
    archetype: "strategist"
    tools: ["search","memory","task_graph_builder"]
  - role: "executor"
    archetype: "coder"
    tools: ["python_exec","repo_api","unit_test_runner"]
  - role: "critic"
    archetype: "qa_reviewer"
    tools: ["verification","factuality_checker"]
```

---

## 3. Context Assembly & Memory Fetch

Now that you know what you’re doing, assemble **everything the agents need before they start**:

1. **User/profile memory:** Preferences, previous tasks, long-term goals (Letta structured blocks).
2. **Episodic memory:** Outputs from earlier attempts, reflections (Reflexion buffer).
3. **Semantic/RAG retrieval:**

   * If doc-centric → LlamaIndex to parse & chunk docs, build retrievers, build context windows.
   * If web/data research → tool to query APIs, search engines.
4. **Working scratchpad:** A space for chain-of-thought, intermediate plans, partial code, etc.

Output: **ContextBundle** (references to memory IDs + retrieved chunks) injected into the first planner agent.

---

## 4. Planner Stage (single or hierarchical)

**Responsibility:** Turn the TaskSpec into a **task graph / plan** (steps, dependencies, success criteria).

* Use a **Planner Agent** (or multi-pass):

  * **Pass 1:** Broad strategy outline (Tree-of-Thought or Program-of-Thought).
  * **Pass 2:** Expand into a DAG/graph of subtasks with required tools, expected artifacts, evaluation criteria.
  * **Pass 3:** Sanity/risk pass — prune impossible branches, insert HITL checkpoints if needed.

Example plan node:

```json
{
  "id": "step_3",
  "goal": "Implement function X and write unit tests",
  "agent_role": "executor",
  "tools": ["python_exec","github_api"],
  "inputs": ["design_doc.md"],
  "success_metrics": ["unit_tests_pass", "lint_clean"]
}
```

---

## 5. Agent Factory / Spawner

Given the plan, you **instantiate agents** with:

* **Archetype config:** prompt templates, role instructions, signature (DSPy style), tool handles, memory scope.
* **Reasoning strategy:** ReAct vs ToT depth, allowed tokens, reflection cycles.
* **Logging hooks:** Every agent is wrapped with tracing, observability, cost meters.

Pseudo-code:

```python
for node in plan.nodes:
    agent_cfg = archetype_library[node.agent_role]
    agent = Agent(agent_cfg, tools=node.tools, memory_scope=node.memory_ids)
    orchestrator.register(node.id, agent)
```

---

## 6. Execution Loop(s)

Execution is typically iterative and asynchronous:

1. **Agent receives task node + context.**
2. **Reason → Act → Observe loop (ReAct):**

   * Reasoning step (hidden CoT or visible trace)
   * Tool call(s) or environment action
   * Observation ingested (tool result, compile error, search results)
   * Optional **reflection / refinement cycle** (Self-Refine, Reflexion):

     * Generate feedback, store in episodic memory, regenerate answer
3. **Emit event:** `{node_id, agent_id, state_delta, artifacts, cost, confidence}`
4. **Orchestrator updates graph state:** Completed, needs review, spawn new subtasks, escalate ambiguity to planner.

This repeats until:

* All nodes done
* Budget/time exhausted
* HITL approval denies/redirects
* Evaluation gate fails (-> re-plan or retry path)

> **Async patterns:** Use event bus (Kafka/NATS), or LangGraph’s state graph where each node is a step function.

---

## 7. Collaboration Patterns

Support different topologies:

* **Centralized controller:** Planner or “manager” agent assigns tasks; workers return outputs.
* **Peer review loops:** Executor produces output → Critic agent reviews → If fail, send back to Executor with critique (Reflexion-style linguistic feedback).
* **Negotiation/consensus:** Multiple agents propose solutions; “arbiter” selects best (Best-of-N / Debate / Voting).
* **Parallel branches:** Research and coding proceed in parallel; final aggregator merges.

---

## 8. Self-Improvement Layer

Embed improvement at two timescales:

### 8.1 At inference/test time (no finetuning)

* **Self-Refine / Reflexion loops:** After each attempt, generate feedback, store it, and re-attempt.
* **RISE-like sequential improvement:** Convert single prompt to multi-turn MDP; allow multiple turns to converge.

### 8.2 Between tasks / offline

* **Trace analysis + DSPy optimizers:** After tasks finish, run optimizers to improve prompts/modules (BootstrapFewShot, MIPROv2).
* **Policy updates:** Update archetype templates, heuristics, routing classifiers with insights from logs.
* **Memory pruning:** Consolidate episodic memories into distilled knowledge (vector stores, skill rules).

---

## 9. Evaluation, Safety & HITL Gates

At defined checkpoints (pre-output, post-tool run):

* **Automated checks:** Unit tests (code), factuality verification (cross-source check), constraint checks (length, style).
* **Benchmarks / scorecards:** AgentBench, Mind2Web, internal KPIs.
* **Human gates:** “Approve/Reject/Ask clarification.” LangGraph/AutoGen can pause graph and wait for human.
* **Security monitors:** Detect data exfiltration attempts, prompt injection, harmful content.

Failures trigger:

* Re-plan (planner revision)
* Retry same node with different tools/agent
* Escalate to human or fallback simple chain

---

## 10. Output Synthesis & Delivery

* **Aggregator / synthesizer agent:** Merges partial outputs, citations, code, and explanations.
* **Formatting / packaging:** Markdown report, PR to repo, CSV, notebook, dashboard.
* **Post-hoc explanation traces:** Provide rationale traces (sanitized), decision logs, interactive timeline.
* **Persist artifacts:** Store in object store + index for future retrieval.

---

## 11. Persistence & Observability

* **State store:** Plan graph, node states, messages, artifacts. (Redis + Postgres + object store)
* **Memory stores:** Vector DB(s) for semantic memory, KV for episodic logs, relational for user profiles.
* **Telemetry:** OpenTelemetry spans, cost meters, token usage, latency metrics.
* **Replay & audit:** Ability to replay a task to debug or to train evaluators.

---

## 12. Deployment Patterns

* **Local dev:** Single-process orchestrator (LangGraph local), SQLite memory, lightweight tools.
* **Prod:** Orchestrator service + microservices for tools (browser, code exec), containerized agents, message bus, scalable vector DB.
* **Hybrid:** Sensitive memory on-prem (Letta/Phidata self-host), cheap tools in cloud.
* **Config management:** Templates/versioning in Git; hot-reload archetypes; feature flags for new strategies.

---

## 13. Concrete “wiring” examples

### 13.1 Minimal research+code example (ReAct + Reflexion)

1. Ingress → classify as “research+code” → template T1
2. Fetch prior mem + relevant docs (LlamaIndex)
3. Planner(agent A) drafts task DAG (ToT)
4. Spawn:

   * Researcher(agent B, tools: web\_search, RAG)
   * Coder(agent C, tools: python\_exec, repo\_api)
   * Critic(agent D, tools: unit\_tests, factuality\_checker)
5. Loop:

   * B collects facts → D validates → if fail, Reflexion loop (B critiques itself)
   * C writes code → D runs tests; fails → Self-Refine loop (C critiques/refactors)
6. Aggregator(agent E) merges report + code, asks human if HITL needed.
7. Persist: store traces, add distilled facts to long-term memory.

### 13.2 Document-heavy legal analysis (Doc RAG + LangGraph HITL)

* Router picks “doc-law” template:

  * LlamaIndex pipeline pre-runs to parse PDFs
  * Planner builds nodes: parse → summarize → cross-cite → risk check
  * Agents spawn with memory of doc chunks; HITL gate after summary for accuracy.
  * Evaluation node runs factuality & citation checks → loop back on failures.

---

## 14. Interfaces & Schemas (keep things inspectable)

* **Agent contract:**

  * Inputs: `goal`, `context_refs`, `tools`, `constraints`
  * Outputs: `artifacts`, `next_actions`, `reflection`, `metrics`

* **Event schema:**

```json
{
  "event": "agent_step_completed",
  "task_id": "uuid",
  "node_id": "step_3",
  "agent": "executor",
  "thought": "... (optional/redacted)",
  "tool_calls": [{"name":"python_exec","args":"..."}],
  "result": {"status":"ok","artifact_ids":["code.py","tests.log"]},
  "reflection": "Need to improve perf...",
  "cost": {"tokens": 1423, "usd": 0.03},
  "timestamp": "..."
}
```

---

## 15. How to decide “what to spawn” (practical heuristics)

1. **Single vs multi-agent:**

   * If task can be sequential and linear with minimal tool use: one agent + ReAct.
   * If task spans distinct disciplines or benefits from independent proposals/reviews: multi-agent.
2. **Depth of reasoning (ToT breadth/DFS depth):**

   * If ambiguity high or many solution paths → enable ToT search w/ pruning.
   * If budget tight → limit branches, use Best-of-N sampling with small N.
3. **Reflection loops:**

   * Enable Reflexion/Self-Refine if output quality is crucial and retries are cheap.
   * Skip for trivial tasks to save cost/latency.
4. **Memory scope:**

   * Give agents *just enough* memory (context windows are finite). Use memory routers to decide which memories to attach.
5. **Safety gates:**

   * If risk classifier high, insert critic/HITL nodes automatically.

---

### TL;DR Pipeline Skeleton

1. **Ingress → Normalize → Classify task & risk**
2. **Select pipeline template → Assemble context/memory**
3. **Planner builds task graph**
4. **Agent Factory instantiates role agents with tools & strategies**
5. **Async ReAct/ToT execution loops + Reflection/Self-Refine**
6. **Critics & checkpoints evaluate; HITL as needed**
7. **Aggregator synthesizes final outputs**
8. **Persist artifacts, memories, traces; run offline optimizers**
9. **Update archetypes & routers from telemetry (continuous improvement)**

---

### Some Other Directions For Further Research:

* A LangGraph/AutoGen graph diagram or code skeleton for this.
* YAML schemas for templates/archetypes.
* A concrete implementation using your stack (Docker, Ollama, Jupyter, etc.).
* Integration plan for your existing RAG + DSPy optimizer loops.
