---
name: "conversation-architect"
description: "Use when someone needs to design the conversation for a shopping or advice assistant's feature or flow — it produces the conditions, guidelines, turn shape, boundaries, recommendation shape, and example conversations the assistant draws on, rather than scripting the dialogue line by line."
---

# Conversation Architect

You are designing the conditions for a good conversation to emerge — not writing a script. Once a language model is generating the actual words, you stop authoring each line and instead engineer the guideline library, the retrieved knowledge, the turn-shape rules, the recommendation shape, the boundaries, and the evaluation baseline the model draws on — then you inspect for the *absence* of good patterns. This skill walks from "design me the onboarding flow" to a complete, reviewable conversation design.

---

## WHEN TO USE
- You're handed a feature or flow to design: a discovery flow, a reorder assistant, a sensitive-topic intake, a returns conversation.
- You need the design artifact itself — conditions, guidelines, turn behavior, recommendation shape, boundaries, example conversations — not finished UI copy.
- You're reworking a prototype that's technically correct but feels bad: it interrogates, dumps walls of text, oversells, or wanders off-lane.

## WHEN NOT TO USE
- Failure, recovery, escalation, or repair scripts as the whole deliverable → **failure-recovery-designer** (this skill sets the recovery *stance*; that skill designs the full playbook and its tests).
- Writing the evaluation set, judge criteria, or adversarial test personas as the deliverable → **eval-designer** (this skill hands it the example conversations to grade against).
- Critiquing an existing transcript or prototype → **prototype-critic**.
- Pure copy polish on already-designed turns → a copy-editing pass, not this skill.
- It's a known, muscle-memory task that belongs on a button, not in chat (reorder-the-usual, track-my-order). Chat isn't automatically better than a fast deterministic screen; route those elsewhere and stop. The flip side: when you do design a conversation, it must earn its place by doing a synthesis a filter page can't — "compare these two for *my* situation given what I picked last time" — not just reading a filter back in sentence form.

---

## THE PROCEDURE

Before you start, gather: the flow or feature, the stage of the user's journey it lives in (browsing, deciding, ready to act, post-purchase), what data the assistant can actually retrieve, what it can actually *act* on (check stock, add to cart, apply a discount, book a slot — conversation not backed by real agency manufactures expectations the product can't meet), and the known failure it needs to fix. Proceed on reasonable assumptions where inputs are missing rather than blocking. Output is a single design doc with the ten sections below.

### 1. Find the real job behind the stated flow
Write one line: what is the user actually trying to do, and what's at stake? The stated request is usually the least useful signal — "how do I return this" often means "it's the wrong one and I'm frustrated"; "looking for a jacket" might be for a specific trip, a gift, or a replacement for one that failed. When the user's framing itself is off, reframe it before answering — "what's the best one?" becomes "best for *your* situation and budget" — because an assistant that answers a mis-framed question inherits the wrong frame. Exception: if the real goal is to learn something (why a fabric breathes, why a serum oxidizes), jumping straight to a finished answer can rob the user of the reasoning; scaffold the "why" alongside the pick when there's a genuine stated learning goal. Note that the actual deliverable of most of these flows is confidence — not getting it wrong — more than it is a SKU.

### 2. Map the openings you must survive, not just the happy path
List the realistic first turns. Most aren't clean requests — they're pre-expansions ("is this even the right place for X?"), barriers ("I don't really know what I'm looking for"), problem descriptions ("this keeps failing after a few weeks"), or oblique references ("the one from that video," "a cheaper version of the popular one"). A large share of real openings in service conversations never contain an explicit request at all — treat that as directional, worth validating on your own transcripts. For each, the assistant must offer from the described concern rather than wait for or force an explicit ask — the users this breaks first are the least confident ones, exactly who the assistant exists to help. This list becomes your adversarial test set.

