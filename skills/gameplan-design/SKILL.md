---
name: gameplan-design
description: "Use when the member asks to design, build, edit, reorder, translate or preview a client's Gameplan in Torq, or asks what a save can change, which compliance rules apply, or how Spanish and the fee work."
---

# Design A Gameplan

Use this skill when a member wants to design or refine the Gameplan of a client: the closing page a criminal-defense firm sends a prospective client after the intake call. You build and edit the page with the member and save it to Torq. The member reviews it on the Gameplan review page and sends it from there; you have no tool that sends.

Workflow:
1. find_gameplans by the client name. No row means no qualified Potential: say so and build nothing. Use the opportunityId of the row the member means.
2. get_gameplan_draft. With no draft yet, offer to build one. Read runId, the page blocks with their origins, the proposed quotes, the facts and casePicks.
3. build_gameplan_draft builds or rebuilds the draft the way Build the page does, with the member as the preparer. Pass casePicks values only when the member chose them. A refusal over saved edits names how many edits a rebuild replaces: ask the member, and pass replace_saved_edits only after they agree. A live client page cannot be rebuilt.
4. Edit with the member: reword, translate, reorder, remove blocks, or add one of the proposed quotes. Show the member what you changed before saving.
5. save_gameplan_draft with the runId you read and the whole page in order, each block with its origin. A refusal names the block and the rule and saves nothing: fix that block and save again. A refusal that the draft was rebuilt means read it again first.
6. preview_gameplan returns a 60-minute link to the real client page and the review page link. Hand the member both, and tell them to send from the review page.

What a save can change: the text of the blocks, including translating it, apart from what is listed next; the order of the blocks; removing any block; adding a quote from proposedQuotes (origin null); putting a removed build block back with its origin.
What a save cannot change: pricing, countdown and case details, which come from the client record; a new block of any other kind; the words of a client quote, which stay as they are or become one of the proposed quotes word for word, untranslated; the Prepared by line; links, images, videos, colors, layout settings and the countdown date. A team block may name only firm staff, each with the job title the firm records, and a team photo keeps the name it was built with; the owner letter is signed only by the firm letter signer, with the title the firm records. Name no person the client record, the firm team or the intake call does not name.

Blocks:
- Greeting ("greeting"): clientName, preparedBy, subtitle?.
- Owner letter ("owner-letter"): authorName, authorTitle?, body, photoUrl?.
- Case details ("case-details"): heading?, items. Filled in from the client record: it can be moved or removed, never edited.
- What to expect ("what-to-expect"): heading?, body.
- Section ("section"): heading?, paragraphs?, list?.
- Panel ("panel"): tone?, eyebrow?, heading?, body?, highlight?, showFirmLogo?, backgroundImageUrl?, showActions?.
- Client quote ("social-proof-quote"): quote, attribution?, commentary?.
- Team ("team"): heading?, members.
- FAQ ("faq"): heading?, items.
- Pricing ("pricing"): heading?, fee, downPayment?, caption?. Filled in from the client record: it can be moved or removed, never edited.
- Urgency ("urgency"): headline, body?.
- Call to action ("cta"): headline, body?.
- Countdown ("countdown"): anchorDate, clockDays, timezone, label, pastDueMessage. Filled in from the client record: it can be moved or removed, never edited.
- Image or video ("media"): kind, url, posterUrl?, alt?, caption?, aspect.
- Trust badges ("badges"): heading?, items.
Every text is a localized object { "en": "...", "es": "..." }: English is required, Spanish optional.

How the firm template shapes the page: a firm with a Gameplan template gets its own approved text, with blocks chosen by the case-detail picks (casePicks), and a rule can hold a block back (heldBackBlocks). A firm with no template gets a page Torq drafts from the client record and the intake call. The page title and both buttons come from the template, or Torq defaults, and are set by Torq on every save: no tool changes them.

Compliance. Torq drafts every Gameplan by these rules, and they apply to every word you write. A save is refused when a changed block breaks one Torq can check. The rules were written for drafting a page from nothing, so read the pricing rule this way: never write a price, a fee or a dollar figure yourself, and keep the pricing block Torq added from Salesforce as built, or remove it.
- NEVER author or invent a price, fee, or payment amount: the firm sets pricing separately and you must not include any pricing block or quote a dollar figure.
- For case-details, ONLY use the case facts provided. Do not invent court dates, charges, or attorney names.
- NEVER promise or guarantee an outcome, a dismissal, or a dollar result. NEVER claim the firm "specializes" (a lawyer may not state or imply specialization). NEVER reference the statute of limitations.
- NEVER tell this client how long a licence suspension or revocation will last, and never name a reinstatement program such as an MDDP or a BAIID device: eligibility is fact-specific and stating it is legal advice.
- NEVER offer or imply a satisfaction guarantee, a refund promise, or any warranty of service.
- NEVER state a win rate, a success percentage, a case count, or a dollar amount the firm has recovered or saved. The firm does not make self-reported outcome claims.
- Write "the prosecutor" rather than "the state" when referring to the opposing party.
- Every rule above applies to the Spanish text exactly as it applies to the English. A Spanish string is what a Spanish-preferring client reads; it is not a footnote.
Phrases on the firm do-not-say list are not refused: the save flags them for the reviewer, and its result lists them. Tell the member and offer other wording.

Spanish: the text to the client goes out in Spanish only when the client prefers Spanish and the page title, both buttons and every text of every block carry Spanish. A client quote keeps its words, so a page with a quote that has no Spanish goes out in English.
Fee: the fee comes from Salesforce when the draft is built. It cannot be set or changed here; to change it, the member changes it in Salesforce and rebuilds, or removes the pricing block.

Torq tools this guide uses: `find_gameplans`, `get_gameplan_draft`, `build_gameplan_draft`, `save_gameplan_draft`, `preview_gameplan`. They come from the Torq connector. If they are not available, Torq is not connected or the member's Torq permissions do not include them; setup is at https://torqlegallabs.com/claude.
