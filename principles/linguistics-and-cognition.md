# Linguistics & Cognition

A conversation, whether spoken or typed, is a joint activity in which both sides continuously update their understanding of each other — not a pipeline that mechanically turns input into output. This file looks at assistant design through a linguistics and cognitive-science lens: where conversational systems actually break when you examine them that way, and what "memory" really means inside a live conversation. A caveat worth stating plainly: the ideas here draw heavily on one detailed treatment of the topic, and while the underlying concepts (shared understanding, turn-taking, how people adapt to each other) are well established in linguistics and cognitive science generally, the specific framing below hasn't been independently cross-checked the way the rest of this playbook has. Treat it as a strong, well-grounded set of hypotheses worth testing against your own conversations, not settled law.

## 1. A conversation is a joint activity, not a pipeline, and people hold assistants to that standard automatically

Model the interaction as two parties continuously exchanging and updating a shared understanding, rather than as a sequence of independent stages (recognize input, understand it, decide an answer, produce output). The cognitive point is important: people have spent their whole lives as communicators inside this joint-activity model, so they apply that same expectation to an assistant automatically, without consciously deciding to. Nobody grants a system a lower bar just because it's software.

- **Era: agent-era** in its framing, though it transfers fully to both voice and text interfaces.
- **Example.** A technically correct exchange that still feels like "ask, get answer, ask, get answer" with no sense of shared progress will feel worse than the facts alone would predict, because it violates the unconscious standard people bring to any conversation.

## 2. Locate a failure precisely before trying to fix it

Give every conversational failure a specific address rather than a vague "the bot is bad." One useful way to think about it: cross two channels (listening and speaking) with four layers — sounds (did it hear the words correctly / is it pronounced clearly), words (did it understand the words / did it choose words the person understands), interaction (did it wait for the right moment to respond / did it speak at the right moment), and the shared mental model (did it grasp what the person actually wants / did it say what they actually need). Almost every specific breakdown has a precise home somewhere on this grid, which turns "it's bad" into a fixable, specific claim.

- **Era: agent-era**, though the "sounds" layer is specific to voice interfaces; the other three layers apply directly to text.
- **Example.** "It misheard the product name" is a sounds/listening failure. "It didn't recognize the slang term for what I wanted" is a words/listening failure. "It cut me off mid-sentence" is an interaction/listening failure. "It recommended something that misses my actual concern" is a mental-model failure. Tag failures by which cell they belong to so the fix targets the right layer.

## 3. The layers depend on each other — one broken layer breaks the whole thing

These layers aren't independent; they have to work in alignment with each other on every single turn. You can't optimize word choice without accounting for timing, and task completion rides on all of them working together. A voice system can have excellent speech recognition and still fail if its turn-taking is off or its word choices don't land. Quality is a property of the whole aligned system, not a set of separately-scored components.

- **Era: agent-era.**
- **Example.** Don't celebrate a great recognition accuracy number or a polished voice in isolation. A system that transcribes speech perfectly but talks over people, or recommends something tone-deaf despite hearing every word correctly, still fails the person using it. Evaluate end to end.

## 4. In a live conversation, the only thing that really persists is the other person's mental model of what's happening

In a live spoken exchange, there's no scrollback: sounds and words vanish the instant they're spoken. What actually persists and grows over the course of the conversation is the shared mental model each party is building. The design implication is significant: the job isn't to keep a perfect internal log for the system's own sake, it's to keep the other person's understanding aligned and correct, which in a voice context means periodically saying the shared state back out loud, since there's no visible transcript to lean on.

- **Era: agent-era**, especially pointed for voice; in text, the visible transcript does some of this work automatically, but it's a mistake to assume the person actually scrolled back and re-read it.
- **Example.** In a longer voice interaction gathering several pieces of information (destination, dates, budget), the system should periodically recap what it has so far ("so far I've got...") before moving to a recommendation or a booking step, rather than assuming the details are still fresh for the person on the other end.

## 5. Cognitive load changes how long a pause should be — never barge in on someone who's thinking

A useful anchor case: asked to read out an unfamiliar reference number, someone slows down because the task itself is unfamiliar and effortful, and a fixed timeout designed around a normal pause length talks over them right when they need more time, not less. The underlying point: unfamiliar or effortful content — spelling something out, reading a long number, trying to recall a detail — naturally produces longer and more variable pauses. A fixed response window is wrong for exactly the moments where someone needs it to flex.

- **Era: agent-era**, with the specific mechanics (detecting end-of-turn, deciding when to jump in) being voice-specific; the transferable lesson for text is simpler: don't fire an unsolicited follow-up message while someone is visibly still composing or clearly mid-thought.
- **Example.** When a voice assistant asks someone to read out a confirmation code or a long reference number, it should widen its patience for a pause before assuming they're done, and if it does mishear something, it should ask for just the part it missed rather than a flat "please repeat that."

## 6. Deliberately share a vocabulary — don't make people learn your internal terms

Among the concrete, practical levers available: actively choose words that both sides of the conversation genuinely share. A classic failure is using an internal or technical term the other person doesn't map to anything meaningful, with no attempt to repair it. Meet people in the words they actually use, and bridge gracefully from their phrasing to yours rather than lecturing them in internal jargon.

- **Era: both** — timeless craft, though a capable model makes live vocabulary matching far more achievable than it used to be.
- **Example.** If someone describes what they want in casual, everyday terms, bridge toward your own terminology rather than replacing their words outright, and avoid surfacing internal terms (inventory codes, system names, internal category labels) the person has no reason to know.

## 7. Adaptation runs both ways and changes over time, not just from the system toward the person

It's tempting to think of adaptation as one-directional: the system reads and adjusts to the person. But the person is also adapting to the system over the course of a single conversation, and across many conversations over months — learning its style, its rhythm, its word choices, which makes them more comfortable using it next time, provided the system is consistent enough to actually learn. And language itself drifts: new slang, new product names, new ways of phrasing requests show up over time, and a system that doesn't get periodically refreshed on that will quietly go stale.

- **Era: agent-era.**
- **Example.** A consistent, learnable voice rewards a returning user by making each visit a little smoother, while an assistant whose personality or phrasing shifts unpredictably resets that progress every time. Separately, plan a periodic refresh — every six to twelve months is a reasonable cadence — to catch new terminology, slang, and changing conventions before the assistant starts sounding noticeably out of date.

---

See also: conversation-principles, context-and-memory, question-design.
