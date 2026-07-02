For **Agent AI Engineering**, a generic runbook isn't enough. Production agent systems fail in ways that traditional APIs and even RAG systems do not.
At the Principal Engineer level, you should think in terms of **failure domains**, **detection**, **mitigation**, and **recovery**.

# Agent AI Engineering Production Runbook

## 1. LLM Failures

### Symptoms

* Hallucinations
* Invalid JSON
* Infinite reasoning
* High latency
* Token limit exceeded
* Context overflow

### Detection

* Schema validation
* Output validation
* Latency alerts
* Token usage monitoring

### Mitigation

* Retry with lower temperature
* Switch model
* Repair JSON
* Context compression
* Fallback prompts

---

# 2. Planning Failures

### Symptoms

* Wrong execution plan
* Missing steps
* Duplicate tasks
* Circular planning
* Deadlock

### Detection

* Plan validation
* DAG validation
* Duplicate detection
* Dependency checks

### Mitigation

* Re-plan
* Planner retry
* Human approval
* Rule-based planner fallback

---

# 3. Tool Calling Failures

### Symptoms

* Wrong tool selected
* Tool timeout
* Invalid arguments
* API failure
* Authentication failure

### Detection

* Tool health
* Argument validation
* Contract testing
* API monitoring

### Mitigation

* Retry
* Alternate tool
* Cached response
* Human intervention

---

# 4. Memory Failures

### Symptoms

* Lost conversation
* Wrong memory recalled
* Duplicate memories
* Memory poisoning

### Detection

* Memory validation
* Similarity thresholds
* Freshness checks

### Mitigation

* Memory pruning
* Re-ranking
* Version rollback
* Isolation per tenant

---

# 5. RAG Failures

### Symptoms

* Wrong documents
* Empty retrieval
* Duplicate chunks
* Stale knowledge

### Detection

* Retrieval precision
* Citation validation
* Groundedness score

### Mitigation

* Hybrid search
* Query rewriting
* Re-indexing
* Retriever fallback

---

# 6. Multi-Agent Failures

### Symptoms

* Agents waiting forever
* Message loops
* Duplicate execution
* Conflicting answers
* Lost messages

### Detection

* Distributed tracing
* Agent state tracking
* Timeout monitoring

### Mitigation

* Supervisor agent
* Circuit breaker
* Dead-letter queue
* Retry policies

---

# 7. MCP Failures

### Symptoms

* Tool discovery failure
* Context mismatch
* Authentication failure

### Mitigation

* MCP server failover
* Tool cache
* Protocol validation

---

# 8. A2A Failures

### Symptoms

* Agent unreachable
* Wrong protocol version
* Duplicate messages
* Ordering issues

### Mitigation

* Retry
* Version negotiation
* Idempotency
* Message persistence

---

# 9. Context Engineering Failures

### Symptoms

* Context overflow
* Missing instructions
* Prompt conflicts
* Context drift

### Mitigation

* Context compression
* Summarization
* Priority-based context selection

---

# 10. Evaluation Failures

### Symptoms

* Regression after deployment
* Hallucination increase
* Low faithfulness

### Mitigation

* Automatic rollback
* Golden dataset evaluation
* Canary deployment

---

# 11. Gateway Failures

### Symptoms

* Provider outage
* Rate limits
* High latency

### Mitigation

* Model routing
* Provider failover
* Load balancing
* Response caching

---

# 12. Infrastructure Failures

### Symptoms

* GPU OOM
* Pod crash
* Autoscaler failure

### Mitigation

* Autoscaling
* Node replacement
* Batch scheduling
* GPU migration

---

# 13. Security Failures

### Symptoms

* Prompt injection
* Jailbreak
* Secret leakage
* Tool abuse

### Mitigation

* Guardrails
* Input/output filters
* Least-privilege tool access
* Human approval for sensitive actions

---

# 14. Cost Failures

### Symptoms

* Token explosion
* Infinite agent loops
* Excessive tool calls

### Mitigation

* Token budgets
* Maximum reasoning steps
* Tool quotas
* Budget enforcement

---

# 15. Observability Failures

### Symptoms

* Missing traces
* No telemetry
* Blind spots

### Mitigation

* OpenTelemetry
* End-to-end tracing
* Structured logging
* Central dashboards

---

# Production Incident Examples

### Incident 1: Infinite Agent Loop

**Root Cause:** Planner repeatedly delegated the same task.

**Detection:** Max execution depth exceeded.

**Resolution:**

* Stop execution.
* Mark task as failed.
* Trigger replanning.
* Alert operator if retries exceed threshold.

---

### Incident 2: Wrong Tool Selected

**Root Cause:** Ambiguous tool descriptions.

**Resolution:**

* Improve tool metadata.
* Validate tool arguments.
* Introduce tool-ranking logic.

---

### Incident 3: Hallucinated Database Update

**Root Cause:** Agent fabricated a successful write.

**Resolution:**

* Verify tool results before responding.
* Require transaction confirmation.
* Add post-execution validation.

---

### Incident 4: Memory Poisoning

**Root Cause:** Incorrect information persisted to long-term memory.

**Resolution:**

* Version memories.
* Require confidence thresholds.
* Support memory rollback.

---

### Incident 5: Vector Database Outage

**Root Cause:** Retrieval service unavailable.

**Resolution:**

* Fail over to secondary vector store.
* Use keyword search as fallback.
* Notify users of degraded retrieval.

---

### Incident 6: LLM Provider Outage

**Root Cause:** Primary inference endpoint unavailable.

**Resolution:**

* Route to backup model/provider.
* Serve cached responses where appropriate.
* Degrade gracefully for non-critical features.

# Production Readiness Checklist

* Health checks for all agents
* Planner validation
* Tool contract testing
* MCP compatibility testing
* A2A interoperability testing
* RAG evaluation before release
* Automated prompt regression tests
* Circuit breakers
* Retry with exponential backoff
* Idempotent tool execution
* Dead-letter queues
* Human approval for high-risk actions
* Distributed tracing
* Cost guardrails
* Security guardrails
* Continuous evaluation

## SRE Metrics for Agent Systems

* Agent success rate
* Goal completion rate
* Planning accuracy
* Tool success rate
* Tool retry rate
* Average reasoning steps
* Tokens per task
* Cost per task
* Time to first action
* End-to-end task latency
* Hallucination rate
* Groundedness score
* Memory retrieval accuracy
* RAG precision/recall
* Human escalation rate
* Multi-agent coordination success
* Provider failover frequency
* Mean time to detect (MTTD)
* Mean time to recover (MTTR)

This level of operational thinking—covering failure modes, detection, mitigation, recovery, and measurable operational metrics—is what distinguishes production-ready Agent AI engineering from building simple LLM demos.
