# AI-Assisted Proposal Review — MATACS Assessment

**Full name:** Kamran Hassan  
**Assessment reference:** MATACS-TH-2026-02  
**Role:** Associate Software Developer  
**Time actually spent:** approx 55 mins


## How the proposed tool works

1. **An admin sets the rules.** For each project category, the admin chooses the required qualifications, scoring areas, weights, and scoring methods. These settings can be changed through admin screens, without changing program code.
2. **A reviewer uploads proposals** and selects the project category.
3. **AI reads the documents** and extracts facts such as prices, timelines, experience, licences, and warranties. It also records where each fact came from.
4. **The system checks the facts and requirements.** Missing or unclear information goes to a person for review. A proposal that fails a mandatory requirement is not scored.
5. **The system scores eligible proposals** using the saved rules, then shows the ranking and reasons behind it.
6. **A person makes the final decision.** The tool helps with the review; it never awards a contract by itself.

## Files in this repository

- [Process flow diagram](diagram/flow.png) — a visual guide from upload to ranking, showing AI, automatic checks, and human review.
- [Answers to the five questions](WRITEUP.md) — how the design works, why it is reliable, how people stay in control, and how risks are handled.
- [AI extraction prompts](PROMPTS.md) — the exact instructions the tool would send to AI to read a proposal.
- [Expected results](ranking.json) — the sample A–E ranking, scores, and short reasons.

.

## How I used AI tools

I used ChatGPT to help organize the process diagram, draft the written explanation and extraction prompt, and check the sample calculations. I questioned an earlier approach that fixed scoring values inside the code, because the assessment says an admin must be able to change the criteria. I revised the design so the admin saves the weights, formulas, and their settings, while the program simply applies them.


## Important note about sample scores

MATACS supplied the criteria and their weights, but did **not** supply exact scoring formulas. The formulas in [WRITEUP.md](WRITEUP.md) are **example choices for this design**, not rules given by MATACS. The sample scores use stated assumptions about project dates, which a reviewer would need to check before a final award.
