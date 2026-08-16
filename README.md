[![Stars](https://img.shields.io/github/stars/andykear/FileMaker-XML-scrubber?style=social)](https://github.com/andykear/FileMaker-XML-scrubber)
[![License](https://img.shields.io/badge/license-CC%20BY%204.0-green)](https://creativecommons.org/licenses/by/4.0/)

# FileMaker Second Opinion

A reasoning skill for AI-assisted FileMaker development. Built from production experience. Now released as v1 after months of refining the logic against real work.

It contains no techniques and no knowledge. It corrects one bias: an AI's tendency to mistake the common FileMaker solution for the one that holds up in production.

## The problem

FileMaker's accessibility is its great strength. It is also the source of a quiet problem for anyone using AI to build in it.

A huge, capable, largely self-taught community means the platform's common patterns are everywhere in the material a model learns from. The deepest patterns mostly are not. The techniques that matter at scale live in client work and production systems that never got written up in public.

So the training data is weighted toward the common solution. And for a specific class of problems, the common solution and the professional one are not the same thing. A model gives you the common one, confidently, because that is what the weight of the data says.

This would not matter if wrong answers announced themselves. Many do. A bad calculation returns the wrong value, a mistyped field name throws an error, you fix it and move on.

The dangerous ones are different. The common answer works in the demo and degrades silently later. Record volume. Concurrent users. WAN latency. A growing found set.

A filtered portal that is fine on two hundred rows and unusable on two hundred thousand. A uniqueness constraint that holds on manual entry and does nothing on a scripted import. An unstored calculation that is instant when you test it alone and a bottleneck once real users are on the hosted file.

The schema looks right. The demo passes. It fails in production, quietly, weeks later, under conditions the original question never mentioned.

That gap is what this skill closes.

## What it does

First it classifies. If this answer were wrong, would the user find out immediately? If yes, answer directly and stop. No ceremony.

If the failure could be silent, it drafts the obvious answer and then challenges it. What would a production developer reach for that the obvious answer misses? A less common approach, a different layer, a newer mechanism, knowledge from outside the usual FileMaker pattern.

Candidates get checked against the requirements the question actually states. The skill is not allowed to invent record counts, latency or scale to justify a fancier answer. If the question states a version, platform or execution context, that context must be respected.

A candidate that survives becomes the answer, with one line on why the common approach is weaker under the stated conditions. If nothing survives, it says so. The common answer done correctly is often already the professional one.

The goal is not more elaborate answers. It is making the model earn the right to give the obvious one.

Two disciplines inside that pass do a lot of the work.

The skill separates how FileMaker behaves from why it behaved that way in your file. A documented mechanism is fact. Whether it caused your symptom is a hypothesis until the evidence says so, and where possible the answer hands you a check that settles it.

The second is about how AI reads Claris Help, and this one you can demonstrate for yourself. Ask a model a FileMaker behaviour question and watch what it does. It searches, finds something that looks like the answer, and stops reading. But in Claris Help the behavioural reality often is not in the body text. It is in the Notes and platform sections underneath. The body says what a feature does. The Notes say when it does not, on which platform, in which execution context, under which conditions. A model that stops at the body gets the happy path and misses the exception that breaks your file.

The skill does not let a page count as read until the Notes and platform sections have been. It searches for the feature's own terminology rather than keywords that conveniently confirm the model's theory, and it keeps "I could not find it" separate from "Claris does not document it", which are different findings a first pass conflates constantly. During development, this discipline alone produced a striking improvement in right answers to the problems posed. Not the whole skill. Just reading the page properly.

The skill itself is deliberately short. There is nothing in it to look up.

## What it is not

Not a knowledge file. No function reference, no technique catalogue, no worked recipes. That is the job of the reference repos below, and this composes with them rather than replacing them.

A model can have perfect access to the function reference and still choose the wrong architecture. It can quote the correct Help page and still diagnose the wrong cause. It can produce syntactically perfect XML and still build a system that degrades in production.

Knowledge solves knowledge problems. This addresses a reasoning problem.

## Why it will not last

The skill is intentionally self-invalidating. As models improve and this way of thinking spreads, the gap between the common answer and the professional one closes, and the correction stops earning its keep. The skill says so itself, in its own final section: when the second pass consistently confirms the draft, retire it. That is the intended outcome.

Use it while the window is open.

## Status

Built from using AI on production FileMaker work, watching where its answers held and where they quietly did not, and diffing the same problems solved with and without the skill until the difference was clear enough to write down. Every comparison was judged one way: did the result hold up in a real system. The strongest signal has been on production files, exactly the cases it was built for. Where a comparison needed a known-good baseline, one existed: a large body of accepted FileMaker answers built up over years of client and community work.

On that material it has changed answers that looked right but carried a silent production risk, and caught documentation and applicability gaps a first pass missed. Encouraging. Not a benchmark.

## Using it

The skill is a single file, SKILL.md. Nothing to build, nothing to configure.

For Claude Code, copy it into your project as `.claude/skills/second-opinion/SKILL.md` and it loads automatically. For claude.ai, add it to a Project's knowledge or attach it to a conversation. It works alongside other skills, including the reference repos below, and applies itself only to FileMaker technical work.

It needs a model that can search and fetch web pages to run the Claris Help grounding. Without that, the classification and challenge passes still work; the documentation discipline does not.

## The rest of the collection

Second Opinion is the reasoning layer. These are the repos underneath it, all empirically derived through round-trip testing.

**[Script XML Skill](https://github.com/andykear/FileMaker-XMLsnippet-Claude-Skill)**
Makes AI generated scripts paste correctly. Full step ID dictionary and the hidden paste handler rules.

**[Layout XML Skill](https://github.com/andykear/FileMaker-XMLsnippet-Layout-Claude-Skill)**
Paste ready layout objects. All object types, flags decoded, element order confirmed.

**[Field Definitions](https://github.com/andykear/FileMaker-XML-field-definitions)**
Field and table definition XML, verified down to auto enter, validation and calculation options.

**[XML Inspector](https://github.com/andykear/FileMaker-XML-inspector-open-source)**
Reads a Save as XML export in the browser. Finds unreferenced fields, broken references, diffs two versions.

**[XML Scrubber](https://github.com/andykear/FileMaker-XML-scrubber)**
Strips API keys, passwords and internal hostnames from FileMaker XML before you share it with an AI tool.

**[AI Vocabulary](https://github.com/andykear/FileMaker-AI-vocabulary)**
Verified names and internal IDs for FileMaker functions and script steps, so an AI stops inventing them.

## Licence

CC BY 4.0. Use it, adapt it, build on it, keep the attribution.

**Andrew Kear** · Claris Partner · Claris MVP · [clockworkct.co.uk](https://clockworkct.co.uk)
