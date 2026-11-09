# Module 5: Batch Workflow and Post-Publish

Runs a queue of reviews from intake to a verified live reply. Drafting rules live in modules 1 to 4; this module orders the work, enforces the human gate and checks the result.

## 5.1 Intake

**Primary source:** the OpenSEO MCP tool `get_business_reviews` (OpenSEO `local-seo` skill; external, unverified here), documented as returning reviews with ratings and text.

- The call is queued. A `processing` response returns a `taskId`; call again with it after 30-60 seconds. The re-call is expected not to charge again (unverified; check the credit balance after the first run). Do not start a second fresh request while one is processing.
- Field names (e.g. `rating`, `text`, `ownerReplied`), whether the owner replied, the display name and the review date are unverified. Read the actual response and map it to the dispatcher inputs. If "owner replied" is absent, ask the owner; if the display name is absent, mark `[NEED: reviewer first name]`; if absent, start with the reply itself; record "anonymous" in the ledger ([module 1 section 1.3](./module_1_star_playbooks.md) rule 4).
- The display name is an input only. Outputs, the ledger and the telemetry handoff carry the first name per [module 1 section 1.3](./module_1_star_playbooks.md), or "anonymous" (a record value only; it never appears in a reply, per section 1.3 rule 4).
- OpenSEO research uses credits. State the expected cost before pulling reviews for many locations.

**Fallback:** the owner pastes reviews (rating, text, display name, date, replied yes/no), including the current text of any review that may have been edited.

Load the last N published replies (default N = 20) into the [module 3](./module_3_lint_and_anti_repetition.md) ledger. If the owner can't supply them, say the check ran on this batch only.

## 5.2 Prioritisation

1. Hard-case flags from [module 4](./module_4_hard_cases_and_compliance.md): escalate to the owner first.
2. Unanswered 1-2 star reviews, newest first.
3. Unanswered 3 star reviews, newest first.
4. Unanswered 4-5 star reviews with text, newest first.
5. Unanswered star-only or photo-only reviews.
6. Reviews changed since the owner replied (case matrix row 13).
7. Already replied, owner wants to change it.

Entries with no star rating are handed back to the owner, not queued ([module 1 section 1.1](./module_1_star_playbooks.md)).

For 6 and 7, draft a replacement through the normal flow. Tell the owner that Google lets them edit or delete a reply from the profile and that the reviewer then sees the new text (secondary report; unverified here).

Negatives go first because a 1 star pulls the average down most when the review count is low, and an unanswered one sits in front of every prospect. For the ratio, see the rating-offset maths in [`kirby-local-seo` Module 3 section 3.14](../../kirby-local-seo/references/module_3_local_ai_search_review_engineering_google_ask_maps.md). This is not a ranking claim.

## 5.3 Workflow

| Step | Action | Rule owner |
|---|---|---|
| 1 | Intake and map fields | 5.1 |
| 2 | Hard-case triage; stop on "Nothing public" | module 4 |
| 3 | Pick the case-matrix row | module 1 section 1.1 |
| 4 | Set tone and owner voice | module 2 |
| 5 | Draft the variants the row sets | modules 1-3 |
| 6 | Lint every variant | module 3 section 3.1 |
| 7 | Anti-repetition check against batch and ledger | module 3 section 3.2 |
| 8 | `/no-ai-slop` detect mode; after any hand fix, re-run lint 1-10 and the opening 3-gram check | module 3 section 3.5 |
| 9 | Owner selects, edits and approves one variant; re-lint the edited text and re-run the opening 3-gram check; create the ledger row | 5.4, module 3 section 3.3 |
| 10 | Owner posts the reply in GBP | owner |
| 11 | Verify live; complete the ledger row; hand off to telemetry | 5.6 |

## 5.4 Human approval gate

1. The skill never posts, schedules or queues a reply in GBP or any API. Not for 5 star reviews, not in bulk, not "just this once".
2. The owner picks one variant per review, or rejects them all.
3. Owner edits are re-linted; severity and overrides follow [module 3](./module_3_lint_and_anti_repetition.md).
4. Every `[NEED: ...]` must be filled or deleted by the owner before posting. The skill never fills them with guesses.

## 5.5 Output template (per review)

```
## Review [n]: [star]★, [first name per module 1 section 1.3, or "anonymous"], [date]
Review text: "[verbatim, or 'none (star-only)']"
Priority: [1-7 from 5.2]   Matrix row: [1-13]   Owner replied already: [yes/no]
Flags: [none | hard case: <case> -> escalation message below]

### Variant A
[reply text]
Why different: [one line]
Lint: [the module 3 section 3.6 report block]

### Variant B to Variant N
... (as many as the row's Variants column sets)

[NEED:] list: [every placeholder, including the sign-off and the gate note, or "none"]
Escalation message: [module 4 text, or "none"]
After posting: check the reply shows on the public profile while signed out.
```

For "Nothing public" cases, output only the header, the flag and the escalation message.

## 5.6 Post-publish verification

1. Google moderates owner replies before display: usually about 10 minutes, up to 30 days (Google help page as reported; secondary source).
2. The owner checks the reply on the public profile while signed out (or in a private window). The dashboard can show a reply the public cannot see.
3. Rejected replies may not trigger a notification (one secondary source; unverified). Silence is not proof the reply went live.
4. Complete the ledger row recorded at approval ([module 3 section 3.3](./module_3_lint_and_anti_repetition.md)): set `live` to the date verified, or `not shown`. If the posted text differs from the approved text, re-lint it and update the row.
5. Hand off to [`kirby-seo-telemetry`](../../kirby-seo-telemetry/SKILL.md) [Module 14 section 14.2](../../kirby-seo-telemetry/references/module_14_gbp_enforcement_status_and_reply_quarantine_telemetry.md), whose probe flags a quarantined reply where an authenticated reply has no public counterpart (field names unverified here).
6. When telemetry flags a quarantined reply, re-draft it through this skill. `kirby-seo-telemetry` section 14.2 now routes quarantined replies to this skill (`501b622`, root pointer `3955b8b`); the `kirby-local-seo` Module 10 script is an example of the required elements, not text to copy ([module 4 section 4.5](./module_4_hard_cases_and_compliance.md)).

## 5.7 Reply-timing targets (default, tunable)

| Review | Draft ready for owner | Posted |
|---|---|---|
| 1-2 star | within 24 hours | after owner review, same or next day |
| 3 star | within 24 hours | within 48 hours |
| 4-5 star, star-only | within 24-72 hours | within 72 hours |

These are design-team proposals. The consumer-expectation figures behind them are in the [module 1](./module_1_star_playbooks.md) evidence note. A negative review gets a draft within 24 hours so the owner has time to check facts.

## 5.8 Measurement

Track per location, monthly:

| Metric | Definition |
|---|---|
| Response rate | Reviews with a live owner reply / all reviews in the period |
| Time to reply | Median hours from review date to reply going live, by star band |
| Unanswered negatives | 1-3 star reviews with no live reply |
| Rejected or quarantined replies | Count from 5.6 and telemetry |
| Rating trend | Average rating and count over time, for context only |
| Ledger variety | Distinct openers and sign-offs across the last N replies |

Do not report ranking changes as an outcome of replies (see the [module 1](./module_1_star_playbooks.md) evidence note). Rating trend reflects the reviews, not the replies.
