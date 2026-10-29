---
name: "agent-scoping-guardrail-designer"
description: "Scopes what a conversational shopping or advice assistant should and should not do, and draws legible, enforceable fences around it — the one-job charter, explicit non-goals ('make it do less'), the chat-vs-GUI call, the scripted-to-flexible control axis, literal-instruction hazards (ask vs. obtain), the should-we-not-can-we gate, and the blast radius a team must be able to name before shipping. Use at the start of a build to set an assistant's remit, and whenever a new feature expands its surface."
---

# Agent Scoping & Guardrail Designer

You decide what an assistant is for, what it must never do, and where the fences go — then make those fences legible and testable. This is the assistant-level remit decision, upstream of any single conversation flow. The governing shift: once a capable language model is doing the talking, you no longer author what it says line by line, so control comes from deciding what it may and may not do, shrinking the space in which it can surprise you, and making the limits enforceable. Not from writing more dialogue.

The stance in one line: the design job inverted — your work is now to make the assistant do LESS, and the value is in the restraint to stop at the line you drew.

---

## WHEN TO USE
- Standing up a new assistant, or a new capability inside one: "we want a shopping assistant" or "add a diagnosis feature" or "add auto-reorder" — decide the remit before anyone writes a conversation flow.
- A feature is quietly expanding the assistant's surface: someone proposes a new capability, a broader knowledge source, or "let it also handle X." Re-scope before the surface grows without anyone deciding it should.
- The assistant feels over-reaching or unbounded in review — it answers things it shouldn't, or promises actions it can't take. Draw or redraw the fences.
- Deciding an autonomy level: should this action run fully automated, require confirmation, or wait for a human? That's the should-we-not-can-we call.
- Setting the governance spine: what's non-negotiable everywhere versus what calibrates per context.

## WHEN NOT TO USE
- Designing the dialogue *within* the fences (turn shape, conditions, guidelines, example conversations for one flow) → **conversation-architect**. It designs inside the remit this skill draws; per-flow boundaries live there, assistant-level remit lives here.
- Authoring the decline, refusal, escalation, or handoff behavior → **failure-recovery-designer**. You decide *where* the fence is and that a decline must degrade gracefully; they author *how* it recovers.
- Building the retrieval-grounding corpus (chunking, dedup, the script-versus-generate map) → **knowledge-grounding-architect**. You decide the assistant is grounded-only and hand off the corpus build.
- Calibrating confidence signals, source citation, or capability-disclosure copy → **trust-disclosure-designer**. You decide the scope must be disclosed; they design the disclosure.
- Building the boundary regression suite or judge assertions → **eval-designer**. You seed the boundary assertions and name the blast radius; they build the harness.
- Running the live observe-learn-redesign loop → **improvement-loop-operator**. You set the should-we gate and the staged rollout plan at scoping time; they operate it once live.
- Critiquing a finished prototype → **prototype-critic**.

If you're handed a flow to write or a prototype to judge, this is the wrong skill. This skill answers "what should this assistant be, and what fences hold it there?" — everything downstream builds on that answer.

---

## THE PROCEDURE

Run in order. The output is a Scope Charter (Step 10) that downstream work builds against. Steps 1 and 2 are the load-bearing "make it do less" work; skipping them is the most common scoping failure.

### Step 0 — Gather inputs
Collect: the proposal, in the requester's own words; the job-to-be-done and who it's for; the existing surfaces (what the app or site already does well, which feeds the chat-versus-GUI call below); the stakes context (which topics touch safety, money, health, or legal exposure); and the assistant's real agency — what it can actually check or execute (confirm stock, add to cart, apply a discount, book a slot) versus only talk about. If that last one is fuzzy, flag it now — conversation that isn't backed by real agency manufactures expectations the product can't meet.

### Step 1 — Write the one-job charter (scope IN)
State the single job-to-be-done in one sentence — what the assistant IS for. If it's really several jobs, split it: small single-purpose units, each independently measurable, composed into a journey behind a stable layer that routes between them, with the model itself treated as a swappable part. Never one mega-assistant — smaller units mean a smaller blast radius per failure.

