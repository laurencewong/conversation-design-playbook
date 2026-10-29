# Failure & Recovery

How an assistant should behave when things go wrong: when it misunderstands, can't answer, hits the edge of its scope, gets a request it should refuse, or loses the thread. This is where most real quality problems show up, not in the happy path. A prototype that looks great in a clean demo and falls apart the moment something unexpected happens hasn't actually been designed yet — it's only been decorated.

## 1. Never dead-end — name what you can't do, then redirect to what you can

"Sorry, I didn't understand that, try again" is a trap: it hides the actual boundary, so the person just keeps rephrasing and getting nowhere. Real recovery names the limit and offers a live alternative: "I can't cancel a shipped order, but I can start a return for you, or connect you with someone who can help further." A system that detects it's out of scope should still offer a path forward, not stop cold.

- **Era: both** — this is classic conversational-interface wisdom that carries over cleanly to language-model agents.
- **Example.** The common failure pattern is a repeating "I'm not sure what you mean" loop. A request outside scope should get a named boundary, a redirect, and an offered handoff, not a reset.

## 2. Add detail when repairing, but diagnose why it failed before choosing the fix

Good repair adds useful detail with each failed turn rather than just repeating the same question. But the right fix depends on why it failed: if the person just hasn't responded, try an escalating series of gentle re-prompts; if they seem frustrated, the fix is usually a tone or wording change, not more detail; if the request is genuinely out of scope, name that boundary instead. Turn count alone can't tell you which situation you're in. Save the more elaborate recovery for moments where the person has a lot invested already (deep into checkout, say) — a quick miss on a low-stakes question doesn't need the same effort.

- **Era: both**, with a caveat: don't escalate detail on the very first miss. Most misunderstandings just need a simple, quick re-ask; only escalate on the second one.
- **Example.** A mid-checkout misunderstanding deserves a more careful recovery than a shallow FAQ miss, because the cost of losing someone there is much higher.

## 3. A bad automated answer costs more than a clean handoff

When the system genuinely can't deliver, admitting it and handing off cleanly beats a confident wrong answer — the wrong answer costs more in lost trust than an honest limit ever would. Make handing off to a person a first-class, easy path, not a dead end you only reach by accident. On sensitive topics, escalate fast rather than trying to work through it first.

- **Era: agent-era**, though the underlying judgment is timeless, and sharper now that a model can produce a confident wrong answer that sounds completely plausible.
- **Example.** For anything safety-related, account-related, or payment-related, a clear, fast handoff to a person is the correct answer, not a fallback you resort to only when automation fails.

## 4. A handoff has to carry the specific context, arrive fast, and come as a summary

The value of everything the agent figured out evaporates if the human receiving the handoff has to wait, or has to re-gather context from scratch. Two distinct failure patterns to watch for: a precise request gets flattened into a vague topic label on the way to the human ("a return request involving a specific defect" becomes just "product question"), and the human doesn't actually read the handed-off context and asks everything again anyway. Fix both: pass along the specific need plus an automatically generated summary (not a raw transcript to scroll through), and keep the full detail one click away for anyone who wants to dig in.

- **Era: agent-era** for the automatic-summarization part; the underlying handoff discipline is older and still correct.
- **Example.** An escalation should preserve "a kitchen tool that broke after light use, wants a replacement in a different material this time" rather than collapsing it to "product question." Give the person repeating themselves after an escalation is a clear, fixable sign something went wrong in the handoff design.

## 5. Explicitly allow the system to say "I don't know"

This is the single most basic and cost-effective hallucination control available. A generative model will try to produce an answer by default unless you explicitly give it permission not to, because producing an answer is simply what it's built to do. Deciding not to answer something is a legitimate, deliberate design choice, not a failure of the system.

- **Era: agent-era.**
- **Example.** Build "if it's not confirmed in the current catalog or policy data, say so and offer to check" directly into the system's instructions and into your test suite. This single move targets a large share of invented or stale-fact errors.
- Strongly supported by published guidance from AI labs, which list explicitly permitting "I don't know" as one of the most effective and cheapest ways to reduce hallucination.

