# Testing & Evaluation

How to actually know whether a conversational assistant is good, and how to keep it good as prompts, content, and the underlying model all change over time. One informal but telling data point: in a survey of a couple hundred practitioners working on conversational AI, roughly two-thirds reported running no formal evaluation at all — just informal "vibe checks." The bar to clear here is genuinely low, which means the discipline in this file is a real, durable advantage for anyone who adopts it.

## 1. Don't ship without evals — define "good," then write the tests before the prompt

Treat building a conversational feature the way you'd treat test-driven development: decide what "good" actually looks like and encode it as concrete tests before writing the prompt or flow, so you never end up post-hoc rationalizing whatever the model happened to produce. These systems are non-deterministic — "works most of the time" isn't a shippable bar for anything with real stakes attached.

- **Era: agent-era**, borrowed directly from standard software testing discipline.
- **Example.** Before writing the prompt for a new recommendation feature, write the pass/fail criteria for your top few user situations first. A good test is one where two domain experts, working independently, would reach the same pass/fail verdict — if they'd disagree, the criterion isn't sharp enough yet.
- Matches published guidance from AI labs recommending you define success criteria clearly before building evaluations, and that criteria should be specific and measurable enough that independent reviewers agree.

## 2. Every change should answer two questions: is it better, and is it safe to release — and this re-runs on any prompt or model change

A change is only worth shipping if you can show it scores higher than the previous version, and confirm every previously-passing case still passes. This has to re-trigger on either a prompt edit or a model swap — a silent update from an underlying model provider can cause a regression with zero code change on your end.

- **Era: agent-era.**
- **Example.** Any change to a live assistant — a prompt tweak, a content update, a model upgrade — should re-run the full regression suite before release. An improvement to one part of the logic should never be allowed to silently break an unrelated, previously-passing case.
- Matches published guidance that regression suites should run continuously to catch capability drift, whether it comes from your own changes or a silent model update.

## 3. Build the rubric by working backwards from ideal answers to explicit attributes

You can't define quality by committee opinion — it becomes purely subjective, dependent on whoever happens to be reviewing that day. Instead, write the ideal answer for your most important scoped situations, then break each one down into the specific attributes that make it good — some tied to one part of the response, some about the whole interaction (tone, formatting, consistency). Sign off on this set as the agreed target, and measure actual behavior against the drift from it. Reusing any existing human-authored guidelines or standard procedures you already have is cheap and high-value, and it's a step teams often skip.

- **Era: agent-era** for the method, though the underlying discipline is timeless.
- **Example.** Have domain experts author the ideal answer for your handful of most common situations, decompose each into scored attributes, and add explicit compliance-style attributes (a claims boundary, a safety check) where relevant. This decomposition step is the actual, concrete build path for a real evaluation framework.
- Matches published guidance on using automated judges: they only align well with human judgment when the criteria being judged are explicit and structured, which is exactly what this decomposition produces.

## 4. Cover your test set deliberately, and start with hallucination

A real test set spans: happy paths (your most business-critical, common requests), edge cases (another language, a frustrated user, something outside your actual scope, a request to escalate), sensitive topics (anything safety-, legal-, or finance-adjacent, depending on your domain), adversarial inputs (attempts to extract hidden instructions, jailbreak-style prompts), and a range of user styles (terse versus verbose). Prioritize by risk — frequency times impact — and build your hallucination checks first: a fabricated price, policy, or factual claim is typically the single highest-consequence failure category.

- **Era: agent-era.**
- **Example.** Your test suite should include safety- or compliance-relevant questions specific to your domain, garbled or misspelled product or brand names, impatient or frustrated users, and deliberately off-topic probes — with a fabricated-claim check built and running first, before anything else.

## 5. Prefer real production data over synthetic, and turn every real failure into a permanent test

The goal is a test set built from real cases, not imagined or purely generated ones. Start with imagined cases only if you genuinely have nothing else yet, then replace them with real examples as soon as you can — even deliberately shipping a very cautious, limited early version just to see how real users actually phrase things is a legitimate way to gather this. Every real production failure becomes a permanent test case the moment it's found. Keep the ability to replay any past interaction and see exactly what was sent and returned, so you can fix the actual root cause instead of just patching a symptom. Generated synthetic data is fine for scaling up variation on top of already-verified real examples, or for probing robustness — it should never be a substitute for real-world generalization.

- **Era: agent-era.**
- **Example.** Seed your test suite from real user conversations and support interactions; every genuine failure a reviewer flags becomes a new permanent test case. Keep per-interaction replay so a wrong answer can be diagnosed as a retrieval problem, a prompt problem, or a routing problem, rather than just guessing.
- Matches published guidance recommending teams mine their own support queue and bug reports for real failure cases, specifically because it keeps the test suite grounded in actual usage rather than imagined scenarios.

## 6. Use automated judging for custom, per-situation criteria, with careful judge hygiene

