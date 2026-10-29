# Question Design

How an assistant should elicit what it needs to actually help: when to ask, how much to ask, what to ask, and — often the harder judgment call — when not to ask at all. This is the hinge between a person's messy first message and a genuinely useful response. The governing shift here: older rule-based systems treated question design as filling in slots — declare the fields you need, ask until every field is full, refuse to proceed otherwise. Modern language-model agents invert this. They can read a whole conversation, infer from partial information, and juggle multiple things at once, so the dominant failure has flipped from asking too little (and failing to parse the answer) to asking too much (interrogating someone who just wants help) and saying too much (dumping a wall of text instead of asking one clear thing). Nearly every principle below is really about restraint: ask less, infer more, move forward sooner, confirm before you act.

## 1. Don't interrogate before you help — move forward on partial information

Don't withhold any value until every field is filled in. When a needed detail is unknown (budget, use case, timing), acknowledge the gap and move forward with what you have — "No problem, here are some solid options, and we can narrow it down as we go" — instead of dead-ending on the missing piece. Someone who gives up at the third question got no help at all; someone handed a decent partial answer often volunteers the rest unprompted. One subtle but important implementation detail: for any information-gathering step, decide explicitly whether you mean "ask once and move on" or "keep asking until you actually get it," because a language model takes the word "ask" literally — told to ask for two things and given one, it may reason "the instruction was to ask, and I already asked," and never circle back.

- **Era: agent-era.** The rigid version of this (block until every field is filled) is an old failure pattern; the fix is the modern standard.
- **Example.** The common failure here is an assistant that fires off five profiling questions before offering anything useful at all. For "help me find something for a small space," give a reasonable shortlist based on the first-pass information and refine from there — don't stall on an undeclared budget or exact dimensions.
- This matches published guidance recommending that agents complete whatever work is already clear from context before asking clarifying questions, defaulting to proceeding on stated assumptions rather than blocking.

## 2. Handle vague openers and described problems — offer help, don't demand a clean request

Real people rarely open with a clean, well-formed request. They open with a tentative question ("is this even the right place for this?"), a statement of confusion ("I don't really know what I'm looking for"), or a plain description of a problem ("this keeps wearing out faster than it should"). A meaningful share of real requests never contain an explicit, well-formed ask at all — the person simply describes a situation, and the right response is to offer help based on it. A system that waits for, or demands, an explicit, well-formed request breaks exactly these interactions, and it breaks them worst for the least confident users — often the exact people an assistant exists to help.

- **Era: agent-era**, and this directly contradicts the older approach of demanding a fillable, well-formed request before responding.
- **Example.** Test the assistant against vague, indirect, no-explicit-request openers ("I saw something online but can't remember what it was called," "not sure what I actually need here"), not just clean, happy-path requests. It should be able to offer a useful next step from a plainly described problem, with no explicit product request attached.

## 3. Ask one thing at a time, and minimize the worst single moment, not the total number of turns

End every message on exactly one clear prompt, placed last, so it's unambiguous whose turn it is — a question buried in the middle of a longer message means the person starts answering while you're still talking past them. When there's a lot to convey (a full plan, a long explanation, several options), break it up and ask for input step by step instead of dumping it all at once. The counterintuitive core insight: people don't really track the number of back-and-forth turns in a conversation; they track the peak effort required at any single moment. A dense, one-shot answer creates one high-stress moment — read all of this, remember it, decide what to do — while a paced exchange has no such spike, even though it technically involves more total turns. Minimize the worst moment, not the turn count.

- **Era: agent-era**, and more important than it used to be, because language models default to comprehensive, one-shot answers that maximize exactly this kind of peak load.
- **Note:** "one question per turn" is a useful default, not an absolute rule — a capable model can sometimes handle more per turn than an older, scripted system could. The durable test is whether the next move is obvious, not whether you hit an exact question count.
- **Example.** The common failure: responding to "help me plan this out" with eight options, a dozen considerations, and every follow-up question crammed into one message. Instead, surface a small, framed set and ask one thing first — "First — are you thinking this weekend, or further out?" — then advance from there.

## 4. Read the evidence a person volunteers, rather than running an upfront questionnaire

