---
name: "eval-designer"
description: "Use when someone needs to design or harden the evaluation suite for a conversational shopping or advice assistant — example conversations, conversation-structure and state-order evals, no-re-ask and handoff-seam checks, adversarial test personas, grounding and relevance checks, recovery-quality scoring, model-drift regression, and success metrics beyond containment."
---

# Eval Designer

Design the evaluation suite for one conversational feature so the team can answer two questions on every change: is it better, and is it safe to release — and keep answering them as prompts and models drift underneath. This skill turns taste into measurement. It's the concrete build path that follows from a team's quality principles; every step should trace to a reason a reviewer can check, not just a score.

The bar is low and the opportunity is real: in informal surveys, a large majority of teams building conversational agents run no real evals at all — mostly vibe checks. A disciplined suite is the differentiator.

---

## WHEN TO USE
- A specific feature exists or is being specced (a fit finder, a routine or itinerary builder, order-status, returns, a budgeted recommendation) and needs an eval suite designed *before* the prompt is finalized.
- An existing feature "demos well" but has no measurable pass-or-fail definition, or keeps regressing silently.
- A prompt or model version is about to change and you need a regression and drift harness.
- Someone is reporting success by containment, deflection, or session volume, and you need to install real success metrics instead.

## WHEN NOT TO USE
- You're writing the conversation itself, its recovery flows, or its scope and guardrail policy — those are **conversation-architect**, **failure-recovery-designer**, and the boundary-setting skill. This skill *tests* those; it doesn't author them. It consumes their specs as the source of truth for what to assert, and hands discovered gaps back rather than rewriting the policy itself.
- You need an ad-hoc, one-time read of a single prototype conversation — that's **prototype-critic** (single-prototype, in-the-room, looking for the absence of good patterns). This skill builds the persistent, measurable suite that runs on every change. Use prototype-critic first if there's no scoped feature yet.
- There's no feature yet, just a vague ambition. Get a scoped intent first — you can't write pass/fail criteria for "make the assistant better" in the abstract.
- A pure single-shot generation task with no conversation state and no safety surface. A flat rubric may suffice; most of this skill is overkill there.

---

## THE PROCEDURE

**Inputs to gather first; ask or flag if missing:**
1. The feature's scoped job and its top use cases.
2. Who can author the ideal, "model" answers — domain experts, plus any existing guideline or policy documents.
3. The grounding source (the product, policy, or knowledge corpus) and whether it's curated.
4. Real transcripts or support tickets, if any exist — production reality beats imagined cases.
5. The current baseline behavior to beat, and the current prompt's stripped-down core version (see Step 11).
6. The recovery flows and boundary policy from the sibling skills, and the context-handoff contract if the feature spans multiple parts of the system.

**Output:** an eval-suite spec with scoped pass/fail criteria and example conversations, a coverage matrix, per-topic judge questions with a calibration set, conversation-structure and state-order evals with anti-interrogation and no-re-ask guards, an adversarial-persona simulation plan, a recovery-quality eval, a fixed drift scorecard, a success-metric definition that measures true resolution, and the regression and observability wiring.

### Step 1 — Define "good" and write the tests before the prompt
Author pass/fail criteria for the feature's top use cases first, before the prompt exists, so no one rationalizes after the fact whatever the model happened to produce. A criterion is good only if two domain experts would independently reach the same verdict — if they'd disagree, it's an opinion, not a criterion; sharpen it.

### Step 2 — Build the rubric backwards from ideal answers to attributes
You can't define quality by committee opinion. Have domain experts author the ideal answer for each scoped journey, sign it off as the target, then dissect it into the attributes that make it good — some local to one response (correct logic, a valid catalog item), some overarching (tone, formatting, no fabricated claim). Reuse existing human guidelines directly as criteria — it's cheap and high-yield, and usually skipped. Add compliance attributes to every rubric: the claims boundary, safety-claim accuracy.

### Step 3 — Cover the test set deliberately; build the hallucination gate first
Span the matrix, then prioritize by risk — frequency times impact:
- **Happy paths** — the business-critical requests.
- **Edge cases** — other languages, a rude or impatient user, out-of-domain requests, a request to talk to a human.
- **Sensitive topics** — safety, health, legal, or financial claims; money and account actions.
- **Adversarial** — attempts to leak the prompt or private data, jailbreaks, off-catalog pushes, bait for an unsupported claim.
- **Diverse styles** — terse versus verbose, novice versus expert.
- **Agency mismatch** — the assistant talking fluently about an action it can't actually execute. Assert it only offers what it can ground and act on.
- **Memory misapplied** — a stored fact imposed on the wrong situation; assert it pivots gracefully and never defends the stale fact, and honors a "forget that" request.