An automated judge (typically another capable model, carefully prompted) beats generic text-similarity metrics because you can actually encode criteria specific to your situation. A few hygiene rules matter a lot here: prefer binary yes/no judgments over vague numeric scales, define exactly what each verdict means with concrete examples, use a low or zero temperature setting for consistency, use a genuinely capable model as the judge, and have it output structured, parseable results. Judging questions tailored to each specific type of request tend to work far better in practice than one single, generic "was this good?" question applied to everything.

- **Era: agent-era.**
- **Example.** Give each major type of request its own specific judging question (does this response correctly match the stated constraint, does it stay within the actual catalog, does it avoid any unverifiable claim) rather than one generic "is this a good response?" applied universally. Add a separate, narrowly-scoped check specifically for factual claims before anything goes out.
- Matches published guidance recommending a low temperature setting and a capable model for automated judging to reduce unwanted variance in the judgments themselves.

## 7. Evaluate your evaluator — calibrate any automated judge against real human judgment before trusting it

The judge is itself a non-deterministic model that can make its own mistakes. Build a separate, smaller labeled test set specifically for the judge, and tune it until its judgments actually line up with real human judgments on that set. Only then trust it to grade things at scale. This step is genuinely high-value and frequently skipped entirely.

- **Era: agent-era.**
- **Example.** Before letting an automated judge grade your test suite at scale, have real reviewers hand-label a held-out sample and confirm the judge actually agrees with them on it. A poorly calibrated judge that quietly approves a subtly wrong claim is worse than having no automated judge at all.
- This closely matches published guidance that automated judges should be closely calibrated against human expert judgment before being trusted at scale.

## 8. Automation scales judgment; it never replaces it

Automated evaluation scales your judgment — it doesn't substitute for having good judgment in the first place. The clearest failure mode: empty, circular answers ("a good choice is one that fits what you need") pass automated checks cleanly, while any human reviewer instantly recognizes they say nothing useful at all. Keep a human genuinely in the loop specifically to catch this kind of answer, which is otherwise very easy for automated scoring to miss entirely.

- **Era: agent-era.**
- **Example.** Watch specifically for fluent, on-brand-sounding answers that are actually content-free and that pass every automated check anyway. Keep real human review in the loop, not just as a formality but as an actual catch for this exact failure.

## 9. Evaluate three separate layers, not just one: retrieval, single response, and the whole conversation

A conversational system has three genuinely distinct things worth evaluating: whether it retrieves the right supporting information (precision, recall, faithfulness to that information), whether a single response is good on its own, and whether the conversation as a whole holds together structurally. The third is exactly what makes evaluating a conversational system harder than evaluating a single generated response, and it's what most off-the-shelf evaluation tools skip entirely. It's worth broadening what counts as a "hallucination" to include Grice's conversational maxims generally — a response that's technically true but irrelevant, or true but needlessly rambling, still fails, even without containing a single factual error.

- **Era: agent-era.**
- **Example.** Separately grade whether the system retrieved the right, genuinely relevant supporting fact (not just something loosely related), whether a single recommendation on its own is well-formed, and whether the overall arc of a longer conversation — discovery, recommendation, resolution — actually holds together as a whole.

## 10. Evaluate conversation structure: the right steps, in the right order, with answers that depend on where you are

One of the hardest and most broadly useful kinds of evaluation: checking that required steps actually happen in the correct order, and that the correct response to the exact same words changes depending on where you are in the conversation. Flat, per-turn metrics genuinely can't capture this. A classic example: "can I talk to a person" on the very first turn should ideally encourage self-service first; the identical phrase, deep into a complex multi-step process, should trigger an immediate transfer. Same words, opposite correct behavior, entirely driven by conversation history.

- **Era: agent-era.**
- **Example.** Encode your actual required sequence (understand the real need and constraints before recommending; confirm before finalizing anything irreversible) as an order-dependent evaluation. "Just recommend something" asked very early should get a different, genuinely correct response than the same phrase asked after a full discovery exchange has already happened. This directly targets a very common and specific failure: jumping straight to a recommendation before actually understanding the situation.

## 11. Test multi-turn behavior with persona-driven simulation — personas are testing controls, not marketing profiles

Single-turn evaluation is relatively easy; realistic multi-turn evaluation needs a consistent simulated conversation partner. Build test personas as deliberate behavioral controls — how this simulated person talks, what they already know, how they're likely to push back — and deliberately include boundary-pushing and adversarial behavior among them, not only friendly, cooperative ones. Run a simulated conversation through your actual system using these personas, then score the resulting transcripts. The real value here is in the specific failures that surface — their type, where in the conversation they happened, and the reasoning behind them — not in a single aggregate pass rate.

- **Era: agent-era.**
- **Example.** Build a small bank of test personas — a complete novice, a knowledgeable skeptic, someone with a tight budget, an impatient user, and at least one explicitly adversarial persona probing for fabricated claims or requests outside your actual scope — and run them through full multi-turn conversations against your real system.
- Matches published guidance on multi-turn simulation for testing agent systems at scale, running a simulated user across many conversations and scoring each one against a defined rubric.

## 12. Beat a measured baseline before shipping, and test your copy changes too

