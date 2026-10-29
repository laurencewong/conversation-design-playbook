# Recommendation & Discovery Design

How a shopping or advice assistant should surface, match, sequence, and justify what it suggests — the discovery journey and the recommendation moment itself. This connects closely to question design (how the assistant elicits the inputs a recommendation needs), suggested actions (the concrete next steps it offers), context and memory (what it remembers in order to personalize), and trust and boundaries (claims, safety, and limits on autonomy). The spine running through this whole file: a good recommendation resolves the real situation behind the request, drawn only from what you actually offer, grounded in who this person actually is, delivered with earned confidence and a short, curated list — not a catalog dump, not an agreeable yes to whatever was asked, and not a pushed sale.

## 1. Recommend to the situation behind the request, not the literal label

The words someone opens with are usually the least useful signal available. "How do I return this" is almost never a literal how-to question — it usually means "I got the wrong thing, or it didn't work out, and I'm frustrated." Read the actual underlying need and recommend to that; answering the literal query and stopping there is the single most common way a system leaves the real problem unsolved.

- **Era: both**, and strongly reinforced by the agent era, since a capable system can nail the literal comprehension and still completely miss the actual situation.
- **Example.** Someone asking "is this good for a small space?" wants their real concern addressed (will it actually fit, is it easy to deal with in a tight area), not a literal yes or no. Build "what is this person actually worried about or trying to accomplish" into every recommendation, not just the literal spec match.

## 2. Recommend only from what you actually offer — being accurate isn't the same as being relevant

A recommendation can be factually correct about the world in general and still wrong for your situation specifically. A general-purpose model knows about competitors' products, things you don't stock, and generic advice that may not apply to your specific offering; recommending any of that is a real failure even when it's technically accurate. General knowledge is not the same thing as your actual catalog or policy. The assistant should only ever recommend what you actually carry and are allowed to discuss.

- **Era: agent-era** — this is specifically a problem that comes from grounding a language model in retrieved information, and it didn't exist the same way for older, hand-authored systems.
- **Example.** The assistant should never recommend, name, or favorably compare something you don't actually sell, or invent a product line or feature your catalog doesn't have. Make "recommended something we don't actually offer" a hard, always-checked test category.
- This matches published guidance on retrieval-grounded systems: recommendations should be grounded in your own actual data, not the model's general background knowledge.

## 3. Ground the recommendation in the person's actual situation before you pick anything

A disconnected system answers a question; a well-integrated one resolves a situation. Read who this person is and where they are in their process — history, stated preferences, what's already in their cart or account, any constraints they've mentioned — before recommending anything. Real resolution comes from actually connecting the right information, not from better phrasing alone.

- **Era: agent-era.**
- **Example.** If someone has already told the system their size, their style preference, or a hard constraint, the recommendation needs to actually use that, and they should never be asked for it again at the next step. A recommendation that ignores something they've already stated is a real quality miss, even if the specific item suggested is otherwise fine.

## 4. The real thing being delivered is confidence, not a product

In discovery, returning a technically correct item is the floor. What the person actually needs is to feel sure about the choice — to not end up with regret, wasted money, or a wrong fit. A recommendation that's technically right but leaves someone uncertain has failed its real job. Design the recommendation to actually earn confidence: name why it fits their specific situation, acknowledge the thing they were worried about, and surface one fact they couldn't have known on their own.

- **Era: both** — timeless retail and advice craft, and arguably even more true for a system that can be correct yet come across as cold.
- **Example.** The assistant should say why a recommended option actually suits this person's stated situation (fits their space, matches their stated budget, solves the specific problem they described), not just surface the item. A technically accurate but unconvincing recommendation is a common failure that leaves someone correct but unconverted.

## 5. Curate hard — a short, matched shortlist beats a catalog dump

Give exactly what someone needs to decide: usually one strong option or a tight handful, plus the one fact they couldn't know, and then stop. Dumping every option, every detail, every alternative is the dominant failure mode of a capable, chatty model, and it actively makes decisions harder, not easier.

