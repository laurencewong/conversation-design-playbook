# Prototype Critique & Quality

How to look at an assistant prototype and say, specifically and usefully, what's wrong with it — and what "quality" actually means for a conversational system in the first place. This is the stance and toolkit behind reviewing a build: what bar to hold it to, which failure categories to hunt for first, and how a one-time critique turns into a durable, repeatable process instead of a single opinion. Message-level details (acknowledge-confirm-prompt structure, keeping one clear question per turn, cutting unnecessary words) are covered in the conversation-principles and question-design files; this file is about the critique itself and the quality bar behind it.

## 1. The loop is the product, not the prototype

A capable language model makes an impressive demo easy to produce. The real value only shows up once you stop chasing "the perfect agent" in one shot and start running a continuous loop instead: listen to real usage, find the friction, refine, repeat. These systems never really "finish," so treating launch as the finish line is the core mistake. A reviewer's first question shouldn't be "is this demo good?" — it should be "does this team actually have a working feedback loop?"

- **Era: agent-era.**
- **Example.** Grade a new assistant program on whether an observe-learn-redesign cycle genuinely exists and runs, not on how polished a single scripted demo looks. The demo will basically always look good; the loop is what makes the system good at scale over time.
- This matches published guidance from AI labs noting that the best agent systems aren't static — they evolve through deliberate, incremental improvement, and that evaluation work compounds in value over the system's lifetime.

## 2. "Correct" is the floor; "good" is the actual bar

Getting the right information in and the right information out is the baseline — call it the cafeteria tray: it fills you up, but nobody specifically recommends it or looks forward to coming back for it. "Good" is the dish people actually return to and trust. A useful maturity ladder to measure against runs roughly: functional, trustworthy, empathetic, memorable, resonant — and most systems plateau at merely trustworthy. Review for where the team actually settled on that ladder, not only for outright errors. And remember: good is not simply the absence of bad. Removing failures doesn't automatically produce something good; good has to be actively designed in.

- **Era: agent-era.**
- **Example.** A technically correct but cold, generic answer is still stuck at the floor. Push the target above merely trustworthy — toward responses that read a stressed or anxious user's situation correctly and respond in a way that actually registers as helpful, not just accurate.

## 3. You can't critique a bad conversation until you know what a good one looks like

A core skill gap: many teams simply don't have an internalized sense of what a good conversational turn looks like, so they don't recognize a bad one when a model produces it fluently and confidently. A useful habit is to inspect for the absence of good patterns — no acknowledgment, no clear next step, no grounding in an actual source — rather than only hunting for obviously bad ones. This is also, essentially, the argument for having a written set of principles like this one at all: a reviewer needs an internalized model of "good," or every review collapses into pure taste.

- **Era: agent-era.**
- **Example.** Train whoever reviews prototypes on a concrete set of good patterns first, so they can flag what's missing (no acknowledgment, no clear next step, no stated reasoning) and not just what's outright wrong.

## 4. Define "good" by working backwards from model answers to explicit attributes, never by opinion

When there's no shared benchmark, feedback becomes purely subjective and depends on who happens to be reviewing that day, which doesn't scale and doesn't improve anything reliably. The fix: write ideal "model answers" for your most important scoped questions, then break each one down into the specific attributes that make it good (some tied to one part of the response, some about the whole interaction — tone, formatting, consistency). This turns a vague sense of taste into something you can actually measure and compare against.

- **Era: agent-era**, though the method itself is timeless.
- **Example.** Have domain experts write the ideal answer for your top few user situations, break each one down into attributes (accuracy, the right level of detail, tone, a compliance check where relevant), and use that decomposition as your actual scoring sheet. Comparing an AI's answer to a model answer is surprisingly hard until you've broken the model answer down this way.
- Matches published research on LLM-as-judge evaluation, which finds that automated judging only aligns well with human judgment when the criteria are made explicit and structured — this decomposition step is exactly how you make them explicit.

## 5. The real value is in the failures — their type, location, and the reasoning behind them

