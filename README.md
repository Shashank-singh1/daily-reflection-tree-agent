# Daily Reflection Tree Agent

A deterministic end-of-day reflection system built using a structured decision tree and a standalone web-based AI agent.

### Key Highlights
- 37-node decision tree across 3 psychological axes
- Fully deterministic (same input → same output)
- No LLM calls at runtime → zero hallucination risk
- Built for real user reflection, not just evaluation

# Why this is different

- Most AI agents rely on LLMs → this system avoids them entirely
- Reflection is created *during questions*, not just at the end
- Branching adapts to user state (good day vs bad day)
- Designed with behavioral psychology, not just logic# Daily Reflection Tree — Submission

## How to test (30 seconds)

1. Open `agent/index.html`
2. Click through the reflection
3. Notice:
   - No randomness
   - Deterministic branching
   - Personalized summary based on answers

# DT Fellowship Assignment | DeepThought Growth Teams

---

## Repository Structure

```
/tree/
  reflection-tree.json     ← Part A: full tree data (37 nodes)
  tree-diagram.md          ← Part A: Mermaid visual diagram + node count

/agent/
  index.html               ← Part B: standalone web agent (no dependencies, no LLM)

/transcripts/
  persona-1-transcript.md  ← Both transcripts in one file (Victim/Entitled/Self-centric + Victor/Contributing/Altrocentric)

write-up.md                ← Design rationale (max 2 pages)
README.md                  ← This file
```

---

## Part A: The Tree

**File:** `tree/reflection-tree.json`

The tree is a JSON array of 37 nodes. Each node has:

| Field | Description |
|-------|-------------|
| `id` | Unique string identifier |
| `parentId` | Parent node (for reference) |
| `type` | `start`, `question`, `decision`, `reflection`, `bridge`, `summary`, `end` |
| `text` | What the user sees. Uses `{NODE_ID}` interpolation for prior answers |
| `options` | Array of strings (for questions) or routing rules (for decisions) |
| `target` | Default next node |
| `signal` | State accumulation tag (e.g. `axis1:internal`) |
| `axis` | Which reflection axis this node belongs to |

**Tracing a path:** Follow `target` for non-decision nodes. For decision nodes, match the previous answer against `options[].match` and follow `options[].goto`. Every path converges at `SUMMARY` then `END`.

**Node counts:**

| Type | Count |
|------|-------|
| start | 1 |
| end | 1 |
| question | 13 |
| decision | 9 |
| reflection | 10 |
| bridge | 2 |
| summary | 1 |
| **Total** | **37** |

**Visual diagram:** See `tree/tree-diagram.md` — renders with any Mermaid viewer (GitHub, Mermaid Live Editor at mermaid.live).

---

## Part B: The Agent

**File:** `agent/index.html`

A single-file web agent. No build step. No dependencies. No LLM calls at runtime.

**To run:**
```bash
open agent/index.html
# or
python3 -m http.server 8000  # then visit localhost:8000/agent/
```

**How it works:**
1. Tree data is embedded directly in the HTML (same structure as `reflection-tree.json`)
2. `ReflectionEngine` class walks nodes, resolves decisions, accumulates state
3. UI renders each node type differently — questions show option buttons, reflections show a styled card, bridges auto-advance after 1.4s
4. Summary node computes dominant axis signals and selects from 8 pre-written closing prompts
5. All text interpolation uses `{NODE_ID}` → `state.answers[NODE_ID]`
6. Zero randomness. Same answers → same path → same summary. Every time.

---

## Design Summary

Three axes, in sequence:

1. **Locus of Control** (Rotter, 1954 + Dweck, 2006): Did you navigate today or did it happen to you?
2. **Contribution vs Entitlement** (Organ, 1988 + Campbell et al., 2004): Were you thinking about what you gave or what you were owed?
3. **Radius of Concern** (Maslow, 1969 + Batson, 2011): Was your frame self-referential or did it include others?

The tree has **16 distinct paths** through it. All converge at the same summary node, which produces one of **8 context-specific closing prompts** based on the axis signal tallies.

**Tone contract:** The tree does not judge. A person on the "external/entitlement/self-centric" end leaves with self-awareness and one concrete action — not shame. The reflections were each drafted and then re-read from the perspective of someone who just picked the "wrong" answer to check for lecture-tone.

---

## What I Would Add With More Time

1. Day-over-day persistence (pattern tracking across sessions)
2. Signal carry-forward between axes (Axis 2 opening adapts to Axis 1 outcome)
3. "Challenge mode" for repeat users who consistently land well
4. Question rotation pools to prevent habituation

---

This is not just a tree. It's a structured way of thinking about your day.