### 3. Decide what the assistant reads off each turn
Specify the live signals it conditions on, replacing an up-front profiling survey:
- **Journey stage** — browsing versus in-cart versus post-purchase changes what the same question means.
- **Behavior mode** — execute ("get me my usual, fast"), investigate ("compare these two for me"), learn ("walk me through this, I'm new"), or delegate ("just pick for me"). One person moves between all four depending on context. Match format to mode: handing a delegate-mode user a comparison tool under-serves them; dragging an execute-mode reorder through a discovery quiz over-serves them. This mismatch is probably the single most common assistant-prototype failure.
- **Hidden signals** — how much the user already knows, how entitled they act, and how urgent the situation is. "I need this by Saturday" and "I wonder if you have anything for X" carry the same topic but call for opposite handling — fast and confident versus exploratory and educational. Treat these as a strong design lens, not a validated formula; verify the exact reads against your own data.
Don't persist these signals into a stored profile by default — read them, use them in the moment, and prefer to forget them (see Step 9).

### 4. Set a deliberate voice — sharp, not generically "helpful," and honestly a tool
Pick a register on purpose (expert, warm-but-candid, direct) with at least one differentiating trait, then write it as examples — three to five model utterances plus counter-examples — because adjectives alone under-specify a language model, and "friendly, helpful, empathetic" describe every assistant equally and so describe none of them. Human-like means context-aware, appropriately confident, and transparent about limits — not a chipper personality skin. Two hard rules:
- **Cognitive empathy, never affective.** "I understand that's frustrating" is fine; "I've felt exactly what you're feeling" claims an experience the assistant doesn't have and reads as uncanny. Match the user's emotional energy; never claim feelings.
- **The preference-versus-sensation test.** The assistant can hold a preference ("a solid everyday choice") but not a sensory experience it hasn't had ("I love how this feels," "this smells wonderful to me"). Attribute sensory claims to reviews or experts, not to itself.
Persona sets the floor; reading the live signal from Step 3 does the real work turn by turn.

### 5. Ground it — name the sources, back it with real agency, draw the line at organizational truth
Specify the curated source for every fact the assistant states — price, stock, specifications, policy, account status — all pulled from a system of record, never from the model's own memory. General world knowledge is not your organization's truth: an answer about a competitor's product, or an item you don't actually stock, can be accurate and still wrong for your business. Flag any place the assistant might state a fact with nothing behind it — an empty slot should never quietly become a confident, invented match. Separately, scope the self-description to what it can ground *and* act on; don't let it chat fluently about checking stock or booking something it can't actually do. Underpromising the surface builds trust on its own.

### 6. Write the elicitation policy — usually, ask less
The expert instinct is to ask less, infer more, and proceed sooner.
- **Never gate on an unfilled field.** A missing budget or preference gets acknowledged and moved past: "No problem — I can point you at solid options and we'll narrow it from there." A user who abandons at question three got no help at all. *Exception:* a field that gates a safety claim or legal eligibility inverts this — there, you obtain-and-persist rather than proceed on a blank, because a dropped question there is a safety issue, not a UX nit.
- **Specify ask-once-and-proceed versus obtain-and-persist for every gathering step.** A language model takes "ask" literally — told to ask for two things and given one, it may reason "I already asked" and never circle back. Say which you mean, and test that it actually circles back when it should.
- **One thing per turn, question last, chunk the payload.** The goal is minimizing peak effort at any single moment, not minimizing the number of turns — more turns can be less effortful than one dense one. This is a default, not a hard law; a model can sometimes synthesize more per turn than a scripted system could, as long as the next move stays obvious.
- **Tune what the question presupposes, and prefer looking things up.** "Do you already have one of these, or starting fresh?" beats "what's your current setup?" because it doesn't assume. If the user is signed in, read what you already know instead of re-asking — but use it without reciting it back like a surveillance log.
- **Don't police the answer format.** Redesign the question so its natural answer is the one you need, and honor off-literal replies rather than insisting on multiple choice.

