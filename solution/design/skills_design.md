# Skills design

## 1. The task as we understand it

The agent plays a new hire on a product R&D team for up to 48 months. Each month brings story events, each resolved by choosing one option. At the end of each quarter the agent spends up to 3 Energy points on Energy actions and chooses one main action. Every six months there is a performance review (grades S to D) and a promotion window across ten levels (L1 to L10).

The visible statistics are Health and Dignity (0 to 10), Skill, Network and Output (0 and above), Wealth, Level, Energy and CurrentLevelDuration. Exact formulas, failure thresholds, hidden risk and event probabilities are not published, and many consequences settle months after the decision that caused them.

A good run must therefore balance two goals that pull against each other: **survive** all 48 months, and **progress** through reviews and promotions. The final score rewards level, wealth, end-of-run Health and Dignity, skill, risk control and network.

## 2. Skills and how responsibilities are divided

We use a single agent (JiuwenSwarm 0.2.4b3, `"mode": "agent"`) with three Skills. We split the work into **assessing** (what matters most right now?) and **choosing** (which option serves that?), because the two need different information and mixing them made the instructions long and inconsistent.

| Skill | Responsibility | Used |
|---|---|---|
| `career-state-assessment` | Turns the current state into a short status and exactly one priority. | Before every decision |
| `event-decision` | Chooses a story-event option against that priority. | Story events |
| `quarterly-planning` | Allocates 3 Energy points and picks the main action against that priority. | Quarterly phase |

### career-state-assessment

- **Purpose:** to decide what matters most right now, once, so the choosing Skills don't each re-derive it.
- **Information used:** the latest `observe` result (statistics, month, event, choices), warnings and feedback from the last action, the public handbook (read once), and `check_latest_logs` only when something is unclear.
- **What it judges:** whether Health and Dignity are comfortable, getting low or low relative to their 0 to 10 range, and their trend; whether Wealth is positive; which of Skill, Network and Output is lagging; any warning about overwork, standing or accumulating risk; months to the next review and CurrentLevelDuration; and the last review grade and promotion outcome.
- **Output:** four short lines (Risks, Lagging, Timing, Priority). The priority is one of `recover`, `protect`, `reduce-risk`, `prepare-review` or `grow-balanced`, taken in that order of precedence, so survival always outranks growth.

### event-decision

- **Purpose:** to pick one option for a story event.
- **Information used:** the option texts, the published effect directions, the current status and priority.
- **Method:** estimate each option's likely effect on each statistic in words (no invented numbers), mark options with delayed costs (overwork, damaged relationships, cut corners), score the options against the priority, and break ties toward the safer option. It never trades a large Health or Dignity loss for a small gain, treats repeated small harms as serious.

### quarterly-planning

- **Purpose:** to allocate the 3 Energy points and choose the main action.
- **Information used:** the published Energy and main actions with their effect directions (restated briefly inside the Skill so the agent doesn't need to re-read the handbook), the priority, and the review timing.
- **Method:** a mapping from each priority to preferred actions, plus cross-cutting rules: use all Energy; don't take Health- or Dignity-costly actions in consecutive quarters unless comfortable; don't neglect any of Skill, Network or Output for several quarters; invest in Skill and Network just after a review and in Output just before one.

## 3. How the outputs combine into a decision

1. `observe` returns the state, the event or phase, the choices and the feedback text.
2. `career-state-assessment` produces the status and one priority.
3. Depending on the step type, `event-decision` or `quarterly-planning` picks a choice using that priority.
4. The agent calls `take_action` with the choice and a one-sentence reason in `notes`.
5. The outcome and the next month's feedback flow into the next assessment, so the agent adapts during the run without a separate memory Skill.

The single priority is the only interface between the Skills. That keeps each Skill independent and easy to change, and it keeps the per-decision reasoning short, which matters for token efficiency over more than 200 decisions.

## 4. Scripts and reference files

None of the Skills uses a `script/` or `reference/` directory. The decisions are judgements about natural-language options, and there is no deterministic computation a script would do better. The only published facts the agent needs repeatedly (the Energy and main-action effect directions) fit in a few lines inside `quarterly-planning`. A separate reference file would add a tool call and more tokens on every quarter without adding information.

## 5. What the Skills deliberately do not do

- No hard-coded numeric thresholds. Judgements are relative to each statistic's published range, and to trends and feedback.
- No event-specific scripts or memorised answers for the development dataset.
- No use of engine or dataset internals.
