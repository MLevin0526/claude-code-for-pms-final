---
name: review-checklist
description: Reviews a product brief against the PM's standard five-point checklist before it goes any further. Use when the user says "review this brief", "run the review checklist", "check this brief", or points at a brief (.md, .docx) and wants it checked before it moves on.
---

# Review checklist for briefs

Run the same five checks, in this order, on whatever brief the user points at. Do not ask the user to explain the checks again.

## Steps

1. Find the brief. Use the path the user gave. If they gave none and there is one obvious candidate in the current folder (e.g. `brief.md`), use it and say which. Otherwise ask which file. For a `.docx`, read its text before checking.
2. Read the whole brief, start to end.
3. Run the five checks below. For each, give a verdict of **Pass**, **Partial** or **Fail**, and quote or point to the section that supports it. If a check fails, say what is missing, not just that it is.
4. Report in the format at the bottom. Review only: do not edit the brief unless the user asks.

## The five checks

1. **Owner named.** The brief names a person who owns it (not just a team or "TBD"). Pass: a named person, ideally with their role. Partial: a team or role only. Fail: no owner.
2. **Success measure.** The brief says how we will know it worked: a metric, a target or direction, and ideally when we will look. Pass: a measurable signal. Partial: vague ("improve", "better experience") or a metric with no target. Fail: absent.
3. **Scope matches start to end.** Compare the scope stated at the start (summary, goals, in/out of scope) with what the end actually delivers (requirements, solution, deliverables, next steps). Flag anything that appears at the end but not the start (scope creep), or promised at the start but missing at the end. Pass: they match. Partial: small mismatches, list them. Fail: they clearly diverge.
4. **Problem before fix.** The problem is explained before any solution is proposed, and the proposal responds to that problem. Pass: problem section comes first, with evidence or who is affected. Partial: problem is thin, or a fix appears before the problem is fully laid out. Fail: jumps to a solution, or no problem stated.
5. **Dates noted.** Both a date received and a date due are written down. Pass: both present. Partial: only one. Fail: neither. Do not guess or infer a missing date; report it as missing.

## Output format

Start with one line: the brief reviewed and an overall call: **Ready to move on**, **Fix these first**, or **Not ready**. Use Ready only if all five pass.

Then a table:

| # | Check | Verdict | Evidence / what's missing |
| --- | --- | --- | --- |

Then a short **Fix before it goes further** list, one line per Partial or Fail, in the order they appear in the table. Leave this out if everything passes.

Keep it brief. Do not add checks beyond these five; if something else stands out, mention it in one line at the end under **Also noticed**.