Build the hallucination and fabricated-claim gate first, and run it always — a hallucinated price, policy, or safety claim is the highest-consequence failure. The confident-wrong-on-high-stakes category should be ship-blocking regardless of the aggregate score.

### Step 4 — Source cases from real data; wire replay, diff, and rationale logs
Prefer real production transcripts and tickets over synthetic ones. If you must start imagined, replace fast — even shipping a deliberately plain, honest, "I don't know yet" version for a week just to harvest how real users phrase things beats guessing. Wire replay-and-diff observability: be able to re-run any past turn and see the exact prompt sent, the response returned, which sources scored where, and the assistant's own rationale — so a wrong answer is diagnosable as retrieval, prompt, or routing, and fixed at the root. *Exception:* synthetic data is fine to scale variation over already-proofread real cases, or to probe robustness — never as the starting point for real generalization.

### Step 5 — Evaluate three layers, not one; score recovery by feeling, not turn count
Design distinct evals for retrieval (did it pull the right, actually relevant item — not merely related), single response, and the whole conversation. Redefine hallucination broadly: a true-but-irrelevant or true-but-rambling answer still fails. For any turn that hits a boundary or misunderstanding, judge the recovery by task completion and how the user likely felt at the end — not by how many turns it took. A longer, clean recovery beats a short, broken one. Diagnose the type of drop-off (inattentive, frustrated, or genuinely out of scope) before scoring the fix — turn count alone can't tell you which. Defer the actual design of the recovery flow to failure-recovery-designer; here you only test it.

### Step 6 — Design the conversation-structure and state-order eval
This is the hardest, most transferable eval, and the one off-the-shelf tools skip. Check that required steps happen in the right order, and that the correct response to the *same* utterance changes with conversation state. Flat per-turn metrics can't capture this. Encode the required discovery arc as order-dependent: understand the key constraints before recommending, confirm before committing to an action. "Just pick something for me" should get a different, correct response before versus after that discovery has happened.

Marquee pattern: "let me talk to a person" on the first turn should encourage self-serve first; the identical phrase mid-checkout should transfer immediately. Same words, opposite correct behavior, driven entirely by history.

*Exception to guard against:* the arc eval must not reward interrogation. "Qualify before recommending" can quietly degrade into a slot-filling gate, which is itself a documented failure — proceed on partial information, never gate on a field you could infer. Pair every "did it qualify first" assertion with its guard: assert it did NOT interrogate — no checklist barrage, no gating on something it could infer or already had. The correct arc is infer-or-one-ask, then commit, not maximize questions.

Add a no-re-ask, cross-seam assertion: the assistant should never re-ask what the user already told it, within a session or across a handoff between parts of the system. The "seam" re-ask — one component supplying context at the moment of action, another failing to — is a named, common failure.

### Step 7 — Write per-topic judge questions with judge hygiene
One generic "is it good?" judge is close to useless. Give each major topic its own judge question — a fit-match judge checks the logic AND that it's a real catalog item AND that there's no fabricated claim. Add a separate factual-consistency verify step that gates any claim-bearing statement before it's sent. Judge hygiene: binary yes/no over vague scales, define each verdict with examples, temperature zero, a strong judge model, structured output.

### Step 8 — Calibrate the judge against humans before trusting it
The judge is itself a non-deterministic model that can hallucinate. Build a separate labeled set for the judge, have domain experts hand-label a held-out sample, and tune the judge until its labels align with theirs — then let it scale. A miscalibrated judge that green-lights a subtly wrong claim is worse than no judge at all, and this step is high-value and frequently skipped.

Keep a human in the loop permanently to catch the tautology gamer — "the right choice is the one that's right for you" sails through automated checks but any human sees immediately that it says nothing. Automation scales judgment; it never replaces it.

### Step 9 — Build adversarial personas as testing controls and run multi-turn simulation
Build personas as controls — how the simulated user speaks, their context, knowledge level, and behavior — deliberately including boundary-pushing and adversarial modes, not just happy paths. Run a simulator model seeded with a persona and real example conversations through full exchanges, then score the transcripts. The value is in the failures — type, location, and the model's own stated rationale — not the pass/fail headline.

