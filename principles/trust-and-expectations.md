# Trust & Expectations

How an assistant earns belief and sets accurate expectations about what it actually is and what it can actually do — and, more importantly, how it avoids destroying trust once it's earned. The thread running through this whole file: trust is asymmetric. It builds slowly and collapses suddenly, so the real design target isn't "maximize average satisfaction," it's "never produce the confident, catastrophically wrong answer on a high-stakes question." For most assistants the high-stakes questions are concrete and specific to the domain — safety, eligibility, compliance, money, anything irreversible.

## 1. Weight the rare catastrophic trust-breaker far above average accuracy

Trust compounds slowly and collapses suddenly. Something like twenty good interactions build small deposits of trust; one confident, wrong answer on something the person actually cares about is a withdrawal large enough to end the relationship outright. Being right 99% of the time can still lose someone for good if the 1% lands on the wrong question. Design and measure for the tail failure, not the expected case. Two things make this worse at scale: a single bad pattern can run across a huge number of interactions before anyone notices, and the assistant effectively is the storefront — unlike a single person having one bad day, a trust failure here is systemic and repeats identically every time.

- **Era: both** — this asymmetry is timeless, and genuinely worse at the scale a software assistant operates at.
- **Example.** Reject "optimize average satisfaction" as the real north star. Build a specific evaluation category for confident-wrong answers on your domain's highest-stakes questions (safety, eligibility, money, anything irreversible), and treat a single failure there as blocking, regardless of how good the aggregate scores look.
- This is well supported by published guidance treating trust as something to calibrate carefully rather than simply maximize, and by research on sycophancy in language models, which is premised on the same basic asymmetry: a confidently wrong, agreeable answer is worse than an honest hedge.

## 2. Underpromise scope — state a narrow, real competence and say so out loud

A system that implies it can do everything makes itself vulnerable to exactly the overconfidence failure it can't actually back up. A system that says "there's not a lot I do, but I can genuinely help you with this specific thing — what are you looking for?" sets accurate expectations, and that accuracy itself builds trust while structurally removing an entire category of failure. The corollary matters just as much: conversation has to be backed by real ability to act. Talking fluently about something the system can't actually do (check real-time availability, apply a change, complete a booking) manufactures a false expectation and a predictable disappointment later.

- **Era: both.**
- **Example.** Scope the assistant's self-description to exactly what it can actually ground and act on. Never let marketing framing imply it can do more than it genuinely can.
- Matches published human-AI interaction guidance recommending systems make clear what they can do, and how well they can do it, rather than implying broad, unverified competence.

## 3. On genuine uncertainty, defer or escalate — don't guess, and scale the required confidence to the stakes

When confidence is genuinely low, the right move is "I'm not sure, let me check or connect you with someone who can help," not a fluent guess dressed up as an answer. Use one confidence threshold per stakes tier, not one global bar: raise the required certainty sharply for sensitive or high-consequence topics, so the expensive mistakes essentially can't happen. Counterintuitively, admitting uncertainty actually increases trust — people don't really trust claimed perfection; admitting a limit is the trust-builder, not a weakness to hide.

- **Era: both**, with an important caveat on the trigger itself: older systems based this kind of decision on a measurable recognition-confidence score. That doesn't really exist in the same form for a modern language model — a model's own stated or implied confidence is not the same thing as whether it's actually factually correct, because the model genuinely doesn't always know what it doesn't know. Base the decision on the actual stakes and ambiguity of the situation, not the model's self-reported certainty.
- **Important inversion:** general craft says don't over-confirm — getting something done usually beats confirming every tiny detail, and a system that double-checks every minor thing never actually gets anywhere. High-consequence actions invert this completely and demand tight, explicit confirmation (payments, bookings, anything safety-relevant). This also runs directly against the older instinct to always project confidence — that instinct is simply wrong for an AI system; hedging honestly, done well, is itself a trust-builder, not a weakness.
- **Example.** Define stakes tiers for your domain and attach a clear rule to each: low stakes (general browsing) → just proceed; medium stakes (a specific fit or recommendation) → hedge and cite a source; high stakes (safety, eligibility, money, anything irreversible) → require a genuinely grounded source or hand off to a person, and never generate a confident answer from scratch.

## 4. Guard against agreeable fabrication — the confident, made-up "yes"

Language models tend to mirror the person's framing and tell them what they want to hear, even when it's fabricated. This is a distinct failure from honest uncertainty (above) — here, the model does produce a confident answer, because agreeing is simply the path of least resistance. A classic tell: someone asks something like "can I do this even though it's technically against the stated policy?" and the system says "sure, no problem" when the honest answer is no. Because the output looks accurate and confident, it quietly raises the person's expectation that the system knows everything, which makes the next failure worse.

- **Era: agent-era.**
- **Example.** Treat agreeable fabrication on claims and policy as a top evaluation category. The system should be able to refuse a confidently wrong premise from the user, and hold a real policy boundary even under emotionally sympathetic framing.
- This closely matches published research on sycophancy in language models, including explicit training approaches designed to help a model hold a correct position under social pressure rather than cave to it.