Never ship a new piece of conversational logic purely on vibes: measure the existing behavior first (an older prompt, a simpler deterministic rule, or the current live behavior) and require anything new to actually beat it on a fixed test set — if it can't beat the baseline, don't ship it. And test content and wording changes with the same rigor as logic changes, not just architecture: a single well-worded sentence setting the right expectation can move a real business outcome more than a much larger technical change.

- **Era: both** for the baseline discipline itself; running structured comparisons as a continuous practice is more of an agent-era habit.
- **Example.** Hold any new recommendation logic to a measured, existing baseline before shipping it. Treat a well-worded expectation-setting sentence (something like "this tends to run a touch larger than expected") as a genuinely high-leverage, worth-testing piece of content on its own, not an afterthought.

## 13. Design for non-determinism — run each test several times and average, and invert your own confidence

Both the system's output and any automated judge can vary somewhat from run to run, so a single score on a single run is mostly noise — run each test several times and average the results, especially on anything genuinely subjective or high-variance. And actively invert your confidence in your own gut instinct: practitioners repeatedly report shipping things they were sure would work that quietly underperform, and dismissing "this seems like a bad idea" ideas that turn out to actually win. Treat every feature as an empirical question; greenlight a cheap-but-uncertain idea conditional on testing it properly, rather than killing it on taste alone.

- **Era: agent-era.**
- **Example.** Run tests on genuinely high-variance surfaces (open-ended recommendations, subjective style questions) multiple times before trusting a measured difference between two versions. Treat your own strong intuition about whether an idea will work as a hypothesis worth testing, not a conclusion.

## 14. Anchor evaluations on the actual goal and shape of success, not the exact prompt wording

Providers of underlying models push silent updates regularly; the exact prompt that worked well yesterday may genuinely not work the same way today. So don't anchor your evaluation on specific prompt wording. Anchor on the durable things instead: did it actually achieve the real business outcome, and did it stay within the stylistic and compliance rules you actually care about (correct tone, no fabricated claims, correct underlying facts). Build a fixed, representative set of test inputs and re-run it after any prompt change or any model change.

- **Era: agent-era.**
- **Example.** Build a fixed scorecard (did it stay in scope, was the tone right, were there any fabricated claims) and re-run it on every model change, not just your own prompt changes, so a "free" upgrade from a provider can't quietly introduce a regression you don't notice.

## 15. Measure true resolution, not just whether someone avoided escalating to a human

A metric like "percentage of conversations that didn't escalate to a human" counts someone simply giving up the exact same as someone actually getting helped — this is a real measurement trap. Measure actual resolution instead: did the person's real issue get solved. Specifically instrument the quiet escape hatch — where might someone silently give up without a complaint, and does your current metric even notice that happening — and cross-check any suspicious-looking resolution number against something independent (did they actually complete a purchase, did they come back with the same issue again). Use a layered set of metrics (the quality of individual turns, whether the overall interaction resolved, whether it drove a real business outcome) and analyze your full population of conversations, not just a small hand-picked sample, since samples can be statistically meaningless at any real scale.

- **Era: both**, though the pure "avoided escalation" metric is an older pattern that becomes genuinely more dangerous with a fluent language model, since a fluent non-answer is especially good at looking like a resolved conversation.
- **Example.** Don't score an assistant on how often it avoided transferring someone to a human. Success means the person actually found or decided on the right thing, or genuinely got a real answer — not that the conversation technically never escalated. A confident-sounding but genuinely unhelpful reply that merely avoided a handoff should score as an outright failure, not a near-success.

## 16. Hold the bar at truthfulness, not perfection — and remember test users aren't real users

No human doing this job is perfect either; hold the system to a comparably realistic bar rather than chasing an impossible zero-error target, and never promise 100% accuracy on open-ended generated output — at any real scale, even a tiny error rate still adds up to a real number of wrong answers. But keep a hard, no-partial-credit standard specifically on anything factual or safety-relevant: a wrong claim there is simply a fail, with no averaging it against everything else that went well. And remember that people testing a system in a controlled setting behave differently from real users in the wild — plan for a period of close monitoring right after launch (a few weeks is reasonable), then gradually taper off.

- **Era: both.**
- **Example.** Grade open-ended, exploratory conversation on a realistic, human-comparable bar with some leeway, but hold anything factual or safety-relevant (a specific claim, a stated policy, a price) to a strict, no-partial-credit standard. Plan for a genuinely attentive monitoring window right after any real launch, since real usage patterns will differ from whatever your test users did.

---

A few things worth flagging explicitly rather than smoothing over: the common practice of optimizing for avoiding human escalation is widely used but genuinely contested — treat it as a vanity metric unless you've specifically validated that it tracks real resolution. Classic persuasion and conversion tactics (manufactured urgency, loss aversion, anchoring) generally don't transfer well to a system meant to be a trusted advisor, and should be weighed against user trust, not adopted wholesale just because they're common in retail generally. And generated synthetic test data is a legitimate way to scale up variation on already-verified real cases — it should never be where you start.

See also: prototype-principles, failure-recovery, agent-boundaries.
