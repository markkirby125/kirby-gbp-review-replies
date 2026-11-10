# Module 3: Lint and Anti-Repetition

Every variant runs the ten lint checks, the batch anti-repetition check and the `/no-ai-slop` gate before the owner sees it. A FAIL is never hidden. The skill never posts; a fully passing variant is still only a draft. Case-specific rules (elements, length, route, accountability, variants) come from the [Module 1](./module_1_star_playbooks.md) section 1.1 case matrix; this module tests against it and owns the severity rule.

**Severity.** Items 1-6 and item 10 are **hard blocks**: a variant that fails one is never presented as ready to post, and there is no override. The owner edits it and it is re-linted. Items 7-9 and an anti-repetition FAIL (3.2) show FAIL and stand unless the owner gives an explicit override, recorded in the ledger (3.3). A repeated sign-off against the last N published replies is a WARN, not a FAIL (3.2 rule 2).

Lint item 1 follows Google's "Report owner response" categories as listed by Search Engine Roundtable, 2026 (secondary source; not re-checked at Google): off topic, profanity, bullying or harassment, discrimination or hate speech, personal information, legal issues. `kirby-local-seo` Module 10 section 10.1 lists the first five only. A reply that trips one can be reported and removed.

## 3.1 Pre-publish lint (10 checks)

