# PITCH.md

Six lines and a lever. Your words. The last two are scored.

Built: A support agent for disrupted flights, with Larkspur's nine tools, seats_left written by us, and fare_rules over MCP.
Does: It finds the booking, looks for flights with free seats, holds one, and explains the fare rules in plain words.
Number: 61,706 to 64,120 tokens in, total of the five tickets.
Safety check: It holds a seat but never books it, only the customer's own click does. We saw it in the trace for K7PQ2M.
Next: Let the agent answer customers in Spanish, not only in English.
Still broken: When a customer sends two booking codes in one message, the agent only looks up the first one.
Lever: <cost | speed | intelligence>

## Priya asked

Costs:
Wrong:
Runs it:
Left out:
