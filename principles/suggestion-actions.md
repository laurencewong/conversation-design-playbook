# Suggested Actions & Affordances

How an assistant offers the person's next move: suggestion chips, buttons, carousels and product cards, proactive prompts, next-step recommendations, how options are framed, escalation controls, and plain discoverability. This is the steering layer of a conversation — the part that reduces someone's effort and tells them what to do next without burying them in text. Affordances aren't decoration, and they aren't a crutch for a weak underlying model. They're how you actually control the experience: cutting peak cognitive effort, signaling whose turn it is, keeping someone moving toward a confident decision, and keeping an open-ended system on rails. The recurring failure here is a model defaulting to what's basically old-fashioned phone-tree behavior — dumping dense option lists and instructions so thick the person can't act — or the opposite, a flat answer that leaves someone with no obvious next move at all.

## 1. Every turn expecting input should end with a clear next move

For each response, ask two things: is it obvious what the person should do next, and is it obvious it's now their turn. A concrete closing prompt or suggestion does double duty — it elicits an answer and it hands control back at the same time. A turn that ends without one leaves the person unsure whether to respond at all. Never bury a question in the middle of a longer message with more text following it; put the prompt last, so whose turn it is stays unambiguous.

- **Era: both** — turn-clarity matters regardless of medium, and matters even more for free-text interfaces where there are no buttons implicitly signaling "your move."
- **Example.** Every assistant turn should make the next tap or reply obvious ("want the full breakdown, or just the quick version?"). Flag any turn that ends without a clear next move as a defect, since it's a common and easily fixable cause of someone simply dropping off.

## 2. Calibrate how much you suggest at once — cut peak effort, never dump the menu

The human mind doesn't really track the number of steps in a conversation; it tracks the peak effort required at any single moment. A one-shot, dense answer — a full plan, six options, detailed technical notes, all at once — creates one high-stress moment; a chunked back-and-forth creates none, so more turns can actually be less effortful overall. The intuitive "fewer clicks is always better" instinct is a trap. Surface a small, framed set, ask one thing, and advance. The telltale sign of a system defaulting to old phone-tree behavior is over-prompting: dumping option lists and cramming instructions into a turn so densely the person can't actually interject or respond naturally.

- **Era: both.**
- **Example.** Someone asking "help me put together a plan" should get one small, framed next step ("first — are you thinking this weekend, or further out?"), not a dense wall of six options and a dozen considerations all at once. This is probably the single most common failure in assistant prototypes: the over-dense wall-of-options response.
- This matches general chatbot usability research recommending that systems display only a small amount of information at a time.

## 3. When you can't meet the exact request, suggest the single closest alternative — and make the case for it

If the exact thing someone wants isn't available (out of stock, fully booked, not quite the right fit), don't recite a list of alternatives — offer the one closest match as a simple yes or no, and frame the bad news together with that alternative rather than as a dead end on its own. Check the relevant constraint throughout the flow, not only at the very end after someone has already committed to a choice.

- **Era: both.**
- **Example.** "That size is sold out right now, but this one runs a touch larger and tends to be what most people in a similar situation end up choosing — want to see it?" is a far better pattern than a flat "unavailable" or a long list of substitutes to sift through.

## 4. Funnel the close — a closed "anything else about this?" beats an open "what else can I help with?"

The closing question should acknowledge that most conversations naturally wind down to an end. A closed "would that be all, or is there anything else about this specific thing?" feels comfortable and complete. A fully open "what else can I help with?" implies there should be more, and leaves the person with an odd, slightly unsettled pause before they can actually leave the conversation.

- **Era: both.**
- **Example.** End a resolved thread with a closed, topic-anchored question rather than a generic re-opener. This small wording choice measurably affects how clean and complete the ending feels.

## 5. Pre-empt the question someone's about to ask

Through testing and real usage, you'll discover the questions people reflexively ask right after a recommendation ("but how much is it," "does it actually work for my specific situation," "how long does shipping take"). Answer these before they're asked, folded directly into the recommendation itself, rather than making someone ask and wait for each one in turn. This keeps the conversation moving instead of forcing someone to repeatedly interrupt with the obvious follow-up.

- **Era: both.**
- **Example.** Don't say "this is a great option" and leave price, fit, and shipping time for the person to ask about one at a time. Fold the one or two most predictable follow-up questions directly into the recommendation itself.

## 6. Default to a hybrid of free text and light structure

Let people type freely, surface the specific topics or actions the system can actually handle, and fall back to simple structured choices when the system is genuinely uncertain what they mean. Trust what people actually do over what they say they prefer: in practice, people often say they prefer open text, then visibly struggle when actually asked to compose a message from scratch. A combination of both tends to beat either extreme on its own.

- **Era: both**, with one caveat: a rigid, button-only fallback is an old pattern. For a capable language model, "structured fallback" can mean a few lightly suggested phrasings rather than a hard button tree, and vary the format so the experience doesn't start to feel like a repetitive phone menu.
- **Example.** Let someone type "something for a dull, blah-feeling room" freely, surface a few relevant categories as light suggestions, and fall back to a short structured question only when the request is genuinely too ambiguous to act on.

## 7. Render multiple structured results as something visual and selectable, not a flat wall of text

When a response returns a genuinely structured set of results — several comparable options — don't dump them as a plain text list. Use cards, a carousel, or similar visual structure with clear action buttons (see details, compare, select) so the results are easy to scan and actually move someone toward a decision.

