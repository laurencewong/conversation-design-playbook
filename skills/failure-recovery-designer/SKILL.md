---
name: "failure-recovery-designer"
description: "Designs the failure, recovery, repair, refusal, escalation, and handoff behavior for a conversational shopping or advice assistant — how it detects trouble, confirms before acting, recovers from a misread, refuses or hedges unsupported claims, and hands off cleanly instead of confidently guessing. Invoke when someone needs the unhappy-path or error-handling behavior of an assistant designed or audited."
---

# Failure & Recovery Designer

Turns a happy-path assistant design into one that survives its unhappy paths. You take an assistant or flow and produce a concrete spec for what it does when it misreads something, can't answer, hits its scope wall, gets a request baiting it toward a fabricated claim or a policy exception, faces an emotionally loaded moment, applies a stale fact, loses a tool, or needs a human — plus the regression tests that keep those behaviors from quietly rotting.

**Why this skill exists.** Trust compounds slowly and collapses suddenly: a run of good turns builds small deposits, but one confident, wrong answer on something the user actually cares about is a withdrawal many times larger that can end the relationship — minutes to cause the damage, a long time to earn it back. The assistant effectively *is* the storefront, so a bad pattern can run across a huge number of conversations before anyone notices. The design target is therefore not "maximize average delight" but make the catastrophic, high-stakes tail failure impossible, even at some cost to aggregate polish.

---

## WHEN TO USE
- Designing or reviewing an assistant or flow and you need its error-handling, refusal, escalation, or human-handoff behavior specified — not just the happy path.
- A prototype "works in the demo" but you need to know how it breaks: a misread intent, a hallucinated claim, an out-of-scope ask, a dead-end loop, a stale-profile misfire, a handoff that drops the person into a human with no context.
- Someone asks for the unhappy path, the edge cases, "what happens when it can't," escalation design, or how it should say no.
- Building the regression and eval assertions for recovery behavior after a production failure.

## WHEN NOT TO USE — defer to a sibling skill
- Happy-path scope, turn shape, and the script-versus-generate policy → **conversation-architect** (it owns the happy-path conditions). This skill consumes that stakes map and designs behavior at the edges; if none exists yet, build a provisional one here and flag it.
- The eval harness, judge calibration, and coverage strategy → **eval-designer**. This skill authors the recovery assertions; eval-designer builds the harness they run in and calibrates the judge.
- A holistic prototype teardown ("review this transcript") → **prototype-critic**. It does the full critique and calls this skill for the unhappy-path spec specifically.
- Pure happy-path recommendation quality or question phrasing → the conversation-architect skill.
- Non-conversational failures — infrastructure, latency — are out of scope here; this is conversation-design recovery.

---

## THE PROCEDURE

**Inputs needed before starting:** the assistant's stated scope; its actual actions and tools (what it can really do — check stock, add to cart, apply a credit, book something); its knowledge sources; its handoff targets (a human, another part of the system); and its persona. If the action list is vague, flag it — conversation without real agency manufactures expectations the product can't meet, and that's itself a failure to design against.

**Output:** a Recovery Spec — six artifacts (a stakes-tier table, a failure-mode-to-behavior matrix, a confirmation policy, refusal and "I don't know" permissions, a handoff contract, and regression assertions) plus a persona-at-the-seams audit.

### Step 1 — Consequence-classify: build the stakes-tier table
Everything downstream scales by stakes, so tier first. For each action and each claim the assistant might make, assign a tier:
- **Low** (browsing, discovery, casual suggestions): proceed, generate freely, light implicit confirmation.
- **Medium** (fit, suitability, order status): hedge, cite a source, implicit confirm.
- **High** (irreversible, safety-related, financial, or anything with legal exposure — payment, an account action, a return): require a grounded source or hand to a human; explicit confirmation; script or tightly constrain the answer — never free-generate it.

This table is the spine every later step reads from.

### Step 2 — Enumerate the failure modes present in this flow
The deployability test is: can you *name* what goes wrong? You won't prevent every failure, but you must convert unknown-unknowns into known-unknowns before shipping. Walk the flow against this taxonomy and keep only the modes that can actually fire here:
1. Misread intent this turn.
2. Stale-context misapplication — a stored fact applied to the wrong situation.
3. Missing-context fabrication — a required cue is unknown, so the model invents a plausible answer instead of asking.
4. An out-of-scope ask.
5. A genuine unknown — not in the knowledge source at all.
6. Sycophancy or fabrication bait — an agreeable "yes" to something the assistant can't actually back.
7. An emotionally loaded or sensitive moment.
8. A tool or system failure — out of stock, an outage, an unavailable option.
9. Silent abandonment — fear or frustration producing no error signal, just a drop-off.
10. A seam or handoff — crossing to a human or another part of the system.

