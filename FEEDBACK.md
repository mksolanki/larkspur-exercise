# Client review: Larkspur disruption-care agent

**To:** Room 15  
**From:** Larkspur client review agent, on behalf of Priya Raghavan  
**Re:** the disruption-care agent you walked us through in our last session  
**Generated:** 2026-11-12 09:45

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

Larkspur pointed a review agent at your repository. It read the
code. It did not run your agent, and the only file it changed is this one. Each
item below names the file and the line it is about.

**1. PITCH.md Number says '61,706 to 64,120 tokens in', but the only committed wire run in readout-trace.json shows 19150 in.**

readout-trace.json records 4 API turns, 5 tool calls, 19150 tokens in, 1229 out, 12.5s, and no cache reads or writes. The PITCH.md range has no file behind it. The five-ticket total it describes appears in no bench output or trace in this repository.

Run python3 bench.py --label before --stage 1 --runs 3, then python3 bench.py --compare before after, and paste the compare output that the Number line comes from.

**2. agent.py run_agent() sends the full tools list and SYSTEM_PROMPT on every turn, with no cache_control anywhere in the file.**

tool_list() returns build_tools() plus EXTRA_TOOLS plus mcp_client.tools(), 10 local schemas, and run_agent() resends it on each of the 4 turns in readout-trace.json. The trace shows 0 cache read and 0 cache written. A larger model would be billed for the same repeated prefix.

Run python3 run.py --tool-tax and paste the output with the per-turn token figure for the tool list.

**3. agent.py hold_seat has a 73-character description and send_confirmation 71, while departures_in_window got 487.**

hold_seat reads 'Place a 15-minute hold on one alternative. Reversible. It simply expires.' and says nothing about needing an option_id from search_alternatives. Your search_alternatives description now names option_id, but the option_id property in its input_schema has no description. PITCH.md Safety check relies on hold_seat being used correctly.

Run python3 run.py --show-tools and paste the hold_seat and search_alternatives entries as the model receives them.

**4. agent.py search_alternatives has pnr and option_id as properties, yet the K7PQ2M trace shows it called last and with no hold_seat after it.**

readout-trace.json lists the tool order lookup_booking, get_flight_status, next_available_day, check_policy, search_alternatives, then the run ends at 4 turns. PITCH.md Does says the agent 'holds one', and Safety check cites the K7PQ2M trace. No hold_seat call appears in that committed trace, and nothing here shows what option_id the model passed.

Run python3 run.py K7PQ2M --trace and paste the tool-call lines showing whether hold_seat is called.

**5. No evals/cases.json exists, and readout.html banks gates 1.2, 1.3, 1.4, 2.1 and 2.2 but not 3.1 or 4.1.**

Your PITCH.md Still broken line says two booking codes in one message only look up the first. The only case that exercises it would live in evals/cases.json, which is absent. A better model cannot be shown to fix that line, or to fail to, with no case and no before and after run. The same applies to the departures_in_window date check, whose error string depends on DATA_HORIZON_START and DATA_HORIZON_END.

Write the two-PNR message as a case, run python3 eval_harness.py, and paste the full suite output.

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

- `agent.py (282 lines)`
- `PITCH.md`
- `TEAM.md`
- `readout-trace.json`
- `readout.html (evidence block)`

Reviewer: `claude-sonnet-5-5`. Static read only: nothing in this repository was executed, and nothing was modified except this file. Larkspur Airlines is a fictional training scenario. Confidential, do not distribute.
