# Model weight tiers

Use these when the harness lets you pick a model per teammate. A workstream's
**weight** is the reasoning and risk of its hardest part, not its average.

| Weight     | Models                   | Use it for                                                                                                  |
| ---------- | ------------------------ | ----------------------------------------------------------------------------------------------------------- |
| Super high | Claude Fable             | Novel design or algorithms, shared contracts, security, money, concurrency, data migrations, deep ambiguity |
| High-mid   | Claude Opus, GPT Sol     | Substantial multi-file logic, non-trivial integration, tricky state and edge cases                         |
| Mid-low    | Claude Sonnet, GPT Terra | Well-specified work that follows existing patterns: endpoints, components, tests against a fixed contract  |
| Low        | Claude Haiku, GPT Luna   | Mechanical work: copy, config and env wiring, renames, fixtures, docs, boilerplate, read-only search       |

## Split by weight

Carve the parts that need deep reasoning (shared contracts, tricky logic, risky
paths) into small workstreams of their own. Heavy models then do only that, and
lighter tiers take the bulk. In the plan, show a table: workstream, owned files,
weight, model, reason.

## Availability

- **Check once, before assigning.** T3 Code: call `orchestrator_capabilities` and
  take the newest model per family (e.g. `claude-fable-*`, `gpt-*-sol`). Claude
  Code: the `Agent` tool's `model` takes `fable`, `opus`, `sonnet` or `haiku`.
  Elsewhere: the models the harness lists. Another provider's model (e.g. Sol
  under a Claude lead) needs a harness that runs it, such as T3 Code's
  `delegate_task`.
- **Tier unavailable:** use the nearest heavier tier, else the nearest lighter
  one. List each substitution in the plan.
- **Two models in a tier:** keep workstreams that need close back-and-forth with
  you on your own provider. Spread the rest across providers to balance rate
  limits.
- **No model choice:** every teammate inherits your model. Skip weights.