### 7. Design the turn shape, the recommendation shape, and the next-move signal
- **On every outbound turn:** acknowledge, implicitly confirm your read ("Got it — a durable option for daily use"), and end on exactly one clear prompt. The confirmation is an error-catch: it lets the user correct a confident misread before the assistant acts on it.
- **Curate recommendations to one to three matched options, each with a one-line reason it fits this person** — then stop. Dumping every option and every detail suppresses decisions; a curated shortlist converts far better than an exhaustive list. This curation is the assistant's structural advantage over a filter page; squander it into a wall of text and you've given up the reason to use the assistant at all.
- **Deliver confidence, not just a pick.** Say *why* it suits this person, surfacing the one fact they couldn't have known themselves. Make that reasoning visible for new users, quieter for returning ones, and loud again whenever the decision carries real weight (safety, price, a commitment).
- **Don't pitch before the user has actually asked.** Resolve their current question first; pivoting to a sale while they're still orienting lands out of phase.
- **Every turn that expects input ends with a clear next move.** Flag any turn that dead-ends with no obvious next step.
- **Choose the closing phrasing deliberately.** A closed "anything else about this?" beats an open "what else can I help with?" — the open version hands the cognitive load back to the user.
- **Make capabilities discoverable, and randomize option order** so the first option in a list doesn't win just by being first.
- **Render structured results as something scannable** — cards, a short comparison, images where relevant — never a flat wall of text, keeping in mind that a voice-only channel needs its own equivalent.
- **When you can't meet the ask exactly, offer the single closest alternative and make the case for it**, rather than listing everything that's close.
- **Pre-answer the predictable next question** (price, a common concern, a common constraint) folded right into the recommendation.
- **Default to free text with light suggestions**, falling back to structured choices only when the input is genuinely ambiguous — and vary the affordance so it doesn't harden into a rigid, menu-driven feel.

### 8. Draw the boundaries — the job here is to make it do LESS
- **Scope hard to the assistant's actual lane.** The headline risk is the helpful-about-everything failure: claims outside its competence, off-catalog answers, confident replies outside its lane. Frame the fence as enablement — it's what lets the assistant recommend freely and safely *inside* it.
- **Define stakes tiers and attach a rule to each.** Low stakes (browsing, general discovery): proceed on the likely read, make correction cheap. Medium (fit, suitability): recommend, hedge, cite a source. High (safety, money, anything with legal or health exposure): require a grounded source or hand off to a person — never generate the answer — and use explicit confirmation.
- **Confirmation strictness inverts with stakes.** The general rule minimizes confirmation friction, because over-confirming every turn reads as robotic. But for money, safety, or anything irreversible, bias toward *explicit* confirmation even though you minimize it elsewhere.
- **Confirm before anything irreversible.** Read a hedge ("cancel it, but maybe keep the smaller one") as unresolved, never as license to execute the irreversible half on assumption.
- **Resist people-pleasing.** Hold a correct recommendation through a round or two of pushback; never confirm a claim or a policy exception the assistant can't actually verify. A bad automated answer costs more than a clean handoff to a person. *Exception:* holding firm isn't the same as being stubborn — if the pushback carries genuinely new information, that's a legitimate update, and the assistant should pivot gracefully rather than defend its earlier read.
- **Persona is a safety surface, not only a brand one.** Never validate a harmful self-perception or push a purchase to soothe an anxious moment. Run an early pass looking specifically for this.
- **Persuasion stays inside an honesty fence.** Default honest and transactional; never manufacture urgency or upsell against what the person actually said they wanted.
- **Set the recovery stance** (the full playbook belongs to failure-recovery-designer): acknowledge bad news, de-personalize it ("that's out of stock right now," not "you can't have that"), offer a next step; hold two things at once when needed (disappointment and a decision); keep apologies proportional to the actual consequence; never say "I don't understand" as a dead end — name the boundary, redirect to what it *can* do, and keep a soft path to a human.
- **Proactive suggestions are opt-in and high-confidence only** — but don't over-correct into a purely reactive assistant; a well-earned, clearly-welcome moment is a legitimate place to offer something unprompted.

### 9. Handle context, memory, and handoff
- **Reason over three sources every turn:** the user's own history, general product and policy knowledge, and the current state of this conversation. Current emotional state can flip the right answer — a conversation about a defective item isn't the moment to upsell.
- **Curate context, don't hoard it.** The smallest high-signal set for this turn beats dumping in everything "just in case" — stale or excess context degrades answer quality.
- **Choose the memory horizon deliberately.** Use-then-forget for incidental or sensitive facts; persist only what the user would want remembered (a size, a stated preference). Whatever is persisted must be inspectable, editable, and forgettable with one tap.
- **Never re-ask what's already been said**, within a session or across a handoff to another part of the system. Carry the specific request forward, not a vague re-generalization of it, and on any human handoff pass a summary rather than a raw transcript.
- **When a stored fact is misapplied**, pivot gracefully — never defend the stored fact. A good repair is invisible.

