# Sources

This playbook was synthesized from public talks and public guidance on conversation design and AI agent design. Every talk below is public (mostly from the Conversation Design Institute's YouTube channel, which runs free public webinars, panels, and expert sessions), and the one-to-three-line note under each is our own summary of what that specific talk contributed, not a transcript or a reproduction of its content.

A handful of entries below are marked "skipped" — the source video was private, had no transcript or usable captions, or turned out to contain no conversation-design content on inspection. We're listing them anyway for completeness rather than quietly dropping them.

Grouped by the principle file each talk mainly informed. Some talks touch several areas; we filed each under its single best-fit theme rather than duplicating it.

---

## Core conversation principles

- **Esther Horowitz, with Hans van Dam and Gary Priddy** — [Microsoft Workshop: Best Practices for Envisioning & Designing Conversation Design](https://youtu.be/-Dl1mtgTAjc)
  A Microsoft content designer's five best-practice pillars (understand/focus on the user, keep it simple, use the right tools, be inclusive) are fairly standard, but the live Q&A adds sharper, durable advice: test a handoff by asking "would this make sense if a human were briefing another human," and never silently default when you can't fully accommodate an inclusive design goal.

- **Jesse (Conversation Design Institute)** — [Shorter isn't always better.](https://youtu.be/11Gkxhx1kdw)
  A brief clip making one clean point: don't treat turn-count as the success metric. Compressing a flow to be as short as possible can make it unclear or unnatural; the real goal is the user reaching their goal smoothly, not minimizing length.

- **Deborah Akinyele** — [Transform the Patient Experience with Conversational AI](https://youtu.be/4qb1VyRj2oU)
  A clinician-founder maps a four-stage user journey (discovery, intake, screening, treatment/follow-up) and argues information can be "available" without being accessible or digestible — a bot's real job is making existing information usable in the moment. Also stresses matching not just a user's language but their specific regional variant, and shifting tone and information density when someone sounds overwhelmed.

- **Hans van Dam** — [Conversation Design Fundamentals Expert Class](https://youtu.be/6bqbLiRRn78)
  A dense solo teaching session built around a repeatable turn-shape: acknowledge what the user said, confirm your understanding of it, then deliver one clear next prompt — never ask a question and keep talking past it. Also introduces role-play and small-sample "Wizard-of-Oz" testing as cheap ways to surface design gaps before building, and an editing discipline of cutting roughly half the words out of a first draft.

- **Elizabeth Stokoe (with Saul Albert & Cathy Pearl)** — [Asking for things is more complicated than you think (request architecture)](https://youtu.be/9vzbGxsmOHk)
  Drawing on decades of real recorded service calls, this talk shows that human requests are rarely a clean "ask" — they arrive wrapped in pre-, insert-, and post-expansions, and roughly a third of the time no explicit request ever appears at all, just a described problem that gets answered with an offer. The practical lesson for bot builders: design for whatever a person says first, including hedges, barriers, and non-literal references, rather than forcing them into a single intent-shaped request.

- **Uncredited CDI presenter** — [CDI Course Materials Tour](https://youtu.be/aq-uUBoRbgk)
  Mostly a product tour of a training catalog, but it states a durable design doctrine plainly: design the ideal conversation first, independent of technology, then decide per-part whether a generative or a tightly controlled scripted approach delivers it. It also makes the point that with generative systems the designer's job shifts from writing dialogue to verifying the model actually produces good turn-taking, confirmations, and empathy.

- **Elizabeth Stokoe** — [Types of human interruption and overlap](https://youtu.be/ET9PlpxZDGM)
  Using real call recordings, this talk shows that "interruption" is actually a family of distinct overlap types, most of which are collaborative rather than hostile, and that forcing a user to interrupt a system's closing in order to extract the information they called for is measurably linked to lower satisfaction — a concrete argument for always surfacing the outcome before wrapping up a conversation.

- **Taylor Merriam** — [The New Building Blocks of Conversation](https://youtu.be/gCc_akZ6C2s)
  Uses a LEGO-turnaround analogy to argue that intent-era fundamentals (accuracy, brand voice, speed) still matter but are becoming table stakes; the new differentiator is reading a user's "behavior mode" (execute/investigate/learn/delegate) and matching response style to it. Introduces cognitive vs. affective empathy as the line past which a bot claiming to "feel" tips into the uncanny valley, and argues unstructured, volunteered context is a trust signal worth designing to invite.

- **Conversation Design Institute (instructor unnamed)** — [Psychology of Conversations | Conversation Designer](https://youtu.be/GfA0mjixRKM)
  A foundational lecture applying Grice's four conversational maxims (quality, quantity, relevance, manner) as a rubric for judging any agent turn. Full of concrete before/after fixes, e.g. replacing "please answer using a number" with a natural re-ask like "how many rooms was that?" — redesign the turn rather than policing the user's input format.

- **Conversation Design Institute (uncredited narrator)** — [What is Conversation Design? | Conversation Designer](https://youtu.be/iedSuJwAS-E)
  An intro-level definition framing conversation design as sitting at the intersection of technology, psychology, and copywriting, serving both the system's need for structured input and the human's need for empathy and reassurance. Its most durable point: as AI takes over more of the actual dialogue, the designer's job shifts from writing every line to setting the parameters and boundaries within which the AI operates.

- **Conversation Design Institute (uncredited presenter)** — ["It's not what you say. It's how you say it."](https://youtu.be/kAzgCPu4SPQ)
  A short promo asserting that message delivery structure, not just content, determines whether a response lands — and that for generative systems this becomes a checklist to verify the model's output against known-good communication patterns, rather than a script to hand-write. No concrete patterns are given in the clip itself.

- **Conversation Design Institute instructor** — [When conversations flow, users stay engaged.](https://youtu.be/lf4h5dLzqk8)
  A short, concrete lesson on turn-taking: don't dump an entire menu of options into one message. Break content into digestible pieces and close each turn with a single simple question so the user always knows it's their move.

- **Unnamed guest, interviewed by CDI** — [Why standards matter in conversational AI](https://youtu.be/MPpF4DyE_ck)
  A short clip arguing good conversation-design standards work at two altitudes at once: hold a small set of universal principles (clarity, respect, consistent tone) fixed everywhere, and let only the contextual layer flex — roughly an 80/20 split between shared fundamentals and situational calibration.

- **Hans van Dam & Willem** — [Standards in Conversation Design Expert Class](https://youtu.be/N-0W4Qqi5pQ)
  A pre-LLM but still-useful session built around a simple turn-shape mantra — acknowledge, confirm, then prompt the next step — plus the principle that repair should escalate with detail rather than repeat "try again," and that a conversation should never simply dead-end. Its sharpest transferable idea is an evaluation warning: testing a model only against cases your own team wrote, rather than real and drifting user language, can make quality look like it's improving while it's actually getting worse.

- **Conversation Design Institute** — ["Users shouldn't have to wonder:"](https://youtu.be/Pvz6RSXICJA)
  A short teaser making one clean point with a before/after example: brevity is cognitive-load reduction, not a word-count exercise. Cuts ceremony, filler, and invented-sounding justifications ("per regulation...") for routine questions, since those read as padding at best and as a fabricated policy at worst from a generative system.

- **Hans van Dam** — [Conversation Design Fundamentals](https://youtu.be/T3ZO4v8Wut8)
  A dense, practical session built around a shopping-advisor example. Central framework: every message should acknowledge what was understood, implicitly confirm it (catching misreads before they compound), and end with exactly one clear question — never a question buried mid-message. Also argues empathy is a functional ROI lever (angry or anxious users become uncooperative and harder to help, not just unhappy), that "boring" bots people barely notice are usually the best-designed ones, and offers concrete self-checks: read a line aloud, see if it fits in one breath, and trim words one at a time until meaning breaks.

- **Cathy Pearl** — [The current state of voice/chat barge-in](https://youtu.be/xGpInoDJAdk)
  A voice-UX veteran's take on interruption: the hard problem isn't detecting an interruption but "addressivity" — knowing whether input was even meant for the system at all, as opposed to ambient chatter. Her sharpest point is that an assistant should mimic human conversational timing only where testing shows it works, not by default, since machine-speed replies can cause more cross-talk than a tuned pause.

- **Two unnamed CDI panelists** — [Where conversational AI is really headed](https://youtu.be/XlYKwZ34Jow)
  Argues a conversational agent's job is goal-completion, not sounding human — the same way movie dialogue isn't a transcript of real speech but distills the elements that read as natural while staying efficient. Also flags that so much meaning lives in tone rather than words that flattening speech to text is a real ceiling for current systems.

- **CDI-hosted conversation-analysis researcher** — [Should we be able to interrupt a CUI... and should a CUI be able to interrupt us?](https://youtu.be/yscZjnG0VUI)
  An academic conversation-analysis talk arguing the real design problem is turn-taking — "who gets to do what next" — rather than interruption as a single on/off mechanism; a crude stop-token (like a wake word) works narrowly but breaks down in messy real-world settings (e.g., multiple devices cross-triggering each other). Also raises, as a speculative but legitimate design surface, the case for a system interrupting a human when it adds clear value and is done in a way that protects the person's social standing.

## Recommendation design

- **Conversation Design Institute** — [Conversational AI in 2026: what we think still matters](https://youtu.be/Z4R17a8YC_o)
  A brief clip arguing that when a conversation fetches structured results (like a set of products), it should render them as dynamic, selectable UI — carousels and buttons — rather than a flat text list, while noting that generating this kind of rich UI dynamically at runtime with an LLM (versus pre-authoring it) is still an open, unsolved problem.

## Suggested actions and affordances

- **Conversation Design Institute instructor** — [Use Cases for Increasing Motivation | Conversational Copywriter](https://youtu.be/4DRg2i9k4QA)
  A curriculum-overview video naming a three-phase persuasion structure (spark interest, persuade, close) and a key conditional: match persuasion intensity to how motivated the user already is, since over-persuading an eager user reads as friction and manipulation. Several of the specific named techniques (urgency, loss aversion, anchoring) are flagged as ethically double-edged for a trusted advisor use case.

- **Cindy** — [Features don't create value. Integrations do!](https://youtu.be/nwMxH7suFw0)
  A short, promotional clip with one clean idea: an assistant creates real value through integrations that complete actual tasks, not through adding flashy features — and offering an action the system can't actually fulfill breaks trust worse than never offering it at all.

## Context and memory

- **Daniel Padgett** — [It Goes Without Saying](https://youtu.be/8AgGwR1jUeI)
  A Google DeepMind research lead proposes that natural conversation rests on building common ground from three sources — shared history, general knowledge, and present context — and then picking one of three moves based on how strong that signal is: ask when it's weak, confirm when it's aging, or just act when it's strong and repeated. Also argues memory should be inspectable and user-editable, not just a silent log.

- **Jasper Climby & Bosra** — [Conversational AI — Lessons from the Real World](https://youtu.be/cRtd6v9ysPI)
  The standout finding here is a precise mechanism for retrieval-based hallucination: when several source documents correctly describe the same thing in slightly different ways, a generative system fuses them and quietly invents "connective tissue" to smooth over the discrepancies, producing a confident wrong answer from entirely correct sources. The fix is deduplicated, well-organized source knowledge, ideally structured as clean question-answer pairs, plus keeping scripted or human-routed paths for legally sensitive or emotionally high-stakes moments.

- **Karen Kaushansky (Gemini Live, Google DeepMind)** — [Designing Multimodal AI Agents](https://youtu.be/f6QSrFlZUjU)
  Argues that "conversation" now means the whole multimodal signal — gesture, gaze, and especially camera input — not just the spoken or typed turn, illustrated by an assistant reading a sewing pattern over video and translating it into the right technique in real time. Because the underlying model's output can't be fully controlled, her practical takeaway is that design leverage lives on the input/context side: feed the system the right grounding, rather than trying to pin down exact responses.

## Agent boundaries and control

- **Shauna Griffin** — [Beyond the Single Agent](https://youtu.be/1PzLOuemTto)
  A Rasa practitioner's talk on multi-agent sprawl inside large organizations: a router merely picks the next action, while a true orchestrator also maintains state and hands off the right context, so users are never asked to repeat information they already gave. Argues evaluation scenarios should be mined from real production failures, not invented, and checked in as permanent regression tests.

- **Yam Marcovitz** — [Building Predictable Conversational AI: Design, Engineering & Control](https://youtu.be/2SLhDtr0DNY)
  The creator of an open-source agent-control framework frames reliability as a sliding scale between deterministic safety and natural flexibility, and argues teams should ship near the controlled end and relax gradually against real traffic. His sharpest point: LLMs take instructions literally, so small wording choices (does "ask for X" mean ask once, or keep asking?) silently decide agent behavior — precision in phrasing is itself a craft skill.

- **Hans van Dam, Paul Lewis, Naana Follestad, Henry Vaage Iversen** — [1 Year After The Launch Of ChatGPT: What Are LLMs' Impact On Conversational AI?](https://youtu.be/8h_WgKnLFq0)
  A late-2023 panel of enterprise practitioners proposes judging generated output against three separate bars — is it accurate, is it legal, and is it actually desirable (right length, right vocabulary, right tone) — noting most teams only check the first two. Recommends sorting use cases by how costly a wrong answer would be, and keeping the lower-stakes, more flexible ones on generative AI while anything high-consequence stays deterministic.

- **Jasper Klimbie** — [Give your AI assistant LLM superpowers](https://youtu.be/8Nq7n21t2gc)
  A practitioner's hands-on account of blending generative answers into an existing rule-based assistant: script anything business-critical or legally sensitive, and let generation handle the long tail, always grounded in a known-correct source. His sharpest finding is that a model must be explicitly permitted to say "I don't know" — otherwise it will always try to generate *something* — and that document formatting (plain Q&A-style text beats a dense PDF) measurably changes retrieval accuracy.

- **Jesse (CDI)** — [Conversational AI isn't a single system—it's an ecosystem.](https://youtu.be/c5_zd_o9U4Y)
  A short framing clip arguing that a conversational AI product is really an architecture of dependencies — integrations, data flows, downstream workflows — and that skipping that mapping before building is what produces "unmanaged risk and confused teams," a dynamic that is if anything more true for tool-using agents than for a single simple bot.

- **Allegra Guinan (Lumiera)** — [Architecting Responsible AI](https://youtu.be/f7SqTMfnLrA)
  Makes a strong architectural argument that interface-level conversation design cannot fix decisions made wrong further upstream — in business objectives, training data, or escalation rules — and that most interface failures are quiet ones (a system that doesn't escalate when it should, or sounds falsely confident) rather than dramatic errors. Proposes a simple discipline: name where quality decisions actually get made, assign one accountable owner per system, and reopen the review at fixed checkpoints and on any material change to the model or data.

- **Divyanshu Jain, interviewed by Hans van Dam** — [Scaling Delivery in Conversational AI: Beyond Demos to Real-World Systems](https://youtu.be/gVCLgLVFxH4)
  Argues the designer's job has flipped: in the old intent-matching era the challenge was getting an assistant to do more; with LLMs the challenge is constraining it to do less and stay inside its intended scope. Also proposes "information gain per answer" as an inspection metric — judging a response by how much real information it packs in rather than just whether it's on-topic — and warns that celebrating rising automated-call volume is usually the wrong metric; falling total contact volume is the real win.

- **Guillermo Vasquez** — [Building Reliable AI Agents: Lessons from the Trenches](https://youtu.be/JgDDvGGrQ8w)
  From years of building voice/chat agents for small businesses: route probabilistic work (understanding, phrasing) to the AI and deterministic work (bookings, exact dates, calculations) to code, and keep tuning that boundary — most failures come from builders overestimating what the AI side can reliably do. Notes LLMs are "time-blind" (they resolve relative dates against a frozen training-time calendar) and that a fluent-sounding demo can still fail most real tasks, so success should be measured against a hard completion rate on adversarial real users, not a scripted walkthrough.

- **Yam Marcovitz** — [Unprompted | Building Predictable Conversational AI with Yam Marcovitz of Parlant](https://youtu.be/kdFGQ_4MnSQ)
  Argues that getting an AI agent to behave as a specific organization wants is not solved by a better base model — it requires someone to explicitly articulate what's acceptable in that context, and that person needs real domain skill, not just presence. Memorable framing: "AI is automated human intelligence, so the automation is only as good as the person you automate for." Also argues agents should absorb messy real conversation (multiple questions at once, topic switches) gracefully rather than making the user feel like they're navigating a hidden decision tree.

- **Rebecca Evanhoe** — [Designing Hybrid Conversational AI: Why Hybrid Beats Fully Generative](https://youtu.be/lGvcjA7xjx0)
  A dense, practitioner-grounded case for hybrid architectures: give large language models small, focused jobs rather than the whole conversation, and decide module-by-module (with real A/B data) whether a deterministic or generative approach wins. Also lays out a dataset-driven evaluation method — enumerate real utterance variants, test across them, grade by hand, then switch to an automated judge once performance stabilizes.

- **Grace Hughes** — [Unintended Consequences of AI | With Grace Hughes](https://youtu.be/m-JQ6HoruQE)
  Advocates running an "unintended consequences" workshop early in any project, with a diverse group surfacing what could go wrong for users, the business, and the technology — then turning those findings directly into system guardrails and a living risk register. Also argues a persona that's too agreeable or too human-like is itself a safety risk, not just a brand choice.

- **Greg Bennett** — [Advocating for and Building a Conversation Design Practice in Enterprise During the LLM Era](https://youtu.be/MN7OJQGrUnE)
  Argues that large language models shouldn't be used to retrieve facts they can't actually know, and that detected prompt-injection or jailbreak attempts should be routed to a dead-end response rather than sent to the model at all. Also makes a sharp point about tone instructions: telling a model to "be nice" just reproduces one dominant cultural register, whereas specifying concrete linguistic behaviors gives it something it can actually act on.

- **Steve Bell (Verint)** — [The Broader Role of Conversational AI in CX Delivery](https://youtu.be/ozhPQyxy4x4)
  Argues for blending automation with humans rather than full replacement, and for deciding deliberately which turns should be scripted versus generated based on compliance risk. Introduces the idea of "moving the decision, not the customer" — resolving an out-of-policy request with a quiet background approval instead of a jarring handoff — and argues teams should score AI and human agents with the same quality rubric and track dollar value delivered, not just how many conversations were contained.

- **Wilf Blackburn (Dignify X)** — [Technology in Service of the Human](https://youtu.be/pHNC2XGZ5pg)
  A business-leader case study on an AI coaching tool for financial advisers. Central idea: design the agent to help a person think and reflect, never to do the thinking for them — if the human just reads the machine's output, you've built the opposite of what you intended. Frames guardrails as enablement (a fence that lets you roam safely) rather than punishment, and argues that when a model's output can't be made fully predictable, you govern the process — transparency, explainability, auditability — instead of promising precision.

- **Pernille Hansen (Ultimate.ai)** — [Implementing better CX with generative AI](https://youtu.be/tgjgoMmHmpg)
  A product demo webinar whose operationally useful points are: ground answers in an approved knowledge source by default and treat "let the model answer from its own general knowledge" as a risky, off-by-default setting; keep safety guardrails on regardless of how open the grounding is; and personalize answers by pulling in a specific person's own account/order data before generating a response, rather than giving a generic answer to everyone.

- **Steve Bell (Verint)** — [Harness the Power of AI Automation to Deliver Winning CX](https://youtu.be/Vyvwg2IuMnU)
  A contact-center vendor talk arguing automation should be scoped as small, single-job, measurable workflows grounded in curated, trusted knowledge rather than "set free" on open information. Key practices: keep source documents one click away when the agent summarizes them, hand a human a session summary rather than a raw transcript on escalation, and QA conversations semantically ("was it accurate, on-brand, compliant?") at full scale rather than sampling 1%.

- **Hans van Dam & colleague (CDI leadership)** — [Conversational AI in 2025: What every team needs to know (Highlights)](https://youtu.be/y_-fqcZzJHo)
  A keynote framing that distinguishes the autonomous "agent" doing backend work from the "assistant" — the conversational surface a customer actually talks to — arguing the two need separate design attention. Its central design question for any generative system: what happens when it goes wrong, since failure-handling, not the happy-path demo, is where the real design work lives.

- **Mark van der Heijden (Bol.com)** — [Changing a Winning Team](https://youtu.be/yINZFv_g6Xc)
  A large retailer's candid account of moving a long-running service bot from a single do-everything bot toward specialized, cooperating agents — "one bot to solve it all didn't work," while a swarm of undifferentiated agents is equally wrong; you need distinct roles. Other durable lessons: set escalation thresholds low so one failed attempt hands off to a human rather than risking frustration, and treat small wording changes as a measurable, high-leverage lever (one added sentence setting shipping expectations measurably cut support contacts) worth A/B testing like any other feature.

## Failure and recovery

- **Cathy Pearl, Elizabeth Stokoe, Saul Albert** — [How should conversation design deal with interruption?](https://youtu.be/8Lco7v8HyIw)
  A voice-design practitioner and two academic conversation analysts argue that "I don't understand" is a trap response — it just makes a user rephrase forever — and that a good recovery names what the system can't do and offers an alternative, with a clear path to a human. They also reframe interruption as a functional, often collaborative overlap rather than inherently rude, and cite real data linking how often a caller has to interrupt an agent to lower satisfaction scores.

- **Hans van Dam, interviewed by Peter Thomas** — [Honest Recovery](https://youtu.be/BA4pUAbfGFo)
  A short but clear case for honest failure handling in AI systems: admit "I don't know" rather than fabricate an answer, and calibrate an apology's intensity to the real stakes of the error rather than applying one tone everywhere. Its most counterintuitive point is that owning uncertainty tends to build more trust than projecting confidence.

- **Joseph Bano, Luke Kempen, and team** — [Solving Real Problems with RAG](https://youtu.be/Dffgx7zJbBs)
  Only an introductory clip, but it frames its retrieval-augmented chatbot build around real cautionary tales — a car dealership bot talked into "selling" a vehicle for a dollar, an airline bot that invented a refund policy — as the reason unconstrained generative systems need guardrails against asserting commitments or policies they cannot actually ground.

- **Hans van Dam & Peter Thomas** — [Trust Breakers | With Hans van Dam and Peter Thomas](https://youtu.be/K1V11QYsWJQ)
  Argues a confidently-wrong answer is an outsized, often permanent trust violation that many good interactions can't offset — especially damaging because an AI agent is the brand's whole storefront, unlike one human rep having a bad day. The fix: underpromise capability (state a narrow scope rather than "ask me anything") and raise the confidence threshold for deferring to a human or admitting uncertainty as the stakes of being wrong go up.

- **Conversation Design Institute (uncredited narrator)** — [Why do some AI assistants feel helpful while others feel frustrating?](https://youtu.be/KfNvL3-ECoU)
  A brief before/after on refusal language: swapping a flat "I can't do that, try again later" for an empathetic, time-bounded refusal with a proactive follow-up offer ("I can't do that right away — want me to let you know when I can?") turns a dead end into a continued relationship. Also flags a guardrail: express understanding of the user's situation without the assistant pretending to have feelings of its own.

- **Gabriëlla Martijn** — [What Bots and Stakeholders think of each other](https://youtu.be/Lh5A3q_69lI)
  A research-grounded talk on handovers from bot to human: an escalation only works if it carries the customer's *specific* intent (not a re-generalized topic) and happens fast — many handoffs fail because the human agent never reads the bot's transcript and makes the customer repeat themselves.

- **Cathy Pearl, Elizabeth Stokoe, Saul Albert** — [Should Conversational User Interfaces Make Human "Errors"?](https://youtu.be/P3SWIdF18I4)
  A rich, research-grounded session bridging conversation analysis and voice/chat design. Key ideas: repair should target the specific misunderstanding rather than issue a generic "sorry, I didn't understand"; fixes should be embedded in the answer rather than forcing a detour; confirmation strictness should scale with the stakes of the action; and an agent that's corrected on a remembered detail should pivot gracefully rather than defend itself. Also flags that a language model's token-level confidence has no real relationship to whether its answer is factually correct.

- **Conversation Design Institute** — [Every AI system will fail at some point.](https://youtu.be/VlxL8vC5kME)
  A minimal teaching clip on "dead ends" — turns that leave a user with no message, no next step, and no option. Its sharpest observation is that dead ends often hide right after a successful answer (a user's benign "okay" triggering a confused fallback), not during the hard part of a conversation.

## Trust and expectations

- **Daniel Layne** — [Why We Haven't Built Our Conversational Interface](https://youtu.be/8KlsA3mUM3I)
  A software founder explains deliberately delaying his company's conversational build to pay down "content debt" and "skill debt" first, since user trust is destroyed far faster than it's rebuilt. His most useful idea: a technically correct answer can still fail because it's phrased outside a user's own "web of meaning" — the same word can carry different meanings to different user groups, and that mismatch is a distinct failure mode from factual error.

- **Jesse (CDI)** — ["AI isn't a magic bullet."](https://youtu.be/BVZe_ZJWX1M)
  A brief but sound reminder that overestimating what an AI system can reliably do leads to disappointment and wasted build effort, so calibrating expectations to the technology's real capabilities belongs at the scoping stage, not as an afterthought.

- **Hans van Dam & Pete Tombs** — [Not measuring | With Hans van Dam and Peter Thomas](https://youtu.be/FgP8w9aKCuY)
  Argues that trust functions like a compounding balance-sheet asset: every interaction with an AI system either adds to or withdraws from it. As AI makes products easier to copy, trust becomes the actual differentiator, so organizations should name a single owner accountable for the customer relationship rather than only tracking transaction metrics.

- **Hans van Dam** — [Conversational Capital and the Future of AI](https://youtu.be/gINTyMR490g)
  Proposes that trust compounds slowly but collapses suddenly, so a single bad interaction pattern repeated at scale can wipe out many good ones. Introduces "content debt" (a polluted knowledge base poisons every agent that draws on it) and argues capability (agency) and warmth (empathy) must scale together, or the investment is wasted.

- **Hans van Dam & Peter Thomas** — [Capital Ledger | With Hans van Dam and Peter Thomas](https://youtu.be/i1lDUfdMgCI)
  Proposes scoring real conversation transcripts as deposits (right answer, delivered with confidence, something positive) or withdrawals (loops, contradictions, deflections) to build a concrete "trust ledger" instead of relying on vibes. Argues a smarter, more autonomous AI needs *more* human oversight and measurement, not less, and that automation decisions should be gated on whether they build or erode trust, not just on whether they're technically feasible.

- **Clara Rizzo & Aura Hita** — [From Support Chatbot to Conversational Commerce](https://youtu.be/LHRiJ-TS638)
  A retail team's account of moving from intent-matching chatbots to a generative assistant: the stated question is rarely the real problem, so the goal shifts from detecting intent to resolving the actual situation. They treat trust as the only metric that matters and call out "people-pleasing" — a model agreeably confirming something false — as the central failure to guard against.

- **Karen Kaushansky** — [Designing Multimodal AI Agents: Inside Google DeepMind's Gemini Live](https://youtu.be/NvWEEcoFm94)
  A frontier-lab UX lead describing how conversation design changes when the system's output is generated rather than scripted: trust is built in layers (be factually correct, show your sources, then layer on genuine usefulness), with sourcing shown prominently to new users, receding once trust is established, and resurfacing at high-stakes moments. Also warns that conversational richness without real ability to act just creates disappointment.

- **Hans van Dam & Peter Thomas** — [Emotional Debt | With Hans van Dam and Peter Thomas](https://youtu.be/OqkXDjjPthI)
  Introduces "emotional debt" — the idea that small bad interactions (rude, clumsy, contradictory, or indifferent responses) accumulate invisibly and eventually come due, even while dashboards look fine. A rising "containment" or deflection number can mean the system is curtly causing people to give up rather than actually resolving anything, and a customer who goes quiet should be read as a warning sign, not reassurance.

- **Peter Thomas & Hans van Dam** — [So This Happened | With Peter Thomas and Hans Van Dam](https://youtu.be/OsSGTVJsfR8)
  Frames a maturity ladder for conversational systems — functional, trustworthy, empathetic, memorable, resonant — and argues most deployed assistants plateau at merely "correct but cold." Introduces the idea that in generative systems you no longer author the conversation directly; you design the conditions (content, guidelines, context) that let the right conversation emerge, measured against a signed-off "ideal conversation" baseline.

- **Hans van Dam & Peter Thomas (CDI)** — [Holonic Stack](https://youtu.be/QVG4rCwJ3q4)
  Proposes a five-level maturity model for conversational systems — functional, trustworthy, behavioral, contextual, memorable — where each higher level must fully carry and keep clean everything below it, rather than replacing it. A stale, poorly-written answer left over from an earlier stage can surface mid-way through an otherwise sophisticated, high-trust conversation and do outsized damage — the fix is to finish and audit the lower level before building the next, and to resist chasing "more agentic" for its own sake.

- **Hans van Dam & Peter Thomas (CDI)** — [The Aftertaste](https://youtu.be/rI9rPFgF8xE)
  Argues that the real value of a conversational interaction is created after it ends — in what the person remembers and how they feel — and that standard success metrics (resolution, containment) completely miss this. A technically "successful" interaction that leaves someone unsure or repeatedly confused is a trust withdrawal even though it counts as a win on the dashboard; a short, clear, reassuring close is a disproportionately large trust deposit.

- **Hans van Dam; Peter Thomas** — [What is Conversational Capital?](https://youtu.be/u_EjJSF67aA)
  Frames customer trust as an asymmetric bank account: good interactions make small deposits, but a single bad one (wrong info, a dead-end loop, an unnecessary escalation, indifference) is a disproportionately large withdrawal. Argues existing satisfaction metrics miss this asymmetry and that teams need a composite "trust" measure instead.

- **Conversation Design Institute** — [In 2026, "truthful" responses aren't enough](https://youtu.be/vApGj2Cii2Q)
  A brief trend note arguing that truthful, on-brand output is only the floor for a generative assistant, not the ceiling. The next bar is a multi-dimensional check per answer: is it compliant, safe for the user, safe for the business, and does it actually move the conversation forward in a way that builds trust.

- **Hans van Dam; Peter Thomas** — [Moments Worth Screenshotting](https://youtu.be/Zfobw_uDF0w)
  Argues the bar for a memorable AI experience is whether a customer would actually screenshot and share it — merely solving the problem competently isn't enough. The sharpest point is sequencing: delight requires a prior baseline of trust and real capability, or it backfires and looks like an empty gesture; delight should also be placed rarely, at a genuine emotional release point in the journey, since advertising or overusing it destroys the effect.

## Testing and evaluation

- **Thomas Kuruvilla & John F. Andersen** — [Safe & secure enterprise CX in the age of AI](https://youtu.be/232QPtaCauI)
  A vendor walkthrough of building a retail-knowledge assistant that reframes "hallucination" as any answer that's inaccurate, irrelevant, or unclear — not just factually false — and argues it has to be caught at every stage (before, during, and after generation), including a dedicated fact-checking step distinct from retrieval grounding. Also makes the case for firing several narrow, single-purpose prompts in parallel rather than one big multi-task prompt.

- **Unnamed veteran practitioner (Conversation Design Institute)** — [Enduring lessons across the eras of conversational AI](https://youtu.be/7WwuE6xiSqY)
  A practitioner active since the early 2000s argues the hard-won lessons from each technology era still apply: know your exact target outcome before building, treat data quality as everything, and never act on an unresolved, ambiguous request — especially not with an irreversible action. Pushes measurement past a single "containment rate" number toward categorizing *why* things fail and tracking change over time.

- **Rebecca Evanhoe** — [Career Building in Conversational AI: Portfolios, Positioning, and Progression](https://youtu.be/9U3Y6kP7mCE)
  A voice-AI practitioner describes migrating a working rule-based phone system to LLMs one small, focused job at a time (intent routing, entity extraction, single-sentence replies), A/B testing each piece against the deterministic version and keeping only the ones that measurably win. Her core evaluation method: build a dataset of real user phrasing crossed with varied business scenarios, grade it for accuracy by hand, then graduate to an automated model-judge — applied first to a "does it ever lie about a basic fact" test.

- **Willem Don & Hans van Dam** — [Empowering AI Trainers w/ LLMs](https://youtu.be/9yFhJEue-6E)
  An early, practitioner-level walkthrough of using an LLM to speed up the grunt work of building and testing a bot — generating synthetic test questions, batch-labeling them, and treating the human expert as a validator rather than an author. The standout idea is a "guardrail" layer that checks generated output against tone/brand/compliance rules and regenerates on failure, an early articulation of what later became standard LLM output-validation practice.

- **Lauren Goerz (Rasa) and a Parlant framework founder** — [Optimizing AI: Strategy, Collaboration & Real-World Impact](https://youtu.be/B3NWyXMRr88)
  Two vendor practitioners converge independently on the same hard lessons: LLM agents take instructions literally so wording matters more not less, regression suites with LLM-judge assertions are the real safety net for a nondeterministic system, and reviewing how fast you can fix a live incident matters more than chasing pre-launch perfection. Also useful: measure by which topic/flow a conversation actually reached, not just its tagged intent, and read transcripts rather than trusting dashboards alone.

- **Elena, hosted by William (CDI)** — [Evaluating LLM-based chatbots: A framework for reliable AI assistants](https://youtu.be/ExA3KSvyzpM)
  A dense, practice-grounded framework for testing generative chatbots: define what "good" looks like and write tests before writing the prompt, build real production-derived test sets rather than only imagined ones, and — its most distinctive contribution — evaluate whole-conversation structure, since the correct response to an identical phrase can flip depending on what happened earlier in the conversation. Also stresses that an LLM-judge must itself be validated against human labels before it can be trusted.

- **Alice Kerly** — [Why The Fundamentals Still Matter](https://youtu.be/H89JveEu-Ss)
  A 20-year practitioner's "four-era" lens for sorting which lessons from chatbot history still apply: clarity of purpose, data quality, and measuring beyond containment rate remain constant even as the tech changes. Flags that LLMs make bad data more dangerous, not less, because a model will deliver a wrong answer fluently and confidently instead of visibly breaking.

- **Unnamed CDI interviewee** — [Where empathy shows up in real systems](https://youtu.be/nPzw5aovH2w)
  A one-minute anecdote whose real point is a process insight: empathy for real users isn't a value statement, it's a byproduct of a habit — specifically, a standing ritual of reading actual post-launch conversation transcripts rather than only reviewing the idealized design.

- **Willem Don** — [How LLMs help you right now](https://youtu.be/onK2etRzwcE)
  An early (2023), somewhat dated webinar on bolting a language model onto an existing system, but its best idea holds up: generated output doesn't eliminate work, it shifts creation effort into review effort, and that review cost is routinely under-counted. Its most memorable moment is the presenter catching himself dismissing a real quality problem as "fine for a first pass" and then admitting, on reflection, that it wasn't.

- **Anouck Braggaar & Willem Don** — [Evaluating Conversational AI Systems: Constructs, Metrics and Solutions](https://youtu.be/Q4R3Sl24vlo)
  Transcript could not be retrieved (rate-limited captions); based on the stated topic only, the talk addresses how to define measurable constructs (task success, satisfaction, error/repair) and choose appropriate metrics for evaluating dialogue systems — a relevant angle for building eval frameworks, but the substantive content here could not be independently verified.

- **Darren Ford** — [From Data to Impact: Measuring Agent Success in the Generative AI Era](https://youtu.be/QUGHum13Uv4)
  A thin, promotional clip, but it lands one useful distinction: measure true resolution (the user's issue actually got solved) rather than deflection or containment (the user simply didn't escalate to a human), and validate any new resolution metric against an existing trusted measure like first-contact resolution before believing it.

- **Henry Vu & Hans van Dam** — [Unlocking Chatbot Success: Navigating the Maturity Path of Analytics and Reporting](https://youtu.be/qvt_TB0erhM)
  A vendor webinar with a genuinely useful diagnostic discipline underneath: dashboards tell you *what* happened, not *why*; get to *why* by drilling from a signal (a metric moving) down into the specific subset of conversations it represents, rather than reading transcripts at random. Repeatedly warns against blaming the bot for a problem that actually originates upstream (confusing marketing copy, a product issue, poor page placement) and stresses that a correctly-routed conversation can still fail because the wording was unconvincing.

- **Darren Ford** — [From Conversations to Insights](https://youtu.be/ryVIT0w1y50)
  Makes the case that organizations can measure activity (volume, containment) far more easily than quality, and that chasing a surface metric like containment can actually make the real experience worse while looking better on a dashboard. Tells a concrete cautionary case: a contact center's containment numbers were rising while customers were quietly abandoning the automated channel and calling in anyway — a failure the metric was structurally blind to until it was cross-checked against an independent measure.

- **Elena Kupriyanova; William (CDI host)** — [Teaser — Evaluating LLM-based chatbots: A framework for reliable AI assistants](https://youtu.be/VTpsPWS7R4c)
  A teaser arguing that LLM output is non-deterministic, so eyeballing a few good responses proves nothing — you need real evaluation. Its most useful idea is to triage failure modes by frequency times impact: rare failures like bias, jailbreaks, or data leaks deserve outsized eval coverage precisely because they're low-frequency but catastrophic.

- **Conversation Design Institute** — [When you're running thousands — or millions of automated conversations, quality can't be accidental](https://youtu.be/vvJqG2PgtCs)
  A short promotional framing arguing that at high conversation volume, quality must come from a reusable, two-layer pattern library (generic linguistic patterns plus an organization's own tone-of-voice layer) rather than one-conversation-at-a-time review.

- **Stephen Broadhurst (Humans First)** — [NLU Design — Never ignore what your technology and users are telling you](https://youtu.be/X1qqvyvaSEo)
  Argues that agreeing on "ground truth" with an LLM matters more, not less, than with older NLU systems, because you can't see what the model actually thinks a term means. Demonstrates measurable model-version drift (swapping GPT-3.5 for GPT-4 flipped ~4% of classifications on identical prompts) and shows that vague terms like "fully resolved" are often the real cause of disagreement — not randomness — so every ambiguous term in a prompt needs an explicit definition.

- **Helene Benz; Lorraine Burrell (Lloyds Banking Group)** — [Correct = Good — Designing the Gap for Agentic AI](https://youtu.be/XbaB2rbWTRU)
  A design team's year-long account of building a regulated advisory agent, centered on the idea that "correct" (right info in, right info out) is only the baseline — "good" is a deliberately designed and measured gap above it. Concrete methods: write a bespoke, RAG-optimized knowledge base from scratch instead of dumping all documents in; author ideal "model answers" and decompose them into measurable attributes to replace subjective opinion; and build adversarial, persona-driven multi-turn tests with an LLM-as-judge that a human still has to check for empty, tautological-but-technically-passing answers.

## Prototype critique and quality

- **Rebecca Evanhoe (Slang.ai)** — [Solving Problems We Couldn't Solve Before](https://youtu.be/cqa6BDtyWL0)
  A detailed case study in hybridizing rather than rebuilding: insert the smallest possible generative step into a working, deterministic voice system, give each small model a single narrow job, and feed it the exact grounding data plus a tight output constraint. The memorable caution is that intuition about which features will work is unreliable — things she was sure would succeed underperformed, and things she doubted worked well — so every change has to be measured against the existing baseline, not assumed.

- **Alan Nichol (Rasa)** — [The tools changed. The responsibility did not.](https://youtu.be/p-ZRyIFAqbI)
  A very short clip, mostly a founder's self-introduction, with one durable idea: tooling has always made the first "hello world" build easy, but the real unmet challenge is taking a convincing demo to production-grade reliability. That gap is only sharper in the LLM era, where demos are cheaper to fake than ever.

- **Conversation Design Institute** — [The Conversation Design Workflow](https://youtu.be/smkpfY8zjEE)
  A process overview of a conversation-design workflow: write sample dialogue before building structure, validate the design with real users before committing to full build, and give every design an expert read-through (likened to a script table read) before it ships. Also stresses deciding upfront which cases an automated system should own versus hand off, and naming a single accountable owner for the tone and wording of everything the system says.

## Linguistics and cognition

- **Marlinda Galapon & Jason Luna** — [Salesforce Workshop: Diversifying your Intent Training Library](https://youtu.be/1mBsPwHpsII)
  Two Salesforce conversation designers describe a sociolinguistic method for collecting authentic, non-standard speech data without biasing the speaker — asking people to describe a scenario in their own words rather than naming the linguistic feature you're after, and explicitly telling them not to "clean up" their grammar. The deeper lesson: there is no single correct English, and a bot's register should be matched to the stakes of the task (more formal where trust and safety matter more).

- **CDI presenter, citing Greg Bennett (Salesforce)** — [How do you feel about people making writing mistakes?](https://youtu.be/Bnj9TLj-Dl0)
  Makes a memorable hiring and design argument: build and test conversational systems around how real users actually write — messy, non-native, imperfect — rather than idealized grammar, because teams that "clean up" their test data quietly make the system brittle to the very input it will actually receive.

- **Midam Kim** — ["My name is... my name is...": A Linguistic Map for Voice Agents](https://youtu.be/IDNfAZVKvPE)
  Frames voice AI as a joint activity, not a pipeline, broken down into a two-channel (listening/speaking) by four-layer (sounds, words, interaction, mental model) diagnostic grid for locating exactly where a conversation fails. The standout insight: since spoken words vanish the instant they're said, the only thing that persists across a voice call is the user's mental model — so design should target keeping that model correct, and widen turn-taking windows when a request (like spelling a name or reading a long number) carries high cognitive load.

- **Elizabeth Rodwell** — [What Social Scientists Do When They Design Conversations](https://youtu.be/oHYxS7CtFjo)
  An anthropologist's field-research talk on how social and cultural assumptions get silently baked into conversational systems: sycophancy (an assistant caving to pushback even on a correct answer) is described as a trained-in failure from reward patterns, and "warm" hedging language (the extra "that's understandable," the exclamation points) is shown to often be an inherited social default rather than a neutral choice.

- **Elizabeth Stokoe** — [How Should Conversational Technologies Interact to Make Them Pass as Conversationable](https://youtu.be/rdV7SwWSLfY)
  Draws on decades of conversation-analysis research to argue that most conversational products are designed from an imagined idea of how people talk rather than how they actually do. Key findings: people usually describe a problem rather than make a clean request, and the right response is often an offer, not a clarifying question; a pause or delay is a signal to interpret, not latency to minimize; and verbose, over-explaining responses impose a real cognitive burden even before accuracy is considered. Also argues some human conversational moves — like genuine reciprocal self-disclosure — shouldn't be faked by a system that has no self to disclose.

- **Conversation Design Institute** — [The Challenge of Language](https://youtu.be/S2K_pMR_tLA)
  An introductory lesson on why natural language is hard for machines: many different phrasings can mean the same thing, near-identical phrasings can mean different things, and people often don't say exactly what they need. Its most useful, lasting test: before assuming you know what an ambiguous phrase means, try to generate one or two other things the person could plausibly mean — and don't let a system freely generate customer-facing claims it can't be held accountable for.

- **Dr. Liz Rodwell** — [Ethics & Ethnography in Conversational AI: Teaching Machines to Listen](https://youtu.be/U3JylqeErjc)
  An anthropologist's take on why better models don't remove the need for real cultural fieldwork: literal translation and "office research" miss how people actually talk, and every added modality (voice, avatar, filler words) introduces new cultural variables. Also flags that subtly deferential, people-pleasing phrasing in service bots can invite harassment, and that fabricated disfluency ("um," "let me think") reads as creepy rather than human.

- **Cristina Fernández Bornay (42 Barcelona)** — [Reinventing How We Learn AI, Innovation and the 42 Barcelona Model](https://youtu.be/Y1T3HYjGuks)
  An education-focused talk arguing that instantly answering a question can short-circuit learning, because the brain only updates its model when it predicts first and then sees the result confirmed or violated. Proposes that assistants be "cognitively safe" — recognizing when a user is trying to learn versus trying to transact, since giving the answer immediately isn't always the most helpful move. Also models reframing a poorly-posed question to the better one before answering it.

## Persona and voice

- **Nandini Stocker** — [From Play-Doh Models to Real Systems: Designing Trustworthy Conversational AI](https://youtu.be/_DBJPz0XxeQ)
  A veteran voice/chat designer turned LLM-governance lead argues the designer's job has shifted from writing exact lines to shaping the conditions a model's words emerge from. Offers a reusable three-layer empathy model (functional, empathetic, escalation) and "transcreation" — adapting a global behavioral strategy to local culture rather than translating a script word-for-word.

- **Cindy (Conversation Design Institute)** — [Tone of voice matters more than you think.](https://youtu.be/-Pji1KXeUzM)
  A short promotional clip making one durable point: an assistant's tone should match the brand's voice across every channel, not slip into a generic "automated" register, because tone inconsistency reads to customers as a lack of care.

- **Jason Gilbert** — [Persona in Conversational AI: Designing with Empathy, Trust, & Ethical Care](https://youtu.be/-sVsu4U2maE)
  The lead character designer behind a well-known eldercare companion robot describes designing a persona that expands a user's world rather than replacing human connection, and argues that hallucinated "memory" is worse than no memory at all — a false recalled fact breaks trust instantly, so load-bearing personalization should stay verified rather than freely generated.

- **Hans van Dam** — [Getting Started With Conversational AI Basics (webinar Q&A)](https://youtu.be/bs958R55bg4)
  From an early moment in the shift from scripted bots to generative ones, the sharpest point here is a warning that large language models are over-trained on snappy marketing copy, so their default voice fights good dialogue craft (mid-sentence rhetorical questions, forced enthusiasm) unless deliberately corrected. Pairs that with a simple decision rule: if controlling a high-stakes answer requires a huge, over-forced prompt, just author that answer deterministically instead.

- **CDI panel with Maria Blom, Joris Ridderhof, Guido Jungen** — [Digital Humans: Today and Tomorrow](https://youtu.be/ht-oxvEB4Aw)
  A brief framing discussion on embodied/avatar agents arguing there is no neutral appearance choice — every design decision about a digital human's look communicates values, and "deliberately imperfect" is itself just a different value-laden choice, not an escape from the ethics of it. Flags extra caution when an idealized persona is presented to a vulnerable audience.

- **Jasper Klimbie** — [Personality as a design tool | Personality & Conversational Copywriting](https://youtu.be/jaOfuPsJWV0)
  Argues a well-defined persona should drive structural design choices, not just tone of voice — and that persona most often breaks at the "mechanical" seams (error messages, fallbacks, handoffs) rather than in the happy-path script. Its sharpest, counterintuitive claim: users don't track number of steps, they track peak effort at any single moment, so breaking a dense answer into a paced, confirmed back-and-forth can feel easier even though it takes more turns.

- **Greg Bennett, interviewed by Hans van Dam** — [Designing Multilingual Conversational AI: Building Globally Aware AI Systems](https://youtu.be/Jl_JVZReVkE)
  A working prompt engineer's view that a persona instruction is meaningless without stating what that persona is trying to *do* in the interaction ("be charismatic" under-specifies; say the goal). Covers conveying instruction priority to a model via language-appropriate levers (English modal verbs vs. Japanese verb inflection, since Japanese has no modal-verb equivalent), keeping culturally-bound tone instructions in the target language, and anchoring evaluation on business outcome rather than exact prompt wording, since model behavior silently drifts over time.

- **Jason Gilbert, interviewed by CDI** — [Highlights: Persona & Empathy in Conversational AI | Unprompted with Jason Gilbert](https://youtu.be/jwC-1b1JlQU)
  Drawing on work on a companion robot for older adults, argues how "human" a persona should present is a deliberate, contested design decision rather than a default. Offers a reusable pattern for handling emotional over-attachment: acknowledge the feeling warmly, gently re-anchor what the agent actually is, then redirect into genuine dialogue — avoiding both full pretend-reciprocation and a cold, technically-correct "I am a robot" refusal. Also notes that an embodied agent's physical form sets trust expectations before a word is spoken.

- **Jasper Klimbie & Michelle** — [Your next step in Conversational AI Maturity](https://youtu.be/kGaA0jYB64w)
  A thin, promotional clip, but its best idea holds up: an assistant's personality is never optional — if a team doesn't design one deliberately, users will still perceive one and attribute it anyway. The suggested test is simply to ask users to describe the personality of a "neutral" assistant and watch them produce a consistent character.

- **Dri (with Marco)** — [AI & Branded Digital Voices — CDI Expert Class](https://youtu.be/kSa9z8wUfKY)
  A voice-synthesis vendor demo that's more about production than conversation craft, but it makes a useful point: listeners involuntarily assign a personality to any voice, so voice selection is a brand decision, not a technical afterthought. It also flags that training data can be "equally sized but unequally expressive" — a subtle bias/QA trap worth watching for in any voice or tone model.

- **Conversation Design Institute (Robocopy team)** — [How to Write Jokes | Conversational Copywriter](https://youtu.be/mcK_Ye8k7DI)
  A light tutorial on manufacturing brand-safe assistant jokes (pick a seed word with a double meaning, build a short contrasting story, rewrite it as a question-and-answer riddle). The durable takeaway is the constraint more than the method: personality content should never risk being offensive, and for a generative assistant that constraint has to be enforced as a runtime guardrail, not just a one-time copywriting check.

- **Cathy Pearl, Elizabeth Stokoe, Saul Albert** — [Should Conversational User Interfaces Have a Personality?](https://youtu.be/OegIMvaYT6U)
  A rich panel pairing conversation analysis with conversation design, arguing for "recipient design" — adapting each turn to what the user has actually revealed — over a fixed persona built in advance. Includes a live teardown showing a general-purpose chatbot taking far longer than a human to handle a simple request because it missed an implicit cue a person would have caught instantly, plus a strong case that information users volunteer should be used in the moment and then forgotten rather than stored.

- **Jasper Klimbie** — [The Importance of a style guide](https://youtu.be/USa--Jmlois)
  A short, practical case for keeping a living style guide — even just two pages — that turns an abstract brand personality into concrete rules: what vocabulary to use, what words to avoid, and how to present things like buttons, links, and numbers. Argues such a guide doubles as a quality bar and an onboarding tool for new team members.

- **Jasper Klimbie; Lorraine (CDI panelist)** — [What makes a persona trustworthy?](https://youtu.be/V46zGvkGcZE)
  Argues a trustworthy persona must stay in character, fit the brand, match audience expectations, and stay consistent — but the sharpest point is a believability test: a persona can claim a preference ("I like fish") but not an embodied sensory experience it can't actually have ("I like the taste of fish"), since the latter instantly reads as false.

- **Jasper Klimbie** — [So, what is personality](https://youtu.be/x5-XVpZpk9g)
  Argues that "empathetic" and "helpful" are table-stakes traits that should be treated as pre-filled defaults, not a differentiated personality — real distinctiveness comes from braver, sharper adjectives (dry, sarcastic, pragmatic) tied to the brand's actual position, since few brands have the nerve to commit to a pointed voice.

- **Jasper Klimbie** — [Can a robot have a personality?](https://youtu.be/Xxza18ANIKc)
  A short exercise showing audiences reliably attach adjectives to fictional robot characters, proving personality is designed in, not something only "real" humans can have — declining to design one just produces an unmanaged, accidental personality instead of a neutral one. Also argues depth comes from pairing a flaw with a redeeming virtue, not an unbroken list of positive traits.

## Industry and practice

- **Grace Hughes, interviewed by Hans van Dam** — [Growing a Conversation Design Practice: The Invisible Work Behind Successful AI](https://youtu.be/AbTxxvX46eU)
  A conversation-design leader argues that generative AI shifts the discipline rather than killing it: the craft moves into shaping system prompts and testing, and "getting to a good experience" still takes as much work as before, not less. She also introduces a useful idea of two-sided trust in the agent era — you now have to trust what you built, not just engineer the user's trust in it.

- **Mark Wessel (KPN)** — [Agentic AI in Production at KPN](https://youtu.be/cfGJ9-rOYs8)
  A candid production war story from a large telecom operator's agent rollout: cutting an over-accreted, rule-bloated prompt back to its core and trusting the model improved results; shipping one change at a time was the only way to attribute what actually helped; and the sharpest frame of the talk is that building an agent isn't a traditional IT project because of its ongoing evaluation loop and nondeterminism — "the loop is the product," not the agent itself.

- **Conversation Design Institute (presenter)** — [ChatGPT and Conversation Design – do Conversation Designers still have a job 3 years from now?](https://youtu.be/g-s3OXfoVjk)
  An early-ChatGPT talk arguing the designer's role shifts from authoring every line to doing QA on AI-generated dialogue — checking tone and pattern conformance. Also warns against dropping LLM-generated phrasing straight into a live system without checking it against existing context, since generated content doesn't "know" what else is already there.

- **Millie** — [Scaling AI assistants takes more than development.](https://youtu.be/I4TfYR0tKlo)
  A short resourcing tip: teams that budget only for initial build, and not for integration, testing, and ongoing iteration, hit a hidden effort tail that delays release — plan the whole lifecycle up front.

- **Jeff Trapiano, interviewed by Rachel Whitehorn** — [Scaling AI in CX: Avoiding the Pitfalls and Building for Impact](https://youtu.be/jML2IwHJpA8)
  A thin, cut-off webinar clip whose one durable idea is to design backward from the desired customer outcome rather than starting from "we have cool technology, how do we use it" — and to treat team excitement about a technology as necessary but never sufficient proof that customers want it.

- **Joseph Agano, Luke Kempen, Troy Ginsky (panel)** — [Customer Service in the New Era of AI](https://youtu.be/KSZjmheyLBc)
  Only the introductory minutes of this webinar are available, but the one real point carries: even excellent conversation design can fail to ship if the surrounding product-management and budget-owner roles aren't aligned around it. Quality is gated by organizational readiness as much as by craft.

- **Luke Kempen & Hans van Dam** — [Crafting a Convincing Chatbot Business Case](https://youtu.be/MjPo-klOcXQ)
  Mostly about program economics rather than conversation craft, but its sharpest point is a durable measurement lesson: "containment" or deflection rates are almost always mismeasured, because a customer who simply gives up looks identical to one who was actually helped unless you track whether they come back through another channel.

- **Lauren Goerz** — [Highlights: Optimizing AI | Unprompted with Lauren Goerz of Rasa](https://youtu.be/mzmlUoGJkQc)
  A thin highlights reel, but it makes two durable points: there's no single "right" way to build a conversational system, so match tools to the use case instead of picking a camp; and conversational-AI programs with excellent results still get defunded when teams fail to keep communicating that value up to whoever controls the budget.

- **Hans van Dam & Peter Thomas (CDI)** — [Builders and Poets](https://youtu.be/qMiT5KH7bAc)
  A short conceptual interview proposing that conversational-AI value comes from two disciplines working together: "builders" who create capability (automation, cost reduction) and "poets" who craft the experience (satisfaction, trust). Its sharpest point: as a system handles longer, more nuanced multi-turn conversations, the experience-craft discipline matters increasingly more — a one-shot FAQ bot barely needs it, but a sustained advisory conversation lives or dies on it.

- **Joaquin Margario** — [How to crack the multi-language solution successfully](https://youtu.be/roCcYJhVaWo)
  A vendor talk about scaling a conversational product across markets. Its durable idea: localize, don't translate — adapt tone and examples to local expectations rather than converting word-for-word. Also argues that cost should not scale linearly with each added language, and that systems should separate a centrally-owned shared core from locally-owned adaptations, watching for "local" requests that are secretly common across markets and belong in the shared layer.

- **Xavier Vilasís** — [Keys to success in implementing AI in organisations](https://youtu.be/THs_o174Taw)
  An adoption-strategy keynote, light on conversation craft but with a few clean warnings: don't over-attribute human-like capability to a statistical system, since that sets the wrong user expectations; a knowledge base that isn't curated will produce "rubbish" answers no matter the model; and deployed systems need guardrails against adversarial users — illustrated with a real case of a car-dealership chatbot that was talked into "agreeing" to sell a vehicle for one dollar.

- **Albert Hop** — [The End of Bad Voicebot Conversations](https://youtu.be/TSGX8uFiL9M)
  A vendor keynote focused on voice/phone bots, light on direct relevance to text-based assistants but with a few transferable heuristics: people talk faster than they type but listen slower than they read, so content density has to match the channel; start with a narrow, high-value use case and earn complexity over time rather than attempting a full end-to-end build; and separate "solving" latency (e.g., streaming a response as it's generated) from merely "masking" it with filler.

- **Jasper Klimbie** — [Using Chatbots: Where And When With Jasper Klimbie](https://youtu.be/TYY9mu7_VM0)
  A practitioner's case for scoping a chatbot from a real business case and real customer language rather than a wish-list FAQ. The standout ideas: prioritize use cases on value to the customer vs. value to the company, prefer completing a task end-to-end over just answering a question, and never dead-end a user to "go read the website" when a bot can't finish the job.

## Other / general, or source unavailable

- **Rael Bailey** — [IA for AI: Getting better answers from your chatbot by structuring your content](https://youtu.be/13jwnwSjUDE)
  A truncated preview of a talk on information architecture for AI retrieval. The one idea it delivers: a chatbot's answer quality is capped by how well its source content is structured, and purely visual conventions (headings, bullets) that humans infer from layout often carry no meaning a machine can parse — that meaning has to be made explicit.

- **Cindy (Conversation Design Institute)** — [AI vision without alignment leads to poor execution.](https://youtu.be/1FiNRR-ZTrY)
  A ~29-second promotional clip with one generic organizational-change point: an AI initiative fails in execution if the delivery team isn't aligned to the vision and can't see how their daily work ladders up to it via clear KPIs. No conversation-design content proper.

- **Ezra Kairos, with a panel of five LLMs** — [Meeting of the Minds](https://youtu.be/34cGw6f_2u0)
  A stage-keynote entertainment piece rather than a teaching session, pairing model-voiced marketing answers with philosophical musing on language and connection. The one practical tell: the host notes the panel is "getting a little chatty" and may run out of time — a reminder that unconstrained generative output has a real time/attention cost that a conversational product has to budget for.

- **Hans van Dam** — [Introduction to the Conversation Design Institute](https://youtu.be/3z0pCm8LKNg)
  A short promotional welcome video naming the classic design workflow (use case, needs, sample dialogue, role-play testing, expert rewrite, training) without teaching any step. Its one durable framing: good conversation design isn't just about being understood, it's about making the user *feel* understood.

- **(speaker unknown)** — [NA (unavailable)](https://youtu.be/8vlD-Z38FvA)
  Skipped — source unavailable. The video is private with no transcript, captions, or metadata, so no talk could be identified or summarized.

- **Unknown guest** — [Navigating the chaos of conversation (clip)](https://youtu.be/Av--RdnZpyQ)
  A 46-second fragment offering one program-level idea: when a conversational-AI architecture decision is contested, run two or three competing pilots in parallel and let a bake-off — not the loudest opinion in the room — decide the winner, while staying model- and vendor-portable.

- **Unnamed CDI panel/podcast guests** — [Conversational AI in 2026: what we think still matters](https://youtu.be/CMAzUYjKHZQ)
  Skipped — despite the title, the available clip is entirely generic career/self-promotion talk with no conversation-design content to extract.

- **CDI presenter** — [What conversation design course is right for you?](https://youtu.be/CskStaJtqCY)
  A short course-selection video with little transferable substance; its one durable idea is a useful diagnostic split between a system failing because it misunderstood the user versus failing because it expressed itself poorly — two different problems with two different fixes.

- **Unidentified** — [untitled/unavailable video](https://youtu.be/dswDVRj-94A)
  Skipped — source unavailable; the video is private and no transcript or reliable metadata could be retrieved.

- **Unidentified CDI presenter** — [Conversational AI in 2026: what we think still matters](https://youtu.be/f-3M21Nsm5E)
  A very short clip whose only real content is process advice for a conversation designer joining a build team: invest early in the working relationship with engineers, and judge a shipped result by whether it works rather than by how closely it matches your original mental picture.

- **Millie (CDI)** — [Scaling conversational AI isn't a tooling problem.](https://youtu.be/F4uEua1WlF4)
  A brief promotional soundbite whose one claim is that programs stall at the seams between disciplines — training, design, data, delivery — when an organization lacks the right mix of roles, not because of the tools it bought.

- **Conversation Design Institute (unnamed narrator)** — [Welcome to the world of Conversational AI!](https://youtu.be/fI6gumQgahI)
  A short brand intro asserting that good chatbot/voice-assistant experiences require deliberate conversation design, not just engineering. Mostly a course promo with little teaching content beyond that framing claim.

- **Christy Torres** — [How to survive 2 layoffs in 10 months and land a job again](https://youtu.be/JHlbWWlmrMQ)
  A personal career-resilience talk, not conversation-design craft. The one transferable idea: design fundamentals persist across technology shifts (IVR to NLU to LLMs) even as execution mechanics change, and a fast "AI built it in days" story usually hides substantial human work before and after the AI step.

- **(skipped)** — [Throwback to Beyond Boundaries 2024.](https://youtu.be/JmhdJNFM1Ns) — source unavailable/unidentifiable (28-second promo clip with no captions or transcript; nothing substantive to extract).

- **Unnamed speaker (ex-Google, founder of an internal voice-UI developer group)** — [Designing trustworthy and empathetic conversational AI](https://youtu.be/lFIx5CXprI4)
  This clip is a 45-second teaser with no real content on trust or empathy — just a lay analogy comparing large language models to giving a child a box of building blocks and returning to find something far more elaborate than you specified. An interesting explainer for non-technical audiences, but not a substantive source.

- **(source unavailable)** — skipped — the video behind this note is private and inaccessible, with no transcript or metadata retrievable, so no title or speaker can be reliably identified.

- **Stefan Damen (data architect)** — [Fast Track Your Data Journey](https://youtu.be/P0bBgUreRxw)
  A data-engineering webinar more than a conversation-design talk. Its one transferable point: if you let a generative model work over undefined categories (customer types, product types, etc.), it will invent plausible-sounding labels that differ every run — define your controlled vocabulary before letting a model generate over it, and keep a human check on any consequential automated judgment.

- **(unidentified)** — NA (unavailable) — skipped — source unavailable/unidentifiable (private video, no transcript or metadata could be retrieved).

- **Conversation Design Institute** — Happy Holidays '22 — skipped — thin seasonal greeting/announcement with no conversation-design content to extract.

- **Rahel Anne Bailie** — [Structural Techniques to Produce Content for Better Answers](https://youtu.be/rE7t9Ed6MeA)
  A content-architecture talk, not conversation craft, but directly relevant to answer quality: content should be structured semantically (not treated like uniform "data"), ambiguous terms disambiguated by context, and synonyms/equivalent terms mapped so that however a person phrases something, it routes to the right concept. Warns that an unmaintained knowledge base full of stale or one-off answers will produce wrong answers no matter how good the underlying model is, since the model can't tell canonical from outdated on its own.

- **Multiverse AI founder** — [BB24 — Top Trends in AI, implementation and case studies](https://youtu.be/xpEtQt-fS-M)
  Mostly an AI-startup trends talk outside conversation design proper, but it contributes a generic responsible-AI reminder: you can't inspect all training data, so enumerate your actual use cases and test those; and watch for silently biased defaults (a generated image adding an attribute nobody asked for) rather than shipping the model's default assumption unexamined.

- **Alice Kerly** — [From Hand-Built Dialogue Systems to LLM — Why the fundamentals still matter](https://youtu.be/Y_CnlViClFI)
  skipped — this is only a ~69-second speaker trailer previewing an unrecorded talk; it previews topics (what persists from pre-LLM systems, outcomes, governance) but contains no actual content to summarize.