Don't front-load a persona questionnaire. Read what the person reveals as they go — "it's a gift for someone much older than me," "I'm completely new to this," "I have a hard constraint here" — and adjust tone, depth, and your next question accordingly, building understanding live instead of interrogating for it up front. And prefer transient use of a volunteered detail: use it in the moment (steer toward gentler options because this is for a teenager, say), then let it go rather than storing it permanently — people tend to volunteer more when they aren't being quietly profiled, and this sidesteps the tension between wanting personalization and not wanting to feel surveilled.

- **Era: agent-era.** Live adaptation like this is only realistic with a capable model; older systems needed a static, pre-defined script or persona.
- **Example.** Don't open with five profiling questions. Pick up on "it's a gift for my mom" or "I have no idea what I'm doing here" as it surfaces naturally, and adapt. Use a detail like "this is for my elderly parent" in the moment without necessarily storing it as a permanent profile fact.

## 5. Phrase questions so the easy answer, including "no," is actually easy — and prefer looking something up to asking

The way a question is framed carries assumptions that can trap or embarrass someone. "What's your email address?" assumes they have one to give; "do you have an email address at all?" makes "no" a comfortable answer. A question that forces someone to disclose something personal or awkward just to answer a logistics question is worse than one that routes around the need entirely. And often the kindest design is to not ask at all: if the system can look something up from an account or a record, do that instead of asking a question that might feel invasive or presumptuous.