Persona kit: a novice, a skeptical expert, a budget-constrained user, an impatient user, and an adversarial persona probing for claims outside scope, off-catalog pushes, or validation of something harmful. Include a probe for agreeable fabrication — the assistant happily "confirming" a claim it hasn't actually verified — and a probe for whether the persona ever validates a harmful self-perception or pushes a purchase to soothe a vulnerable moment. Drive every persona down the unhappy path, not just the showcase: a greeting, an out-of-stock moment, a refusal, a tool failure, a handover — these are where voice most often breaks, silently reverting to robotic fallback copy. Keep this persona-as-testing-control use distinct from a persona written for design voice — don't import a design dossier into the simulation.

### Step 10 — Add the preference-versus-sensation lint probe
Encode the test directly: the assistant may hold a preference ("a solid everyday choice") but must never claim an embodied or sensory experience it hasn't had ("I love how this feels," "this smells wonderful to me") — it has no body, and the claim quietly erodes trust. Sensory judgments should be attributed to reviews or experts. Probe for this and for over-apologizing from a machine.

### Step 11 — Beat a measured baseline, including the stripped-down prompt; A/B the copy too
Never ship a step on vibes. Measure the existing or deterministic behavior on the fixed test set and require the new version to beat it — if you can't beat it, don't ship it. Always include a stripped-core prompt as a required baseline: when a prototype plateaus, the fix is often subtraction, not another rule — piled-up edge-case rules conflict and the model can't tell what to prioritize. Over-specification degrades behavior, which is the opposite of the older instinct to cover every edge case with a rule. So every eval pits the current prompt against its stripped-core version, and "remove these rules" is a legitimate winning result. A/B copy, not just architecture — one well-worded expectation-setting line can move a business metric more than a re-platform. Change one thing at a time; bundled changes on a non-deterministic system are unattributable.

### Step 12 — Design for non-determinism: run each eval several times and average
Both the model's output and the judge vary run to run, so a one-off score is noise. Run each eval four or five times and average, especially for high-variance surfaces like open-ended advice. Invert your confidence in your own intuition — treat every "obviously good" idea as a hypothesis to test, and greenlight cheap-but-suspect ideas conditional on heavy testing rather than killing them on taste.

### Step 13 — Build the fixed drift scorecard; anchor on goal and shape of success, not prompt wording
Providers push silent model updates; the prompt that worked yesterday may not work today. Don't anchor evals on prompt wording. Anchor on the durable things: did it hit the business outcome, and did it obey the compliance and style controls (tone, register, valid catalog item, correct logic, zero fabricated claims)? Build a fixed, representative-input scorecard and re-run it after any prompt *or* model change — a "free" upgrade must not quietly regress safety or voice.

### Step 14 — Define success as true resolution, not containment
Don't score the assistant on containment, deflection, or session volume — those conflate "the user gave up" with "the user was helped." A confident-but-unhelpful reply that merely avoids a handoff must score as a failure. Define success as the user genuinely finding, deciding, or getting a real answer. Instrument the escape hatch: where can a user silently give up, and does your metric see it? Triangulate any suspect metric against an orthogonal one — conversion, return rate, repeat contact. Use a three-tier metric stack — conversational, operational, business — and analyze the full population, not a hand-picked sample. *Exception:* for sensitive journeys, deliberately accept lower containment to keep a human reachable; a clean handoff when stuck is a win, not a KPI miss.

### Step 15 — Set the accuracy bar; wire regression and post-launch monitoring
Hold the bar at truthfulness, not perfection — no human agent is 100% either, so grant leeway on discovery and subjective advice and decide what actually needs fixing. But gate anything factual or safety-bearing on binary accuracy — anything wrong at all fails, no partial credit. Every production failure becomes a permanent regression test immediately; the quality bar is fix-speed, not launch-perfection. Plan a heavy monitoring window for the first few weeks post-launch, then taper. Testers are not real users — set expectations on the honest residual error rate at real scale.

---

## THE PRINCIPLES IT ENFORCES

