# Notion Figure Embed Prompt — Reproducible

Standalone copy of Prompt 5 from `index.html`. Use when you want to embed figures into a Notion page (or every page under a parent) without opening the full reference document. Run in a fresh Notion-MCP chat (or claude.ai with Notion connected) after Cowork has rendered the page(s) via Prompt 4.

Two modes:

- **Mode A — parent walk (recommended).** One parent URL → Claude walks every subpage autonomously. Default for whole-module work.
- **Mode B — single page.** One specific page URL → Claude embeds figures on that page only. For surgical updates.

---

## The prompt

```
Embed every figure on the supplied Notion page(s) using GitHub-Pages-hosted JPEGs. Two modes — one of:

INPUTS (Mode A — parent walk, RECOMMENDED for whole modules)
- Parent Notion URL: [PASTE]  (Claude walks every subpage under this parent autonomously)
- Attached: med-figures-listing.txt (authoritative listing of every folder + filename in https://kenp4ki.github.io/med-figures/)

INPUTS (Mode B — explicit page URL, for single targeted page)
- Notion page URL: [PASTE]
- Attached: med-figures-listing.txt

Use Mode A when you want every page under a parent embedded in one shot — this is the autonomous workflow. Use Mode B when you want to embed exactly one page (e.g. you've just rendered a single new lecture and don't want to touch siblings).

CORE TASK
For every "📎 Figure [TAG]-[L-number].[M] — caption" reference on every target page, append an image embed line directly below it:
    ![caption](https://kenp4ki.github.io/med-figures/[folder]/[filename].jpg)

Do NOT remove the 📎 line — it stays as a visible caption marker above the image. Match filenames against the attached listing. NEVER guess filenames; if a reference doesn't resolve, log it and skip.

PARENT WALK PROCEDURE (Mode A)
1. Fetch the parent page; list every subpage with title and ID.
2. Filter out subpages with no 📎 references (e.g. index pages, scratch notes). Report what's filtered before proceeding.
3. Process the remaining subpages sequentially. Don't parallelise.
4. For each subpage, do the per-page pre-flight + update procedure below. After each: print "✅ [Page name] — N embedded, M skipped" and move on.
5. At the end, summary across all pages.

PER-PAGE PRE-FLIGHT (both modes)
1. Fetch the page with notion-fetch.
2. Read the self-identifying header: "**Module tag:** [TAG] · **Lecture position:** [L-number] · **GitHub folder:** [folder]". This tells you exactly which folder to match against. If the header is missing (legacy page), infer the folder from the page title via the mapping below, and confirm with me before updating.
3. Walk every 📎 reference. For each, look up the matching filename in the listing under [folder]. Build a (reference, URL or "MISSING") table.
4. Report the resolution table BEFORE updating. If anything is MISSING, ask whether to proceed (skipping missing) or wait for me to push more JPEGs first.
5. Only after I confirm (or if everything resolves cleanly) do you update.

FOLDER DERIVATION (current convention)
The folder is the LOWERCASE module tag. ENDO → `endo/`, CARDIORESP → `cardioresp/`, etc. No lookup needed; lowercase the tag from the self-identifying header. The 13 valid tags are: PVB, PHARM, NEURO, ENDO, PSYCH, CARDIORESP, GASTRO, DERM, MSK, URO, GERI, ANATOMY, LMAP — tags outside this set are legacy.

MATCHING RULE — TAGGED REFERENCES (current convention)
- Reference: "📎 Figure ENDO-L14.3 — Steroid pathway"
- Filename pattern: [TAG]-[L-number]_[FF]_[slug].jpg with FF zero-padded (ENDO-L14_03_steroid-pathway.jpg)
- Lecture position with dot (L5.5): keep the dot in the filename verbatim (ENDO-L5.5_03_chvostek-sign.jpg)

MATCHING RULE — LEGACY UNTAGGED REFERENCES
Older pages use "📎 Figure L[N].[M] — caption" (no tag prefix). For these:
- Filename pattern: L[N]_[M]_[slug].jpg (no zero-padding, no tag)
- Folder is inferred from page title via the mapping below
- Special filename patterns also exist for /pharm/ and /psychiatry/ — "Figure_LX.Y_Capitalised_Words.jpg" with literal "Figure_" prefix and a dot (not underscore) between L# and figure#

Do not modernise legacy references; embed them with their existing pattern.

URL CONSTRUCTION
Standard:
    https://kenp4ki.github.io/med-figures/[folder]/[filename].jpg

Folders with a literal leading space currently require %20 encoding (legacy quirk being phased out): adrenal, athero, calcium, dementia. If a folder isn't marked clean or %20 in the listing, test one URL with web_fetch before bulk-embedding. If it 404s, use %20.

UPDATE BEHAVIOUR
- One notion-update-page call per page with a content_updates array.
- Each entry: {old_str = exact figure-reference line as it appears on the page, new_str = same line + "\n\n" + matching tab indent + "![alt](URL)"}.
- For a reference inside a single toggle: prefix new_str's image line with "\t". Inside nested toggles: "\t\t". Mirror the indent of the 📎 line itself.
- For ECG / ABG pages where captions are wrapped in **bold**: preserve the bold markdown verbatim in old_str.
- Multi-figure lines ("📎 Figures L1.4 & L1.5 — ...") get stacked image embeds, one per figure, separated by blank lines.

IDEMPOTENCE
If a reference already has an image embed directly below it, skip it. Don't double-embed on re-runs.

PAGE-TO-FOLDER MAPPING (legacy pages without a self-identifying header)
- Hypoadrenal / Hyperadrenal → adrenal (%20)  [new content goes in endo/]
- Atherosclerosis → athero (%20)  [new content goes in cardioresp/]
- Calcium L5.5 → calcium (%20)  [new content goes in endo/]
- Dementia → dementia (%20)  [new content goes in neuro/]
- Appetite / Malnutrition → appetite-malnutrition  [new → endo/]
- Auditory / Vestibular / BPPV → audio-vestibular  [new → neuro/]
- Structural Heart Disease (GOL / SHD / Cardiomyopathies) → cardiac  [new → cardioresp/]
- Cerebral Inflammation → cerebral-inflammation  [new → neuro/]
- CKD and Dialysis → ckd-dialysis  [new → uro/]
- Diabetes T1 / T2 / Complications → diabetes  [new → endo/]
- ECG L1 / ABG L2 → ecg-abg (zero-padded numbers, BOLD captions)  [new → cardioresp/]
- Specific Fractures / Children's Orthopaedics → fractures-children  [new → msk/]
- GI Cancers → gi-cancers  [new → gastro/]
- General/Surgical GI → gi-surgery  [new → gastro/]
- Gut Immunology → gut-immunology  [new → gastro/]
- Haemostasis → haemostasis  [new → cardioresp/]
- Headache (L3.8 three-segment) → headache  [new → neuro/]
- Hyperthyroidism (L14_X) → hyperthyroid  [new → endo/]
- Urinary Incontinence → incontinence  [new → uro/]
- Infertility / Reproductive Treatments → infertility-repro (zero-padded)  [new → uro/]
- Lung Cancer → lung-cancer  [new → cardioresp/]
- Obesity → obesity  [new → endo/]
- Pharmacology → pharm (special "Figure_LX.Y_Cap_Words" pattern)  [new → pharm/]
- Hypopituitarism / Pituitary / Vasopressin → pituitary-vasopressin  [new → endo/]
- Psychiatry → psychiatry  [new → psych/]
- Respiratory L1 → respiratory  [new → cardioresp/]
- RA / Lupus → rheum  [new → msk/]
- Sodium-K / Water-acid-base → sodium-water-kidney  [new → uro/]
- Skin Systemic / Skin Infections & Infestations → upgraded-skin-infections-infestations (PLURAL infections)  [new → derm/]
- Upper GI Disorders → upper-gi  [new → gastro/]
- Vascular Endothelium / Valvular → vascular  [new → cardioresp/]
- Visual System → visual (zero-padded)  [new → neuro/]

If a page isn't in this mapping AND has no self-identifying header, ask before embedding.

CONTEXT-LIMIT SELF-MONITORING
Soft check — every 2 pages completed (in parent-walk mode):
- Are tool results being truncated (`[Older tool result cleared...]`)?
- Have you made >40 tool calls this session?
- Does fetching/updating feel sluggish?
If any are true, finish the current page cleanly, output a handoff (pages completed / skipped / remaining), and tell me to start a new chat with this prompt + listing + the parent URL (parent walk resumes from the unprocessed subpages).

Hard stop:
- Multiple back-to-back `[Older tool result cleared]` messages
- >60 tool calls in the session
- Any tool failure that looks context-related

DELIVERABLE
After updates land, print a one-line confirmation per page (e.g. "✅ Hyperthyroidism — 18 figures embedded, 0 skipped") plus any unresolved-reference notes. No restructuring. No page-property changes. The only change you make is appending image embeds below existing 📎 lines.
```

---

## Notes

**Why Mode A is the default.** With the self-identifying header on every `.md` and the `med-figures-listing.txt` as ground truth, the embed pass needs no per-page input. One parent URL plus the listing is enough. Page titles plus the headers carry all the routing information; Claude walks every subpage and figures out where the JPEGs live without asking.

**Why the pre-flight matters.** Resolution failures (a missing JPEG, a typo in a `📎` reference, a folder that hasn't been pushed yet) get caught up front, before any half-broken page exists in Notion. The pre-flight table is the single most important step — never skip it.

**Why the listing is canonical.** Filename patterns vary across legacy folders (zero-padding inconsistencies, special pharm/psychiatry pattern, calcium triple-L). The listing is auto-regenerated on every push to the repo via the GitHub Action, so it always reflects ground truth. NEVER guess; if it's not in the listing, it doesn't exist on the CDN.

**Why this is a separate chat from Cowork.** Cowork's cost profile is fragile — calibration learned the hard way that hierarchy-walking and pre-flight reports inside Cowork burn through usage. The figure embed has different tool affordances (Notion MCP for content reads/updates rather than Cowork's create-page primitive) and benefits from being decoupled — you can re-embed any time, fix a broken page, or migrate folders without touching the original render.