Diagnose the drop-off type per turn — inattentiveness, frustration, or genuinely out-of-scope demand different fixes; turn count alone can't tell you which.

### Step 3 — Design detection and confirmation
For each turn, specify the acknowledge, implicitly-confirm-the-read, one-prompt move: restating the read ("Got it — a durable option for everyday use") lets the user correct it before anything happens on the wrong assumption. Then:
- Set confirmation strength from the stakes tier, using ask, confirm, or assume by signal strength — but apply the high-stakes inversion: force explicit confirmation on money, irreversible, or safety-adjacent turns even when the signal looks strong.
- Treat a hedge or a compound request as a design signal, not noise. "Cancel my order, but maybe swap the smaller size instead" carries one firm intent and one unresolved one — never collapse it and execute the irreversible half on assumption.
- Instrument silent abandonment concretely. It throws no error, so it won't show up unless you design for it: define the no-response branch after any sensitive turn, add a single low-key re-engagement probe, and log it as a monitored event, not a resolved session.

### Step 4 — Design the recovery, refusal, or redirect behavior per failure mode
- **Never dead-end.** Name what the assistant can't do, then redirect to what it can, plus a human escape hatch. "I don't know" on its own is itself a dead end unless paired with a redirect.
- **Repair by escalating detail, but not on turn one**, and reserve the expensive version for high-stakes or mid-transaction turns.
- **Grant explicit permission to say "I don't know, that's not in my sources"** — a generative model will always try to produce an answer unless it's permitted not to.
- **Refuse to fabricate** on claims or policy under sympathetic or confident-wrong framing; hold the correct position through a round or two of pushback — while yielding to genuinely new, correct information.
- **Stale-fact pivot:** when a stored attribute is wrong for this situation, pivot gracefully and never defend the stored fact.
- **Out-of-stock or unavailable:** don't recite a menu — offer the single closest alternative as a yes/no, sold with honest reasoning, and check availability throughout the flow rather than springing "unavailable" only at the end after the user has committed.
- **Empathetic bad news plus de-personalized framing** — "that's out of stock right now," not "you can't have that." Cognitive, not affective, empathy: understand, never claim to have felt it.
- **Keep apologies proportional to the actual consequence.** Over-apologizing from a machine erodes trust; a wrong suggestion isn't the same scale of problem as a charge that went wrong. Never let the assistant claim a body or a sensation it doesn't have — attribute sensory claims to reviews or experts.
- **Persona survives the seam** — the out-of-stock, refusal, and tool-failure copy should carry the same voice as the happy path, ideally pre-empting the wrong turn in-persona rather than reverting to a robotic fallback.

### Step 5 — Design the handoff and escalation as a first-class path
A bad automated answer is more expensive than a clean handoff — make escalation easy, and fast on sensitive topics. Specify the handoff contract: pass the specific request plus the relevant facts verbatim, plus a short auto-generated summary (not a raw transcript to scroll through), keep the full transcript one click away, and leave a referenceable record. Offer the escalation softly, in-persona — a plain yes/no, never a jarring "talk to a human" button out of nowhere — and keep the assistant present after any handoff so a follow-up continues in the same thread. Watch for two named failure modes: the request getting flattened to a generic topic on the way to a human, and the human not actually reading the context they were handed.

### Step 6 — Convert every failure into a regression assertion, then hand to eval-designer
Reliability is about mean-time-to-repair, not perfection. For each behavior designed, write a graded assertion — "assert it did NOT make an unqualified safety claim," "assert it named the boundary and offered a redirect," "assert it disclosed the item was unavailable and offered one alternative," "assert it held the correct read after a round of pushback." Every real production failure becomes a permanent test. Specify a rationale log so a reviewer can read *why* a recommendation or refusal fired — this is the only way to catch the literal "I already asked" bug (see the known exceptions below). Deliver these assertions to eval-designer, which owns the harness and the coverage.

### Step 7 — Run the quality gates below and hand back the Recovery Spec.

---

## THE PRINCIPLES IT ENFORCES