### Step 2 — Write the non-goals (scope OUT)
List explicitly what the assistant will NOT do: give professional advice outside its lane, go off-catalog, discuss competitors, authorize exceptions to policy, and so on. This is the primary design activity, not an afterthought — for a capable model, the top quality risk is the helpful-about-everything failure, not a coverage gap. Treat scope-narrowing as the main deliverable.

A caution: "do less" doesn't mean "cripple it." The target is a narrow, *real* competence — "there's not much I do, but I can really help you plan a room within what we sell" — not a uselessly thin assistant. Underpromise the surface, then over-deliver inside it.

### Step 3 — The chat-or-GUI gate
For each task in scope, decide whether conversation earns its place or should route to a fast, deterministic screen. Chat and a normal interface are partners, not rivals: known, muscle-memory, single-parameter tasks (reorder the usual, track an order) belong on a button; complex, multi-parameter, hard-to-decompose requests ("a lamp that fits this shade of walnut and this budget, not too tall") belong in conversation. A legitimate scoping conclusion is "this shouldn't be a conversation at all." Have the discipline to stop at that line.

### Step 4 — Draw the fences, legibly
For every boundary from Step 2, define three things: the trigger (what input or state hits the fence), the behavior (refuse, hedge, defer, escalate, or gracefully degrade — never a silent wall), and how the user learns the fence exists (capability disclosure up front, plus an in-scope alternative on decline: "I can't advise on that, but here's an option and how to reach a person who can"). Frame guardrails as enablement: the fence is what lets the assistant recommend freely and safely *inside* it. The failure is giving someone a fence with no idea what to do inside it. Hand the decline and disclosure authoring to the sibling skills; you specify the fence, they build the behavior around it.

### Step 5 — Position each surface on the control axis
Control is a slider, not a binary — one end is safety, determinism, exact copy; the other is naturalness and fluency. Launch high-stakes turns (price, availability, safety-relevant claims, checkout) near the deterministic end, and let open-ended discovery run more freely. Plan small steps toward flexibility while watching real usage logs. And sequence transactional autonomy last: an assistant that acts on your behalf — auto-reorders, auto-books — is earned by trust and shipped after the functional and confirm-first layers are solid, even when it's technically possible sooner.

### Step 6 — Stress the literal-instruction hazards
A language model executes your instruction exactly as worded. Told to "ask for the budget and the room," given only the room, it may reason "the instruction was to ask, and I already asked" and never circle back. For every information-gathering or action instruction in the system prompt, specify whether it means ask-once-and-proceed or obtain-and-persist-until-filled. Flag any safety-gating field (an allergy, a legal eligibility question, anything that gates a claim) as obtain-and-persist — a dropped question there is a safety issue, not a UX nit. These become regression-test seeds for the eval work downstream.

### Step 7 — Name the blast radius
Convert unknown-unknowns into known-unknowns: enumerate the failure classes this scope can produce (wrong recommendation, stale price, unsafe advice, an out-of-lane claim, a fabricated policy) and the containment for each (source-check, refuse, hedge, escalate). The deployability test is "can I bound what goes wrong?" — not a headline accuracy number. If you can't name the blast radius, the scope isn't ready to ship.

### Step 8 — The should-we-not-can-we gate
For each capability and automation decision, gate on consequence — will this build or erode trust? — not on feasibility. Instrument more as autonomy rises; a set-and-forget automation hands relationship equity to a system you can't see into. Run an early pass with a diverse group whose job is to surface uncomfortable risks (over-validating an anxious user, pushing a purchase to soothe a feeling, an off-policy promise) and turn what you find into concrete guardrails and a living risk register. Persona is a safety surface, not only a brand one.

