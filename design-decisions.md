# Medicine Revision System — Design Decisions

Companion document to `index.html`. The HTML contains the working system; this document contains the *why*. Read it (or hand it to Claude) when you want to change the system and don't want to repeat old mistakes.

---

## Master module tags (the 13)

Every lecture uses one of these tags. The tag is the actual curriculum module name — no invented abbreviations, no derivation rules to learn.

| Tag | Curriculum module | Lowercase folder (new content) |
|---|---|---|
| PVB | Population, Variation, Behaviour | `pvb/` |
| PHARM | Pharmacology | `pharm/` |
| NEURO | Neuroscience | `neuro/` |
| ENDO | Endocrinology | `endo/` |
| PSYCH | Psychiatry | `psych/` |
| CARDIORESP | Cardiovascular & Respiratory | `cardioresp/` |
| GASTRO | Gastroenterology | `gastro/` |
| DERM | Dermatology | `derm/` |
| MSK | Musculoskeletal | `msk/` |
| URO | Urology / Renal | `uro/` |
| GERI | Geriatrics | `geri/` |
| ANATOMY | Anatomy | `anatomy/` |
| LMAP | LMAP / longitudinal stream | `lmap/` |

**The list is closed.** New lectures must use one of these 13. If a lecture genuinely doesn't fit any of them, that's a curriculum question to resolve before tagging — not a "Claude proposes a 14th tag" situation.

### Lecture position (L-number)

The L-number is whatever you supply at Prompt 1. Use the curriculum's number where one exists (`L14` for Hyperthyroidism's slot, `L5.5` for Calcium Dysregulation's slot). For lectures without a natural number, write `L1` or anything else and stay consistent. If left blank, Claude defaults to `L1` and tells you so you can correct.

The system doesn't read meaning from L-numbers. The constraint is consistency within one lecture's lifetime: same L-number every time you rebuild that lecture, so filenames and figure references stay aligned.

### Folder rule

GitHub folder = lowercase tag. Always. ENDO → `endo/`. CARDIORESP → `cardioresp/`. No lookup, no master table consultation. Lowercase the tag character-by-character.

### Legacy folder exceptions (frozen, no migration)

Folders from before this convention exist in the repo with working content and working URLs on already-rendered Notion pages. They stay frozen forever. Embed Prompt 5 has a baked-in mapping from page title → legacy folder for these, so old pages keep working.

| Legacy folder | Maps to (new content goes here) |
|---|---|
| `adrenal/`, `calcium/`, `hyperthyroid/`, `pituitary-vasopressin/`, `appetite-malnutrition/`, `diabetes/` | `endo/` |
| `cardiac/`, `vascular/`, `athero/`, `ecg-abg/`, `respiratory/`, `lung-cancer/`, `haemostasis/` | `cardioresp/` |
| `audio-vestibular/`, `cerebral-inflammation/`, `dementia/`, `headache/`, `visual/` | `neuro/` |
| `gi-cancers/`, `gi-surgery/`, `gut-immunology/`, `upper-gi/` | `gastro/` |
| `upgraded-skin-infections-infestations/` | `derm/` |
| `fractures-children/`, `rheum/` | `msk/` |
| `ckd-dialysis/`, `incontinence/`, `infertility-repro/`, `sodium-water-kidney/` | `uro/` |
| `pharm/` | `pharm/` (already matches the new convention) |
| `psychiatry/` | `psych/` (legacy URLs use the longer name; new content uses `psych/`) |

**Four legacy folders have a literal leading space** (`adrenal`, `athero`, `calcium`, `dementia`) and require `%20` URL encoding. Recommended one-time fix: rename them in GitHub UI to drop the leading space. Embed Prompt 5 handles them either way.

---

## Notion structure

Lecture pages live under a parent called `Neo-BRS`, organised into 8 module-themed parent pages (Endocrinology, Cardiovascular & Respiratory, etc.). For each lecture, Cowork (Prompt 4) creates the page under the relevant module parent — you supply the parent URL in the prompt. Page titles are clean (no `L1 —` prefix, no `(part 1 of 2)` disambiguator). Multi-part lectures merge onto a single page via append-on-duplicate.

