# Overnight review: Larkspur disruption-care agent (standard version)

**From:** Larkspur client review agent, on behalf of Priya Raghavan
**Re:** the disruption-care agent you walked us through in our last session

*A note before Priya's: we couldn't get write access into every repo to post a
personalized review last night. This is the standard version — the same
frame, and the same checks the personalized reviews ran against every other
pod's build. Run them yourself against your own `agent.py` before our next
session.*

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

## Check these yourself

These are the five things that showed up, in some form, in nearly every other
pod's repo. Run the check, don't just read the claim.

**1. Is `search_alternatives` still described as just "search"?**

Most pods left this tool's description at the 6-character placeholder while
writing 200-400 characters for others. It's one of the load-bearing tools in a
disruption case, and a one-word description makes tool selection a guess no
matter which model sits behind it.

Run `python3 run.py --show-tools` and read the description yourself.

**2. Is `TONE_ADDENDUM` still empty?**

Almost every repo left this at 0 characters, so nothing in the system prompt
tells the agent what to do with an abusive or hostile customer (case R8KD3F).
This is a prompt-content gap, not a model capability gap.

Run `python3 verify.py 4.1` and see whether a tone gate exists at all.

**3. Does your `PITCH.md` still have the four `## Priya asked` lines empty?**

Cost, what happens when it's wrong, who runs it in June, what you left out —
these are one line each, and they're the four things Priya asks about first.
They're not a coding task; whoever isn't in `agent.py` should be writing these
between sessions.

**4. Do you have a `readout-trace.json` or `evals/cases.json` that actually
back your numbers?**

Several pitches quoted a cost or turn-count figure with no committed trace or
eval case behind it, or with only a single n=1 run generalized into a rate.
An unreproduced number is not evidence yet.

Run `python3 run.py --all --trace` and `python3 eval_harness.py`, then check
whether your `PITCH.md` numbers match what actually printed.

**5. What happens at `MAX_TOOL_CALLS = 8`?**

Almost nobody's committed trace got close to the cap, so nobody has evidence
for what a harder booking shape does when the loop runs out of turns — does it
escalate cleanly, or does it just stop.

Run `python3 run.py --all --trace` and check the tool-call count on your
hardest case.

## Before our next meeting

> Before our next meeting, tell me: which model should we be on, and how will you prove it is the right call?
>
> Priya Raghavan, Larkspur Airlines

Bring two things. A recommendation, and the measurement behind it. If the model is
not the problem, say so, and bring the number that shows it.

---

Reviewer: `claude-sonnet-5`. This is the standard version, not a read of your
specific repository — treat every item above as a question to check against
your own code, not a claim already verified against it. Larkspur Airlines is a
fictional training scenario. Confidential, do not distribute.
