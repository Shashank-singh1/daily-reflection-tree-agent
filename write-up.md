# Write-Up: Daily Reflection Tree — Design Rationale

## Why These Questions

The hardest constraint in this assignment is the absence of free text. When you can't ask "what happened today?", you're forced to do something much more precise: pre-imagine every meaningful answer a tired employee might give and build those answers as options. That forces you to understand the psychological space deeply, not just describe it.

Each question was designed around a single principle: **the question itself should create the reflection, not just measure it**. By the time someone picks an answer, they should have already had a moment of genuine self-awareness — the tree doesn't wait for the summary node to do its work.

**Axis 1 (Locus of Control):** Rotter's original locus-of-control construct (1954) describes a stable trait, but at DT the context is a *single day* — so I needed questions that surface today's micro-locus rather than a person's general disposition. The "weather report" opener is deliberately metaphorical: it primes people to describe their day as *experienced* rather than *analyzed*, which is more honest. The follow-up questions then look for agency evidence within whatever frame they set — "what drove your decision" asks for specificity, which prevents vague generalizations. Carol Dweck's growth mindset research (2006) informed the option language: I avoided language like "I tried hard" (performance orientation) and instead offered options like "I stayed flexible" (learning orientation) to reflect the actual growth mindset spectrum.

**Axis 2 (Contribution vs Entitlement):** Campbell et al.'s (2004) work on psychological entitlement shows it's largely invisible to the holder — people with high entitlement genuinely believe they're underrewarded relative to their effort. This means direct questions ("Do you feel entitled?") produce defensive reactions, not reflection. Instead, I routed via **what they noticed first**: if the first thing they recall about an interaction is how their effort was received rather than what they gave, that's a soft entitlement signal. The follow-up about recognition ("did you need it?") is the critical differentiator — it separates "I wanted credit for my contribution" (healthy self-respect) from "I'll calibrate future giving based on whether I get credit" (entitlement trap). Organ's OCB framework (1988) shaped the contribution options: volunteering for unglamorous work, helping outside your role, sharing knowledge freely.

**Axis 3 (Radius of Concern):** Maslow's 1969 paper on self-transcendence — largely overlooked compared to his hierarchy — argues that the highest functioning humans orient outward. Batson's (2011) perspective-taking research shows that this orientation has to be *active*, not just cognitive. My questions don't just ask "did you think about others" — they ask "did you act on that noticing." The four-option structure in the opening question (me → team → specific colleague → end user) forms a deliberate radius spectrum, so where someone's attention naturally lands reveals their default frame.

---

## How the Branching Was Designed

The tree has **one structural principle**: route based on the user's *frame* before probing within it. Someone who describes today as "Clear skies" is in an expansive state — they can reflect on the precise nature of their agency. Someone who says "Storm I didn't see coming" needs a different entry point: first validate the difficulty, then gently find where their choices lived.

This avoids the most common failure mode in reflection tools: asking a person who had a genuinely hard day the same question as someone who had a good one. The result feels tone-deaf — like a survey that doesn't know you exist. The branching here acknowledges state before probing it.

**Trade-offs made:**

1. **Depth vs. Breadth.** Each axis has two primary branches and two sub-branches, giving 16 possible paths. I considered adding a third branch level for more granularity, but this risks two problems: (a) the conversation feels too long for end-of-day use, and (b) the differences between branches become too subtle for a single question to cleanly separate. Four reflection nodes per axis felt like the honest maximum.

2. **Non-judgment as a design constraint.** Every reflection node was written and then re-read through the lens of: *if I were on the "bad" side of this axis, would this feel like a lecture?* The "entitlement" reflections were rewritten three times. The phrase "the gap between what I deserve and what I give is often invisible to the person holding it" is designed to name the dynamic without weaponizing it.

3. **Interpolation as care.** Using `{A1_OPEN.answer}` in follow-up questions isn't just a technical feature — it signals to the employee that the system was listening. This changes the emotional quality of the interaction.

---

## What I'd Improve With More Time

1. **Day-over-day signal tracking.** The tree captures a snapshot; the insight is in the trend. I'd add a lightweight persistence layer (even a CSV log) to surface patterns — "Last 5 sessions, you've leaned external on Axis 1 three times on Tuesdays."

2. **Branching into Axis 3 from Axis 2 signals.** Currently, Axis 3 opens with a neutral question regardless of Axis 2 outcome. A more sophisticated tree would carry forward the entitlement/contribution signal: if someone is highly contribution-oriented, the Axis 3 question could explore *who* they're contributing *for* (team vs. organization vs. society), deepening the radius rather than re-establishing it.

3. **A 'challenge mode' branch.** For repeat users who are consistently landing "internal / contribution / altrocentric," the questions become too easy to navigate. A branch that detects high-signal runs and introduces harder questions ("Was any of that giving motivated by wanting to be seen as generous?") would prevent the tool from becoming a feel-good ritual rather than a genuine growth mechanism.

4. **Question rotation within nodes.** The same opening question every day creates a habit of answering rather than reflecting. Maintaining a small pool of question variants that rotate by day of week would sustain the freshness that makes reflection actually work.

---

*Sources: Rotter (1954), Dweck (2006), Campbell et al. (2004), Organ (1988), Maslow (1969), Batson (2011)*
