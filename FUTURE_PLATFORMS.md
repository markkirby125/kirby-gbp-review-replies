# Future Platforms (parked for v2)

v1 drafts replies for Google Business Profile only. This file records what a v2 would need for other review platforms. Nothing here is in scope until the owner of this skill reopens it. Every platform claim below is unverified unless stated otherwise.

## Yelp

- **How it differs from GBP:** Yelp is reported to ban asking for reviews at all and to filter reviews it judges solicited, hiding them and excluding them from the rating. Reviews from new or low-activity accounts are reported to land in "Not Currently Recommended". Owners can reply publicly or by private message (unverified).
- **What the repo already knows:**
  - [`kirby-local-seo` Module 6 section 6.12](../kirby-local-seo/references/module_6_gbp_loop_practitioner_profiles_profile_guard.md) (Yelp solicitation filter safeguards; speaker-reported).
  - [`kirby-off-page-seo` Module 27 section 27.2](../kirby-off-page-seo/references/module_27_chatgpt_local_discovery_and_yelp_licensing_mandate.md) (compliant Yelp optimisation; section 27.1 covers ChatGPT's use of Yelp data).
- **Open questions:** Yelp's current rules on owner public comments (length, content, what gets removed); whether public replies or private messages are better for negatives; whether Yelp notifies the reviewer; whether ChatGPT surfaces owner replies alongside Yelp reviews.
- **Minimum change to add it:** a `platform` input; a Yelp row set in the lint (Yelp's own removal categories); a rule that replies never mention or invite more reviews; a private-message variant for negatives.

## Facebook (Recommendations)

- **How it differs from GBP:** Facebook uses yes/no recommendations rather than star ratings, and replies are threaded comments that other users can join (unverified for current Pages experience). A reply can draw a public back-and-forth, unlike GBP's single owner reply.
- **What the repo already knows:** only that review-summary sites group Facebook reviews ([`kirby-local-seo` Module 3 section 3.17](../kirby-local-seo/references/module_3_local_ai_search_review_engineering_google_ask_maps.md)). No reply guidance.
- **Open questions:** whether star ratings still appear anywhere; comment moderation tools available to Pages; whether the business can hide or report recommendations; how threaded replies change the "write for the next 100 prospects" rule.
- **Minimum change to add it:** replace star-band playbooks with recommend / not-recommend bands; add a "do not continue the thread in public" rule; adjust length bands for comment format.

## Trustpilot

- **How it differs from GBP:** Trustpilot permits businesses to invite reviews (unlike Yelp), with its own guidelines on invitations and on replies. Reviews can be flagged by the business and go through Trustpilot's own content process. Mostly used by e-commerce and B2B (unverified).
- **What the repo already knows:** [`kirby-off-page-seo` Module 27](../kirby-off-page-seo/references/module_27_chatgpt_local_discovery_and_yelp_licensing_mandate.md) names Trustpilot as a primary review platform for LLM consensus and pairs it with Yelp for B2B; [`kirby-decision-engine-optimization` Module 2 section 2.4](../kirby-decision-engine-optimization/references/module_2_procurement_micro_disclosures.md) mirrors credentials into Trustpilot bios. No reply guidance.
- **Open questions:** Trustpilot's reply guidelines and prohibited content; whether replies can be edited after posting; how flagging interacts with a public reply; whether UK DMCC Act duties change anything for platforms that allow invitations.
- **Minimum change to add it:** a `platform` input; a Trustpilot lint row set; an order-number rule (never quote it publicly, even though Trustpilot reviews are often order-linked).

## Apple Business Connect (optional)

- **How it differs from GBP:** Apple Maps ratings come largely from in-app thumbs and third-party providers; whether owners can reply to reviews at all is not established (unverified).
- **What the repo already knows:** [`kirby-local-seo` Module 3 section 3.10](../kirby-local-seo/references/module_3_local_ai_search_review_engineering_google_ask_maps.md) lists Apple Business Connect as a citation to claim. No reply guidance.
- **Open questions:** whether an owner-reply surface exists; which provider supplies review text in each country.
- **Minimum change to add it:** none until a reply surface is confirmed.

## Open Items Carried From v1

| Item | Status |
|---|---|
| Whether a phone number in an owner reply triggers Google's "personal information" report category (the category's example is an address or phone number, but it may only mean the customer's) | Unverified. v1 keeps phone numbers off by default regardless |
| Whether Gemini or Google's built-in AI reply drafting in the GBP dashboard is available to UK profiles, and whether it should be offered as an alternative path | Unverified |
| Whether Google notifies reviewers of owner replies and lets them change their review (secondary report) | Unverified; v1 hedges it in the module 4 reviewer-edit row |
| Whether owners are notified when a reply is rejected | Unverified; v1 tells owners to check the reply is live |
| Multilingual replies (non-English reviews): parked for a later version; would need per-language banned lists, register rules and native-speaker review | Unverified |
| Contradictions with `kirby-local-seo` modules 3, 8 and 10 | Fixed in `kirby-local-seo` (`755bab9`, root pointer `d083f68`); each conflict and decision is recorded in [references/module_4_hard_cases_and_compliance.md](references/module_4_hard_cases_and_compliance.md) section 4.5 |