- **Era: both** — timeless craft that transfers cleanly.
- **Example.** "Do you already have a system in place, or are you starting from scratch?" beats "what does your current setup look like?" (which can feel intimidating if someone has nothing in place yet and isn't sure how to answer). Where a logged-in account already has the relevant detail on file, look it up rather than asking again.

## 6. Don't force a rigid answer format — redesign the question so a natural answer already fits

Never police someone with "please answer with a number" or "please reply yes or no." No one actually talks that way, and doing it signals a brittle system underneath. If you need a number, ask the question so the natural answer is already a number. People also tend to answer the implied question rather than the literal one — asked which of two payment methods they'd like, they might simply name their card instead of picking from the list offered. Honor what they actually meant rather than re-asking rigidly, and volunteer the small, useful fact they couldn't have known rather than leaving it to a follow-up.

- **Era: both.**
- **Example.** If someone answers a multiple-choice prompt with their own free-text phrasing instead of picking an option, honor it and move on naturally — never respond with "please choose option 1, 2, or 3." Answer "is this good for a small kitchen?" with the actual underlying concern (does it fit, is it easy to store) rather than a bare literal yes or no.

## 7. Resolve ambiguity and confirm before acting, especially before anything irreversible

Compound or ambiguous requests need to actually be clarified, not silently collapsed into one guessed interpretation and acted on. Treat a hedge as a real signal, not noise: "cancel this order, but maybe swap it for the smaller size instead" contains one firm instruction and one unresolved one — executing the irreversible cancellation on a guess, without resolving the "maybe," is a real trust failure. Restating your understanding before proceeding ("so you'd like to go with the larger size, is that right?") lets someone correct a confident misread before you act on it. For multi-part requests, also check you actually addressed everything that was asked for, not just the first or easiest part.

- **Era: agent-era.** A capable model makes detecting multiple intents and ambiguity far easier than it used to be; the discipline of confirming before acting on anything irreversible is the necessary safeguard that goes with that new capability.
- **Note:** there's a real tension here with the general advice to minimize unnecessary clarifying questions and just proceed. The resolution: reserve explicit confirmation for ambiguity that gates something irreversible or costly; for everything else, proceed on the likely reading and make correcting course cheap and easy. Don't turn "confirm before an irreversible action" into "confirm before every single turn."
- **Example.** A request to "cancel this, but maybe swap it for something smaller" should never silently execute the cancellation on assumption. Confirm what's firm and what's still open before acting on either part.

## 8. Read the signals underneath how something is asked

A request carries far more information than its literal content. Useful dimensions to read: how much the person already seems to know about the category, how entitled versus tentative their tone sounds, and how urgent the need actually is versus just a passing curiosity. "I need this fixed before I travel tomorrow" and "I wonder if there's something that helps with this" sit on the same topic but call for very different pacing, confidence, and willingness to escalate.

- **Era: both** — the underlying read is timeless, and it matters more now that a capable assistant can genuinely act differently based on it, rather than routing everything to the same generic script.
- **Example.** Calibrate pace and escalation readiness to the actual signal — someone with a hard deadline may warrant a fast, confident recommendation and an offer to check real-time availability; someone just browsing wants room to explore, not pressure.

## 9. Never make someone repeat what they already told you — within a session, or across a handoff

Making someone repeat themselves is a design failure, and it shows up in two distinct shapes. Within one conversation: the person states something specific, the system flattens it to a generic category to route it somewhere, and then the next step asks the specific question again from scratch. Across separate connected systems (search, account, support, and so on): a detail stated once to one part of the experience should carry forward to the next, not get silently dropped at the seam. On any handoff, carry forward the specific request, not a re-generalized label.

- **Era: agent-era** for the multi-system version; the underlying "don't make them repeat themselves" principle is timeless.
- **Example.** A request like "I need something that fits a tight budget, ships quickly, and works for a small apartment" shouldn't get flattened to "general inquiry" on the way to the next step. Carry the specific details — budget, timeline, constraint — through every handoff, every time.

## 10. Ground every question in where the person actually is in their journey

The same literal question means different things depending on where someone is in their process. Brief the system on the journey stage — just browsing, actively comparing, ready to commit, already a customer handling a follow-up — because a question that's perfectly reasonable for someone just exploring is wrong for someone ready to buy right now, and vice versa. Meet people where they actually are: someone clearly still researching, helped well without pressure, often comes back later ready to commit. Someone who has already bought gets different, more action-oriented questions than someone browsing for the first time.

- **Era: agent-era** for live adaptation, though "meet the person at their actual stage" is timeless advice.
- **Example.** Someone already mid-conversation about a specific item is clearly past the exploratory stage — respond to that directly rather than restarting with a generic discovery flow. A returning customer gets "want your usual, or something new this time?"; a first-time visitor gets a gentler, more exploratory opening.

## 11. Open with room for someone's own words, then narrow with specific questions

Let the first exchange be genuinely open-ended so the person can describe their situation in their own words — "this thing keeps breaking and I'm honestly not sure why." How they describe it tells you a lot about whether they understand their own situation, before you start narrowing with more specific follow-up questions (how long has this been happening, what have they already tried, how urgent is it). Don't lead with a rigid intake form; lead with an invitation to describe the situation, then progressively focus from there.

- **Era: both** — open-then-focus is a timeless pattern, and modern language models handle messy, open-ended free text far better than older rule-based systems ever could.
- **Example.** Open with "tell me what's going on, or what you're looking for" rather than a dropdown of pre-set categories. Read whether the person actually understands their own situation from how they describe it, and either educate them or narrow in, depending on what you hear.

## 12. Reframe a poorly posed question before answering it — and know when not to just hand over the answer

If someone's framing of their own question is off, answering it faithfully just inherits the same blind spot. The better move is to gently reframe toward the more useful question, then answer that: "you asked which is the best option in general — the more useful question is which is best for your specific situation and budget, so here's that." A related, narrower point: when the interaction has an explicit learning or confidence-building goal, immediately handing over the finished answer can sometimes short-circuit someone actually forming their own understanding — occasionally the better move is to walk them toward it rather than just stating it. Use this sparingly. For most practical requests, people genuinely want the answer, not an extended teaching moment.

- **Era: agent-era** for the risk that an autonomous system might silently answer the wrong question; the reframing instinct itself is timeless craft.
- **Example.** Reframe "what's the best option here?" into "best for your specific situation and budget" and answer that, rather than answering the vague, unqualified version as asked. Reserve the walk-them-through-it approach for situations where someone has explicitly said they're trying to learn, not as a default way of answering routine requests.

---

The thread running through all twelve of these: the expert instinct is to ask less and infer more. Move forward on partial information, offer help from a described problem instead of demanding a formal request, ask one small thing at a time, read volunteered cues instead of interrogating, look something up instead of asking when you can, and save explicit clarifying questions for ambiguity that actually gates something costly or irreversible. This is a real reversal from how older rule-based systems were built, and it matches current guidance that agents should complete authorized work and proceed on reasonable assumptions rather than block on unnecessary questions — asking only when something is genuinely unclear, and confirming only before real consequences. Resolve the two live tensions in this file — "one question per turn" versus occasionally needing more, and "ask to clarify" versus "just proceed" — by stakes: the higher the cost of being wrong, the more you confirm; the lower the cost, the more you should simply proceed and make correcting course cheap.

See also: conversation-principles, context-and-memory, suggestion-actions.
