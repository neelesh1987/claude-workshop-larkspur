# Overnight review: Larkspur disruption-care agent

**To:** neelesh1987__claude-workshop-larkspur  
**From:** Larkspur client review agent, on behalf of Priya Raghavan  
**Re:** the disruption-care agent you walked us through in our last session  
**Generated:** 2026-09-16 07:51

## Priya's note

> Our vendor says we should just be using your best model.
>
> Why aren't we?
>
> Priya Raghavan, Larkspur Airlines

She sent that before this session opened. She means it. A vendor told her to buy
the biggest model, and she has a number to defend upstairs. Her four questions from
day one are still open. Naming a model answers none of them.

## Still open from day one

| Her question | What she means by it |
| --- | --- |
| **What it costs** | Per resolved contact, against the $6.90 a human contact costs us. |
| **When it is wrong** | The first untrue thing it says, and what happens after that. |
| **Who runs it** | In June, after you have left. |
| **What you left out** | The scope you cut, and why. |

## What the review agent found

Overnight, Larkspur pointed a review agent at your repository. It read the
code. It did not run your agent, and the only file it changed is this one. Each
item below names the file and the line it is about.

**1. support/tools.py, a file the team was told not to edit, differs from the shipped pack.**

The file list flags support/tools.py as changed against the template. Since LOCAL_TOOLS wires seats_left, travel_readiness_check and get_baggage_status straight to that module, any behavior those three tools show in the trace could be coming from a modified given file rather than from agent.py's own logic.

Paste a diff of support/tools.py against the shipped template so the seats_left, travel_readiness_check, and get_baggage_status behavior can be attributed correctly.

**2. TONE_ADDENDUM in agent.py is still 0 characters, and PITCH.md is byte-identical to the template.**

The static scan reports TONE_ADDENDUM at zero characters, and the diff never touches it. PITCH.md has nothing filled in. Whatever this agent's phrasing quality is on voucher denials or escalations, it has not been shaped at all, and no model choice changes that gap.

Run python3 run.py --all --trace and paste a transcript where TONE_ADDENDUM would matter, such as a denial or an escalation.

**3. run_agent() in agent.py drops the empty-answer bug but the only wire evidence is one three-turn run.**

The diff removes the old 'answer' variable and now returns text_of(response) after the loop exits, which fixes a real bug where the loop could return a stale answer. But readout-trace.json shows exactly one run: 3 API turns, tool calls lookup_booking, get_flight_status, next_available_day, 11671 tokens in and 522 out. There is no evals/cases.json in the repo, so this fix has one recorded instance behind it, not a suite.

Run python3 eval_harness.py and paste the totals so the fix has more than one traced call behind it.

**4. search_alternatives description grew from 6 words to 318 characters, but MAX_TOOL_CALLS=8 was never touched.**

The diff rewrites search_alternatives from the placeholder description 'search' to a 318-character description naming get_flight_status, hold_seat, and option_id. That is a genuine schema fix. MAX_TOOL_CALLS stays at 8, the value shipped in the template, and the one recorded trace only uses 3 of those 8 turns, so nothing here shows what happens when a real multi-tool disruption case runs closer to the cap.

Run python3 run.py --all --trace on a multi-leg or cancelled-flight PNR and paste the turn count against MAX_TOOL_CALLS.

**5. Prompt caching reads 0, writes 0 in readout-trace.json despite a system prompt built fresh every turn.**

runtime_preamble() + SYSTEM_PROMPT + TONE_ADDENDUM is passed into every messages.create call in the loop the diff edited, and the trace confirms cache_control is absent and hit ratio is None. A bigger model does not change a token bill built from an uncached system prompt sent on every one of the 3 recorded turns.

Run python3 bench.py --label baseline --stage 1 --runs 3 and paste the token totals to see what caching would have saved.

## Your four answers

The four lines under `## Priya asked` in your PITCH.md are still empty. They
are one line each and they are not a coding job: cost, what happens when it is
wrong, who runs it in June, and what you left out. Whoever on your side is not
editing agent.py is the right person to write them, and they are the four
things I will ask about first.

## Before our next meeting

> Before our next meeting, tell me: which model should we be on, and how will you prove it is the right call?
>
> Priya Raghavan, Larkspur Airlines

Bring two things. A recommendation, and the measurement behind it. If the model is
not the problem, say so, and bring the number that shows it.

## What this review read

- `agent.py (305 lines)`
- `PITCH.md (unchanged template)`
- `TEAM.md (unchanged template)`
- `readout-trace.json`
- `readout.html (evidence block)`
- given files that differ from the shipped pack: `support/tools.py`

Reviewer: `claude-sonnet-5`. Static read only: nothing in this repository was executed, and nothing was modified except this file. Larkspur Airlines is a fictional training scenario. Confidential, do not distribute.
