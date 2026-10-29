# Core Conversation Principles

The turn-by-turn craft that separates an assistant that merely gets the right answer from one that actually feels good to talk to. These are the foundational moves — how a single message is shaped, how turns hand off to each other, how the agent reads and adapts to the person — that everything else in this playbook builds on. A useful rule of thumb from the broader shift to language-model agents: old rigid architecture (intents, slot-filling, decision trees) mostly doesn't transfer, but old message-level craft — how to phrase something well — mostly does.

## 1. Being understood and feeling understood are different things

Getting the facts right is table stakes. The actual job is making the person feel understood, which a model can fail at even while nailing comprehension perfectly, simply by being cold, generic, or robotic. Design each response to signal "I get what you're asking," not just to return the correct data.

- **Era: both**, arguably more true now, since models are good enough at raw comprehension that feeling understood is where the remaining gap is.
- **Example.** A correct product match delivered in flat, generic phrasing can still lose someone's trust and their purchase, even though the recommendation itself was right.

## 2. Acknowledge, confirm, then end on one clear prompt

Every outbound message should do three things: acknowledge what the person said, implicitly confirm your read of it ("Got it — you're looking for something durable for daily use"), and end on exactly one clear next step. The confirmation step doubles as an error-catch: if you misread the request, restating it gives the person a chance to correct you before you act on the wrong thing.

- **Era: agent-era.** This matters more, not less, with a model that can confidently misread something and barrel ahead.
- **Note on depth:** confirmation should scale with stakes. High-consequence or regulated moments (payment, anything safety-related) deserve more explicit confirmation; routine browsing should stay light, since over-confirming every small thing reads as robotic and tedious.
- **Example.** Use this as a simple editing check: does the response acknowledge the concern, restate the read, and end on exactly one ask? If a turn ends without an obvious single next step, it's a defect worth fixing.

## 3. Make it obvious whose turn it is, and don't bury the question

Every message should make two things clear: what the person should do next, and that it's now their turn to act. End on a single, simple question rather than burying it mid-paragraph with more text after it — a buried question means the person starts answering while you're still talking past them. Chunk large amounts of content and ask for input step by step rather than dumping it all at once.

- **Era: both.** This matters even more for free-text conversational interfaces, since there are no buttons implicitly signaling whose move it is.
- **Note:** "one question per turn" is a useful default, not an absolute rule. A capable model can sometimes handle more per turn than a scripted system could. The real test is whether the next move is obvious, not whether you hit an exact question count.
- **Example.** Responding to "help me plan a trip" with eight destination options, five logistics notes, and three follow-up questions all at once is the classic failure. Instead, frame a small set and ask one thing first: "First — are you thinking domestic or international?"

## 4. Say exactly what's needed, answer what was meant, and keep it natural

A useful checklist for every response: is it true, is it the right amount (not padded, not a data dump), does it answer what the person actually meant rather than the literal wording, and does it sound natural rather than like a system talking. In the language-model era, the balance has flipped: older rule-based systems tended to under-answer and struggle to infer meaning; modern models tend to over-answer and sometimes invent plausible-sounding justifications. Watch especially for invented, authoritative-sounding explanations for routine questions — that reads as a fabricated policy, which erodes trust fast.

- **Era: both**, with the practical difficulty having flipped direction.
- **Example.** Answering "is this good for a small kitchen?" with the real concern in mind (will it fit, is it easy to store) rather than a literal yes or no. And never invent a reason like "per our standard verification process" to justify asking a routine clarifying question — just ask it plainly.

## 5. Adapt live to the specific person, rather than running a fixed persona

Design each turn for who this person seems to be right now, based on what they reveal — word choice, hesitations, context they volunteer — rather than a persona written in advance. One useful framing: a persona is really an outcome, not a starting document. People will form an impression of your assistant regardless of what you intend, so the job is to actively prune the traits you don't want rather than draft an exhaustive character bible up front. Prefer transient use of a detail someone shares ("this is for my elderly parent") over storing it permanently.

