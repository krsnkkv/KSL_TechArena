# career-survival-final (team KSL)

This is team KSL's final submission for TechArena Career Survival Agent. It runs on JiuwenSwarm 0.2.4b3 in single-agent mode (`"mode": "agent"`). The agent plays one 48-month career through the `career-emulator-engine` MCP tools, using three Skills.

## Skills

| Skill | What it decides | When it is used |
|---|---|---|
| `career-state-assessment` | Reads the latest state, warnings, recent outcomes and the review timing, then sets exactly one priority: `recover`, `protect`, `reduce-risk`, `prepare-review` or `grow-balanced`. | Before every decision. |
| `event-decision` | Picks an option for a monthly story event. It estimates each option's likely effects, flags delayed costs, and scores the options against the current priority. | When the current step is a story event. |
| `quarterly-planning` | Allocates the 3 quarterly Energy points and chooses the quarterly main action, based on the priority and the time to the next review. | When the current step is the quarterly phase. |

Assessment and choice are kept apart, so each Skill stays short and does one job. The priority is the only thing passed between them.

## Design principles

- Survival comes first: when Health or Dignity is low or falling, or a warning appears, recovery outranks growth.
- Options with delayed costs (overwork, damaged relationships, cut corners) are treated with suspicion, and repeated small harms count as serious.
- Review timing matters: invest in Skill and Network after a review, shift toward visible Output before one.
- Promotion needs balanced Skill, Network and Output.
- There are no hard-coded thresholds, event scripts or engine internals. Each judgement is made relative to a statistic's published range and to feedback from the run.

## Files

- `manifest.json`: team, submission name, mode and the agent instruction.
- `skills/*/SKILL.md`: the three Skills. They have no scripts or reference files (see `design/skills_design.md`).
- `design/skills_design.md`: each Skill's responsibilities, inputs and how they combine.
- `design/decision_report.md`: the decision approach, information used, risks, generalisation and the development log.
- `presentation.mp4`: the team video.