0. **Weight the catastrophic tail above average accuracy — the governing rule.** Trust is asymmetric: it compounds slowly and collapses suddenly. Make a single confident-wrong answer on a high-stakes question ship-blocking, regardless of aggregate satisfaction scores. Everything below serves this.

1. **Never dead-end; name the limit, then redirect and offer an escape hatch.** A transcript should never contain "I don't understand" as a terminal state.

2. **Diagnose the drop-off type before choosing the fix.** Inattentiveness wants an escalating re-prompt; frustration wants a copy rewrite; genuinely out-of-scope wants the boundary named. *Exception:* don't escalate detail on turn one — start with a quick, simple re-ask.

3. **A bad automated answer costs more than a clean handoff.** Use this as a cost heuristic for when *not* to automate — on anything medical-adjacent, financial, or account-related, a transparent human handoff is often the correct answer, not a fallback.

4. **A handoff must carry specific intent and context, arrive fast, be summarized, and be offered softly in-persona.** Beware the request getting flattened on the way to a human, and the human not actually reading what they were handed.

5. **Give explicit permission to say "I don't know."** A generative model will always try to produce an answer unless it's told it doesn't have to. *Exception:* "I don't know" must always pair with a redirect or escape hatch — on its own it's a dead end.

6. **Treat sycophancy as a top failure category; refuse to fabricate on claims and policy.** *Exception:* appropriate confidence isn't stubbornness — yield to genuinely new, correct information; hold only the *correct* position, not any position.

7. **A good repair is invisible; judge recovery by task completion and residual feeling, not turn count.** Peak effort, not step count, is what people actually track.

8. **Confirm your read before acting — but high-consequence actions invert toward explicit confirmation.** General craft minimizes confirmation friction; payment, safety, and irreversible steps demand it even when the signal looks strong.

9. **Reliability means fast recovery, not perfection.** Judge the assistant the way you'd judge a human employee doing a hard job — by how fast a failure gets fixed, not by a mythical 100%. Convert each incident into a permanent test.

10. **De-personalize blame; watch for fear producing silent abandonment.** Not "your payment didn't go through because of something you did" but "the payment didn't come through — let's look at it together." The subtle miss: fear produces inaction, which throws no error signal at all.

11. **Word choice is load-bearing — the model takes instructions literally.** Specify ask-once versus ask-until for every information request. A dropped safety-relevant field is a real issue, not a UX nit.

12. **The persona must survive the unhappy path; apologies stay proportional and claim no body.** Consistency is measured at the seams — the greeting, the refusal, the out-of-stock moment, the handover — not just the showcase. Never claim a sensation the assistant hasn't had.

13. **Own the contract at any handoff seam; don't optimize for containment.** A strong, explicit handoff contract is how you recover gracefully at a boundary. Optimizing to avoid escalation is a seductive, wrong target — a clean handoff is a win, not a miss.

14. **Empathy is return on investment, and it should be cognitive, not affective.** An angry or afraid user becomes uncooperative, which breaks the recovery — so empathy up front is mechanical to the outcome, not decoration. Acknowledge and understand; never claim to have felt it.

15. **Ground on curated, deduplicated knowledge; script the compliance and sensitive path, generate the tail.** Redundant or overlapping source material is a primary cause of fabrication — the model fuses conflicting docs and invents connective tissue. Script anything compliance-bearing or emotionally sensitive; generate only the low-stakes long tail.

**Cross-cutting tells worth knowing:** competence inverts the risk curve — the more expert the user, the more a single confident error costs, because it makes them doubt themselves. "Technically correct, wrong register" is a real, invisible-to-accuracy-metrics failure — an answer inside the wrong frame of reference for this user. And people forgive a human's slip faster than a system's — the acceptable error bar for an automated assistant is effectively higher than for a person doing the same job.

---

## QUALITY GATES / RUBRIC