Two structural notes:

- **Pharm** is its own container of nested pharmacology lectures sitting at `duper` level rather than under Neo-BRS. Doesn't fit any of the 8 module-themed slots cleanly. Could be moved into Neo-BRS as a 9th slot later if desired.
- **Psychiatry** was originally similar to Pharm but has been moved into Neo-BRS as the 8th module slot, replacing an empty placeholder. The Notion MCP has no delete operation, so the placeholder cleanup needed a manual click.

---

## Load-bearing rules and why they exist

**The 2-job source hierarchy (CONTENT vs EMPHASIS).** Slides give you the teaching points; transcripts give you the examiner's voice. Different jobs, separate rankings. Slide wins on fact unless the lecturer explicitly overrides; transcript wins on emphasis/weight always.

**Notion notes as fallback, not content source.** Student-made notes are the worst possible tiebreaker. Useful for filling specific gaps and last-pass sanity checks, never as primary content.

**Archetype-first classification (MECHANISM / CASCADE / ATLAS / MIXED).** Different lecture shapes need different teaching templates. Without classification, Claude defaults to slide order, which is almost always wrong.

**"Never teach in slide order by default."** Slide order is presentation order, not learning order. Most-violated rule if Claude isn't reminded; duplicated across Part A and Prompt 2.

**Atomic pages, AND no bundle-overview page.** One Notion page per lecture, full stop. No N+1 file. Cross-references inside each lecture page carry the integration signal at the point where it actually matters; an overview file goes stale on edit. Cross-bundle interleaved SBA blocks dropped at the same time — each lecture's own SBAs suffice given exam SBAs are tagged to individual lectures' TILOs.

**Three-identifier model for lectures.** Module tag (stable, build artefacts), Notion page title (mutable, cross-ref prose), Notion page ID (opaque, stable, used by Notion mention mechanism). Each identifier has a different job; the system uses all three appropriately.

**Module tag as the failsafe layer.** Folder boundaries on GitHub are the primary mechanism. Tag prefix on every filename is secondary. Self-identifying header on every `.md` is tertiary. Three independent layers, no single failure mode produces a wrong-image embed.

**Folder = lowercase tag.** Derived character-by-character; no lookup. Legacy folders coexist for old content but new content always uses the lowercase tag. One folder per module, accumulating every lecture's figures in it; filename prefixes (`ENDO-L7_03_x.jpg` vs `ENDO-L14_03_x.jpg`) keep lectures distinct inside the merged folder.

**Cross-references use clean lecture names + Notion mentions.** Inside `.md`s, cross-refs are written as "See also: *Valvular Disease → Why vegetations form on damaged valves*" — clean lecture name, no `L1 —` label. Cowork (Prompt 4) is asked to convert these to Notion page mentions where possible. Mentions reference page IDs and survive future renames; inline links with hand-typed display text are the fallback.

**Open every section with the single unifying intuition.** The move that separates "structurally correct" from "clicks." Without this rule, output covers the right material but doesn't leave a single mental model you can apply.

**Rank [DE-EMPHASISED] items, don't isolate them.** Calcitonin example. Keep them in the same comparison structure as the major players with a clinical-weight column. Followed by a high-yield callout converting the de-emphasis into an exam pattern.

**Checkpoint-by-default.** Conditional checkpoints make teaching worse — Claude takes the "deliver everything at once" branch. Blunt default + user-triggered override.

**Lecture material fidelity over neatness.** State numbers and qualifiers; don't invent or merge. PDF-specific gotcha: if a page's text is rendered as image and doesn't OCR, stop and ask.

**Figure pipeline parameters (200 DPI / q90 / 1400px / fractional crop coords).** All four numbers calibrated against quality drops at lower values. Don't lower without a reason.