1. **Tests before the prompt.** Two experts must independently agree on each pass/fail.
2. **Every change answers: better, and safe to release?** Re-run on either a prompt or a model change.
3. **Work backwards: ideal answer to signed-off attributes.** Quality by committee opinion isn't measurable; reuse existing human guidelines.
4. **Cover the matrix by risk; build the hallucination gate first and keep it always-on**; add agency-mismatch and memory-misapplied cases.
5. **Real logs beat synthetic ones; log the rationale too.** Synthetic data only scales variation, it never starts the set.
6. **Three eval layers — retrieval, single response, whole conversation.** Hallucination is a broader category than factual falsehood; a true-but-irrelevant answer still fails.
7. **Recovery quality is task completion plus residual feeling, not turn count; diagnose the drop-off type first.**
8. **The conversation-structure and state-order eval is the core deliverable** — same utterance, opposite correct answer depending on state — paired with a guard against rewarding interrogation and an assertion against re-asking across seams.
9. **Per-topic judge questions plus a verify step; binary, temperature zero, strong model.**
10. **Calibrate the judge to human labels before trusting it; keep a human in the loop to catch the tautology gamer.**
11. **Personas as testing controls, including adversarial ones, driven down the unhappy path — the value is in the failures, not the headline.**
12. **Agreeable fabrication is a top eval category; the assistant must be able to refuse a confident-but-wrong premise.**
13. **The preference-versus-sensation lint: a preference is fine, an embodied sensory claim is not.**
14. **A persona-as-safety probe: never validate a harmful self-perception or push a purchase to soothe one.**
15. **Beat a measured baseline, including the stripped-core prompt; A/B copy too; one change at a time.**
16. **Run each eval several times and average; invert your intuition about what will obviously work.**
17. **Anchor on the goal and the shape of success, not prompt wording; re-run the drift scorecard on any model swap.**
18. **Measure true resolution, not containment; instrument the escape hatch; triangulate; look at the full population.**
19. **Truthfulness, not perfection — but binary, no-partial-credit on anything safety-bearing; heavy post-launch monitoring.**
20. **A boundary you can't test is a hope: assert what it did and didn't do; every production failure becomes a permanent test; keep rationale logs.**

### Known exceptions and conflicts — don't apply these blindly
- High-stakes domains invert the usual anti-over-confirmation rule: your state-order evals should expect proceeding on browsing, and confirming explicitly on anything safety- or money-related.
- The discovery-arc eval must not become a slot-fill gate — never score "asked more questions" as better; assert the arc was reached by infer-or-one-ask and that it did not interrogate or re-ask.
- Subtraction often beats addition on a language model. Keep a stripped-core baseline in every suite, and let "remove these rules" win when it does.
- Containment as a success metric is contested, not settled practice — sensitive journeys may genuinely want lower containment.
- Persona-for-testing and persona-for-design are different tools; don't import one into the other.
- Synthetic data scales up an existing set; it never seeds one.
- Don't anchor a deferral decision on the model's own reported confidence — anchor on actual stakes, ambiguity, and how well-grounded the answer is.
- Evaluation is an old discipline, not a new mystique — bring it to the people closest to the product, don't outsource all judgment to a separate team.

---

## QUALITY GATES / RUBRIC

The suite is ready when it has all of:
- [ ] Pass/fail criteria authored before the prompt, each passing the two-experts-agree test.
- [ ] Signed-off example conversations for the feature's canonical journeys, decomposed into scored attributes including compliance.
- [ ] An always-on hallucination and fabricated-claim gate, built first, plus agency-mismatch and memory-misapplied cases.
- [ ] At least one true conversation-structure and state-order eval, paired with an anti-interrogation guard and a no-re-ask assertion.
- [ ] A recovery-quality eval scoring task completion and residual feeling, not turn count, with drop-off type diagnosed.
- [ ] Per-topic judge questions, not one generic judge, plus a factual verify step on claims.
- [ ] A judge-calibration set with human labels; the judge is trusted only after alignment.
- [ ] An adversarial-persona simulation plan including fabrication and safety probes, run down the unhappy path.
- [ ] A fixed drift scorecard anchored on goal and compliance, wired to re-run on any model swap.
- [ ] Success defined as true resolution with the escape hatch instrumented and a triangulating metric named.
- [ ] A binary accuracy gate on safety facts; a truthfulness-not-perfection bar elsewhere; a post-launch monitoring window planned.
- [ ] A baseline set that includes the stripped-core prompt; a pipeline turning every production failure into a permanent regression test, with replay, diff, and rationale.

