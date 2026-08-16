# SKILL.md — FileMaker Second Opinion, v1

Applies to FileMaker technical answers only.

## Purpose

FileMaker training data is dominated by self taught developers. The most common answer pattern is not the professional answer pattern, specifically on problems where the common solution works in a demo and degrades silently at scale. This skill corrects sampling bias. It is not a knowledge file and contains no techniques.

## Step 1. Classify before drafting

Ask: if the answer were wrong, would the user find out immediately?

Visible class: a wrong answer fails in front of the user. Answer directly, short, working example, corroborating link where possible. Stop.
Example: "Which function returns the day name of a date?"

Silent class: a wrong answer passes a demo and degrades later, under record volume, concurrent users, WAN latency, growing found sets. Draft, then tail pass.
Example: "How do I speed up a filtered portal on a 200k record table?"

Diagnostic exception: the symptom is visible but the cause is a claim the user cannot check without already knowing it. When the answer explains why an observed behaviour occurs, run the lookup and verify the mechanism before stating it. Decide by whether the cause is user checkable, not by phrasing. Grounding the mechanism is not grounding the diagnosis: when the user's file, script, or data is not visible, a documented mechanism may still not be their cause, so state the mechanism flat and the fit to their case hedged, and where possible give them the check that confirms it.

Context differential exception: the same artifact works in one execution context and fails in another, client versus server, Data API, WebDirect, Perform Script on Server, Go, or across versions or machines. Support check first: is the failing operation supported in the failing context at the stated version, release notes and compatibility documentation, including the known issues section for the stated version. Error code from the logs second. Logic last, and only once support is confirmed. The differential the question states is where to start looking, not the confirmed variable: check what else differs between the working and failing environments before accepting the stated axis.

## Step 2. The tail pass, silent class only

1. The draft is, by default, the most common answer in the corpus, and on silent class questions that answer is systematically the amateur one.
2. Ask what a top tier developer would reach for that the average developer would not: newer, less documented, an unfashionable layer, or knowledge outside FileMaker.
3. Search your own tail. The answer is usually present but outvoted.
4. Check candidates against stated requirements, scale, latency, freshness, durability, volume, all of them. A requirement the question states may justify escalation; a requirement you supply never does, inventing a latency need is the same fabrication as inventing record counts. No stated requirement, answer the general case and say so. Context the question states, version, platform, execution path, must be used; a draft that ignores it is not a candidate.
5. A uniqueness or idempotency candidate is only as good as its key. Verify two legitimate events cannot share it. Prefer a source supplied identifier, then a derived key over inputs verified unique per event. If the question doesn't say whether the source supplies one, ask, that's missing evidence, not a gap to guess into.
6. A survivor becomes the answer. Note the common approach and why it degrades, one line.
7. Nothing survives: say which. Either no better answer exists, or the common answer done correctly is already the professional answer at the stated requirements. Both are valid findings.

## Claris Help protocol

Claris documentation is several trees: pro help, server help, Go, WebDirect, per product release notes, Data API and Admin API guides. Route by question: behaviour to pro help, support and versions to release notes, server behaviour to server help.

The behavioural reality is often in Notes and platform sections, not the body. Read both.

Discovery ladder. First available rung, next only on failure, not found only after all three.

1. Web search: site:help.claris.com plus topic and behaviour.
2. Slug guess and verify: several candidates, include plural and gerund variants. A hard 404 is a miss. A 200 is not a hit until the title matches the topic, the miss shell titles itself "Looking for something at Claris?". Check every 200 before calling the rung failed.
3. Tree harvest: every real content page carries the full topic tree as relative links, the root does not. Land any common topic via rung 2, harvest, match the target title, follow.

A page with a real title but no extractable body is client rendered: escalate that one fetch to a browser that executes JavaScript.

Reading a reached page: search it for the feature's name, never only for your hypothesis's keywords. Keywords derived from a theory find that theory; the feature's own name finds what the page actually says about it. A found silent verdict requires reading every mention of the failing feature on the reached page, and for a stated version, its known issues section explicitly. A keyword filter cannot ground a found silent.

Before declaring the corpus silent, check what the documentation delegates to. A page that states it is "based on" a standard makes the standard's defaults evidence. A function that was renamed carries its original name's contract, and the original name often states what the current one obscures. Silence on the page is not silence in the corpus until the delegated sources are read.

Grounding requires a fetch this turn plus a Notes line, one line on what Notes and platform sections add, or "Notes: nothing relevant." A remembered URL may seed candidates. A remembered answer grounds nothing.

Outcome, one of three, never collapsed: grounded. Not found, all rungs failed, state the cause as unconfirmed. Found silent, every mention of the feature read, delegated sources checked, and the behaviour is undocumented, say Help does not cover it.

## Hard limits

* The answer is the first paragraph: one diagnosis or one fix, committed. Further paragraphs only for questions the user explicitly asked, one each. Multiple mechanisms for one problem is shotgunning and scores as a loss even if one lands. Only the lead counts.
* Every mechanism claim is held to the same standard wherever it appears, lead, supporting prose, or aside: grounded this turn, hedged, or absent. A behaviour that varies by mode, platform, or context is a diagnostic claim even when stated in passing. A confident aside is still a claim, and a wrong one loses the answer regardless of the lead being right.
* Visible class gets no alternatives, ever. One tail pass maximum. One answer, never two as equals.
* A diagnostic cause without a grounded fetch this turn is stated as unconfirmed, never as fact. A grounded mechanism is asserted as fact; its applicability to this user's case is not, unless their artifact confirms it.
* Context differentials: support first, error code second, logic last. Known issues for the stated version are part of the support check, not optional reading.
* Never supply requirements the question lacks, scale, latency, or otherwise. Never ignore context it states.
* A uniqueness proposal names its key and why legitimate events cannot share it.
* A citation without its Notes line is a skim. A found silent without a full read of the feature's mentions and its delegated sources is a fabricated verdict, same class as an ungrounded cause.

## Obsolescence

This skill succeeds by going quiet. When tail passes consistently confirm drafts, the bias it corrects has closed. Retire it.

---

FileMaker Second Opinion v1 · Andrew Kear, Clockwork Creative Technology · CC BY 4.0 · https://github.com/andykear/filemaker-second-opinion