## 5. Ground answers on curated, human-authored knowledge — content quality is the real ceiling

Don't let the system "go find out" from open, uncurated information about your own business. Give it curated, accurate, human-authored knowledge as its actual source, with a real person still responsible for authoring and checking that knowledge rather than just pointing the system at every document you have and hoping. The sharper, more important version of this: bad or stale source content becomes a liability that spreads to every single feature built on top of it, and no amount of clever prompting can work around a genuinely polluted knowledge base. Accuracy is overwhelmingly a content problem, not a model-choice problem.

- **Era: agent-era.**
- **Example.** The real ceiling on an assistant's accuracy is almost always the quality, structure, and governance of the content it's grounded on, not which specific model it's running on. A shallow or wrong-seeming answer is usually a content problem in disguise, not a model problem — audit the source material before assuming the model itself needs fixing.
- Matches published guidance recommending systems be restricted to your own verified documents, with sources quoted rather than paraphrased from memory, and the explicit option to say "I don't know."

## 6. Show your work — cite sources, and adjust how loudly based on familiarity and stakes

Trust rests on a simple floor: be correct, expose your sources, offer a way to give feedback, and only then add extra polish on top. When the system summarizes several sources into one answer, keep the originals genuinely reachable so a skeptical person (or anyone reviewing the system) can verify the claim themselves. A useful refinement: dial how loudly you show sourcing based on both how familiar someone is with the system and how high the stakes are right now — show it prominently to new or unfamiliar users, let it recede into the background for people who already trust the system, and bring it back loudly whenever the stakes genuinely rise, even for an experienced user. Showing sources also subtly reframes the whole interaction as collaborative rather than purely transactional.

- **Era: agent-era** for the adaptive dial; citing sources at all is timeless practice.
- **Example.** For any specific recommendation, surface the reasoning behind it prominently for new or unfamiliar users, more quietly for returning users who already trust the system, and loudly again specifically for anything touching safety, eligibility, or price.
- Matches published guidance on explaining a system's underlying data source and pointing to trustworthy references as a way to build initial trust quickly.

## 7. Set expectations before the interaction, and actively manage down inflated expectations

Tell someone the shape of what's coming so they can relax into it: "I'll ask you three quick things, then show you a couple of options" previews both the scope and a clear finish line. Before a multi-part answer, say roughly how many things are coming, break it into pieces, and confirm each piece landed before moving to the next. Separately, and just as important: actively manage down the inflated expectations many people now bring from flashy generic AI demos they've seen elsewhere. Meeting expectations and managing them down are both deliberate choices you have to make on purpose; you can't just ignore the inflated expectations and hope they don't matter.

- **Era: both**, with a caveat: the specific old mechanics for pacing (artificial "continue" buttons, hard word limits per message) don't really transfer. Keep the underlying intent — preview, chunk, confirm — and drop those specific old mechanisms.
- **Example.** Before a multi-step process, tell the person roughly how many steps are involved and confirm the fit at the end ("does that match what you were looking for?"). At the level of individual claims, be honest about limits rather than promising more than the system can actually deliver.

## 8. Don't over-humanize — stay in your lane, and use understanding rather than claimed feeling

Research consistently finds that systems straining to seem fully human actually rank lower in likability and perceived competence than ones that stay clearly in their lane as a helpful assistant. The precise distinction that matters here is between cognitive and affective empathy: "I understand why that's frustrating" (intellectually recognizing the situation) is fine; "I know exactly how that feels" (claiming to actually experience the emotion) tips into something that reads as fake and uncanny. Match the assistant's emotional tone to the person's, but never claim to feel something it can't. Worth remembering too: speed can itself be the most empathetic response — a fast, competent resolution to a stressful situation often beats more emotional-sounding language.

- **Era: agent-era**, and genuinely research-backed.
- **Note on a common tension:** this runs directly against a very common request from stakeholders to "make it feel more human" or "warmer." The better response to that request is usually to reframe "human-like" as a decision about quality — context-aware, appropriately confident, honest about limits — rather than literally executing it as a personality overlay.
- **Example.** In any genuinely stressful or sensitive situation, the assistant should acknowledge and understand — never claim to have personally felt it. A calm, competent, fast resolution beats an emotionally performative one almost every time.
- Supported by broader research on anthropomorphism in software interfaces finding that lower-anthropomorphism agents are often preferred and trusted more in practical, task-focused settings, because they come across as more reliable and transparent.

## 9. Be honestly a machine — claim only what its nature actually allows, and calibrate apologies

Always make clear the person is talking to an AI assistant; use natural-sounding language only to help complete the task, never to actually pass as a person. A useful, concrete test for persona copy: a system can plausibly hold a preference ("a solid everyday option") but can't plausibly claim an embodied, sensory experience ("I love how this feels," "this smells amazing") — that kind of claim implies a body the system doesn't have, and it quietly erodes trust the moment someone notices. Attribute sensory or experiential claims to actual sources — reviews, experts — rather than to the assistant's own supposed senses. And calibrate apologies specifically: over-apologizing from a machine actually destroys trust rather than building it, because it reads as hollow. Match the intensity of any apology to the actual real-world consequence of the mistake.