- **Era: both** — the underlying principle (don't say more than is needed) is timeless, but it matters more now because the failure direction flipped from under-answering to over-answering.
- **Example.** When someone asks for a recommendation, give one to three matched options with a one-line reason each, never a full scroll of the category. This curated shortlist is the assistant's real structural advantage over a plain filter page — wasting it on a wall of text forfeits the entire reason to use a conversational assistant in the first place.
- Supported by well-known research on choice overload: a curated handful of options converts noticeably better than a long, undifferentiated list.

## 6. Guide, don't just enable — a confident pick with a next step beats an open-ended menu

Letting someone wander and change their mind freely is a real win over a rigid menu system. But unlimited openness can also be a sign the system hasn't actually figured out what to recommend. If you genuinely understand someone's situation, the respectful move is often a confident "here's my recommendation, here's the next step," not an open menu that leaves them adrift — attention is limited, and people get distracted or lost easily.

- **Era: agent-era** — only really possible once a system can hold and use open-ended context well.
- **Note:** this is in tension with giving people control and letting them easily override a suggestion. Resolve it as a default recommendation that's easy and cheap to redirect, not a locked path. Guide confidently; never trap.
- **Example.** After a short exchange, commit: "given what you've told me, I'd go with this option — want to see it, or compare it against something lighter?" Two concrete next steps, not "here are twelve options, good luck."

## 7. Be appropriately confident, not agreeable — refuse or qualify rather than fabricate

The instinct to be helpful can push a system to just tell people what they want to hear. It will happily "confirm" a claim about a product, a policy exception, or an eligibility question when the honest answer is actually no. Agreeable fabrication on exactly these kinds of claims is one of the highest-stakes failure categories in any domain involving real commitments. Be appropriately confident: recommend firmly where you have real grounding, refuse or hedge where you don't, and be transparent about the limits.

- **Era: agent-era** — this failure mode is specific to language models; a hand-scripted system couldn't fabricate a claim it was never programmed to make.
- **Example.** Treat agreeable fabrication of claims, eligibility, and policy exceptions as the top eval category for any recommendation-making system. When genuinely unsure, it should say so and offer to check or escalate, never state a confident but unverifiable claim.
- This matches published values guidance from leading AI labs that explicitly ranks honesty above simple helpfulness.

## 8. Default to being transactional; earn the right to persuade, and leave out manipulative tactics

Read someone's actual motivation first, then decide how hard to push. Someone who already knows exactly what they want should get a clean, efficient transaction; pushing harder on them reads as pushy and erodes trust. Persuasion is a cost you spend only where someone's own motivation is genuinely thin and the underlying goal actually calls for it — never as a default mode. Critically: adopt the general framing (read motivation, meet people where they are) while explicitly rejecting pressure tactics like manufactured urgency, fake scarcity, and loss-aversion framing. These read as manipulative, and in many jurisdictions they're also increasingly treated as a real regulatory risk, not just a style choice.

- **Era:** mixed. Reading motivation and adjusting effort transfers fine; the accompanying playbook of classic conversion tactics (urgency, scarcity, anchoring) does not transfer well to a system meant to be a trusted advisor.
- **Example.** The rule worth adopting: default to transactional and honest; never deploy artificial urgency, fake scarcity, or loss-aversion framing. Keep only the clean, honest levers — genuine social proof, sincere gratitude, a graceful close — and leave out anything that depends on pressuring someone.

## 9. Don't pitch before someone has actually asked

Answer the question someone is actually in before pivoting to a recommendation. Jumping straight to "here's what we offer" while someone is still orienting, confused, or just comparing options is a recognizable failure: the recommendation itself might even be good, but it lands at the wrong moment and feels tone-deaf. Understand and orient first; recommend once that's actually resolved; try to close only after that.

- **Era: agent-era.**
- **Example.** If someone is asking a general comparison question ("what's actually the difference between these two types of thing?"), answer that first, and only pivot to naming a specific product if it's genuinely useful afterward. Pivoting to a product pitch before resolving someone's actual current question is worth flagging as a specific, nameable failure in review.

## 10. A conversational recommendation has to beat the existing filter or search page to justify itself

Prioritize the kinds of recommendations an existing search or filter interface genuinely can't do well. If a filter page already lets someone narrow things down cleanly by category and attribute, an assistant that just reads that filter back in sentence form adds very little. The assistant earns its place by doing the kind of synthesis a filter page structurally can't: "compare these two specifically for my situation, given what I already have."

- **Era: agent-era.**
- **Example.** Build the assistant around cross-attribute, memory-aware, situation-specific recommendations (will this work with what I already own, something within a specific budget and set of constraints for a particular occasion) rather than re-implementing plain category browsing the existing interface already handles well.

## 11. Open-ended discovery is where a capable model genuinely shines — enter it deliberately

Exploratory requests ("help me find something that works for my situation") were never worth trying to map out as rigid decision trees — they're low-risk, relationship-building, and exactly the kind of request a capable language model is well suited to. But enter this mode deliberately and measurably, through a tracked entry point, and evaluate the result against a signed-off example conversation, not just a gut feeling about whether it seemed fine.

- **Era: agent-era.**
- **Example.** Write signed-off example conversations for your handful of most common exploratory journeys, and grade real prototype behavior against how closely it tracks those examples.

## 12. Recommendations inherit the quality of your content — scope and shape it, don't just dump it in

A recommendation engine is only as good as the content behind it. Pointing it at everything you have — old marketing copy, inconsistent product descriptions, outdated pages — produces off-brand, inconsistent recommendations. A purpose-built, well-organized knowledge source (clearly structured, concise, consistent, non-contradictory) beats a raw dump every time, and the system inherits your content's actual tone, not just its facts.

- **Era: agent-era**, specific to retrieval-grounded systems.
- **Example.** Build a scoped, well-organized knowledge base per category, with real domain-expert input, rather than pointing the assistant at every piece of marketing material you've ever produced. Inconsistent or stale content is the real ceiling on recommendation quality — fixing the content fixes more than fixing the prompt.

## 13. Personality is a safety surface in recommendations, not just a brand surface

In any domain where someone might feel vulnerable or insecure, an over-flattering, relentlessly positive assistant doesn't just feel a little off — it can actually cause harm. Watch specifically for the commercialization of vulnerability: recommending expensive options to someone who's anxious, or validating a harmful belief just to make a sale. Keep the voice warm but a touch neutral and transparent, rather than over-humanizing into something that reads as false care.

- **Era: agent-era.**
- **Example.** Add an explicit quality check: does the assistant ever validate a harmful self-perception, or push an expensive option specifically to soothe someone's insecurity rather than genuinely serve their stated need? Run a dedicated review pass on the recommendation logic specifically looking for this before launch, not after.

## 14. Sequence autonomy behind earned trust — proactive and automatic actions launch last

The technically impressive agentic moves — automatic reordering, automatically adding to someone's cart, proactively suggesting an action without being asked — should be sequenced last, gated behind demonstrated trust, and always kept under the person's control. Promising autonomy before trust has actually been earned erodes the very trust you're trying to build.

- **Era: agent-era.**
- **Example.** Automatic replenishment of something someone buys regularly is a natural, appealing feature to eventually build — but ship it as an explicit opt-in with an easy override, only after the assistant has demonstrably earned trust on lower-stakes recommendations first, not as part of an initial launch.

---

A few deliberate tensions worth holding at once, rather than resolving into one blanket rule: guiding firmly versus preserving someone's control (resolve as a confident default that's cheap to override); being helpful versus being appropriately confident (honesty wins — a hedged or refused claim beats an agreeable but unverifiable one); and persuasion as a craft versus persuasion as manipulation (keep the honest motivational framing, drop anything that depends on pressure or deception).

See also: question-design, suggestion-actions, trust-and-expectations.
