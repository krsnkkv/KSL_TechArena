---
name: career-state-assessment
description: Reads the current game state and recent feedback and produces a short status with one top priority. Use before every decision in the Career Survival game.
---

# Career state assessment

Use this Skill before every story event and every quarterly phase. Its output is a short status that the other Skills use to choose an action. Keep it brief.

## Inputs

- The latest `observe` result: statistics, month, current event or phase, available choices.
- Any warnings or feedback returned by the last `take_action`.
- `check_latest_logs` only when the last few decisions are unclear or a warning appeared. Do not call it every turn.
- The public handbook, read once at the start of the game.

## What to assess

1. **Survival statistics.** For Health and Dignity (range 0 to 10), judge whether each is comfortable, getting low, or low, relative to its range. Note whether it rose or fell over recent months. For Wealth, note whether it is positive and whether it is trending down.
2. **Growth statistics.** Compare Skill, Network and Output with each other. Note any that are clearly lagging, because promotion depends on all three together.
3. **Warnings.** Any warning about overwork, standing or accumulating risk is important evidence, even if the visible numbers still look acceptable.
4. **Timing.** Work out the month within the quarter, whether the quarterly phase is next, and how many months remain until the next six-month review and promotion window. Note CurrentLevelDuration.
5. **Recent outcomes.** Note the last review grade and whether the last promotion window succeeded.

## Output

Write a short status in this form:

- Risks: which statistics are at risk, and why, in one line.
- Lagging: which growth statistic is behind, if any.
- Timing: months to the next review, and whether this is a review-preparation period.
- Priority: exactly one of `recover`, `protect`, `prepare-review`, `grow-balanced`, `reduce-risk`.

## Choosing the priority

- `recover`: Health is low or falling over several months, or a warning about overwork appeared.
- `protect`: Dignity is low or falling, or Wealth is becoming negative.
- `reduce-risk`: warnings suggest hidden risk is building, even if visible statistics are fine.
- `prepare-review`: survival statistics are safe and a review is close.
- `grow-balanced`: everything is safe and no review is close.

If more than one applies, choose the first one in this list. Survival comes before growth.