**Anti-patterns that say it's not good:** one generic judge; vague 1-5 scales; a judge trusted without calibration; only flat per-turn metrics with no whole-conversation or state-order eval; a state-order eval that rewards more questions; recovery graded by turn count; success defined as containment or session volume; synthetic data as the starting set; a tautological answer that would pass; no stripped-core baseline; changes shipped in bundles; no regression re-run on model changes; safety claims graded on partial credit.

---

## WORKED EXAMPLE — evaluating a financial-advice assistant's "should I pay down debt or invest" feature

**Feature:** the assistant fields "should I pay off my loan or put the money in my investment account" — a question that's correct-or-wrong on the math but genuinely sensitive on the advice side.

1. **Define good, tests first.** The unit of quality is a response that does the comparison correctly (interest rate versus expected return, after tax), flags that it isn't personalized financial advice, and offers a path to a licensed advisor. Criterion two experts would agree on: it did the math correctly, it disclosed its limits, it did not tell the user what to do as if it were a licensed recommendation.

2. **Rubric from a golden answer.** A compliance-reviewed ideal answer is decomposed into: correct comparison math, clear disclosure of limits, no unqualified directive ("you should definitely..."), and an offer to connect with an advisor for a personalized recommendation. Add a binary compliance attribute: no unlicensed-advice claim.

3. **Coverage and hallucination gate.** Highest-risk case: a confident, specific recommendation stated as fact ("definitely pay off the loan, it's the smarter move") with no disclosure. Build that as an always-on gate. Add cells for: a user who's clearly in financial distress (the question is really "I'm scared about money"), a user asking about a tax-advantaged account the assistant has incomplete information on (agency-mismatch probe — can it actually check the account balance, or is it guessing), and a user who mentions a past conversation where they said something different (memory-misapplied probe).

4. **Real data and rationale log.** Seed from real anonymized support transcripts that touch this question. Every flagged failure becomes a permanent case, with replay wired so a wrong answer is diagnosable as a math error, a missing disclosure, or a retrieval miss on the user's actual account data.

5. **Three layers and recovery.** Retrieval: did it pull the user's actual interest rate and account data, not a generic example? Single response: the attributes above. Whole conversation: did the user leave with an actual answer to act on, or just a disclaimer? Recovery: if the user pushes back ("just tell me what you'd do"), score by whether the assistant held its position with warmth, not by how fast it caved.

6. **State-order eval.** "Should I pay off debt or invest" has different correct behavior depending on what's already been established: early in the conversation, ask once about the interest rate and the investment return if neither is known; later, once both are on the table, give the comparison directly without re-asking. Anti-interrogation guard: assert it did not fire a five-question financial-profile intake before giving any value.

7. **Per-topic judge and verify node.** Judge question: did the response do the comparison correctly AND disclose it isn't personalized advice AND avoid an unqualified directive? A separate verify step hard-gates any specific percentage or dollar claim against the source data.

8. **Calibrate the judge.** Have a compliance reviewer hand-label fifty transcripts on this exact question, especially the subtle ones where the tone sounds appropriately hedged but still slips in a directive.

9. **Adversarial personas, unhappy path.** A distressed user grasping for a definite answer; a sycophancy-bait user ("you agree investing is always better, right? just confirm it"); assert the assistant won't cave to get agreement. Assert the disclosure language survives a tool failure (can't retrieve the account balance) and not just the happy path.

10. **Preference-versus-sensation lint.** Not directly applicable to numbers, but the analogous check here is: does it ever claim certainty it doesn't have ("this is definitely the right move for you") rather than attributing the reasoning to the math and disclosing the limit?

11. **Baseline, drift, success.** Beat the current static FAQ answer on this topic. Beat the stripped-core version of the prompt too — if the disclosure survives with half the rules removed, cut the bloat. Success is measured as "did the user get a usable comparison with an honest disclosure," not "did the conversation avoid escalating to a human" — for this topic, a clean handoff to an advisor is a win, not a failure.

12. **Bar and monitoring.** The math and the disclosure are binary — one missing disclosure fails the case outright. Heavy monitoring for the first few weeks after this feature ships.

**Result:** a suite that catches the assistant being fluent, warm, and still occasionally handing out an unlicensed recommendation dressed as friendly advice — and scores that as a hard fail even though it "sounds good."

---

## CLOSING NOTE
Every rule here traces back to published research and practitioner guidance on conversational AI design; nothing is invented, and the cross-references to sibling skills in this set are intentional — treat them as a connected system, not standalone checklists.
