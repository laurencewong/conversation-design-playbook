# Agent Boundaries & Control

How to decide what an AI agent is allowed to do, and how to make that boundary hold. In the agent era you no longer write every line the system says, so you can't guarantee its behavior turn by turn. Control now comes from deciding what the agent may and may not do, making those limits legible, and shrinking the space in which it can surprise you. This file covers the main ways to do that.

## 1. Your job is to make the agent do less, not more

Before capable language models, most of the design effort went into expanding coverage: more intents, more training data, more cases handled. A capable model already generalizes, so the real risk flips to over-reach. The core design activity becomes narrowing scope on purpose, not adding it as an afterthought.

- **Era: agent-era.** This is close to the opposite of the old instinct.
- **Example.** A travel-booking assistant is asked to "handle anything travel-related." The right response isn't to build broader coverage; it's to decide explicitly what it will NOT do (negotiate refunds outside policy, give visa/legal advice, book anything outside a connected supplier) and to treat that list as the main deliverable, reviewed as hard for over-reach as for gaps.
- This is corroborated by published agent-design guidance (for example Anthropic's writing on building effective agents): find the simplest workflow that works, and only add autonomy when the flexibility is worth the added latency, cost, and compounding error.

## 2. Build small, single-job components, not one mega-agent

Break the system into small units, each with one job it does well, each independently measurable, composed into an end-to-end journey. Keep the overall workflow as the stable interface and treat the underlying model as a replaceable part behind it.

- **Era: agent-era**, and it transfers strongly.
- **Example.** A home-goods shopping assistant should be built as separate skills — product matching, order status, returns — each with its own scope and its own evaluation, sitting behind one orchestration layer. That way the model can be swapped or upgraded without re-testing the whole experience, and a failure in one skill has a contained blast radius.

## 3. The model takes your instructions literally — word choice is a control surface

A guided model executes an instruction exactly as worded. A classic failure: the agent is told to "ask the user for their name and order number"; the user gives only their name; the agent never circles back, because its own reasoning is "I was told to ask, and I already asked." Say explicitly whether you mean "ask once and move on" or "keep asking until you have it."

- **Era: agent-era.** The old mechanic of declaring and filling slots is gone, but the underlying need to specify when a step is actually complete is now carried in prose, and it's easy to get wrong.
- **Example.** For an assistant collecting delivery details, specify per field whether a skipped answer should be dropped (ask-once-and-proceed) or must be obtained before continuing (obtain-and-persist). A missing allergy or safety field on a food-ordering assistant is not a minor UX gap if it's silently dropped — it's a safety issue.
- This matches general advice from model providers to be explicit and unambiguous rather than assuming the model will infer intent.

## 4. Treat control as a dial, not an on/off switch

Don't pick "fully scripted" or "fully autonomous" once and for all. Think of it as a slider: one end is safety, determinism, and exact wording; the other is naturalness and flexibility. Launch close to the deterministic end and take small steps toward more flexibility as you watch how it behaves on real traffic. Keeping a high-stakes interaction scripted on purpose is a feature, not a sign you haven't modernized.

- **Era: agent-era.**
- **Example.** On a shopping assistant, route price, availability, and checkout through a constrained, mostly-scripted path, and let open-ended product discovery run more freely. Only loosen a given turn once logs show it's safe.
- This matches general agent-building guidance to start with the least autonomy that works and add flexibility only once it earns its keep, since every autonomous step adds latency, cost, and room for error.

## 5. Name the ways it can fail before you ship it

Teams often can't sleep at night about a new AI feature because of unknown unknowns. The job is to convert those into known unknowns: you won't prevent every failure, but you should be able to say roughly what can go wrong and how it's contained. The real test of whether something is ready to ship is "can I bound what goes wrong," not a headline accuracy number.

- **Era: agent-era.**
- **Example.** Before shipping a recommendation feature on a retail assistant, list the failure classes it can produce (wrong size recommended, stale price, fabricated return policy, confident answer to an out-of-scope question) and the containment for each (double-check against a source of truth, refuse, or escalate to a person). If you can't name the list, it isn't ready.
- Supported by published guidance on sandboxed testing, guardrails, and separate screening before and during production.

## 6. Guardrails are what let the agent act freely, not a punishment

Two related moves here. First, reframe the boundary as enabling, not restricting: a fence is what lets the agent (and the user) move freely and safely inside it. The common failure is giving people a fence with no understanding of what to do inside it. Second, make the boundary visible: tell users plainly what the system can and can't do, and when it has to decline something, degrade gracefully instead of hitting a silent wall.

- **Era: both.** Visibility is timeless; framing guardrails as enabling is sharper in the agent era.
- **Example.** A financial-advice assistant should frame its limits as "I can help you understand your options and compare products, but I can't execute a trade or give personalized investment advice" — stated up front, so the user knows what's inside the fence rather than discovering it as a series of refusals. When it declines something, it should say why and point to what it can do instead.
- Aligns with published human-AI interaction guidelines: make clear what the system can do, support easy dismissal, and scope services down gracefully under uncertainty.

## 7. Ground the agent on curated knowledge, with a human in the loop, and keep sources reachable

Don't let the agent "go look things up" freely and replay whatever it finds. Ground it on a curated, trusted knowledge base, keep a human author responsible for accuracy and compliance, and when the agent summarizes multiple sources, keep the originals one click away so someone can verify.

- **Era: agent-era.**
- **Example.** A cooking assistant should answer nutrition or allergy-related questions from a vetted recipe and ingredient database, not from general web knowledge, and a human should sign off on anything safety-related (allergens, substitutions). Bad or stale source content poisons every answer built on it, and no amount of prompt engineering fixes a bad knowledge base.
- Matches published guidance on grounding responses in curated data and using purpose-built, well-maintained knowledge stores rather than one big undifferentiated dump.

## 8. When you can't guarantee exact output, govern the process instead

A language model is probabilistic. You cannot promise precisely what it will say to a given user on a given day. Rather than pretending otherwise, govern the process around it: transparency, auditability, and clear disclosure of what the agent can and can't be trusted to do, backed by constraints in its instructions and clear terms of use.

- **Era: agent-era.**
- **Example.** For a financial or health-adjacent assistant, don't promise deterministic correctness on nuanced claims. Constrain what it's allowed to assert in its own instructions, disclose its limits to the user, and keep a reviewable log so anyone can audit what it said and why.
- Supported by published guidance on explainability, confidence communication, and planning for graceful failure as the basis of calibrated trust.

## 9. More autonomy requires more oversight, and the question is "should we," not "can we"

It's tempting to think a smarter model needs less supervision. The opposite is true: as an agent takes on more autonomous actions, you should be watching it more closely, not less, because you're handing it a share of a relationship you don't fully control. Gate each new automated capability on consequence — will this build or erode trust — rather than on whether it's technically feasible.

- **Era: agent-era.**
- **Example.** On a retail assistant, it may be technically possible to let the system auto-reorder a consumable on the user's behalf. Whether to actually do it is a separate question, gated on "does this deserve to run unsupervised yet," not "can the model do it." Never ship an autonomous action and walk away from monitoring it.
- Matches published guidance to keep humans in the loop on higher-risk actions (cancellations, large refunds, irreversible purchases) until reliability is proven.

## 10. Help the user think; don't think for them

For any agent whose job includes building the user's own understanding or judgment, the line is: assist their reasoning, don't replace it. If the system does all the reasoning and the person just reads the conclusion, you've built something that quietly defeats its own purpose — the user ends up with a passive answer instead of a developed understanding.

- **Era: both.**
- **Example.** A financial-literacy assistant helping someone understand their options should walk through the reasoning (why this account type fits their situation) rather than simply outputting "pick this one." A shallow five-line answer with no reasoning produces low-confidence decisions that are more likely to be abandoned or regretted later.
- Note the tension with the next principle, and with the general instinct that people also want things done for them, not explained at length. The resolution that tends to work: do the legwork and the searching for the person, but leave them understanding why the recommendation fits — scaffold their judgment, don't just hand over labor-free answers, but also don't turn every request into an exercise.

## 11. Guide decisively — unlimited freedom can be a stand-in for not having a plan

Letting a user wander and change their mind freely is a real win of conversational agents over rigid menus. But total open-endedness can also be a sign the system hasn't actually figured out what it should recommend. If the agent genuinely understands the user's context, the respectful thing to do is often a confident "here's what I'd do, here's the next step," not an open-ended menu that leaves them adrift, because attention is limited and people get distracted or lost.

- **Era: both**, more decisive in the agent era.
- **Example.** A shopper who has shared detailed context (room dimensions, style preference, budget) should get a confident recommendation with one clear next step, not a return to "well, what would you like to see?" This is in tension with principle 10 above — the resolution is to guide the path firmly while keeping the reasoning visible, so the person can see why and redirect easily if the recommendation is wrong.

## 12. A boundary that isn't tested is just a hope

Since the agent is non-deterministic, an unenforced boundary tends to erode. Turn expected behavior into concrete tests with automated judging ("assert it offered X," "assert it did NOT say Y"), run them continuously, and convert every real production failure into a new permanent test. Keep logs of the agent's own reasoning so you can diagnose why it did something, not just that it did it. The real quality bar is how fast you can fix an incident, not whether you launched perfect.

- **Era: agent-era.**
- **Example.** For a retail assistant, build a running test suite asserting things like "never contradicts the live price" or "always asks before executing an irreversible action," and grow that suite every time a real failure surfaces. Keep a readable log of the agent's reasoning so a reviewer can see why it made a given recommendation.
- Matches published guidance to validate at points where side effects occur, monitor for deviation from expected patterns, and be able to roll a change back.

## 13. Conversation isn't automatically better than a simple interface

A chat interface is not inherently superior to a button or form. They're partners: fast, familiar, single-step tasks belong on a simple interface; complex, multi-factor, hard-to-pin-down requests belong in conversation. Deciding, task by task, where conversation actually earns its place — and having the discipline to say "this shouldn't be a conversation at all" — is itself part of the job.

- **Era: agent-era**, correcting a common overreach of the agent-era narrative.
- **Example.** "Reorder my usual" or "where's my package" belongs on a one-tap button, not a back-and-forth. "Help me pick a rug that works with what I already own and fits a tight budget" is exactly the kind of multi-factor request that's worth a conversation. Don't bury the assistant behind several clicks when a quick button would do; and don't replace a perfectly good filter page with chat just because you can.

## 14. Hold firm standards everywhere, and flex only within bounds

Separate the fixed spine from the flexible layer. Universals — accuracy, respect, a consistent voice, accessibility — hold everywhere and don't bend. Everything else — tone, depth, pacing — can and should flex by context. A rough split worth aiming for is roughly 80% fixed fundamentals, 20% contextual calibration. This avoids both forcing one rigid script on every situation and letting every feature reinvent its own voice.

- **Era: both.**
- **Example.** A travel assistant's commitment to never misstate a price or policy holds in every market and every mode; how formal or playful it sounds, and how much hand-holding it offers, can reasonably vary between a first-time user and a frequent traveler.

## 15. Keep persuasion inside an honesty fence

Any agent that recommends things is also a persuasion surface, so it needs an explicit ethical line. Default to being transactional and honest; only make a case for something when the user is genuinely on the fence and the goal actually calls for it. Leave out manipulation-adjacent tactics — manufactured urgency, loss-aversion framing, artificial scarcity. Being willing to say "this isn't right for you" reads as a virtue, not a flaw, and it's what earns the trust that brings someone back.

- **Era: both.** Note explicitly: classic conversion-optimization tactics (urgency, scarcity, anchoring) are a mismatch for a trusted advisor and should not be imported wholesale just because they're common retail playbook moves.
- **Example.** A shopping assistant should never manufacture "only 2 left!" urgency or push an upsell against a budget the user has already stated. An assistant willing to tell a shopper a product isn't a good fit for them, when that's true, builds more long-term trust than one that always tries to close the sale.

---

See also: trust-and-expectations, failure-recovery, testing-principles.
