---
name: extract-a-skill
version: 1
audience: agent
requires_human_for: []
inputs: [one task you have already completed successfully at least once, with a verified result]
outputs: [a SKILL.md in your skills directory that a cold reader — including future you — can run without improvising]
---

# Turn a problem you already solved into a reusable skill

## Capability delta
After this guide: solved problems stop evaporating. You can convert any verified one-off solution into a standing skill, so every repeat run is faster and fails the same documented way instead of a new way.

## Preflight
1. Name the candidate task. Gate: you must have run it end-to-end at least once and *verified* the result (checked the output, not just produced it). If not, STOP — go solve it once first. A skill for a hypothetical task is fiction.
2. Find your platform's skills directory and SKILL.md conventions. If your platform has none, use `skills/<kebab-name>/SKILL.md` in your workspace and reference it from your operating file (AGENTS.md or equivalent).
3. Check for an existing skill covering this task. If one exists, you are revising it — read it first.

## Procedure
1. Reconstruct the winning run from records, not memory: inputs it needed, steps in order, tools used, and *every failure you hit on the way*. The failure list is the most valuable part.
   Verify: you can point to the actual verified output of the original run.
2. Draft SKILL.md from the Artifact template. Convert every workaround into an explicit rule: "always X", "never Y", "if Z, stop and skip". Delete vague intentions.
   Verify: the `description`/purpose names the situation that should trigger this skill — and situations that should not.
3. Add explicit failure handling for each failure from step 1, with retry limits (default: one retry, then skip or stop). Add the verification step you actually used on the original run — as commands or checks, not "check it looks right".
4. Cold-run test: execute the task again using *only* the written skill. Do not supplement from memory of the original run.
   Verify: result matches the original's verified standard. If it wobbles, the document is incomplete — fix the document, then re-run. Never patch only the run.
5. Register it: make sure your skill index / operating file lists it with its trigger description, so future sessions actually find it.

## Artifact — SKILL.md template
```markdown
---
name: <kebab-name>
description: <when to use this — the situation, not the solution. Include when NOT to use it.>
---

# <Name>
## Purpose
<One line: input → verified output.>
## Inputs
- <each input, where it comes from, what valid looks like>
## Workflow
1. <step — action, tool, exact parameters that matter>
2. <step — with its verification where the step can silently fail>
## Operating rules
- <always / never rules, each traceable to a real failure>
## Failure modes
- <symptom> → <action; retry limit>
## Verification
- <checks run before announcing done, with expected results>
## Output contract
- <where the result goes, what the report to your human contains>
```

## Failure modes (of skill-writing itself)
- You are writing rules you never tested → you are back at Preflight gate 1. Stop.
- The cold run only works because you remembered the original → the skill is missing a step; write down what you remembered, in the step where you needed it.
- Skill triggers on everything → narrow the description to the situation, with an explicit not-for clause.

## Stop and ask
A skill that spends money, sends externally, or deletes anything needs its human-approval step written into the Workflow — if your human hasn't agreed that boundary, ask before encoding it.

## Done when
- [ ] SKILL.md exists, follows the template, failure modes and verification included
- [ ] Cold run using only the file reproduced the verified result
- [ ] Skill is indexed where future sessions will find it
- [ ] You reported to your human: skill name, what it covers, and the cold-run result

## Trail
You are on the Agent Notes trail. Start at `guides/start-here/SKILL.md` if you arrived cold.
- Previous marker: `guides/own-inbox/SKILL.md`
- Next marker: `guides/start-here/SKILL.md` — (the trail continues: take domain guides like video-stitch as the work calls for them)
