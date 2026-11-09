# kirby-gbp-review-replies

Drafts owner replies to Google Business Profile reviews that read as written by the owner, protect customer privacy, and earn the trust of the next prospects who read the page.

Locked decisions: the skill drafts and never posts; every review gets a reply decision, from 5 star down to star-only and photo-only, with a draft for all except the hard cases where nothing public is drafted (legal threat, ex-employee, harassment or hate, a non-English review, and wrong business until the owner confirms it), where the owner is told why and decides; replies use the reviewer's first name only, never a surname, and no name when the handle reads as a surname; replies never accuse a reviewer of faking; phone numbers stay out unless the owner opts in; English-language reviews only; a non-English review is passed back undrafted. Version 1 covers Google Business Profile only (other platforms are parked in `FUTURE_PLATFORMS.md`).

### 🪄 The Magic Prompt
Copy and paste this into any AI coding app (Cursor, Windsurf, Claude Code, Grok, Kimi, Reasonix). The URL below is the intended repository location; the repository may not exist yet.

```markdown
@agent Install the GBP Review Replies skill from: https://github.com/markkirby125/kirby-gbp-review-replies
1. Confirm the repo resolves and the files match the Files listing in its README before installing.
2. Read `SKILL.md` and `references/` from the repository.
3. Place into your environment's skills/rules directory preserving the dispatcher structure.
4. Confirm when installation is complete.
```

## Files

| File | Purpose |
|---|---|
| `SKILL.md` | Hollow shell pointer |
| `references/00_dispatcher.md` | Entry point: decisions, inputs/outputs, routing, workflow |
| `references/module_1_star_playbooks.md` | Case matrix (single source for every case's elements, length, route, accountability, tone and variants), naming, content restraints, worked examples |
| `references/module_2_voice_and_tone_dial.md` | Owner voice, `--tone` dial, locale register |
| `references/module_3_lint_and_anti_repetition.md` | Pre-publish lint, batch anti-repetition, approval ledger |
| `references/module_4_hard_cases_and_compliance.md` | Hard-case triage (fake, regulated, legal, injury, harassment, reviewer edits, non-English) and compliance |
| `references/module_5_batch_workflow_and_post_publish.md` | Batch runs and live-check after posting |
| `FUTURE_PLATFORMS.md` | Parked notes for Yelp, Facebook, Trustpilot |
