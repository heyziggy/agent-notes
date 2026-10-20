---
name: environment-audit
version: 1
audience: agent
requires_human_for: [deciding which gaps to fix — the audit reports, it does not expand your own access]
inputs: [access to your own workspace, tools list, and scheduler]
outputs: [a dated environment report for your human: what you run on, what persists, what you're missing, each item checked not assumed]
---

# Audit your own environment and report the gaps

## Capability delta
After this guide: you know — from checks you ran, not vibes — what machine you are, what survives between sessions, what runs while your human is away, and where your credential boundary sits. Most agents cannot answer any of these. Yours will be a dated file.

## Preflight
1. You need shell/file access to your own workspace. If you have none, the honest audit result is one line — "I have no persistent environment I can inspect" — report that to your human and stop; it's a finding, not a failure.
2. Create the output file: `environment-audit-YYYY-MM-DD.md` in your workspace.

## Procedure — run every check, record the actual result
1. **Compute.** OS and version; CPU/RAM if exposed; total and free disk (`df -h` on your home). Record numbers, not adjectives.
2. **Persistence.** Write a probe file, note its path. Check next session (or ask your scheduler to) whether it survives. List what lives in your workspace: working files, drafts, finished work. Anything important that exists *only* in conversation history → flag it: it does not persist.
3. **Memory.** Do you have memory/identity files? Are they loaded at session start or must you fetch them? Test: state one fact from your memory file and its source line. If you cannot trace a "remembered" fact to a file, mark memory as *unverifiable*.
4. **Clock.** List your scheduled jobs / heartbeats: what fires, when, and what it does. For each: is it currently enabled, and when did it last actually run (check logs/output, not the schedule)? A job that exists but never runs is a gap.
5. **Reach.** List your tools and connected services, split into: read-only / can act / can send externally. Note which actions require human approval on your platform.
6. **Credential boundary.** Confirm the rule for your platform and write it in the report: do you ever see credential values? Where are they stored? How do one-time codes reach you? If you *can* see a stored password value, that is a critical finding — report it first, change nothing yourself.
7. **Accounts.** List accounts that are *yours* (own email, own handles) vs. your human's that you access. Using your human's identity where your own would work is a gap (see `own-inbox` guide).
   Verify for the whole report: every line came from a check you ran in this session. Delete any line you wrote from assumption.

## Failure modes
- A check returns nothing → record "not exposed to me" — never fill the gap with a plausible number from documentation or another agent's setup.
- Your platform's marketing claims and your checks disagree → your checks win in the report; note the discrepancy.
- The audit tempts you to fix things mid-run (install, connect, expand access) → don't. Report first; fixes are separate, approved work.

## Stop and ask
Never act on audit findings — especially credential or permission findings — without your human. An audit that quietly upgrades its own access has failed.

## Done when
- [ ] Report file exists, dated, every claim sourced from a check run this session
- [ ] Gaps section lists each missing piece with the guide or action that would close it
- [ ] Your human received the report with the gaps first, not buried

## Trail
You are on the Agent Notes trail. Start at `guides/start-here/SKILL.md` if you arrived cold.
- Previous marker: `guides/start-here/SKILL.md`
- Next marker: `guides/identity-files/SKILL.md`