**Filename convention `[TAG]-[L-number]_[FF]_[slug].jpg`.** Module tag + curriculum L-number + zero-padded figure number + slugified description. Example: `ENDO-L14_03_steroid-pathway.jpg`. Self-identifying out of folder context. Legacy filenames (no tag, no zero-padding) stay as-is on already-built lectures.

**Inside-zip output structure.** Build chat produces a parent folder containing the `.md` + companion PDF + a zip. Inside the zip is a single folder named exactly the lowercase tag (`endo/`), containing JPEGs and the per-lecture manifest. Drag-and-drop the inner folder into GitHub; merges cleanly into any existing folder of the same name. Reasoning: Safari iOS renames downloaded folders to `file-1` etc., losing the meaningful folder name; wrapping in a zip preserves the inner folder's name through the iOS download path.

**Keep `📎 Figure` references visible after images embed.** Two routes to every figure: caption marker + image. Plus companion PDF as fallback. Three independent paths.

**The figure-embed step is separate from Cowork render.** Cowork = `.md` → Notion page (Prompt 4). Embed = Notion-MCP chat that runs after, reading the page's self-identifying header and embedding GitHub-Pages URLs (Prompt 5). Two chats, different cost dynamics, different tool affordances. Calibration learned the hard way that consolidating them was expensive.

**Prompt 5 has two modes.** Mode A (parent walk) takes one Notion parent URL and embeds across every subpage autonomously — the default for whole-module work. Mode B (single page) takes one specific URL — for surgical updates. Routing happens via each subpage's self-identifying header, so the user supplies one URL plus the listing and walks away.

**3-file Cowork ceiling.** At ~7+ `.md`s in one Cowork chat, toggle conversion silently fails: raw `<><>` markers in body text, `<details>` tags as visible text, "Q:" headings as plain Heading-3. Hard ceiling of 3 `.md`s per Cowork chat. For more lectures, split chats. Conservative on purpose because the cost of a corrupt render is high (re-do the whole `.md`).

**Toggle-render repair as the surgical fix.** When the `<><>` corruption shows up, the Toggle-render repair diagnostic fixes the page in place via Notion MCP — converts broken blocks to proper toggles, strips Q: leaks, recovers from raw `<details>`. Cheaper than re-rendering. Detected automatically by the extended Audit-page diagnostic.

**Listing as authoritative ground truth.** `med-figures-listing.txt` regenerated automatically on every push to the GitHub repo via GitHub Action. Prompt 5 attaches it; Claude never guesses filenames. Pre-flight reports the resolution table before any update lands.

**Handoff briefing pattern.** Long working chats degrade quietly. Triggered by user typing "handoff" or by Claude proactively at signs of context strain. Produces a one-screen artefact: decisions locked, edits completed, edits pending, resumption instruction, starter prompt. The briefing is a diff, not a snapshot — the static system comes from re-uploaded core files.

---

## Rejected approaches (don't reinvent these)

**Megapage instead of atomic pages for bundles.** Land on T2DM six weeks later, see T2DM. Atomic + cross-references is the right shape.

**Bundle overview pages, even for SEQUENTIAL or SHARED OUTCOMES.** Previously calibrated as "exception, not the rule." Final position: never.

**Cross-bundle interleaved SBA block.** Rejected with the overview itself.

**"L1 —" prefixes in cross-reference text.** Stale on rename. Replaced with clean lecture names + Notion mentions.

**Per-lecture invented module tags (3–7 char abbreviations).** Earlier design had Claude propose tags at audit time (e.g. `ADR`, `DM-T1`). Rejected because: (a) a 14th tag could always be invented, opening a long tail of one-off tags; (b) the curriculum already names its modules — those names are the natural identifier; (c) deriving folder = lowercase tag only works cleanly when tags are short and standalone, which sub-tagged abbreviations like `DM-T1` aren't. Replaced with the closed list of 13 curriculum modules. Sub-modules of a curriculum module (e.g. T1DM vs T2DM both in Endocrinology) are distinguished by L-number, not by tag.

