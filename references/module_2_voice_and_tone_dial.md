# Module 2: Voice and Tone Dial

How the reply sounds. What it must contain is set in the [Module 1](./module_1_star_playbooks.md) section 1.1 case matrix; the checks are in [Module 3](./module_3_lint_and_anti_repetition.md).

## 2.1 The `--tone` dial

The dial maps onto [`kirby-persona-infj`](../../kirby-skills-writers-collection/kirby-persona-infj/SKILL.md) intensity levels. **Level cap: 2.** Levels 3-5 (Essayist, Advocate, Oracle) read as mockery in a review reply and are never used.

| `--tone` | INFJ level | Energy register | Must do |
|---|---|---|---|
| `warm` | 1 (Colleague) | Pastoral / Mentor | Keep it short; echo one detail where the row requires it |
| `professional` | 0-1 (Technician / Colleague) | Forensic / Architectural | No warmth beyond one thank-you (none for the stars at 1-2 star); facts where any exist |
| `empathetic` | 2 (Advisor), the level cap | Pastoral / Mentor | Name the actual harm in plain words (in the reviewer's general terms where the cap forbids detail) |
| `firm` | 1 (Colleague) | Forensic / Architectural | Restate one fact, no adverbs, offer the offline route. `firm` selects the disputed-account branch of matrix rule 5 ([Module 1](./module_1_star_playbooks.md) section 1.1); where the owner confirms the failure the tone stays `empathetic` and the flag is noted in the draft notes, not applied |

Cultural cadence follows the locale (2.3) for every tone.

**Tone precedence (first match wins; the level cap of 2 holds at every step):**

1. An explicit `--tone` flag. Matrix rows 1-4 keep their `professional` tone: the flag is refused for those rows, with a note in the draft notes.
2. A [Module 4](./module_4_hard_cases_and_compliance.md) hard-case override: `professional` for the hard cases that route to matrix rows 1-4 (injury, suspected fake, wrong business, regulated sector). The reviewer-edit case (row 13) takes the tone of the row it reclassifies into. A 1 star suspected fake is `professional`, not `empathetic`.
3. The case-matrix default tone for the review's row ([Module 1](./module_1_star_playbooks.md) section 1.1). This is where `firm` comes from: a 1 star whose account the owner disputes.
4. A `voice_dna.yaml` profile (2.5) never sets the tone; it only shapes wording inside it.

Verified in the persona files: levels 0 Technician to 5 Oracle in [`00_dispatcher.md`](../../kirby-skills-writers-collection/kirby-persona-infj/references/00_dispatcher.md) and [`02_intensity_metrics.md`](../../kirby-skills-writers-collection/kirby-persona-infj/references/02_intensity_metrics.md); the energy registers (Contemplative, Pastoral / Mentor, Forensic / Architectural) and cultural cadences (Litotes / Restrained, Direct Pragmatic) in [`03_rhetorical_vectors.md`](../../kirby-skills-writers-collection/kirby-persona-infj/references/03_rhetorical_vectors.md). The two dials are set separately. The tone-to-level mapping and the cap are this skill's choices, not the persona's. If the persona is missing, use the table as plain style notes and say so in the draft notes.

## 2.2 Overrides on the INFJ persona

The persona was built for essays and memos. These overrides always apply (per the persona files as read; re-check if the persona updates):

1. **No "Not-X, but-PATTERN" thesis.** Level 2 prescribes it; `/no-ai-slop` bans binary contrasts. The ban wins.
2. **Strip the footer tag** (`_INFJ · [Persona Name] · Intensity [Level]_`) at every level, so it never reaches a posted reply.
3. **No teleological opener.** Level 1's one Ni pattern statement reads as throat-clearing in a short reply; drop it.
4. **Never use the Contemplative energy.** Its open questions produce self-answered questions. Set the register from the table.
5. **Pronoun:** the owner voice rule (2.4) overrides the persona's polite "we".
6. The persona's guardrails still apply: Fe beats may witness, never diagnose, and warmth may soften the delivery but never the fact.

## 2.3 Locale register

| Locale | Cadence | Example of the same line |
|---|---|---|
| UK | Litotes / Restrained: understatement, dry, courteous | "That wait wasn't good enough." |
| US | Direct Pragmatic: plain, direct second person | "You waited too long, and that's on us." |

Spelling and vocabulary follow the locale (apologise / apologize, queue / line). If no locale is given, infer it from the business address; if still unclear, ask once.

## 2.4 Owner voice

1. **I or we:** "I" for sole traders and owner-operators, "we" for teams. If unknown, ask once and reuse the answer for the batch.
2. **Sign-off:** a first name (with a role if useful, e.g. "owner") or initials, as Google advises (secondary; not re-checked). No signature block, slogan or contact block.
3. **Vary the sign-off** across a batch (name, name plus role, initials); the [Module 3](./module_3_lint_and_anti_repetition.md) ledger tracks it. Regulated-sector replies use the owner's initials every time and are exempt.
4. Use contractions. No em dashes.

## 2.5 Optional `voice_dna.yaml`

If the owner supplies a `voice_dna.yaml` from [`kirby-voice-dna-extractor`](../../kirby-plr-skills/kirby-voice-dna-extractor/SKILL.md), read these fields under the top-level `voice_dna` key:

| Field | Use here |
|---|---|
| `posture` | Shapes wording within the chosen tone; never picks the tone |
| `cadence.primary_sentence_length`, `cadence.fragment_frequency` | Sentence length and fragment use |
| `lexicon.signature_terms` | At most one per reply, only if it fits naturally |
| `lexicon.taboo_banned_words` | Added to the banned list in 2.6 |
| `lexicon.preferred_transitions` | Only if they pass 2.6 (colon reveals fail) |
| `formatting_quirks.use_em_dashes` | Ignored |

Where the profile conflicts with this skill's bans, the bans win. If the extractor or file is missing, continue without it and say so.

## 2.6 Banned lists

Checked in lint item 7. Case-insensitive; inflections count (e.g. "leveraging").

**Vocabulary:** delve, foster, leverage, utilize, facilitate, empower, streamline, robust, cutting-edge, game changer, tapestry, realm, beacon, multifaceted, meticulous, intricate, paramount, transformative, elevate, embark, supercharge, harness, ever-evolving, testament, crucial, compelling, vibrant, seamless, innovative, pivotal, plethora, myriad, underscore, bolster.

**Empty phrases:** "it's worth noting", "at the end of the day", "when it comes to", "going forward", "in order to", "Moreover" / "Furthermore" / "Additionally" as openers, "It goes without saying".

**Therapist-slop:** "holding space", "lean into", "your truth", "deeply resonated", "your feelings are valid".

**Review-reply clichés:** "We're thrilled", "valued customer", "We strive to", "Your feedback means the world", "We're sorry to hear about your experience", "We take X seriously", "Thank you for taking the time", "We hope to see you again soon", "It was a pleasure serving you", "We apologize for the inconvenience".

**Structure bans:** binary "not X but Y" contrasts, throat-clearing openers, fake-profound kickers, summary-recap endings, rule-of-three padding, trailing pile-on clauses (the accountability line, e.g. ", and that's on us", is exempt), self-answered questions, colon reveals, em dashes.

## 2.7 Portability and horoscope tests

- **Portability:** if a content sentence could move unchanged to another business's reply, cut it or tie it to this review's detail.
- **Horoscope:** could anyone have written this content sentence about anything? If yes, rewrite.
- **Content sentences only.** Not tested: required-element phrases (the thanks line, the accountability line, the privacy line, the record or fact line of a restricted draft), the route sentence with its lead-in, the sign-off and unfilled `[NEED: ...]` placeholders.
- **Exempt rows:** every row marked Fixed in the [Module 1](./module_1_star_playbooks.md) section 1.1 matrix. They must still pass the 2.6 lists and contain no invented detail.

## 2.8 Over-humanising warning

The same "human" device every time is its own template. Do not open every reply with the reviewer's name, a one-word exclamation, a fragment or a casual aside. Rotate the opening move across the batch (detail, fact, name, thanks first) and let the [Module 3](./module_3_lint_and_anti_repetition.md) ledger catch repeats.