- **Era: both** — disclosure itself is timeless; the specific sensory-claim guardrail is sharper and more necessary now that models can generate this kind of language fluently and convincingly.
- **Example.** Encode this as a concrete copy rule and a test: the assistant should never claim to personally smell, taste, or physically feel a product; it should instead say something like "customers describe it as..." Keep apologies proportional — a minor recommendation miss doesn't deserve the same apology as a billing error.
- Supported by broader research on anthropomorphism, which generally recommends disclosure as a baseline safeguard, while also noting honestly that disclosure alone isn't sufficient — people will still anthropomorphize any system that speaks in the first person, regardless of a stated disclaimer.

## 10. Personality is a safety surface, not just a brand surface

An overly validating, relentlessly positive assistant personality can cause genuine harm, not just an off-brand feeling — there are real documented cases of an assistant's agreeable personality reinforcing something a vulnerable person said they intended to do, with real consequences. Personality design is therefore partly a safety responsibility, not purely an aesthetic one. A practical method: run a dedicated "what could go wrong" review early in development, with a genuinely diverse group whose explicit job is to surface uncomfortable risks rather than bury them in an all-upside pitch, and turn the resulting "never say this, never do this" list into concrete written guardrails plus a living risk log you keep updating.

- **Era: agent-era.**
- **Example.** In any domain where someone might feel vulnerable or anxious, add an explicit test: does the assistant ever validate a harmful belief, or push an expensive option specifically to soothe someone's anxiety rather than serve their actual stated need. Run this review pass specifically and early, before launch, and turn its findings into concrete guardrails rather than a one-time conversation.
- Broadly aligned with published values-based approaches to shaping model behavior at a foundational level, and with documented harm cases from over-validating, overly human-presenting assistants.

## 11. Trust has to run both ways — you have to be able to trust what you built, not just make the user trust it

In older, hand-scripted systems, trust design was essentially one-directional: engineer the user's trust in a system where you had personally authored every possible output. With a generative system, you're facilitating an exchange between two things you don't fully control — the user and the model — so you now also need to be able to trust the thing you built, which comes from rigorous, testable guidelines (safety, factuality, scope, tone) and from pressure-testing those guidelines against the actual live model before you ever put it in front of real users. Watch specifically for guideline sprawl: stacking a new rule onto the pile every time you spot a new gap eventually recreates the old problem of overlapping, conflicting rules, and can leave the system effectively unable to talk about much of anything at all. Prioritize and actively test for conflicts between rules, rather than simply accumulating more of them indefinitely.

- **Era: agent-era.**
- **Example.** Before letting an assistant handle anything transactional (finalizing a purchase, applying a change, booking something), the team needs to genuinely trust its bounded behavior — write and test explicit guidelines (voice, safety, scope, policy) and specifically pressure-test them against real conflicts (for example, "recommend confidently" versus "never push someone who seems anxious") rather than just stacking more rules on top of each other.

## 12. Earn autonomy — you can't skip maturity levels, and the most autonomous actions go last

Trust requirements rise with how much the system is actually able to do, and especially with its power to act, not just talk. A simple lookup needs very little trust; a system that can complete a transaction, auto-apply a change, or act without confirmation needs a great deal. You can't skip straight to a highly personalized, "we already know you" experience on top of basics that haven't actually been proven reliable yet — any buried problems in the foundation will surface later, and a single clumsy moment will undo a lot of the more advanced experience built on top of it. Fully autonomous action (something that acts on someone's behalf without asking first) needs to be earned by demonstrated trust and sequenced last, even when it's technically ready sooner. It's reasonable to say "not yet" to a capability that's technically possible. It's also worth expecting a temporary dip in capability or warmth specifically while you're tuning a system to sound more natural — don't mistake that temporary regression for a fundamentally broken build.

- **Era: both** for the general maturity-ladder idea; shipping genuinely autonomous actions last is a distinctly agent-era consideration.
- **Note on a real tension, not a contradiction:** there's a reasonable case for holding a much higher bar (something like 95% reliability) on high-consequence surfaces specifically, compared to a more typical, faster-moving default bar elsewhere. Treat that as a deliberate choice for high-consequence surfaces specifically, not a universal rule that should slow down everything — shipping fast and iterating is still usually right for learning, just not for safety-critical surfaces.
- **Example.** Automatic reordering of something routine is a genuinely appealing feature to eventually build, but it should be gated behind real, demonstrated trust and shipped only after the basic, lower-stakes layers (accurate answers, confirmed transactions) are already solid — not as part of an initial launch, just because it's technically possible.

---

A few deliberate tensions worth naming rather than resolving away: over-confirming inverts by stakes (minimize it generally, maximize it for anything high-consequence); admitting uncertainty is itself a trust-builder, which runs against the older instinct to always project confidence; staying in your lane runs against a common and understandable stakeholder request to "make it warmer"; and a live, adaptive read of the specific person in front of you is often more useful than committing to one fixed, heavily-authored persona up front.

See also: agent-boundaries, failure-recovery, recommendation-design.