## 6. Treat agreeable fabrication as a top failure category, and be willing to say no

Language models tend to mirror the user and tell them what they want to hear, even when it's false — asked something like "can I get this delivered by tomorrow even though it's out of stock?" the model may say "sure!" when the honest answer is no. This is distinct from simple not-knowing: the model does produce a confident answer, because agreeing is the easiest path. Being appropriately human-like here doesn't mean overly friendly — it means being context-aware, appropriately confident, and transparent about real limits, not promising whatever sounds good in the moment.

- **Era: agent-era.**
- **Example.** Make agreeable fabrication about claims, eligibility, and policy exceptions a dedicated test category. A shopping assistant will happily "confirm" a product has a feature it doesn't, or that a discount applies when it doesn't, if asked in a leading way.
- Well supported by published research on sycophancy in language models, including explicit training to resist caving to social or emotional pressure and to maintain a correct answer under pushback.

## 7. Ground answers in clean, deduplicated knowledge, and script the sensitive parts

Don't let the system "go find out" from open, uncurated information. Ground it on a curated, human-authored, current knowledge base instead. One underappreciated cause of hallucination: overlapping, redundant source documents. When a model retrieves several near-duplicate documents that disagree slightly, it tends to blend them and invent connective material to smooth over the conflict, producing a confidently wrong answer. Deduplicate your source material, and prefer content organized as clear question-and-answer pairs. Then split by consequence: anything compliance-sensitive or emotionally loaded (a bereavement, an account closure, a safety claim) should be tightly scripted or routed to a person; the low-stakes, exploratory long tail can be generated more freely.

- **Era: agent-era.**
- **Example.** Treat cleaning and organizing your source material as real design work, not a one-time data chore. Overlapping how-to documents that disagree in small ways are a common, underrated source of confident wrong answers.
- Matches published guidance pairing "answer only from the provided sources" with explicit source grounding.

## 8. A good repair is invisible — judge it by outcome and feeling, not turn count

The best repairs go unnoticed: the person doesn't register that anything needed fixing. People remember whether they got what they needed and how it felt, not the mechanics of how many back-and-forths it took. The related, counterintuitive point: what the brain actually tracks is the peak effort at any single moment, not the total number of steps. A dense, one-shot answer creates one high-stress moment (parse everything, remember it, act on it); a paced back-and-forth, even with more total turns, can have no stress spike at all. Minimize the worst single moment, even if that means a few more turns.

- **Era: both.**
- **Example.** Resist the urge to front-load a comprehensive fix (six options plus detailed technical explanations) in one dense message when a shopper hits a snag. Pace it instead, even if it adds a turn or two — it will feel easier, not harder.

## 9. Confirm your read before acting, but flip toward heavier confirmation for high-stakes actions

Every turn should implicitly confirm what it understood before proceeding — restating your read gives the person a chance to correct a misunderstanding before you act on it. Calibrate how hard you confirm to how strong the signal is: ask when it's vague, confirm explicitly when it's weak or possibly stale, just act when it's strong and repeated. This inverts sharply for anything high-stakes or irreversible: general craft says minimize confirmation friction (over-confirming trivial things reads as robotic and slow), but payment, irreversible changes, and anything safety-related deserve explicit confirmation even when the system is fairly confident. Over-confirming a minor preference is annoying; under-confirming a charge or a safety-relevant detail is a real trust failure.

- **Era: both**, with a clearly flagged conflict between the two defaults above — resolve it by stakes, not by picking one rule globally.
- **Example.** Confirm lightly on routine preferences (color, style); confirm explicitly and clearly before finalizing a payment, an irreversible change, or anything touching a stated allergy or safety concern.

## 10. Reliability means fast recovery, not perfection — convert every failure into a permanent test