- **Era: both**, with a frontier to flag: pre-built, hand-authored visual components for common result types are solid, proven craft. Having a model generate a fully custom interface on the fly, in real time, is a genuinely unsolved and still-emerging area — worth experimenting with, but not yet a settled, reliable pattern.
- **Example.** A response returning several comparable options should show up as a scannable visual layout, not a flat text list that makes someone read through every option linearly just to compare two features.

## 8. Match the suggested action to the person's actual mode, not a generic default

Read which mode someone seems to be in: trying to get a specific, known thing done quickly and efficiently; actively comparing and gathering facts; trying to learn something they don't yet understand; or wanting to hand the whole decision to the assistant. People move between these fluidly depending on context. Match the suggested next action to the mode: handing someone who wants the whole decision made for them a self-service comparison tool under-serves them; dragging someone who wants a specific, known thing done quickly through an extended discovery process over-serves them in the wrong direction. When the mode is genuinely ambiguous, offer two or three clear routes rather than betting everything on one guess.

- **Era: agent-era** — this is a sharper, more useful alternative to designing around one fixed persona, made possible specifically by a capable model's ability to read and adapt live.
- **Example.** This over-serving or under-serving mismatch is probably the single most common failure across assistant prototypes generally. Offer a small number of clear routes (a quick pick, a full comparison, a guided conversation) and infer which one actually fits as the conversation unfolds.

## 9. Use suggested options as a scope guardrail, not just a convenience

How you frame your opening prompt controls the scope of what someone says back. "Ask me anything" invites off-topic chaos and an open-ended, hard-to-handle range of requests. "Tell me what you're looking for — are we talking about this category, this one, or something else?" reliably produces in-scope input. For an open-ended system, offering a small set of framed options is a genuine guardrail against drift, not just a nicety.

- **Era: both**, and particularly relevant for a capable, open-ended system that can otherwise wander off-topic easily.
- **Example.** Open a session with a few framed category options rather than a completely blank "how can I help?" that invites anything at all, including requests the system has no business handling.

## 10. Treat unsolicited suggestions as high-risk — gate them on context, confidence, and whether it's actually a request

Volunteering a suggestion mid-conversation ("want me to add this for you?") is situational and can misfire badly if the timing is wrong. Not every message someone sends is a command to act on — someone thinking out loud ("ugh, this has been a pain lately") shouldn't be force-fit into a triggered action. Treat an unsolicited interjection as something to do only when it's genuinely welcome, well-timed, and high-confidence — not as a default behavior. That said, a well-timed proactive suggestion on a clearly earned, high-value moment is a real feature, not an annoyance; the point is to gate it properly, not to suppress it entirely.

- **Era: both.**
- **Example.** The assistant shouldn't jump to "add this to your cart" every time someone muses out loud about a problem. Gate proactive suggestions on both genuine confidence and a clearly earned, high-value moment, and be careful to distinguish an actual request from ambient thinking-out-loud.

## 11. Every suggested action should move the person forward, never dead-end to "go check elsewhere"

A suggestion that just punts the problem elsewhere — "check our website" or "call this number" — hasn't actually solved anything; the person just has to pick it back up somewhere else, so you've paid the cost of the interaction twice without actually finishing it. Solve things within the conversation wherever you genuinely can. When you truly can't, hand off to a person as the next concrete step, carrying real context forward, and stay present afterward so a follow-up question can continue in the same thread rather than restarting cold. Offer that handoff softly and in a way that fits the voice — a plain yes-or-no ("want me to connect you with someone who can help further?"), not a jarring, oversized "escalate now" button.

- **Era: both.**
- **Example.** A complex or sensitive question should route to a person as a soft next step, carrying the person's actual specific situation along with it — never a vague, re-generalized label, and never a bare "go check our help page" with no real next move.

## 12. Discoverability is its own design problem — show, don't just tell, what the system can do

People rarely discover a capability just from a one-line description somewhere; they need a real, concrete example to hit the "oh, it can actually do that" moment. Surface capabilities and follow-ups as specific, concrete suggested prompts rather than an abstract tagline. Keep suggestion labels short and action-oriented. When presenting a set of choices, randomize the order so the first option shown doesn't win just by virtue of position. Follow-up suggestions tailored to what just happened tend to be more useful than generic, static starter prompts.

- **Era: both.**
- **Example.** Open with concrete starter suggestions ("find something for a specific room," "help me plan out a trip") rather than a vague tagline, and offer suggestions tailored to the context right after each response, not just at the very start of the conversation.

## 13. Codify the small, decidable formatting rules once, in a living style guide

Small, mechanical decisions — how buttons are labeled, whether numbers are spelled out or written as digits in button text, how prices and links are formatted, a clear list of words and phrasings to actively avoid — belong settled once, in a living reference document with paired right and wrong examples. Inconsistent formatting reads as low quality even when the underlying content is perfectly fine, and a settled, specific reference is also the cheapest possible lever for keeping quality consistent across a large and growing surface area.

- **Era: both.**
- **Example.** A short, living style reference that bans over-hyped phrasing and unverifiable claims in button and chip copy, standardizes price and link formatting, and gives clear right-versus-wrong examples pays for itself quickly, especially on the mechanical surfaces (errors, fallbacks, confirmations) where voice most often quietly breaks down.

---

The defining tension running through this whole file is density: enough affordance to reduce peak effort and signal whose turn it is, but not so much that it turns into a dense menu dump on one end, or a rigid, repetitive button-tree on the other. The goal is to calibrate, not maximize. One related tension worth carrying into question design and trust-and-expectations work: the general advice to minimize confirmation friction inverts for high-stakes situations — in practice, people often want noticeably more confirmation before anything expensive, irreversible, or safety-relevant, even though the general rule everywhere else is to minimize it.

See also: question-design, recommendation-design, conversation-principles.