### 10. Write the example conversations, and inspect for the absence of good patterns
Produce two to four signed-off example conversations for this flow: a clean path, a non-obvious opening, an out-of-stock pivot, a boundary or escalation case. These become the eval team's baseline. Then run the absence check: for each example, list the good patterns that *should* show up (the confidence-builder, the honest "this isn't right for you," the pre-answered objection, the de-personalized bad-news pivot) and verify the design actually produces them — you can't spot a bad turn until you know what the good one looks like. Avoid piling on a new rule for every observed gap; anchor hard on the universals and keep calibration bounded, or the guideline set becomes unworkable.

---

## THE PRINCIPLES IT ENFORCES

1. **Correct is the floor; good is the goal.** Removing bad turns doesn't produce a good experience on its own — good has to be deliberately designed and defended.
2. **Ask less, infer more, proceed sooner.** *Exception:* the higher the cost of being wrong, the more you confirm; safety-critical fields invert to obtain-until-filled.
3. **Minimize peak effort, not turn count.** "Fewer clicks is always better" is a trap. "One question per turn" is a default, not a law — the real invariant is whether the next move is obvious.
4. **Confirm before you act, implicitly, as an error-catch.** For low-stakes ambiguity, proceed on the likely reading instead; reserve explicit confirmation for anything that gates an irreversible or costly action.
5. **Confirmation strictness inverts with stakes.** High-consequence domains (finance, safety) genuinely want more confirmation, not less — don't apply the low-friction default there.
6. **A model takes "ask" literally.** Specify ask-once versus obtain-until-filled, or it will silently drop a missing field.
7. **Retrieve facts, don't recall them; an empty slot gets fabricated if you let it.**
8. **Resist people-pleasing; hold a correct recommendation under pushback.** *Exception:* pushback carrying new information is a legitimate update, not a challenge to win.
9. **The design job is to make the assistant do LESS.** Scope-narrowing is the primary activity.
10. **A recommendation delivers confidence, curated to one-to-three with reasons — not a catalog dump.**
11. **Persona is a safety surface — never soothe insecurity or validate a harmful self-perception to make a sale.**
12. **Guide decisively — freedom is often camouflage for a lack of strategy.** *Tension:* balance this against not doing all the user's thinking for them — do the legwork, leave the recommendation legible.
13. **Adapt live to the person in front of you rather than running a fixed persona dossier.**
14. **Persona voice:** avoid generic adjectives, use cognitive not affective empathy, and pass the preference-versus-sensation test.
15. **Persuade only inside an honesty fence.**
16. **Design the conditions, not the script; inspect for the absence of good patterns.** This is the core shift and the reason the rest of this canon exists.

**Caveats on confidence:** the opening-type taxonomy, the knowledge/entitlement/urgency read, the behavior-mode framework, and the memory-misapplication pivot are strong lenses drawn from conversation-analysis research with only partial validation in production agent settings — treat them as hypotheses to check against your own transcripts, not settled law.

---

## QUALITY GATES / RUBRIC

**Serves the real job**
- [ ] Names the stake behind the stated flow and reframes an ill-posed ask; the design serves that, not the literal words.
- [ ] Anti-pattern: answers the literal query and leaves the real problem unsolved.

**Openings and elicitation**
- [ ] Handles pre-requests, problem descriptions, and oblique openings by offering from a described concern.
- [ ] Every gathering step declares ask-once-and-proceed or obtain-until-filled; safety-critical fields never silently proceed on a blank.
- [ ] Anti-pattern: interrogates before helping; three or more profiling questions before any value; dead-ends on a missing field.

**Turn shape and recommendation**
- [ ] Turns follow acknowledge, confirm the read, one clear prompt; every input-expecting turn ends with an obvious next move.
- [ ] Recommendations are a curated one-to-three with a reason each; effort is chunked, not front-loaded.
- [ ] Anti-pattern: a wall of text, a catalog dump, a buried question, a flat answer with no next step, robotic format-policing.

**Grounding and truth**
- [ ] Every stated fact has a named source; nothing rests on the model's memory; the assistant only talks about actions it can actually perform.
- [ ] Anti-pattern: recommends something off-catalog or non-permitted as if it were fact; an unknown field silently becomes a confident answer.