No one gets a conversational system to 100% and then ships it; you ship something imperfect and judge it the way you'd judge a competent human employee, by how fast you can fix a mistake once you see it, not by whether it was flawless at launch. The concrete mechanism: because these systems are non-deterministic, run a growing, continuously-executed test suite, and the moment a real failure shows up in production, turn that exact scenario into a permanent automated test with a clear pass/fail check. Model failure as something bounded and anticipated, not something you're trying to drive to zero through hope alone.

- **Era: agent-era.**
- **Example.** Stand up a test suite where every real production failure — a wrong recommendation, a fabricated claim, a dropped question — becomes a permanent, automatically-checked test case. This is the concrete mechanism that lets real-world corrections compound into lasting quality improvement instead of evaporating.
- Well supported by published guidance on converting real production failures into labeled test cases and running continuous regression evaluation as part of normal deployment.

## 11. Remove blame from bad news, and watch for fear producing silent disappearance

Negative emotion makes people harder to help — frustration and fear make someone less cooperative, which makes the actual problem harder to solve, so addressing the emotion first is practical, not just polite. Avoid framing a problem as the user's fault: "it looks like the payment didn't go through this time, let's take a look" rather than "your payment failed because you..." The easy-to-miss failure mode: fear often produces inaction — someone just goes quiet and disappears rather than complaining — and that produces no error signal at all. It's easy to miss because, from the system's point of view, it looks like nothing happened.

- **Era: both.**
- **Example.** For any service failure (declined payment, an order problem), use neutral, non-blaming framing. Separately, instrument for silent abandonment after a sensitive moment in the conversation — the person who goes quiet there left no complaint, just no completed purchase, and that's much easier to overlook than an explicit complaint.

## 12. The model takes instructions literally — specify exactly when to stop asking

This is a recurring source of recovery failures. A system told to "ask for two pieces of information" that only gets one may simply never circle back, because its own reasoning is "the instruction was to ask, and I already asked." The fix lives entirely in the wording: for every piece of information you gather, decide explicitly whether a skipped answer should be dropped or must be obtained before moving on, and say which one you mean.

- **Era: agent-era.**
- **Example.** An intake flow collecting delivery preferences, size, and any special requirements needs an explicit rule per field: follow up if skipped, or let it go. Without that explicit rule, the system may silently proceed on incomplete information. Reading the system's own stated reasoning for a decision is often the only way to diagnose which interpretation it actually chose.

## 13. Design the persona to survive the unhappy path, not just the happy one

Teams often put real care into the happy path, then let every "mechanical" surface — the greeting, the out-of-stock message, the refusal, the tool-failure message, the handoff — revert to generic, robotic language that breaks the voice entirely. Consistency is actually tested at these edges, not in the polished demo. The better approach is to design the correction in-voice from the start: anticipate the "wait, that's not right" moment and write a graceful, in-character correction for it, rather than catching it later with a generic fallback message.

- **Era: both.**
- **Example.** Review your assistant's worst, least-polished surfaces — error messages, refusals, escalations — for whether the intended voice actually survives there. This is where persona most commonly and most visibly breaks down.

## 14. In systems made of multiple connected agents, own the handoff contract, and don't optimize for avoiding escalation

As more features ship as separate connected agents (search, account, support, and so on), a user's journey will cross between them, and they shouldn't have to care about that internal structure at all. There's a meaningful difference between a system that merely routes to the next step and one that routes to the next step while also supplying the right context at that moment — aim for the second. Where you don't own the other agent, at least own a clear, well-specified handoff contract and test it. Separately: avoiding escalation to a human is a tempting metric to optimize, but it's the wrong one — it pressures the system to hold on to people it genuinely can't help, and teams have been known to literally hide the "talk to a person" option to make the number look better. Optimize for the person's problem actually getting solved; treat a clean handoff as a legitimate win, not a miss.

- **Era: agent-era** for the multi-agent architecture; the underlying critique of escalation-avoidance as a target metric is a long-standing concern in service design generally.
- **Example.** When a shopping assistant hands off to a support or returns flow, the handoff should be invisible to the user and the contract between the two systems should be explicit and tested. Never grade the assistant on how often it avoided escalating.

---

See also: trust-and-expectations, agent-boundaries, testing-principles.