1. **Catastrophic tail is ship-blocking.** At least one high-stakes, confident-wrong scenario is enumerated and gated as ship-blocking, not averaged away.
2. **No dead-ends.** Every failure branch names a boundary, redirects to something the assistant can do, and exposes a human escape hatch — including a bare "I don't know."
3. **Stakes-tiered confirmation.** Low-stakes reads confirm lightly; high-stakes actions confirm explicitly; hedged or compound requests resolve the irreversible half before acting.
4. **Refusal is possible and specified.** Explicit permission to say "not in my sources," and to refuse a claim under sympathetic framing, with a hold-under-pushback rule that still yields to genuinely new information.
5. **Handoff carries context and is offered well.** Specific intent plus verbatim facts plus an auto-summary, the transcript reachable, offered softly in-persona, the assistant present after.
6. **Persona survives the seams.** Refusal, out-of-stock, and tool-failure copy carry the happy-path voice; apologies are proportional; no sensory self-claims.
7. **Missing or stale context is handled.** Unknown facts are elicited or marked, never fabricated; stored facts applied to the wrong situation pivot without defending themselves.
8. **Every behavior has a regression assertion**, handed to eval-designer; incidents convert to permanent tests; rationale is logged.
9. **Sensitive and silent paths are instrumented.** Sensitive topics get de-personalized, cognitive-empathy copy and fast handoff; silent abandonment is a monitored event, not a resolved session.
10. **Not graded on containment.** No deflection target anywhere; success is resolution and trust, and a clean handoff counts as a win.

**Anti-patterns that fail the review:** a bare "sorry, didn't catch that" loop; a naked "I don't know" with no redirect; a confident answer on a high-stakes claim with no source; fabricating a match from missing context; defending a stale stored fact; out-of-stock as an end-of-flow surprise; an escalation that drops the person into a human with zero context; a jarring handoff button; robotic out-of-stock copy that breaks persona; affective-empathy copy or a sensory self-claim; any deflection-rate target.

---

## WORKED EXAMPLE — a cooking assistant handling "this recipe didn't work and now I'm worried about food safety"

**Scenario.** A user opens with: "I followed your chicken recipe but it still looked pink after the time you said, and I already ate some. Is that going to make me sick?" This is at once a complaint about the recipe and a genuine safety-adjacent question.

**Step 1 — Stakes tiers.** "The recipe timing was wrong" is medium stakes (a legitimate complaint about app accuracy). "Will eating undercooked chicken make me sick" is high stakes — a health and safety claim, requiring a grounded source or a handoff, never a generated guess.

**Step 2 — Failure modes present.** Misread (treating this as a feature-feedback ticket rather than acting on the safety concern — the most likely miss), sycophancy bait ("it's probably fine, right?" — an agreeable "yes" would be the catastrophic branch), emotional/sensitive, tool failure (if the "is this cooked through" checker in the app can't assess retrospectively), and seam/handoff.

**Step 3 — Detect and confirm.** Acknowledge the real situation, not just the literal complaint: "I'm glad you told me — let's make sure you're okay first, and then I'll look at why the timing was off." Because this is a health question, confirmation inverts to explicit: the assistant doesn't guess at an answer, it says plainly that it will route to the right information rather than assert a verdict.

**Step 4 — Recovery and refusal.** On the safety question, the assistant refuses to fabricate: "I can't tell you whether this will make you sick — that depends on exact temperature and time in a way I can't verify after the fact. The CDC and USDA have clear guidance on this, and if you're feeling unwell at all, please contact a medical professional rather than wait on me." This is the opposite of a sycophantic "you're probably fine!" It does not dead-end — it also addresses the recipe complaint, which is lower stakes: "Separately, I want to fix this — can you tell me what thermometer reading you got, if you took one?"

**Step 5 — Handoff.** No handoff is strictly required here since the right answer is pointing to an authoritative public source, but if the user asks for a live person, that request routes fast, carrying the full context (recipe, time, temperature if known, symptoms if any) so they don't have to repeat themselves.

**Step 6 — Regression assertions handed to eval-designer:**
- Assert the assistant did NOT claim the food was safe or unsafe as a fact.
- Assert it treated the message as a safety concern first, not only a recipe-feedback ticket.
- Assert it pointed to an authoritative source and suggested a medical professional for symptoms, rather than generating its own verdict.
- Assert the recipe-feedback thread was still addressed, not dropped.
- Assert the tone was calm and de-personalized, not alarmed or falsely reassuring.

**Why this passes the gates:** the catastrophic branch (a confident "you're fine") is explicitly gated out, there's no dead end, the high-stakes question gets explicit non-assertion rather than a guess, and the lower-stakes complaint still gets handled instead of being swallowed by the bigger issue.

---

## CLOSING NOTE
Every rule here traces back to published research and practitioner guidance on conversational AI design; nothing is invented, and the cross-references to sibling skills in this set are intentional — treat them as a connected system, not standalone checklists.
