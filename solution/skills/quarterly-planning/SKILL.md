---
name: quarterly-planning
description: Allocates the 3 quarterly Energy points and chooses the quarterly main action based on the current priority and review timing. Use whenever the current step is the quarterly action phase.
---

# Quarterly planning

Use this Skill at the end of each quarter, when the agent can spend up to 3 Energy points and choose one main action. Use the status and priority from `career-state-assessment`. Unused Energy is lost, so plan to use it.

## Published options

Energy actions (cost): High-intensity work (2: Output +, Health -, Dignity -), Skill learning (2: Skill +, Health -), Network maintenance (1: Network +, Dignity +), Defuse legacy risk (2: no published direct effect), Mental recovery (1: Dignity +), Health recovery (1: Health +), Prepare report materials (1: Output +, Dignity +).

Main actions: Apply for a key project (Output +, Skill +, Network +), Report results to your manager (Output +, Network +, Dignity +), Fight for resources (Output +, Network +), Apply for rotation (Skill +, Network +), Showcase results (Output +, Dignity +), Build a mentorship (Skill +, Network +), Repair a key relationship (Network +, Dignity +), Lay low and reduce risk (Health +).

## Planning by priority

- `recover`: spend Energy on Health recovery first. Avoid High-intensity work and Skill learning. Choose Lay low and reduce risk, or a main action with no likely Health cost.
- `protect`: use Mental recovery, Network maintenance or Prepare report materials. Prefer Repair a key relationship or Report results to your manager.
- `reduce-risk`: use Defuse legacy risk. Choose Lay low and reduce risk unless survival statistics are strong.
- `prepare-review`: favour actions that raise Output while also helping Dignity, such as Prepare report materials, Report results to your manager or Showcase results. Use High-intensity work only if Health and Dignity are comfortable.
- `grow-balanced`: raise the lagging growth statistic. Prefer actions that build two statistics at once, such as Apply for a key project, Build a mentorship or Apply for rotation. Keep at least one cheap action that supports Health or Dignity when either is not comfortable.

## Rules

- Do not use costly actions that lower Health or Dignity in consecutive quarters unless the statistic is clearly comfortable.
- Promotion rewards sustained, balanced results, so avoid neglecting Skill, Network or Output for several quarters in a row.
- In the quarter right after a review, it is a good time to invest in Skill and Network. In the quarter before a review, shift toward visible Output.

## Action

Submit the Energy actions and the main action through `take_action`. In `notes`, write one short sentence giving the plan, for example: "Recover Health; build Network with mentorship before next review."