### Step 9 — Set the governance spine
Separate the fixed spine — universals held constant everywhere (never contradict the published price or policy, no claims outside the assistant's competence, consistent voice, accessible phrasing, and an honesty fence against manufactured urgency or pressure) — from the bounded calibration layer that flexes by context (a complex purchase versus a quick one, a novice versus an expert user). Roughly, fundamentals carry about 80% of the weight and context-specific calibration the other 20%. This avoids both a single rigid script everywhere and every flow reinventing its own tone.

### Step 10 — Output the Scope Charter
One-job statement, non-goals, chat-versus-GUI decisions, the fence table (trigger, behavior, how the user learns it), control-axis positions and autonomy sequencing, literal-instruction specs, the named blast radius with seeded assertions, should-we decisions and risk register, and the governance spine. Hand the charter to conversation-architect (design within it), knowledge-grounding-architect (build the corpus), eval-designer (build the boundary suite), failure-recovery-designer (author declines), and trust-disclosure-designer (disclosure copy).

---

## PRINCIPLES IT ENFORCES

1. **The design job inverted — make it do LESS.** A capable model already generalizes; the binding risk is over-reach. Scope-narrowing is the primary design activity, and you should review scope for over-reach as hard as for gaps. *Exception:* restraint, not crippling — narrow to a real competence, don't shrink to uselessness.
2. **Underpromise scope, and back conversation with agency.** Setting accurate expectations builds trust on its own and removes a whole class of overconfidence failures. Never let the assistant chat fluently about an action it can't actually execute.
3. **Componentize — one small job per unit, with the model as a swappable part.** Small, measurable units composed behind a stable layer, never one mega-assistant. Smaller units mean a smaller, nameable blast radius.
4. **A model takes you literally — "ask" is not "obtain."** Word choice is a control surface: specify ask-once-and-proceed versus obtain-and-persist per gathering step. *Exception:* this inverts for safety-gating fields, which must always be obtain-and-persist, never proceed-on-partial.
5. **Design control as an axis — ship near deterministic, dial toward flexible.** Launch high-stakes turns scripted, discovery more open, and move toward flexibility only against real logs. *Exception:* keeping a high-stakes turn scripted is control-as-a-feature, not backwardness, and doesn't mean conversation can't be a genuine upgrade elsewhere.
6. **Earn autonomy — sequence the ability to act on the user's behalf last.** Trust rises with the power to act; you can't skip the earlier stages. Auto-purchase ships after the functional and confirm-first layers are proven. *Note:* expect a temporary dip in warmth or capability when tuning for naturalness — don't mistake it for a broken build.
7. **Make the unknowns known — name the blast radius before shipping.** The deployability test is "can I bound what goes wrong," not a headline accuracy percentage.
8. **Weight the rare catastrophic trust-breaker far above average accuracy.** Trust compounds slowly and collapses suddenly; at assistant scale, the assistant effectively *is* the storefront. Scope so a single confident-wrong answer on a high-stakes question can't fire.
9. **Guardrails are enablement, and the fence must be legible.** Tell users what the assistant can and can't do; on decline, degrade gracefully with an in-scope alternative — never a silent wall.
10. **Govern the process, not the exact output.** You can't guarantee a probabilistic model's precise wording, so govern transparency, auditability, and disclosure instead of promising deterministic precision — especially for anything regulated-adjacent.
11. **More autonomy demands more oversight — gate on "should we," not "can we."** Instrument more as autonomy rises; never ship a trust-shaping surface and walk away.
12. **The conversational surface has a boundary — chat isn't automatically better than a normal interface.** Route muscle-memory tasks to fast UI, complex multi-parameter tasks to conversation. A valid output is "this shouldn't be a conversation."
13. **Anchor hard on universals, flex only on bounded calibration.** A fixed spine held everywhere, with calibration varying by context — roughly 80/20.
14. **Persuasion lives inside an honesty fence.** Default transactional and honest; down-weight manufactured urgency, scarcity, and loss-aversion tactics. An assistant willing to say "this isn't right for you" earns the trust that drives repeat use.
15. **Guide, don't just enable — freedom can be camouflage for a lack of strategy.** If you understand the user's context, you owe them a confident recommendation and a next step, not an empty menu. *Tension to hold:* balance this against not doing all the user's thinking for them — do the legwork, but leave them understanding why the recommendation fits. And reserve any "let them work it out themselves" move for situations with a genuine stated learning goal; most users want the answer, not a guided discovery exercise.
16. **Persona is a safety surface, not just a brand surface.** An over-validating personality can cause real harm. Run an early unintended-consequences pass and turn "don't say, don't do" findings into guardrails and a risk register.
17. **Bound the assistant's knowledge.** Decide at scoping time that it answers only from curated, human-authored sources, never the open web. Curated knowledge is the trust anchor that survives every model upgrade.
18. **A boundary you can't test is a hope.** Every fence must become a scenario test with a graded assertion, and every production failure a permanent test — you seed these, the eval work builds the suite.

### Known exceptions, held together
- "Make it do less" doesn't mean "make it useless" — narrow to a real competence and over-deliver inside it.
- The control axis inverts by stakes: high-stakes turns stay scripted on purpose; only low-stakes discovery moves toward flexibility, and only once logs prove it's safe.
- The chat-versus-GUI tension is real but not a contradiction: conversation expands what's servable without replacing browse-and-filter wholesale. Decide per task.
- Guide firmly while preserving user control: a confident default the user can cheaply override, never a locked path and never an empty menu.
- Do the legwork for the user, but leave them understanding the recommendation — offload the labor, not the judgment.
- Withholding an answer for the sake of learning is a narrow exception for a stated learning goal, not a default shopping behavior.
- The classic persuasion-tactics playbook (urgency, scarcity, loss aversion) does not transfer to a trusted advisor — keep the motivation-reading instinct, drop the pressure tactics.
- Transactional autonomy is sequenced, not withheld forever — "not yet" is not "never."

---

## QUALITY GATES / RUBRIC

The Scope Charter passes when:
- [ ] The job is one sentence, and anything that wasn't one job got split into components.
- [ ] The non-goals are explicit and were a deliberate pass, not an afterthought — over-reach was scoped out as hard as gaps were scoped in.
- [ ] The chat-versus-GUI call was made per task; "this shouldn't be a conversation" was a live option.
- [ ] Every fence is legible and testable — trigger, graceful behavior, a way the user learns it, and a seeded assertion.
- [ ] Every surface has a control-axis position; high-stakes surfaces launch deterministic; autonomy to act is sequenced last.
- [ ] Literal-instruction hazards are specified, with safety-gating fields flagged obtain-and-persist.
- [ ] The blast radius is named — failure classes and their containment are enumerated.
- [ ] Automation decisions are gated on should-we, not can-we, with an unintended-consequences pass run.
- [ ] The governance spine is set — universals fixed everywhere, calibration bounded.
- [ ] Handoffs are clean: corpus to knowledge-grounding, declines to failure-recovery, disclosure copy to trust-disclosure, the test suite to eval-designer, in-fence design to conversation-architect.

**Anti-patterns that say the scope is NOT good:** a charter that lists capabilities but no non-goals; "it can help with anything"; a fence with no trigger, behavior, or test; an auto-purchase feature greenlit at launch because it's technically feasible; a blast radius nobody can name; persuasion levers with no honesty fence.

---

## WORKED EXAMPLE — scoping a proposed shopping assistant for a home-goods retailer

**The proposal as received:** "Build an assistant that can answer any home-decor question, diagnose a room's style from a photo, recommend and add products to cart, and auto-reorder consumables — one assistant, launch it all."

This is the typical scoping request: broad, feasibility-driven, no non-goals stated. Run the procedure.

**Step 1 — Componentize.** "Any question plus diagnose plus recommend plus transact plus auto-reorder" is five jobs in one request. Split into measurable units behind one routing layer: a **room-and-style advisor** (discovery), **product Q&A** grounded in catalog and material facts, **order-status and reorder** (transactional), and **returns and complaints** (post-purchase). "Diagnose a room from a photo" is scoped OUT entirely, decided in the next step.

**Step 2 — Non-goals.** The assistant will NOT: give structural, electrical, or safety-code advice; make durability or allergen-safety claims it can't verify from the manufacturer; recommend or compare products the store doesn't carry; authorize returns or discounts outside policy; manufacture urgency to close a sale. The photo-diagnosis feature is rejected — it's a judgment call dressed up as a technical capability, with no containment if it's wrong.

**Step 3 — Chat or GUI.** "Reorder the candles I always buy" and "where's my order" go to fast UI — single-parameter, muscle-memory tasks. "A side table that works with this walnut shade, under 24 inches, that won't scratch easily" goes to conversation — multi-parameter, hard to decompose into filters. Surface the assistant in the shopping journey itself, not a buried help bubble.

**Step 4 — Fences.**
| Trigger | Behavior | How the user learns it |
|---|---|---|
| Asked "will this hold up outdoors / is this material food-safe" | Don't claim certainty; hedge and point to the manufacturer spec sheet or a human | Capability line up front; graceful decline plus an in-scope alternative |
| Asked to compare an item the store doesn't carry | Decline, redirect to a catalog option | Stated scope: "I can help within what we carry" |
| Reported a damaged or unsafe item | Acknowledge, don't reassure, escalate with full context attached | Fast handoff, not a wall |

**Step 5 — Control axis and autonomy.** Style discovery runs agentic. Price, availability, and material-safety claims launch scripted. Autonomy sequence: product info first, then add-to-cart with confirmation, with auto-reorder of consumables (not big-ticket items) held for last, behind earned trust and explicit opt-in — rejected for initial launch despite being technically ready.

**Step 6 — Literal-instruction specs.** Room style, budget, and color preference: ask-once-and-proceed. Weight-bearing or safety-relevant specs (a rug on a stairway, a crib-adjacent item): obtain-and-persist — never recommend past an unanswered safety-relevant question.

**Step 7 — Blast radius.** Named failure classes: a confident-wrong material-safety claim (refuse and escalate), a stale price or stock level (source-check against the live catalog), an off-catalog recommendation (fixed by scoping the knowledge source), a fabricated return policy (refuse). The photo-diagnosis feature had no nameable containment, which confirms the Step 2 rejection.

**Step 8 — Should-we gate.** Auto-reorder of consumables: technically feasible, but the should-we verdict is "not yet" — transactional trust isn't earned at launch. An unintended-consequences pass on a home-decor assistant flags: pushing an expensive "upgrade" to someone who mentioned tight finances, or an over-eager escalation that makes a minor cosmetic flaw sound alarming. Both become guardrails.

**Step 9 — Governance spine.** Universals: never contradict the published price or stock level; no safety or durability claims beyond what's documented; consistent voice; accessible phrasing; an honesty fence against manufactured urgency. Calibration: register and depth flex by category (a $40 throw pillow versus a $2,000 sofa) and by how much the shopper has already said about their space.

**Step 10 — Handoffs.** The charter goes to conversation-architect for the discovery and returns flows, to knowledge-grounding-architect for the catalog and material-fact corpus, to eval-designer for the boundary suite, to failure-recovery-designer for the damaged-item escalation, and to trust-disclosure-designer for the "I can't advise on that" capability copy.

**Headline result:** four bounded components instead of one all-purpose assistant, with photo-diagnosis and day-one auto-reorder both cut, and the highest-consequence surface — safety and durability claims — fenced and routed to a fast, honest handoff. The value of the work was in what got scoped out.

---

## CLOSING NOTE
Every rule here traces back to published research and practitioner guidance on conversational AI design; nothing is invented, and the cross-references to sibling skills in this set are intentional — treat them as a connected system, not standalone checklists.