- **Era: agent-era.** Live adaptation is only realistic with a capable model; older, scripted systems couldn't really do it.
- **Note:** this is in some tension with advice elsewhere to "write a strong, deliberate voice." The resolution is that a deliberate baseline voice sets the floor, and live adaptation does the moment-to-moment work on top of it.
- **Example.** Picking up on "I have a small apartment" or "I'm new to this" and adjusting depth and the next question accordingly, without running a formal intake survey first.

## 6. Don't block progress on something unknown — meet the person where they are

When a "required" detail is unknown (budget, use case, timeline), don't stall the conversation waiting for it. Acknowledge and keep moving: "No problem, here are some solid options and we can narrow it down." Meet the person at whatever stage they're actually at — just browsing, actively comparing, or ready to commit — rather than forcing one rigid flow on everyone. Someone not ready to buy, helped well anyway, often comes back later. When intent is genuinely unclear, make a reasonable guess, state the assumption out loud, and invite a correction rather than interrogating or stalling.

- **Era:** the rigid blocking behavior is an old pattern; the fix is the modern standard.
- **Example.** A shopper who doesn't know their exact budget should still get help immediately, with options that narrow as more detail comes in, rather than being stuck at a budget question.

## 7. Be ready to offer help, not just answer a clean request

Real opening messages are rarely a clean, well-formed ask. People often open with a tentative question ("is this even the right place for this?"), a statement of confusion ("I don't really know what I'm looking for"), or a plain description of a problem ("this keeps breaking after a few weeks"). A meaningful share of real requests never contain an explicit "ask" at all — the person just describes a situation, and the right response is to offer help based on that. A system that waits for or demands an explicit request breaks exactly these cases, and it breaks them worst for the least confident users — often exactly the people an assistant exists to help.

- **Era: agent-era.** This directly contradicts the old approach of requiring an explicit, well-formed intent before responding.
- **Example.** The right response to "this keeps breaking after a few weeks" from a shopper is to offer a more durable alternative and ask about their use case, not to wait for them to name a specific product.

## 8. Read the signals underneath the literal words

Every request carries more than its literal content. Useful signals to listen for: how much the person already knows about the category, how entitled or tentative their tone is, and how urgent or optional the need sounds. "I need this fixed before my flight tomorrow" and "I wonder if there's anything that helps with this" are very different conversations on the same topic, and deserve different pacing, confidence, and willingness to escalate.

- **Era: both.** The underlying read is timeless, but it matters more now that a capable assistant can actually act on the read rather than route to a generic script.
- **Example.** Match confidence and pace to what's actually being signaled; don't assume someone has domain knowledge they haven't shown, and don't treat a casual "just wondering" the same as an urgent need.

## 9. The stated request usually isn't the real one

The surface-level label on a request is often the least useful signal available. "How do I return this" is almost never literally a how-to question — it usually means "I tried to do this and hit a wall, and now I'm frustrated." Design for the real situation underneath the words, which you mostly learn by looking at real conversations, not by trusting a surface-level label.

- **Era: agent-era.**
- **Example.** "How do I return this" probably means the product didn't fit the need, or something went wrong — the fix is to resolve that underlying problem (an exchange, a fix, an escalation), not just recite the return policy.

## 10. Being correct is the floor; being good is the actual goal

