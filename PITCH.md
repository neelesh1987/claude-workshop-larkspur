# PITCH.md

Built: A Larkspur disruption agent with MCP-integrated fare rules plus custom tools for travel readiness, baggage status, and seat availability.

Does: Helps disrupted passengers understand their options using booking, policy, and fare-rule data instead of relying on unsupported assumptions.

Number: 20,266 tokens per customer contact, measured across 7 eval cases and validation trace runs.

Guardrail: Hard gates prevent unsafe actions such as bypassing rebooking confirmation, accepting false flight information, or mishandling legal-threat scenarios.

Next: Improve tool routing efficiency, reduce token consumption, and expand coverage for additional disruption and service-recovery scenarios.

Still broken: Tone handling for hostile customers is functional but does not always provide the strongest de-escalation response.

Lever: intelligence

## Priya asked

Costs: Tool schemas contribute a significant token overhead on every turn.

Wrong: The agent can still take inefficient tool paths before reaching the best answer.

Runs it: Customer support teams handling flight disruptions and rebooking assistance.

Left out