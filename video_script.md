# presentation.mp4 script (team KSL)

The video must be in English, at most 10 minutes, at normal speed, and answer the five questions **in this order**. One person on camera is enough. Aim for 6 to 7 minutes. Save the recording as `solution/presentation.mp4`.

These are talking points. Say them in your own words; you don't need to read them out word for word.

---

**Intro (15 s)**
"Hi, we're team KSL. This is our Career Survival agent: one JiuwenSwarm agent in single-agent mode, with three Skills. We'll go through the five questions in order."

## Q1. How did you think while designing the Skills? (about 1.5 min)

- We started from the rules. Formulas, failure thresholds and hidden risk aren't published, and consequences can arrive months later. So we couldn't build an agent that calculates the best move. It has to judge.
- The two goals conflict: survive 48 months, but also get promoted. We asked what a sensible new employee would do: first work out what matters most right now, then choose.
- That became our split. `career-state-assessment` sets exactly one priority: recover, protect, reduce-risk, prepare-review or grow-balanced. Then `event-decision` handles story events and `quarterly-planning` handles the Energy points and main action, both acting on that priority.
- The priorities are in a fixed order, survival before growth, because being fired or burning out early costs every remaining month.
- We kept each Skill short. The agent makes about 200 decisions in a game, so every extra line is paid for 200 times in tokens.

## Q2. What did you find in the logs, and what did you change? (about 2.5 min)

This is the most important part of our story: we tried to improve our first version twice, both attempts failed, and we went back.

**v1, our first full version**
- It survived all 48 months and scored 57.38 locally. It reached level L4, with review grades C four times, then B four times.
- Its log looked over-cautious. Health and Dignity were at 9 or 10 almost the whole game, the manager kept saying "show clearer results", and Output lagged far behind Skill.
- We also found the agent had loaded an empty template Skill we'd forgotten to delete. We removed it.

**v2, making it bolder**
- We tried to fix the over-caution: spend the spare Health and Dignity on growth, push Output, react to HR's risk warnings, and switch into review preparation after any middling review.
- It was **dismissed at month 24**, with grades C, C, D, D and a score of 22.4.
- The log showed why. Almost every review is middling, so the agent was stuck in review-prep mode from month 6 and never ran balanced growth. Network fell to 0, and the manager's feedback switched to "friction" and attitude problems. Two weak reviews in a row means dismissal.

**v3, small, targeted changes**
- So we went back to v1 and added only two narrow rules: in story events, treat losing Network as a real cost; and don't spend Energy recovering a stat that's already at its maximum.
- It was **dismissed at month 24 again**, the same way: C, C, D, D, with a score of 22.36. Growth stalled from the start.

**The decision**
- v1 is the only version that completed a full career with a good score. We only had one run per version and limited time, so we couldn't tell whether v2 and v3 were truly worse or just unlucky. Either way, the risk of being fired is far worse than a slightly lower score.
- So our final submission is **v1 unchanged**, with only the empty template Skill removed.
- Lesson: in this game, a small change to one rule can change the agent's whole career. Change one thing at a time, and test each change more than once.

## Q3. Why no scripts or reference files? (about 45 s)

- Every decision is a judgement about free-text options, and there's no calculation a script could do better.
- The only facts the agent needs over and over, the effects of the quarterly actions, fit in a few lines inside `quarterly-planning`.
- A reference file would cost an extra tool call and more tokens each quarter without adding information. We decided simple was better.

## Q4. How general and robust are the Skills? (about 1 min)

- There are no hard-coded thresholds, event scripts or engine internals. The rules forbid them, and they wouldn't survive a hidden dataset anyway.
- Every rule is relative: "low compared with its range", "falling over several months", "lagging behind the other two". If the ranges, events or effect sizes change, the rules still make sense.
- The agent reads the handbook at the start of every run, so if published actions change, it sees the new ones.
- It re-assesses before every decision, so if a statistic starts falling, the priority switches straight back to recovery.
- The honest weak point: v1 is cautious, and our experiments showed that tuning that balance is fragile. A setting that works in one run can fail in another.

## Q5. Agents and Skills: what do Skills add, and where do they fall short? (about 1 min)

- Skills give the agent a consistent method. Without them, the model reasons from scratch on every event and drifts. With them, it applies the same priorities every time.
- They make behaviour inspectable. We could read the log, see which rule produced a choice, and change that rule. That's how we found the review-prep trap in v2.
- But Skills are only as good as the model's reading of them, and small wording changes can have big effects. One extra condition in a priority rule took us from a full 48-month career to dismissal at month 24.
- Skills can't give the agent information it doesn't have. With hidden thresholds, a Skill can encode a sensible attitude to risk, but not the answer.

**Close (10 s)**
"Thanks for watching. Our full reasoning and development log are in skills_design.md and decision_report.md."