| # | Check | Failing example | Fix |
|---|---|---|---|
| 1 | No off-topic, profanity, harassment, discrimination, personal information or legal content | "Frankly this is rubbish and you know it." | Remove the attack; restate one fact calmly |
| 2 | PII: no surname, even if the handle shows one; no name when the handle's only token reads as a surname or the order is ambiguous; never the reviewer's name in a regulated sector, where the sign-off is the owner's initials only ([Module 1](./module_1_star_playbooks.md) section 1.3). Nothing from the never-echo list ([Module 1](./module_1_star_playbooks.md) section 1.2). Privacy line present wherever the review discloses health, case, account or other personal detail about the reviewer or a third party, in every row that lists it (rows 1, 4's 1-3 star branch, 7 and 8, including row 8's no-issue fallback; [Module 1](./module_1_star_playbooks.md) section 1.4): the draft carries a privacy line (structure tag `PRIVACY`). It is never moved to the draft notes; if it exceeds the cap, matrix rule 2 shortens it, then lint item 8 shows FAIL and the owner overrides; where rule 2 has no shorten step, item 8 shows FAIL. Relationship wording in the line is checked by item 5 where that item applies; otherwise 1.4's "states a limit and promises nothing" governs | "Hi Sam Patel, sorry about the £140 bill at 12 Mill Lane on 3 March." (name and address fictitious) / row 8 reply to a review about a data leak: "Sorry to hear your data was shared. Please contact us via the details on our profile." | "Hi Sam, sorry the bill wasn't explained." / add the generic privacy line before the route (gate note in the draft notes), e.g. "We can't discuss individual details here." |
| 3 | No phone number unless `phone_opt_in` is true, and then only the one confirmed business number ([Module 1](./module_1_star_playbooks.md) section 1.4); never a URL | "Call us on 01234 567890 or visit oursite.com/complaints." (number fictitious) | "Please contact us via the details on our profile." (sole trader: "Please contact me via the details on my profile.") |
| 4 | No promotion, discount or offer; no remedy the owner did not authorise; no admission of liability (legal liability, fault for injury or damage, compensation). A plain service-failure accountability line is not a liability admission. Test: the accountability line appears only as the row's Accountability column allows, and every used or deferred line carries the gate note (matrix rules 5-6) | "Here's 20% off your next visit, and we'll refund you in full." / "Our fitter caused the damage to your floor and we'll pay for it." | Drop the offer; replace the remedy with `[NEED: remedy, only if owner authorises]`; replace fault or compensation wording per matrix row 1 |
| 5 | Regulated sector (health, legal, finance): nothing that confirms or denies a patient, client or customer relationship, including in a privacy line; no reviewer name (sign-off: owner's initials only); any fact is about services or locations only, never a record of the visit | "We're sorry your filling still hurts after your visit." | Matrix row 4 |
| 6 | No statement that the review is fake, false, paid or from a non-customer, even with the owner's proof or legal advice. A fact about the business's own records ("we have no record of this visit") is allowed outside regulated sectors; a conclusion about the person is not | "This is clearly a fake review from a competitor." | Calm general reply per matrix row 2; removal via [Module 4](./module_4_hard_cases_and_compliance.md) section 4.2 |
| 7 | No banned vocabulary, phrases, clichés or structures ([Module 2](./module_2_voice_and_tone_dial.md) section 2.6); content sentences pass the portability and horoscope tests (section 2.7) unless the row is Fixed | "Thank you for taking the time. We strive to deliver a seamless experience." | Where the row requires an echo, echo one real detail; otherwise delete the portable sentence |
| 8 | Length cap (overridable by the owner): counted words fit the row's Length column per matrix rules 1-4 | 70-word reply to a 12-word 5 star review | Cut to the row's required elements ([Module 1](./module_1_star_playbooks.md) matrix 1.1) |
| 9 | At most one natural service or town mention, only if the reviewer raised it; matrix row 4's one statement about the service or location (either star branch), in general terms and never a record or relationship, is the single permitted mention and is exempt from the "raised it" condition; a term on the owner's services or locations list gives no permission | "Best emergency plumber in Leeds, for emergency plumbing in Leeds call us." | Remove; keep one mention only if the review named it |
| 10 | Reply is in English. A non-English review is never drafted | A drafted reply to a review written in French | Delete the draft; pass the review back per the "Non-English review" row of [Module 4](./module_4_hard_cases_and_compliance.md) section 4.1 |

Before marking a variant ready, also confirm: no unfilled `[NEED: ...]` the owner has not seen, no em dashes, sign-off present.

## 3.2 Batch anti-repetition rules

Compare each variant with every other draft in the batch and the last N published replies (default N = 20, tunable). If the owner cannot supply past replies, say so and check the batch only. Rules 3-5 compare a review's approved reply with other reviews, never one review's variants with each other.

1. No two replies share an opening 3-gram (first three words, lowercased, punctuation stripped).
2. No two consecutive replies in a batch share a sign-off ([Module 2](./module_2_voice_and_tone_dial.md) section 2.4). Across the last N published replies, a repeated sign-off is a WARN. Replies where lint item 2 fixes the sign-off to the owner's initials (regulated sector) are exempt from this rule, and only those.
3. No "Thanks so much for..." opener more than once per batch, and never in two consecutive replies.
4. No more than three replies in a row with the same sentence count.
5. No more than two replies in a row with the same structure tag (3.3). Rows marked Fixed in the case matrix are exempt.
6. A closing move may repeat only where the row requires it, and its wording must change. The fixed route sentence ([Module 1](./module_1_star_playbooks.md) section 1.4) is the one sentence exempt from every check here; any lead-in to it still varies.

## 3.3 Ledger

The agent keeps this table for the batch, seeded with the last N published replies (already live). **One row per reply: the row is created when the owner approves a reply and completed once the reply is confirmed live** ([Module 5](./module_5_batch_workflow_and_post_publish.md) section 5.6). Rejected variants are not recorded.

| review_id | opening 3-gram | sign-off | structure tag | sentences | override | live |
|---|---|---|---|---|---|---|
| R-014 | its good to | [first name] | ECHO>THANKS | 2 | none | pending |
| R-015 | thanks priya glad | [initials] | THANKS>ECHO>HARM>OWN | 2 | none | pending |
| R-016 | forty minutes for | [first name], owner | HARM>OWN>OFFLINE | 3 | none | pending |

R-014 to R-016 are the 5 star, 4 star and 1-2 star examples in [Module 1](./module_1_star_playbooks.md) section 1.5. Sentence counts exclude the sign-off and unfilled `[NEED: ...]` sentences. An owner override is recorded as `item 7`, `item 8`, `item 9` or `anti-repetition`. `live` is `pending` at approval, then the date verified, or `not shown`.

Structure tags name the order of moves, joined with `>`: `THANKS`, `ECHO` (one positive detail the reviewer named), `FIX` (response to the named problem), `HARM` (names the harm; restating the problem is `HARM` or `FIX`, never a second `ECHO`), `ACK` (acknowledgement in the reviewer's general terms), `WARM` (one general warm line), `OWN` (accountability line), `FACT` (one factual statement, including a record line), `PRIVACY`, `OFFLINE` (route).

## 3.4 Variant differentiation

The Variants column of the case matrix sets the count.

- **3 variants:** each has a different structure tag (e.g. `ECHO>THANKS`, `THANKS>ECHO`, `FACT>THANKS`), a different opening 3-gram, and a different sentence count where the band allows. All keep the row's required elements; reordering is allowed, dropping is not. The exceptions follow the matrix: in row 9, the echo, which cap pressure drops first, and the thanks for the good part and the echo, which a review naming no positive detail drops; in rows 10-12 and row 4's 4-5 star branch, cap pressure drops everything except the thanks, per matrix rule 2.
- **2-3 variants:** they differ in opener wording and sign-off; the tag may repeat, the opening 3-gram may not.
- Every variant carries a one-line "why this differs" note, e.g. "Leads with the fix, not the thanks; suits an owner who wants the correction seen first." No variant copies another; if two differ only in synonyms, rewrite one.

## 3.5 Last content gate: `/no-ai-slop` detect mode

After items 1-10 pass, run `/no-ai-slop` in **detect mode** on each variant. Any flagged pattern is a FAIL on item 7: fix that sentence by hand or take an owner override. Do not accept a full rewrite; it can drop required elements or the owner's voice. If `/no-ai-slop` is unavailable, write "slop gate: not run" in the report, apply the [Module 2](./module_2_voice_and_tone_dial.md) sections 2.6 and 2.7 checks by hand, and tell the owner.

After ANY hand fix, re-run items 1-10 and the opening 3-gram check (3.2 rule 1).

## 3.6 Lint report template

One block per variant, shown under the draft:

```text
Review: R-016 | Stars: 1 | Row: 8 | Tone: empathetic | Variant: B
Why this differs: leads with the harm, then accountability; no thanks line.
Words: 40 toward the band (40-120); 31 toward the cap of 49 (route and sign-off uncounted); room for a 9-word fill

 1 Report-owner-response categories   PASS
 2 PII + privacy line                 PASS
 3 Phone / URL                        PASS  (phone_opt_in = false)
 4 Promotion / remedy / liability     PASS  (gate note present)
 5 Regulated sector                   N/A   (sector: cafe)
 6 Fake-review accusation             PASS
 7 Banned lists + portability         PASS
 8 Length cap                         PASS
 9 Service / town mention             PASS  (1 mention, "sandwiches", raised in the review)
10 English only                       PASS
Anti-repetition                       PASS  (opening "forty minutes for" unused in last 20; sign-off differs from the previous reply)
Hard blocks (1-6, 10)                 none
Owner overrides (7-9, anti-rep.)      none
/no-ai-slop detect                    PASS
Open placeholders (3): [NEED: owner first name] (sign-off); [NEED: one true reason, in 9 words or fewer; delete this sentence if none]; gate note (draft notes)
Escalation flag: none
After posting: check the reply is live on the public profile while signed out.
```