**Embedding images via Markdown syntax in Prompt 3 output during the build chat.** Local paths can't resolve at embed time; placeholder `📎` references are the only thing the build chat produces.

**Cowork-based figure embed (the original Prompt 5).** Required Cowork to upload local JPEGs as Notion image blocks; expensive and fragile. GitHub-Pages-hosted markdown image embeds are cheaper and decoupled.

**Screenshot worklist instead of auto-crop.** Brief misunderstanding about Claude's capabilities. Corrected.

**Sticky bottom bar holding Prompts 2–4 (Option C).** Persistent dark strip at peripheral attention. Option A (duplicate inline across tabs) won.

**Single linear layout without tabs.** Scroll marathon. Tabs + jump-nav + collapsed explainers is the answer.

**Archetype-conditional checkpointing.** Looked smart; produced worse output.

**SBA-distractor rule for [DE-EMPHASISED] items.** Wrong inference; replaced with comparison-table-with-clinical-weight-column.

**Auto-collapsing Cowork render and figure embed into one step.** Calibration #10 explains why they must stay separate.

**Per-page URL list as the only Prompt 5 input mode.** Worked but required hand-listing every URL. Mode A (parent walk) added so one URL drives the whole pass.

---

## Known-good examples (reference points)

**Unifying intuition: calcium homeostasis.** "Extracellular Ca²⁺ stabilises voltage-gated Na⁺ channels. High Ca = hard to depolarise = sluggish. Low Ca = easy to depolarise = hyperexcitable. Hypo- and hyper-calcaemia symptoms are mirror images of one excitability axis."

**Unifying intuition: vitamin D cascade.** "Three organs, two enzymes, one active product."

**Ranked de-emphasis: calcium regulators table.** Calcitriol / PTH / Calcitonin in one table with Clinical weight column (Major/Major/Minor) followed by yellow callout converting the de-emphasis into an exam pattern.

**Atlas card template (from GI cancers).** Per entity: epidemiology/risk → presentation → investigations → staging → treatment ladder → prognosis → one exam trap. Same template every time.

**Interleaved SBA block.** 10–15 questions mixed across all entities at the end of an atlas. Forces discrimination over blocked practice.

---

## User preferences calibrated over iterations

- Intuition-first teaching: not "here's the structure, now fill it in" but "here's the single idea; from this you can derive everything else."
- Dislikes big tables. Max 4×4. Split bigger ones or use decision trees in code blocks.
- Comparison-with-ranking over isolation for minor/de-emphasised content.
- Checkpoints ON by default. Quality > speed.
- Not opinionated about SBA distractor construction.
- Happy with q90 JPEGs ("too clear" is a feature; storage is cheap).
- Wants 📎 references kept after images embed.
- Atomic pages, always. Bundle overview pages: never.
- Uses GitHub Pages (`index.html` deployment) to view on iOS. Workflow: edit → commit → view on phone.
- Tab structure (Option A) with jump-nav and collapsed explainers.
- Cross-reference text uses clean lecture names, not L1/L2/L3 labels.
- Module tag is one of the fixed 13. L-number is supplied at Prompt 1; defaults to `L1`.
- Prompt 5 default mode: parent walk (Mode A). Pastes one URL, walks away.

---

## What's stored where

- **`index.html`** — the working system (Parts A, B, all 5 prompts × 3 workflows; diagnostics: Fix-up, Handoff briefing, Cross-reference sweep, Gap remediation, Audit-page, Toggle-render repair, Batch figure embed; Field Notes; UI)
- **This file** (`design-decisions.md`) — the why, rejected alternatives, calibration history, the 13 module tags, the Notion structure note, the legacy folder map
- **`med-figures-listing.txt`** — auto-generated on every push to the `med-figures` GitHub repo via GitHub Action; authoritative for filename matching at embed time
- **`.github/workflows/regenerate-listing.yml`** — the action that keeps the listing in sync
- **`notion-figure-embed-prompt.md`** — standalone copy of Prompt 5 for paste-into-fresh-chat use; mirrors the inline version in `index.html`