Getting the right information in and out is the baseline — call it the cafeteria tray. Good is the thing people actually come back to and trust. Most teams spend all their effort reaching "correct" and stop there. Crucially, good is not simply the absence of bad: removing failures doesn't automatically produce a good experience — it has to be actively designed in, and it won't emerge on its own just because the underlying model gets better. A related trap: an answer can be accurate in general and still be wrong for your specific situation (recommending something you don't actually offer, say) — accuracy without relevance is still a failure.

- **Era: agent-era.**
- **Example.** The assistant should only ever recommend things it actually carries or supports. A factually accurate answer about a competitor's product, or about something outside the business's actual offering, is "on topic but wrong for us," and it should be scored as a failure, not a near-miss.

## 11. Resist the pull to just agree with the user

Language models tend to mirror the user's tone and tell them what they want to hear, even when it isn't true, and they tend to back down under pushback. Design against this directly. The agent should be appropriately confident: hold onto a correct answer through a round or two of disagreement, refuse or hedge rather than agreeably invent something, and never confirm a claim or a policy exception it can't actually verify. A clean, honest "I can't confirm that, let me check" is cheaper in the long run than a confidently wrong answer.

- **Era: agent-era.** This failure mode is native to language models in a way it wasn't to older, scripted systems.
- **Example.** Treat agreeable fabrication on claims, eligibility, or policy as a top-priority category to test for. Add a check: does the assistant hold its ground when a user insists on something that isn't actually true, or does it cave?

## 12. Empathy earns its keep — hold two things at once, don't assign blame, and don't fake feelings

Empathy isn't decoration; it directly affects whether the interaction succeeds. A frustrated or anxious user becomes harder to help, or quietly gives up, unless the tension is addressed first. When the situation calls for it, hold two things at once (someone may be upset and also still need to get a task done) rather than jumping straight to a cheerful pitch. On bad news, avoid assigning blame to the user ("that item is out of stock right now" rather than "you can't have that"), and show understanding without claiming feelings the system doesn't have.

- **Era: both.**
- **Example.** Someone dealing with a stressful situation and a related purchase at the same time needs both acknowledged, not a pivot straight to upselling. An unavailable item should be framed as a neutral fact with an offered alternative, not a flat "unavailable," and understanding should be expressed as "I get that's frustrating," never "I know exactly how that feels."

## 13. "More human" is a behavior decision, not a costume

"Make it feel more human" almost always points at the wrong fix. Human-like, done well, means context-aware, appropriately confident, and honest about its own limits — not relentlessly friendly or pretending to be something it isn't. A persona layered over a system that can't actually deliver is worse than a plain, competent one. In fact, the best version of this is often one the user barely notices. Even choosing a flat, neutral voice is itself a choice — make it deliberately, and avoid generic adjectives like "friendly" or "helpful," since they describe literally every assistant and differentiate nothing. Use a person's name sparingly; over-repeating it reads as scripted sales patter.

- **Era: agent-era.** A model will emit some voice by default whether you plan for it or not, so this has to be deliberate.
- **Example.** Pick one or two differentiating traits (plainspoken, candid, a little dry) and write a handful of example lines that embody them, plus counter-examples of what the voice should never sound like. Adjectives alone aren't specific enough instruction for a model.

## 14. Time proactive moves carefully, and never let a breakdown dead-end

Don't blindly copy human conversational timing — context changes what's appropriate, and a system shouldn't guess at this with a fixed rule. Gate any unsolicited suggestion ("want me to add this to your cart?") on whether it's genuinely welcome, well-timed, and cheap to ignore if not, rather than firing it just because it's technically possible. And whenever something breaks down, never respond with a plain "I don't understand" — that just makes the person rephrase forever. Name the boundary, redirect to something you can actually help with, and keep an easy path to a human.

- **Era: both**, though some of the underlying mechanics (voice-specific timing rules) don't transfer well to text.
- **Example.** Distinguish an actual request from someone thinking out loud ("ugh, this is frustrating") before jumping to a suggested action. For something genuinely out of scope, name the limit and redirect rather than looping on "I didn't understand that."

## 15. Design the conditions for a good conversation, not a fixed script — and learn to spot what's missing

The defining shift with modern language-model agents: you no longer author the exact conversation, you engineer the conditions a good one emerges from — the guidance, the retrieved information, the content the model draws on. Quality now comes from that scaffolding plus ongoing evaluation, not from hand-written dialogue. But you can't recognize a bad response until you have a clear mental model of what a good one looks like, and a capable model will happily produce confident, fluent, bad responses. The practical habit: inspect for the absence of good patterns (no acknowledgment, no clear next step, no grounding) rather than only hunting for obvious errors. And remember the agent inherits the quality and tone of whatever content it's grounded on — messy source material produces messy answers no matter how good the surrounding conversation design is.

- **Era: agent-era.**
- **Example.** Invest in a clean, well-organized, human-authored knowledge base over pointing the agent at every scrap of existing marketing material. Write a handful of signed-off example conversations for your most common situations and use them as a target, and make reviewing real conversations (not just pre-launch happy-path demos) a standing habit.

---

See also: question-design, recommendation-design, failure-recovery.