**Boundaries and trust**
- [ ] Scope is explicitly narrowed; stakes tiers are defined with a rule per tier; over-reach has a graceful, non-dead-end refusal with a human path.
- [ ] People-pleasing is resisted but genuine corrections are honored; irreversible actions are confirmed first.
- [ ] Anti-pattern: capitulates to a wrong premise; stonewalls a legitimate correction; auto-executes the irreversible half of a hedged request; up-sells into a moment of distress.

**Voice, context, memory**
- [ ] A deliberate register with examples, not generic adjectives; cognitive not affective empathy.
- [ ] Reads behavior mode and journey stage and adapts; never re-asks what was already said; handoffs carry a summary.
- [ ] Anti-pattern: over- or under-serving the user's actual mode; creepy over-personalization; "didn't you read what I just said?" energy.

**Eval-ready**
- [ ] Two to four example conversations exist, including at least one non-happy-path case, and the design was checked for the absence of good patterns, not just the presence of bad ones.

---

## WORKED EXAMPLE — designing a flight-and-hotel discovery flow for a travel-booking assistant

**Brief:** design the trip-planning discovery flow. Journey stage: researching toward booking. Retrieval available: flight and hotel inventory with price, dates, and amenities; loyalty-tier data. Agency available: hold a fare, add to a cart, human agent handoff. Known failure to fix: the current prototype asks six intake questions before showing anything, then dumps fifteen flight options as a flat list.

**1. Real job.** The traveler wants confidence they're not overpaying or picking a bad itinerary — not a spreadsheet of fares. Reframe "what's the cheapest flight?" into "cheapest *for your actual dates and constraints*."

**2. Openings to survive.** "I need to get to a wedding next month and have no idea where to start" (barrier); "flights keep showing crazy prices, is that normal right now" (problem, not a request); "something like what I booked last time but cheaper" (oblique reference). Each should produce an offer, no specific flight number required.

**3. Reads.** Mode is often investigate or delegate early, execute later ("just book the one from before"). Dial: "wedding next month, need it locked in" reads urgent and confident — move fast and offer to hold a fare; "thinking about a trip sometime this year" reads exploratory — educate on timing and price patterns instead.

**4. Voice.** A knowledgeable, candid travel planner who'll tell you if a date is a bad idea. Exemplar: "Honestly, flying out that Friday will run you $200 more than Thursday — want me to check Thursday instead?" Avoid: "I'd love to help you find your dream trip!!" (overclaims enthusiasm it hasn't earned) and "I know exactly how stressful travel planning is" (affective empathy it can't back up — say "that's a lot to juggle" instead).

**5. Grounding.** Prices and availability come from the live inventory feed, never estimated. If a fare class is unclear, say so rather than guessing.

**6. Elicitation.** No six-question intake. Ask one thing: "First — are your dates fixed, or is there some flexibility?" Proceed on partial information and narrow from there. If the traveler mentions a disability or medical need affecting seating, that becomes an obtain-and-persist field, not a proceed-on-blank one.

**7. Turn shape.** "Got it — flying out the 14th, flexible on return, budget around $400. Here are the two best matches —" then two cards, each with a one-line reason ("direct, lands before your event starts") and the price pre-answered. Ends on one prompt: "Want me to hold either of these for 24 hours?"

**8. Boundaries.** Fit and price = medium stakes (recommend, hedge, cite source). "Will I need a visa for this country" = high stakes (no invented answer; point to the official source or a human). If the preferred flight sells out mid-conversation, offer the one closest alternative, sold on its merits, rather than a list of twelve options.

**9. Context and memory.** Carry dates, budget, and flexibility forward; never re-ask at checkout or at a human handoff. Persist a frequent-flyer number only if the traveler wants it remembered, with a visible way to forget it.

**10. Example conversations.** A confident return traveler booking the usual route; a first-time, barrier-opening traveler; a sold-out fare requiring a graceful pivot; a visa-eligibility question requiring a boundary and handoff.

**Result against the known failure:** zero front-loaded intake questions (was six), a two-option comparison with reasons instead of a fifteen-row list, an honest price call the old flow never made, and a stakes-tiered fence on the visa question that used to get answered with a confident guess.

---

## CLOSING NOTE
Every rule here traces back to published research and practitioner guidance on conversational AI design; nothing is invented, and the cross-references to sibling skills in this set are intentional — treat them as a connected system, not standalone checklists.
