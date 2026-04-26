# Sample handoff briefing — what one actually looks like

This is the briefing the previous chat would have produced if the Handoff diagnostic had existed at the time. Saved as a reference example so future you (and future Claude) know what shape the output takes when the failsafe fires.

The briefing has two halves: a working summary for you to read and verify, then a starter prompt to paste verbatim into a fresh chat.

---

```
---
HANDOFF BRIEFING — overhaul of revision-system: module tags, GitHub Pages embed, no bundle overview, handoff diagnostic
---

DECISIONS LOCKED IN THIS CHAT (apply during continued work):

1. Module-tag system. Every lecture gets a 3–5-char all-caps module tag (ADR, DM, VIS, REPR, CARD; sub-tags allowed for multi-lecture modules e.g. DM-T1 / DM-T2 / DM-COMP) assigned at Prompt 1. The tag flows into figure filenames ([TAG]-L[N]_[FF]_[slug].jpg, FF zero-padded), .md figure references (📎 Figure ADR-L1.3), companion PDF name, manifest filename, and a self-identifying header at the top of every .md ("**Module tag:** ADR · **GitHub folder:** adrenal"). Master tag table seeded in design-decisions.md.

2. Bundle workflow no longer produces an overview .md. Ever. Cross-references between lectures live inside each lecture page via 🧠 callouts at the points where the integration matters; no third file, no cross-bundle interleaved SBA block. Each lecture's own SBA block is sufficient given exam SBAs are tagged to individual lectures' TILOs.

3. Cross-reference text inside .mds uses CLEAN LECTURE NAMES, not "L1/L2/L3" labels. Format: "See also: Vascular Endothelium → Why vegetations form on damaged valves". Reasoning: Notion lecture renames are routine; "L1 —" labels go stale instantly while clean names + Notion mentions survive renames cleanly. Bundle Prompt 4 attempts to convert these into Notion page mentions where possible, falling back to inline links.

4. Prompt 5 (figure embed) is now GitHub-Pages-based, run in a separate Notion-MCP chat after Cowork's Prompt 4 (NOT inside Cowork). Pre-flight verification against med-figures-listing.txt. Reads the .md's self-identifying header to know which folder to match against. Handles both tagged (current) and legacy untagged refs. Full page-to-folder mapping for legacy pages baked in. Idempotent.

5. Prompt 3 ends with a "Next steps" block printed verbatim telling the user to (a) push JPEGs+manifest to GitHub, (b) run Cowork render, (c) run figure embed in a Notion-MCP chat. Removes the "wait what now" moment after the build chat finishes.

6. Per-lecture manifest file. Prompt 3 produces [TAG]-L[N]-manifest.txt alongside the JPEGs, listing every JPEG filename for that lecture. The embed step pre-flights against this as the canonical "what this lecture has", catching missing-from-GitHub failures before any embed lands.

7. New diagnostic prompt: "Handoff briefing." Triggered by user typing "handoff" or by Claude proactively at signs of context strain (tool result clearing, >40 substantive tool calls, accumulated undocumented decisions, mid-task forgetting). Produces (a) decisions locked, (b) edits completed, (c) edits pending, (d) resumption instruction, (e) starter prompt for the new chat. Mirrors the existing context-monitoring pattern from the figure-embed prompt.

8. New diagnostic prompt: "Cross-reference sweep." Walks every page under a Notion parent, finds stale "L1 —"/"L2 —" text refs, rewrites using each linked target page's CURRENT title (or flags for manual review if no link is present). Pre-flight reports the substitution table before any update lands. Idempotent. Run after major Notion rename passes.

9. Three-identifier model for lectures, made explicit: module tag (stable, used in build artefacts), Notion page title (mutable, used in cross-ref prose), Notion page ID (opaque, stable, used by Notion mention mechanism). The system uses all three appropriately.

10. Master tag table seed (in design-decisions.md):
    adrenal→ADR, appetite-malnutrition→APP, athero→ATH, audio-vestibular→AUD, calcium→CA, cardiac→CARD, cerebral-inflammation→CINF, ckd-dialysis→CKD, dementia→DEM, diabetes→DM (with DM-T1/DM-T2/DM-COMP sub-tags), ecg-abg→ECG, fractures-children→FRAC, gi-cancers→GICA, gi-surgery→GIS, gut-immunology→GUTI, haemostasis→HAEM, headache→HEAD, hyperthyroid→HYPT, incontinence→INC, infertility-repro→REPR, lung-cancer→LUNG, obesity→OB, pharm→PHARM, pituitary-vasopressin→PIT, psychiatry→PSY, respiratory→RESP, rheum→RHM, sodium-water-kidney→NAH2O, upgraded-skin-infections-infestations→SKIN, upper-gi→UGI, vascular→VAS, visual→VIS.

11. Notion structure documented: lectures live under Neo-BRS, organised into 8 module-themed parents. Pharm sits at duper level (could move to 9th module slot later). Psychiatry already moved into Neo-BRS as 8th slot, replacing an empty placeholder. Notion MCP has no delete operation; placeholder deletes always need a manual click.

12. Recommended hardening (user agreed to all):
    (a) GitHub Action that auto-regenerates med-figures-listing.txt on every push to the repo so it stays in sync hands-free.
    (b) One-time rename of the four leading-space folders (adrenal, athero, calcium, dementia) in GitHub UI to drop the %20 special case.
    (c) Per-lecture manifest file alongside the JPEGs in each module folder (already baked into Prompt 3).

EDITS COMPLETED (state HOW COMPLETE):

- /mnt/user-data/outputs/index.html: COMPLETE.
  • Workflow lead-in updated for new pipeline (module tags, GitHub Pages embed, three chats per lecture)
  • Part B figure-reference rule updated to [TAG]-L[N].[M] with legacy fallback note
  • Single-lecture Prompts 1, 3, 5: fully rewritten (tag step, self-identifying header, manifest, tagged filenames, GitHub-Pages embed with pre-flight, page-to-folder mapping, context monitoring, next-steps block)
  • Retrofit Prompts 1, 3, 5: same rewrites as single
  • Bundle tab intro and shapes reference: rewritten to drop overview-page production entirely; teaching-order guidance only
  • Bundle Prompt 1: per-lecture module-tag step, caption format updated, cross-ref proposals use clean lecture names
  • Bundle Prompt 3: stripped overview .md production wholesale, stripped cross-bundle SBA block, retagged every filename and figure ref, added per-lecture manifests, per-lecture companion PDFs (not bundle-wide), updated deliverables tree, added next-steps block
  • Bundle Prompt 4: removed "if an overview .md exists, create that as a 4th page", updated cross-ref handling to prefer Notion mentions
  • Bundle Prompt 5: replaced with GitHub-Pages multi-page variant
  • Diagnostic section: added Handoff briefing prompt, added Cross-reference sweep prompt, replaced Batch figure embed with GitHub-Pages variant
  • Field notes: updated "How figures actually flow" for GitHub-Pages pipeline, replaced Prompt 5 field note for new pipeline, added Module-tags field note, added Handoff-briefing field note, replaced "Overview pages are exception" with "No bundle overview pages — ever", added Cross-reference field note, added Notion-structure field note

- /mnt/user-data/outputs/design-decisions.md: COMPLETE.
  • Master module-tag table at top
  • Notion structure section
  • Load-bearing rules updated: bundle-overview removal, three-identifier model, module-tag failsafe, clean-name cross-refs, Cowork/embed separation, listing-as-ground-truth, handoff pattern
  • Rejected approaches updated: bundle overviews even for SEQUENTIAL/SHARED, cross-bundle SBA, "L1 —" prefixes, Markdown image syntax, Cowork-based figure embed, Cowork+embed consolidation
  • Calibration warnings extended: tags-are-sacred, embed-is-separate-chat, handoff-is-diff-not-snapshot, mention-preferred-cross-refs, %20-folder-cleanup recommendation

- /mnt/user-data/outputs/regenerate-listing.yml: COMPLETE.
  • Triggers on push to main (skipping listing-only edits to avoid loop) and manual dispatch
  • Walks every top-level directory; detects leading-space folders; emits the same listing format the existing prompt expects
  • Commits back via github-actions[bot] only when the listing actually changed
  • Drop into .github/workflows/ in the med-figures repo

- /mnt/user-data/outputs/notion-figure-embed-prompt.md: COMPLETE.
  • Standalone copy of Prompt 5 from index.html for paste-into-fresh-chat use
  • Single-page and batch variants documented
  • Page-to-folder mapping for legacy pages included

EDITS STILL PENDING:

None for the system itself. Three things sit outside the system that the user does at their own pace:
1. Push the GitHub Action YAML into the med-figures repo (one-time setup; from then on the listing maintains itself).
2. Rename the four leading-space folders in GitHub UI (adrenal, athero, calcium, dementia) to drop the %20 special case. Once done, the leading-space handling in Prompt 5 becomes a no-op for those folders.
3. After any future Notion rename pass, run the Cross-reference sweep diagnostic to clean up stale "L1 —" / "L2 —" text on existing pages.

OPEN QUESTIONS:

None. All design discussion concluded.

RESUMPTION INSTRUCTION:

The system is complete and ready to use. The next action isn't another build chat — it's the user dropping the new files in place (replace existing index.html and design-decisions.md, add the GitHub Action to the repo, swap the standalone embed prompt) and then trying it on a real lecture to verify the new flow works end to end. If something breaks during a real run, that's the next chat's brief: triage the failure, tighten the relevant prompt, and update calibration warnings. No big design moves expected.

FILES TO RE-ATTACH IN THE NEXT CHAT (when one is needed):

- index.html (the working system)
- design-decisions.md (calibration history + master tag table + Notion structure)
- med-figures-listing.txt (only if doing figure-embed work)

Do NOT re-attach the standalone notion-figure-embed-prompt.md — its content lives in index.html now and they're kept in sync manually.

---
STARTER PROMPT (paste this into the fresh chat verbatim):

I'm continuing work from a previous chat that produced a clean restart point. Re-uploading the core files. Read them — they're the system.

Below is what was decided in the previous chat that's already baked into the attached files (so you have context, not so you re-derive anything). The system is complete; this chat is for using or fixing it, not rebuilding.

[paste the DECISIONS LOCKED, EDITS COMPLETED, EDITS STILL PENDING, OPEN QUESTIONS, and RESUMPTION INSTRUCTION sections from above, verbatim, here]

What I want to do now: [user fills in — e.g. "run the new flow on a real lecture and see what breaks", or "the GitHub Action isn't triggering — help me debug", or "I want to add a 9th module to Neo-BRS for Pharm — walk me through the changes"]
---
```

---

## How to read this example

**The decisions section is the load-bearing one.** Everything else is supporting context. If a decision was reached in the previous chat but isn't in this section, the next chat will re-derive it from scratch — wasting time and possibly arriving at a different answer.

**Edits-completed is honest about state.** Every artefact has its status. "COMPLETE" means saved to outputs and verified. If something were partial, this section would say so explicitly ("PARTIAL — single-lecture and retrofit prompts done, bundle prompts not yet started") so the next Claude knows what to expect when it views the files.

**The starter prompt is short.** It points at the static system (the re-attached files), summarises the deltas (the locked decisions), and hands the next chat a clear next step. It does NOT recreate the system — that's what the re-attached files are for.

**Length test.** Read on a phone screen, the briefing should fit roughly two scrolls. If yours runs longer, you've probably duplicated content that's already in the core files. The briefing is a diff, not a snapshot.
