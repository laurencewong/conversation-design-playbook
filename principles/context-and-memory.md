# Context & Memory

How an assistant should build, hold, apply, ground, and forget what it knows: what it understands about the user right now, what it carries across turns and sessions, and where its facts come from. The common thread is that context is a curation and trust problem, not a storage problem. The usual failure shapes are: re-asking something already said, confidently inventing an answer to fill a gap, hoarding data no one agreed to, applying an old fact to the wrong situation, and losing the thread at a handoff.

## 1. Build understanding from three sources, every turn

Reason from three things at once: the user's own history (past interactions, stated preferences), general domain knowledge (product catalog, policies, how things work), and the current moment (what's happening in this session, the user's stated concern or mood). Don't answer off just the literal last message. Critically, the current situation can flip what the right answer even is — a support conversation about a damaged or unsafe item is not the moment to upsell, the same way recommending a bottle of wine is wrong once you know the person doesn't drink.

- **Era: agent-era** in its sharpened form — the underlying idea (both parties building shared understanding) is old, but reasoning over all three sources on every single turn is the modern bar.
- **Example.** A travel assistant should combine the traveler's past trips, general destination knowledge, and the live context (a flight delay just happened) before responding — not just answer the literal question asked.

## 2. Calibrate between asking, confirming, and assuming — and confirm your read before acting

Match your next move to how strong the signal is. Ask an open question when you know little. Confirm with a quick yes/no when the signal is weak or might be stale. Assume and act when the signal is strong and repeated. Confirming also works as an error-catch: restating what you understood lets the user correct a misread before you act on it wrongly. As the relationship develops, the same request can shift from "ask" to "confirm" to "assume" over time.

- **Era: both.** The underlying decision rule is durable even though it originated in older, more rigid systems.
- **Important inversion:** this is not "always confirm." Confirmation strictness should scale with the stakes. Low-stakes browsing should just proceed — over-confirming trivial things reads as robotic and slows everything down. High-consequence actions (a purchase, an irreversible change, anything safety-related) deserve tight, explicit confirmation even when the signal looks strong.
- **Example.** A recipe assistant can confidently assume a returning user's dietary restrictions after they've been stated and used consistently, but should still confirm explicitly before finalizing a grocery order that includes a substitution for a stated allergy.

## 3. Adapt live to the person in front of you, rather than running a fixed script

Shape each response to who this person seems to be right now, based on what they reveal in the conversation, rather than a persona decided in advance. One useful lens is to read the user's behavior mode: are they trying to execute something quickly, investigate and compare, learn from scratch, or delegate the whole decision to you? People move between these modes fluidly. And use what you've learned about someone without being creepy about it — reference it naturally rather than reciting it back at them.

- **Era: agent-era.** Live adaptation is only practical with a capable model; older systems had to lock in a static script.
- **Example.** On a shopping assistant, someone in "execute" mode ("just reorder my usual order, don't make me think") should not be dragged through a discovery quiz, and someone in "delegate" mode ("just pick one for me") should not be handed a comparison tool. This mismatch — over-serving a quick task or under-serving an open-ended one — is one of the most common assistant failures.

## 4. Give the agent the right context, not all of it

The instinct to stuff everything into the model's context "just in case" produces confusion, not clarity, and actively hurts quality. Treat context as a curation problem: find the smallest set of genuinely relevant information for this specific turn. On real-time or cost-sensitive surfaces, past a certain point more context costs you speed and money with no accuracy gain.

- **Era: agent-era.**
- **Example.** Don't pour a user's entire purchase history and every product fact into every single turn of a shopping assistant. Pull in the specific details relevant to the recommendation at hand.
- Well supported by published guidance from AI labs describing "context rot" — the finding that recall quality degrades as irrelevant tokens accumulate, and that every piece of stale data actively degrades performance. Aim for the smallest set of high-signal information, not the largest.

## 5. Don't block progress on a missing detail — acknowledge it and keep moving

When a piece of information is unknown (a budget, a preference, a date), don't stall the conversation until it's filled in. Acknowledge the gap and move forward anyway: "No problem, I can still point you toward good options and we'll narrow it down as we go." Many people want some kind of help even before they can specify exactly what they want.

- **Era: both** — the rigid version of this failure (demanding every field before proceeding) is an old pattern; the fix transfers cleanly to modern agents.
- **Example.** An assistant helping someone plan a trip without a fixed budget yet shouldn't dead-end. It should offer a reasonable range of options and narrow from there as more detail comes in.

## 6. When context is missing, the model invents to fill the gap — so force it to ask or flag unknowns

A language model doesn't return a blank when information is missing; it invents something plausible to fill the hole. So the risk of a confidently wrong answer rises with how much you leave unspecified. Either elicit the missing fact explicitly or mark it as unknown — never let an empty field silently turn into a fabricated answer.

- **Era: agent-era.**
- **Example.** If a user's size or a key preference is unknown, a shopping assistant must ask or hedge, not invent a plausible-sounding match. This is one of the most severe failure classes, because it looks exactly like a correct, confident answer.

## 7. Ground facts in a curated source of record, and treat "content debt" as a real liability

Facts like price, availability, policy, or loyalty balance should come from a curated, trustworthy system via retrieval, never from the model's own memory, which has a cutoff date and no access to your live data. The sharper version of this rule: bad, stale, or contradictory source content spreads to every feature built on top of it, and no amount of prompt tuning can fix a polluted knowledge base. Data quality work has to happen upstream of prompt work, not instead of it.