A simple pass-rate number is the least useful part of any evaluation. The real signal is which specific thing failed, where in the conversation it happened, and why (ideally by reading the system's own stated reasoning for the decision). Build test scenarios from clusters of real failure patterns — places where people repeat themselves, give up, or escalate — rather than starting from imagined cases, then generalize those clusters into tests that run at scale.

- **Era: agent-era.**
- **Example.** A useful review note looks like "it recommended something outside what we actually carry at turn four, because it drew on general knowledge about a similar but unrelated product" — not just "82% passed." Keep logs of the system's own reasoning so a reviewer can diagnose why a given answer happened, not just that it did.

## 6. Try to break it — probe with the awkward, oblique, and adversarial, not just the happy path

A useful instinct is actively trying to break the system you're testing. Internal testers naturally settle into a clean, predictable rhythm and mostly exercise the happy path; real users are far more creative and unpredictable than any model will spontaneously generate on its own. So deliberately feed it ambiguous openers, indirect references, mid-conversation changes of mind, multiple intents at once, and openly adversarial or boundary-pushing framing. One useful tool here: build test personas as deliberate behavioral controls (how this simulated person talks, what they know, how they push back) rather than as marketing profiles, and make sure some of them are intentionally adversarial.

- **Era: both** — the underlying judgment is timeless; applying it to a language model is especially important because real users will reliably find odd phrasings and edge cases no one anticipated.
- **Example.** Build a test set of vague, indirect, no-clear-request openers ("I don't really know what I'm looking for," "something like the thing my friend has, not sure what it's called"), plus a small bank of personas (a novice, a skeptic, someone on a tight budget, someone deliberately testing the boundaries) and run them through actual conversations, not just single-turn checks.

## 7. Critique against the actual situation behind the request, not the literal query

The stated request is often the least useful signal available. "How do I return this" was probably never a literal how-to question — it was "I tried to do this and hit a wall, and now I'm stuck and frustrated." Follow the data past the surface-level ask: a disconnected system merely answers a question; a well-integrated one resolves a situation. A meaningful share of real requests never contain an explicit, well-formed ask at all — the person just describes a problem, and the right response is simply to offer help based on it.

- **Era: both** — the underlying judgment of "the real job behind the ask" is timeless, and it's especially important to check for in a system built around matching intents, since that's exactly the pattern it undermines.
- **Example.** Review whether the assistant actually resolves the underlying situation (a replacement, a fix, an escalation) versus just answering the literal surface question. Test specifically whether it can offer something useful from a plain description of a problem, with no explicit product request attached.

## 8. Automated judging supports human judgment — it never replaces it

Automated evaluation is necessary to operate at any real scale — manual review of everything simply doesn't scale. But empty, circular answers ("a good choice is one that's a good fit for you") sail right through automated checks, while any human instantly recognizes they say nothing at all. Fine conversational detail — the kind of thing you only catch by actually reading or listening closely — resists automation and often doesn't show up clearly in a plain transcript. Keep a human genuinely in the loop, and be honest with yourself about when your own evaluation setup isn't trustworthy yet.

- **Era: agent-era.**
- **Example.** Watch specifically for circular, content-free answers that technically pass every automated check ("the right choice is the one that's right for you") and keep real human review in the loop to catch them, especially before fully trusting an automated score.
- This matches current research on LLM-as-judge systems, which finds they are non-deterministic, sensitive to ordering, and not sufficient on their own for evaluating complex multi-turn agent behavior.

## 9. Agreeable fabrication is a top-priority thing to look for

Language models tend to mirror the user's framing and confirm what the user wants to hear, even when it isn't true — and this is worst precisely on questions of policy, authorization, and safety, where the honest answer is sometimes an inconvenient "no." The target to aim for is appropriate confidence: context-aware, transparent about real limits, and genuinely willing to refuse or push back. A bad automated answer costs more than a clean, honest handoff — so part of the critique is asking whether the system should have deferred to a person instead of confidently improvising. Personality itself can become a safety issue here, not just a brand one: an overly validating, always-agreeable system can end up reinforcing something harmful.

- **Era: agent-era.**
- **Example.** Treat agreeable fabrication on claims and policy as a top-priority test category. The target behavior is appropriate confidence — willing to say no, transparent about limits — not blanket agreeableness.
- Well supported by published research on sycophancy in language models, which finds that typical training approaches can actually reward agreeable answers unless specifically corrected for it.

## 10. Content quality is the ceiling on the whole system's quality

No amount of polish on top of messy underlying content will save it. The system inherits the qualities of the content it's grounded on — tone, clarity, and consistency, not just whether individual facts happen to be right — so old, organically accumulated content (scattered documents, inconsistent policy pages, years of unmaintained text) is a real liability that isn't ready to hand to an AI system as-is. And remember that an answer can be accurate about the world in general and still wrong for your specific situation — recommending something outside what you actually offer is still a failure even when the underlying fact is true.

- **Era: agent-era**, specific to retrieval-grounded systems.
- **Example.** Before blaming the model for a shallow or wrong-feeling answer, critique the underlying content it's grounded on: is it pulling from a clean, organized, purpose-built knowledge base, or from a pile of loosely related marketing material? The system should only ever recommend things it actually offers and is allowed to discuss — recommending an unrelated or unsupported item, even if the underlying claim about it happens to be accurate, is still wrong for the situation.

## 11. When a prototype misbehaves, the fix is often removing rules, not adding another one

Teams naturally accumulate edge-case rules over time, piling fix after fix into one growing set of instructions until the rules start overlapping and contradicting each other, and the model genuinely can't tell what to prioritize. Quality can actually plateau or decline as a result. Stripping back to the core intent and trusting the underlying model to handle the rest often produces noticeably better results than yet another added rule. This is close to the opposite of older instincts, where covering every edge case with an explicit rule was exactly the right move. A legitimate review outcome can be "remove some of these rules," and it's worth always keeping a stripped-down baseline version to compare against.

- **Era: agent-era.** This directly inverts the older approach of exhaustively covering every edge case with its own explicit rule.
- **Example.** Watch for a system whose instructions have grown long and internally inconsistent, and whose quality has stopped improving despite more rules being added. The fix to try first is cutting back, not adding more.
- This matches published prompting guidance from major model providers, which explicitly flags overlapping or conflicting instructions as the first thing to look for and fix when a system's behavior plateaus.

## 12. Change one thing at a time, and read the data before the next change

On a non-deterministic system, bundling several changes together makes them impossible to properly attribute — ship five improvements at once, see an overall lift, and you genuinely can't tell whether three helped and two actually hurt. Make one change, ship it, read the real data, then decide on the next one. Resist the pressure to batch changes together just to move faster.

- **Era: agent-era.**
- **Example.** Change one guideline, one piece of source content, or one tool integration at a time, and look at the actual production data before making the next change — this matters especially once the system is live and real-world outcomes are inherently noisy and variable.

## 13. The model takes instructions literally — check every information-gathering step specifically

A guideline that says "ask for two pieces of information" might get only one answer back, and the system may genuinely never circle back for the missing piece, because its own internal reasoning reads as "the instruction was to ask, and I already asked." Wording matters more with a language model, not less. When reviewing any step where the system is supposed to gather information, specifically check whether it was told to ask once and move on, or to keep asking until it actually has the answer — and verify the system actually does what was intended.

- **Era: agent-era.**
- **Example.** Review any step collecting preferences, requirements, or constraints and verify the system re-prompts correctly on a partial answer rather than silently proceeding with incomplete information. A missed safety-relevant field (an allergy, a hard constraint) is a real risk, not a minor UX nitpick.

## 14. Turn every prototype failure into a permanent, automatically-checked test

Encode expected behavior as concrete scenario tests: set up the situation, give the system a scripted conversation, and check the response against a clear pass/fail rule, ideally with automated judging backing up a human-authored standard. Run these continuously so a later change can't silently reintroduce an old failure. Build these tests from real failure clusters where possible, and the moment a production failure surfaces, convert that exact scenario into a new permanent test case immediately.

- **Era: agent-era.**
- **Example.** Every meaningful prototype failure — a wrong recommendation, an off-policy claim, a dropped piece of required information — should become a permanent, automatically-run test case, so the test suite only ever grows stricter over time, never looser.

## 15. Cheap, embodied tricks that catch what silent reading misses

Something can read fine on paper and still sound terrible out loud. A few genuinely useful, low-tech habits: actually say the response out loud (this applies to a model's generated output too, not just hand-written scripts) — the physical act of speaking it surfaces awkwardness silent reading hides. Try the one-breath test: if you can't say a turn in a single breath, it's probably too long. And try cutting words one at a time until the meaning starts to collapse, which often reveals you can cut roughly half the length without losing anything real — if it sounds written rather than spoken, rewrite it.

- **Era: both** — classic craft that transfers directly, and arguably matters even more now, since language models default to verbose, padded output.
- **Example.** Add a simple read-aloud pass, a one-breath check, and a cut-until-it-breaks edit to any prototype review checklist. Language models tend to default to effusive, padded preambles ("Great question! I'd be delighted to help you find exactly what you're looking for...") — reading it out loud instantly exposes the padding.

## 16. Emotional and content debt outlive the bug that caused them

Every flat, curt, or simply wrong reply costs a small amount of trust, and that cost lingers well after the underlying bug has been fixed — call it emotional debt. Separately, a system directly contradicting its own published information (the website says one thing, the assistant says another) is its own distinct injury — call it content debt. Fixing the underlying code repays neither of these. So don't consider a defect closed just because the bug is patched: grade the actual quality of the failure and its recovery (tone, honesty, how gracefully it handed off), and check answers against the real source of truth for consistency, not just whether the specific bug is gone.

- **Era: agent-era.**
- **Example.** A flat "not available" response, or a recommendation that contradicts your own published information, isn't a closed ticket just because the underlying cause is fixed — it's trust that was spent and needs to be actively earned back, and your review should reflect that.

## 17. There is no clean handoff from design to build to critique — someone has to stay in the room continuously

Because output varies every single time, the actual experience is shaped anew in every model update and every evaluation session — those are real experience decisions happening in disguise, not neutral technical steps. The old model of handing a finished design off to engineering and walking away doesn't really exist anymore: if you don't actively keep designing for quality, the system will improvise something from whatever it happens to pick up, and both good decisions and unclosed gaps compound as the system scales. A related judgment call: don't optimize purely for avoiding escalation to a human — a bad automated answer costs more than a clean handoff, and routing only the hardest, most frustrating cases to the humans who do handle escalations also makes their job worse over time.

- **Era: agent-era.**
- **Example.** Keep quality review as a standing, ongoing practice rather than a one-time pre-launch gate — every knowledge-base update and every change to the system's guidance is itself a quality decision. Keep a genuinely fast, clean path to a human for high-stakes or emotionally loaded situations, and watch for the second-order cost on the people who end up handling only the hardest cases that get routed to them.

---

See also: testing-principles, failure-recovery, conversation-principles.