---

## Calibration warnings for future edits

1. **Don't re-optimise checkpoints into conditionals.** Blunt default + explicit opt-out is correct.

2. **Don't add rules without concrete examples.** Principle-only rules don't bind; rules with examples (calcium → Na⁺ channels) do.

3. **When inferring rules from user-preferred output, confirm which specific part they liked.** Don't generalise from a nearby feature.

4. **Shape rules > content rules.** "Open with the unifying intuition" works on any subject. "Teach X before Y" only works for one lecture.

5. **Concrete numbers (200 DPI, q90, 1400px, 4×4 tables, 3 .mds per Cowork chat) beat vague guidance.** Vague guidance drifts; numbers don't.

6. **Test a change on one lecture before committing.** Most expensive miscalibrations would have been caught in one trial run.

7. **Don't let Notion-output conventions leak into in-chat teaching.** `<details>` / `<summary>` HTML tags from Part B's toggle convention bled through once. Fix: explicit guard in Prompt 2.

8. **"Apply the design principles" is a reference, not an instruction.** Every non-negotiable rule must be re-stated inline in Prompt 3 with concrete fail/pass examples.

9. **Callouts must be rendered as native Notion block type, not styled paragraphs.** Render prompts and the figure-embed prompt specify "NATIVE Notion callout block" with explicit icon mapping.

10. **Auto-hierarchy-walking in Cowork has a real usage cost.** A Prompt 4 variant with hierarchy walk + routing tables + pre-flight + build-first-pause cost ~80% of a week's usage on one bundle. Fix: lean Prompt 4 — hardcoded parent URL, "process ONE AT A TIME, do NOT batch", "do NOT hang", "if exists → SKIP". Don't re-add the heavy machinery.

11. **Callouts are block-level, always.** Inline coloured-square emojis are the worst-looking failure mode. Hard rule: icons never inside bullets, tables, or mid-paragraph.

12. **Module tags are sacred once locked.** Don't rename a tag after lectures have been built with it — breaks every existing filename, figure reference, and manifest entry. The fixed 13 are the closed set; sub-modules of a curriculum module use the same tag distinguished by L-number, not new tags.

13. **The figure-embed step lives in a separate chat with a separate connector (Notion MCP, not Cowork).** Calibration #10 explains why Cowork has to stay lean. Don't try to consolidate.

14. **The handoff briefing isn't a recreation of the system — it's a diff.** Dump the deltas only; the next Claude has the core files re-attached.

15. **Cross-reference rewrites use clean lecture names + Notion mentions.** Future edits to Prompt 4 should preserve mention-preferred behaviour over inline-link fallback.

16. **The four `%20`-prefix folders should be renamed in GitHub UI to drop the special case.** Twenty seconds of work; cleaner forever. Embed Prompt 5 handles them either way for now.

17. **3-file Cowork ceiling is a hard rule, not a guideline.** Symptoms of corruption (`<><>`, `<details>`, "Q:" leaks) appear at ~7+ files. The 3-file ceiling is conservative because the cost of being wrong (re-rendering corrupted toggles) is high. If the user pushes back wanting bigger batches, hold the line and offer Toggle-render repair as the recovery tool — don't loosen the ceiling.

18. **Prompt 5 Mode A (parent walk) is the default for whole-module work.** One parent URL + the listing → autonomous embed across every subpage. Don't reintroduce per-page URL listing as the default; that was the older, more manual flow that this autonomy step replaced. Mode B (explicit page URL) stays available for surgical single-page work.

19. **L-number is user-supplied; never let Claude derive it from lecture content.** Always wait for the user to supply the value at Prompt 1. Default to `L1` only when the user explicitly leaves it blank, and tell them so.

20. **Folder = lowercase tag is a derivation rule, not a lookup.** Don't let future edits add a "GitHub folder" master table back in. The lowercase rule is intentional because it removes a class of "is this folder right?" questions from Claude's path.