- **Era: agent-era.**
- **Example.** A home-goods assistant's knowledge base is its product data, material facts, and policy text. A messy or outdated product feed is a liability no prompt engineering can patch — if a size chart is wrong in the source, no instruction will make the agent state it correctly.
- This matches published guidance recommending retrieval tools for grounding responses in current data, and purpose-built, well-maintained knowledge stores rather than one undifferentiated dump.

## 8. Make memory inspectable, editable, and forgettable

Persistent memory shouldn't be a one-way log. Users should be able to see what the system believes about them, correct it, delete it, and reset to a non-personalized default. In any privacy-sensitive category, giving people control over their own stored data matters more than raw recall — honoring "forget this" is a core trust behavior, not an edge case.

- **Era: agent-era.**
- **Example.** A financial assistant that remembers a user's stated goals or risk tolerance should expose a simple "here's what I remember about you" view with a one-tap way to clear it. A wrong stored fact in a sensitive category isn't just an annoyance; it's a real accuracy and trust problem.
- This is well supported by published guidance recommending the ability to erase or reset previous personalization choices back to a non-personalized default.

## 9. When a stored fact doesn't fit the current situation, pivot gracefully instead of defending it

A distinct failure shows up when the system applies something it remembers to the wrong situation — recalling a stated preference and wrongly imposing it on, say, a gift purchase for someone else. When corrected, the right move is to adapt immediately ("got it, I'll broaden the options"), not argue ("but you told me earlier that..."). A good correction here is nearly invisible to the user.

- **Era: agent-era.**
- **Example.** A shopping assistant that recalls a user's stated preference for compact furniture shouldn't force that preference onto a gift purchase for someone else's much larger space. When the user clarifies, it should simply adjust.

## 10. Decide deliberately whether memory is transient or persistent — there's a real tradeoff, not a single right answer

There are two legitimate defaults, and the choice should be made deliberately rather than assumed. One approach is transient, use-it-and-forget-it personalization: use a volunteered detail in the moment, then let it go, which sidesteps privacy concerns and tends to make people share more freely because they're not being profiled. The other is persistent, cross-session memory: carry history forward so a returning user gets continuity, which is now technically easy and genuinely useful. Neither is universally correct. Persist low-sensitivity, durable preferences people clearly want remembered; keep incidental or sensitive details transient. Whatever you persist should stay subject to the inspect/edit/forget rule above.

- **Era: agent-era** for both postures; the tension is sharper now that persistent memory is cheap and easy to build.
- **Example.** A cooking assistant should probably remember a stated dietary restriction across sessions (the user wants that remembered), but should treat a one-off detail like "cooking for a guest with a shellfish allergy this one time" as transient unless told otherwise.

## 11. Never make the user repeat what they already told you, across sessions or across handoffs between agents

As a product grows multiple connected agents or skills (search, account, support, and so on), the user's journey will cross between them. A system that merely routes to the next step is not the same as one that actually carries the right context along with it; the latter is what you want. The user should never have to care about your internal architecture. The clear failure sign: a user states something once and a later step asks for it again.

- **Era: agent-era.**
- **Example.** If someone tells a shopping assistant their size and style preference, and the conversation later hands off to a returns or support flow, that flow should already have those facts, not re-ask for them.
- Well supported by published agent-handoff guidance, which generally has state and conversation history transfer automatically between connected agents.

## 12. On handoff to a human, pass a specific summary, not a raw transcript and not a vague topic label

When an agent escalates to a person, all its earlier work is wasted unless the handoff carries the user's specific situation forward and happens quickly. Give the human a short, readable summary rather than a wall of raw transcript to scroll through, while keeping the full transcript available if they need to dig in. Leave a persistent record so a future contact isn't starting from zero.

- **Era: both** — handoff craft itself is old, but the automatic summarization is a new capability worth using well.
- **Example.** A support handoff for "a size issue with a recent order, trying a smaller size next, product was otherwise fine" should arrive at the human as exactly that summary, not flattened into "sizing question," and not as an unreadable full transcript dump.

## 13. Close the loop — ask how it actually went, and feed that back in

Real memory isn't only what a user told you; it's whether your suggestion actually worked out for them. The agent should check back in later, folded naturally into a related follow-up rather than a formal survey, and use what it learns to improve future personalization.

- **Era: agent-era.**
- **Example.** "How did that recipe turn out?" on a later visit both improves the system's model of the user and reads like something a knowledgeable, attentive assistant would naturally ask.

## 14. Notice the real stakes behind a request, and gently reframe a poorly posed question before answering it

There's almost always something behind a literal functional request. "Looking for a gift" might really mean a wedding, an apology, or a last-minute obligation, and the right answer depends on which. Relatedly, when someone's framing of their own question is off, it's often worth quietly reposing it before answering — "which is the best option" becomes "best for your situation, budget, and goal" — rather than answering the literal, poorly-framed version and inheriting its blind spot.

- **Era: both.**
- **Example.** "Which laptop is best?" is usually better answered as "best for what you're actually going to do with it and what you're willing to spend," gently surfaced rather than assumed.

---

See also: trust-and-expectations, question-design, failure-recovery.
