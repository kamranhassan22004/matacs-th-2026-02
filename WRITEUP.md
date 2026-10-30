# Design Write-up — MATACS-TH-2026-02

## 1. Which steps use AI, and which use normal rules?

An admin first sets up a project category, including the must-have requirements, scoring areas, weights, and scoring methods. These settings are saved, **not written permanently into the code**. A reviewer uploads PDFs and selects a category. The tool reads the PDF text, and AI picks out facts such as price, experience, timeline, licence, and warranty, with supporting text. AI must not guess missing facts.

Normal program rules then check the mandatory requirements, calculate marks using the admin's settings, and sort the results. AI can help write plain-English explanations, but it cannot decide the marks or the winner. This keeps scoring predictable.

## 2. How are results consistent and easy to explain?

The tool saves the criteria and settings used for each group of proposals as a **criteria version**. If the same checked facts and settings are used again, the calculations give the same results. Saved facts are reused rather than rereading PDFs each time.

For every proposal, the reviewer can see whether each must-have requirement passed, the supporting words from the proposal, each criterion's marks and weight, the calculation, and the final reason for its position. The screen shows two decimals, but calculations keep full precision. If two final scores are exactly equal, the lower-priced proposal goes first; if prices also match, the proposal letter decides. New evaluations do not erase old results.

## 3. Where do people review or change results?

A reviewer checks unclear facts and suspicious instructions. If a must-have requirement is not met, the proposal is **ineligible**. If an important fact is missing and cannot yet be checked, it is **flagged** and not ranked. Reviewers can correct facts with evidence or override recommendations with a recorded reason. A human always makes the final award decision.

The audit record stores who acted and when, document evidence, criteria and AI versions, scores, corrections, and final decision.

## 4. What if the admin changes the criteria?

The tool saves the updated settings as a **new version**. For example, raising Price from 25% to 35% requires other weights to change so the total stays 100%. Earlier scores stay linked to the old version. New reviews use the new version. To apply new rules to old proposals, the team starts a new recorded scoring run.

## 5. What could go wrong, and how do we prevent it?

- **PDF read incorrectly:** keep the original words and page references; ask a person to check unclear fields.
- **AI makes up information:** require supporting text for every extracted fact; otherwise mark it missing.
- **A proposal tries to instruct AI:** treat proposal text as data, not commands. Ignore and record the suspicious instruction attached to proposal C; do not give it extra marks.
- **Unfair or changing scores:** apply the same saved rules to every bidder, show the calculations, and keep a record of changes.
- **Missing details:** do not invent a licence or completion date; flag the proposal when a required fact is unclear.
- **Cost and privacy:** extract only what is needed, reuse checked information, limit access, and use only the fictional samples for this exercise.

## Example scoring rules used for the sample ranking
## these are just assumed values for scoring, it can be change according to the requirements
**These are proposed settings, not formulas supplied by MATACS.** The admin could choose these scoring methods and numbers through the category setup screen:

| Area | Example calculation | Why this approach? |
|---|---|---|
| Experience (30 marks) | 2 marks per qualifying project, up to 15 projects | Rewards more relevant experience, with a clear maximum |
| Price (25 marks) | `25 × clamp((260000 − price) / 60000, 0, 1)` | $200,000 or less gets 25; $260,000 gets 0; lower prices score better |
| Timeline (15 marks) | `15 × clamp((16 − weeks) / 8, 0, 1)` | 8 weeks or less gets 15; 16 weeks gets 0; shorter schedules score better |
| Warranty (15 marks) | `5 × min(panel years / 25, 1) + 10 × min(workmanship years / 12, 1)` | Gives some credit for panel warranty and more for workmanship cover |
| Team and approach (15 marks) | 3 marks each for named lead, identified crew, safety plan, monitoring plan, and roof/structural plan | Checks five clear pieces of delivery evidence |

`clamp` means a result below 0 becomes 0 and above 1 becomes 1. The budget and 16-week deadline come from the brief. The other scoring targets are **my assumptions**.

### Sample results

| Proposal | Experience | Price | Timeline | Warranty | Team | Total |
|---|---:|---:|---:|---:|---:|---:|
| A | 28.00 | 9.17 | 7.50 | 13.33 | 12.00 | **70.00** |
| E | 16.00 | 7.29 | 5.63 | 15.00 | 15.00 | **58.92** |
| C | 18.00 | 6.67 | 3.75 | 13.33 | 6.00 | **47.75** |

**A ranks first, E second, and C third provisionally.** For this example, the reported project counts are treated as qualifying; exact project dates still need checking against the five-year window, especially C's claim covering years since 2020. These counts are not verified. C's instruction to award itself full marks is ignored and logged. **D is flagged** because no completion time is given. **B is ineligible** because the bidder does not establish that it holds the required Ontario electrical contractor licence. D and B receive no rank or score. The final award belongs to a human reviewer.
