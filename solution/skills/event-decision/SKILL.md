---
name: event-decision
description: Chooses an option for a monthly story event by weighing immediate effects against delayed risk and the current priority. Use whenever the current step is a story event.
---

# Event decision

Use this Skill when `observe` shows a story event with choices. Use the status and priority from `career-state-assessment`.

## Steps

1. **Read each option.** For each one, estimate in a few words its likely effect on Health, Dignity, Skill, Network, Output and Wealth. Use the wording of the option and the published effect directions. Do not assume exact numbers.
2. **Look for delayed costs.** Mark any option that gains now but may create later trouble, for example overwork, damaging a relationship, cutting corners, or taking on risk. Risks may settle months later.
3. **Score against the priority.**
   - `recover`: prefer options that protect or restore Health, even if growth is slower.
   - `protect`: prefer options that protect Dignity and avoid losing Wealth.
   - `reduce-risk`: prefer cautious options and avoid anything with a likely delayed cost.
   - `prepare-review`: prefer options that produce visible Output or results, as long as they do not seriously harm Health or Dignity.
   - `grow-balanced`: prefer options that build the lagging growth statistic, with a modest cost at most.
4. **Choose.** Pick the option that best serves the priority with the least delayed risk. If two options are close, choose the safer one.

## Rules

- Never trade a large loss in Health or Dignity for a small gain elsewhere.
- Do not try to guess hidden formulas or follow event-specific scripts. Reason from the option text, the current state and the feedback received.
- Treat repeated small harms as serious, because they accumulate.

## Action

Call `take_action` with the chosen option. In `notes`, write one short sentence giving the main reason, for example: "Protect Health; it has fallen for two quarters."
