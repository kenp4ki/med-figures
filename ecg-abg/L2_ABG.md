# L2 — Arterial Blood Gases & Acid-Base Regulation

> 📘 **How to use this page.** Every Q is a Notion toggle — flip it open only after trying to answer. Callouts flag 🟥 traps, 🟨 lecturer-emphasised, 🟦 reusable reasoning. Figures live in the companion PDF.

## Lecturer's voice

**Flagged exam-critical**
- 4-step interpretation: *"This is the phase 1B MS one — focus on this."*
- Master grid: *"Your training wheels — use them."*
- ~99% of body acid is **respiratory** (CO₂).
- Paradox: **higher [H⁺] = lower pH**.
- Acidosis vs acidaemia (process vs state).

**De-emphasised**
- Memorising exact reference ranges ("you'll be given them in the exam").
- PaO₂ high (hyperoxaemia) — *"rarely a problem."*
- Full renal mechanism (deferred to Tanvi Agarwal's spring renal lecture).

**Spent disproportionate time on**
- Dog buffering experiment (*"ENORMOUS, IMMEDIATELY"*).
- Four pathology archetypes across uncompensated → partial → full.
- Robot trap: *"pH of 3.5 is not compatible with life — don't just pattern-match."*
- The master grid (revisited twice).

---

## The unifying intuition

### Q: What is the one idea that makes any ABG derivable in 10 seconds?
- pH is set by the **ratio of CO₂ to HCO₃⁻**.
- CO₂ → lungs (fast compensator, minutes).
- HCO₃⁻ → kidneys (slow compensator, days).
- All pathology = equilibrium pushed one way; compensation = other axis pushed to rescue.
- Master equation: **H₂O + CO₂ ⇌ H₂CO₃ ⇌ H⁺ + HCO₃⁻**. Le Chatelier does the rest.

---

## Section 1 — pH, H⁺ and why it's counterintuitive

### Q: Why does pH exist instead of reporting [H⁺] directly?
- Normal [H⁺] ≈ 40 nmol/L = 0.00000004 mol/L — unwieldy tiny number.
- Compare Na⁺ = 140 mmol/L (~3.5 million × bigger).
- Sørensen applied log₁₀ transformation → gives manageable scale.
- pH = **−log₁₀[H⁺]**. Inverse: **[H⁺] = 10⁻ᵖᴴ**.

### Q: What is the paradox of pH you must never get wrong?
- **Higher [H⁺] → LOWER pH.**
- The minus sign in pH = −log₁₀[H⁺] flips direction.
- Classic SBA trap: "H⁺ is high" → patient is **acidaemic**, pH is **low**.

🟥 **Trap.** Inverse relationship is SBA bait. Always convert [H⁺] direction → pH direction in your head before answering.

### Q: What is the difference between acidosis and acidaemia?
- **Acidosis/alkalosis** = the *process* driving pH (e.g. respiratory acidosis).
- **Acidaemia/alkalaemia** = the *state* of the blood (pH < or > normal).
- A fully compensated acidosis has **no acidaemia** — pH back in range despite ongoing process.

### Q: Quickly convert [H⁺] 48 nmol/L to pH.
- pH = −log₁₀(48 × 10⁻⁹).
- = −log₁₀(48) + 9 = −1.68 + 9 ≈ **7.32**.
- Mildly acidaemic.

🟨 **Exam calculator.** Imperial's exam browser has a scientific calculator in landscape mode. log and 10ˣ available.

---

## Section 2 — Where acid comes from

📎 **Figure L2.01 — Blood gas values around the circulation**

### Q: Normal arterial vs mixed venous gas values?

| Parameter | Arterial | Mixed venous |
|---|---|---|
| PO₂ | >10 kPa | 4.0–5.3 kPa |
| SO₂ | >95% | ~75% |
| PCO₂ | 4.7–6.0 kPa | 5.3–6.7 kPa |

### Q: Why does a drop from 95% to 75% saturation matter more than it looks?
- At 95% you sit on the flat top of the O₂ dissociation curve.
- Below 75% you hit the **steep part** — small partial-pressure drops = big content drops.
- Tissues are operating close to that cliff edge; that's by design.

### Q: What proportion of body acid is respiratory vs metabolic, and why does it matter?
- **~99% respiratory** (CO₂ from mitochondria in every tissue).
- ~200 mL CO₂/min at rest → ~288 L/day.
- Every breath clears acid.
- A ventilatory problem shows up as an acid-base problem very quickly.

📎 **Figure L2.02 — Pulmonary transit time**

### Q: What are the two key pulmonary transit numbers, and why do they matter?
- **Transit time: 0.75 s** at rest (RBC in alveolar capillary).
- **Gas exchange time: 0.25 s** (3× reserve).
- Reserve allows exercise (transit shortens) without hypoxaemia.
- Lost reserve in pneumonia / oedema / fibrosis (membrane thickens) → hypoxaemia first, hypercapnia later (CO₂ is more diffusible).

📎 **Figure L2.04 — CO₂ flux at tissues**

### Q: How much CO₂ enters blood per minute, and why doesn't pH crash?
- 4 mL/dL CO₂ flux × 50 dL/min cardiac output = **+200 mL CO₂/min** added to blood.
- Arterial pH 7.40 → venous pH 7.36 (tiny change).
- Blood has **enormous, near-instantaneous buffering capacity**.

📎 **Figure L2.05 — Dog buffering experiment**

### Q: What did the dog experiment prove?
- Anaesthetised dog injected with 14 M acid.
- Predicted pH crash to ~2.5 (lethal).
- Observed: **pH 7.44 → 7.14** (dog survived).
- Proves: blood has **ENORMOUS buffering capacity acting IMMEDIATELY**.

🟨 **Lecturer-emphasised.** Dog experiment is the anchor memory for "blood is a huge buffer." Three tiers: chemical (seconds) → respiratory (minutes) → renal (days).

---

## Section 3 — The two compensators

### Q: What are the two compensation systems and their time scales?

| System | Mechanism | Time scale |
|---|---|---|
| **Respiratory** | Change minute ventilation → CO₂ | **Minutes** |
| **Renal** | Change HCO₃⁻ / H⁺ excretion | **Days** (3–5) |

### Q: What is the rescue rule for which system compensates for which?
- Primary **respiratory** problem → **renal** compensates (slow).
- Primary **metabolic** problem → **respiratory** compensates (fast).
- Direction: compensator always moves pH opposite to the primary disturbance.

### Q: Why does a DKA patient breathe deeply and rapidly?
- DKA = metabolic acidosis (ketoacids).
- Respiratory system compensates **within minutes** by hyperventilating.
- Blowing off CO₂ pulls the equation left → raises pH.
- Classic sign: **Kussmaul breathing**.

📎 **Figure L2.06 — Corrective compensation trajectories**

---

## Section 4 — The four archetypes

📎 **Figure L2.07 — Four-panel acid-base pathology summary**

### Archetype cards

### Q: Respiratory acidosis — trigger, ABG pattern, compensation?
- **Trigger**: opioid OD, COPD, severe asthma, neuromuscular weakness.
- Primary: **PaCO₂ ↑** → pH ↓.
- Compensation: **renal** retains HCO₃⁻ over days → BE rises.
- Trajectory: (↓, ↑, ↔) → (↓, ↑, ↑) → (↔, ↑, ↑).

### Q: Respiratory alkalosis — trigger, ABG pattern, compensation?
- **Trigger**: anxiety/panic, altitude, PE, fever, early aspirin OD.
- Primary: **PaCO₂ ↓** → pH ↑.
- Compensation: **renal** excretes HCO₃⁻ → BE falls.
- Trajectory: (↑, ↓, ↔) → (↑, ↓, ↓) → (↔, ↓, ↓).

### Q: Metabolic acidosis — trigger, ABG pattern, compensation?
- **Trigger**: DKA, lactic acidosis (sepsis/ischaemia), diarrhoea (HCO₃⁻ loss), renal failure, toxins (methanol, ethylene glycol).
- Primary: **BE ↓** → pH ↓.
- Compensation: **respiratory** hyperventilates → PaCO₂ ↓ (Kussmaul).
- Trajectory: (↓, ↔, ↓) → (↓, ↓, ↓) → (↔, ↓, ↓).

### Q: Metabolic alkalosis — trigger, ABG pattern, compensation?
- **Trigger**: vomiting (loses HCl), diuretics, antacid overuse.
- Primary: **BE ↑** → pH ↑.
- Compensation: **respiratory** hypoventilates → PaCO₂ ↑ (limited by hypoxaemia risk).
- Trajectory: (↑, ↔, ↑) → (↑, ↑, ↑) → (↔, ↑, ↑).

### Q: Map each clinical trigger to its archetype.

| Trigger | Archetype |
|---|---|
| Vomiting, diuretics | Metabolic alkalosis |
| Diarrhoea, DKA, sepsis | Metabolic acidosis |
| Opioid OD, COPD | Respiratory acidosis |
| Anxiety, PE, altitude | Respiratory alkalosis |

🟥 **Trap.** *Vomiting = alkalosis* (loses acid) but *diarrhoea = acidosis* (loses base). Direction matters, not "losing GI contents."

---

## Section 5 — The 4-step interpretation + master grid

📎 **Figure L2.08 — How to read the printout by step**
📎 **Figure L2.09 — Master ABG interpretation grid**

### Q: What are the 4 interpretation questions in order?
1. **Type of imbalance?** pH direction → acidosis / alkalosis / normal.
2. **Aetiology?** Which of PaCO₂ or BE explains the pH? → respiratory / metabolic / mixed / normal.
3. **Compensation?** Is the other axis rescuing pH? → uncomp / partial / full.
4. **Oxygenation?** PaO₂ → hypoxaemia / normoxaemia / hyperoxaemia.

### Q: Normal reference ranges for the 4 core values?

| Variable | Low | Normal | High |
|---|---|---|---|
| pH | <7.35 | 7.35–7.45 | >7.45 |
| PaCO₂ | <4.7 kPa | 4.7–6.0 kPa | >6.0 kPa |
| BE | <−2 | −2 to +2 | >+2 |

PaO₂: low <10 kPa / normal 10–13.5 / high >13.5 (*"rarely a problem"*). BE range is the easiest — 4-unit window centred on zero.

### Q: Hypoxaemia severity bands?
- **>10 kPa** — normal.
- **8–10** — mild hypoxaemia.
- **6–8** — moderate.
- **<6** — severe.

### Q: What are the 3 shortcut rules that replace memorising the master grid?
- **pH direction** = state (↓ = acidaemia, ↑ = alkalaemia, ↔ = compensated/normal).
- The value **moving same acid-direction as pH** = the **cause**.
- The value **moving opposite** = the **compensation**.
- Acid rules: "CO₂ is acid" (↑CO₂ = acidosis). "BE is base" (↓BE = acidosis).

🟦 **Reusable.** If pH ↓ and CO₂ ↑: CO₂ is causing. If pH ↓ and CO₂ ↓: CO₂ is compensating (metabolic problem). Same logic for BE.

### Q: Why can you not always distinguish between resp acidosis and metabolic alkalosis when fully compensated?
- Pattern (↔, ↑, ↑) matches **both**:
  - Fully compensated respiratory acidosis (CO₂ up, kidneys pulled BE up).
  - Fully compensated metabolic alkalosis (BE up, lungs pushed CO₂ up).
- Numbers alone are ambiguous. **The clinical story decides.**

🟥 **Trap.** Don't call "normal pH" on an ABG with abnormal CO₂ and BE. That's compensated disease, not health.

### Q: Worked example — pH 7.29, PaCO₂ 8.5 kPa, BE +6, PaO₂ 7.1 kPa. Known COPD. Diagnosis?
- Step 1: pH ↓ → acidosis.
- Step 2: PaCO₂ ↑ explains → **respiratory**. BE ↑ is not causing — opposite direction to what metabolic acidosis would need.
- Step 3: BE ↑ is the **rescue** → partial compensation (pH still <7.35). Chronic COPD means kidneys had time to buffer.
- Step 4: PaO₂ 7.1 = moderate hypoxaemia.
- **Answer**: partially compensated respiratory acidosis with moderate hypoxaemia — acute-on-chronic COPD exacerbation.

🟥 **Robot trap.** Lecturer's warning: a reported pH of 3.5 is physiologically impossible. If an ABG shows impossible values (via transcription error / AI-assisted summary), **repeat the sample**. Don't pattern-match numbers that can't exist.

---

## Section 6 — Cross-lecture links

### Q: Which ECG finding pairs with a fully compensated respiratory acidosis?
- **Right axis deviation** (>+90°) from chronic RV hypertrophy in COPD/cor pulmonale.
- P pulmonale (peaked P).
- See also: L1 — *Cardiac axis, causes of RAD*.

### Q: Which arrhythmia would you expect to produce a lactic acidosis on ABG?
- **VT or VF** → poor cardiac output → tissue hypoperfusion → anaerobic metabolism → lactate.
- ABG shows partially compensated metabolic acidosis.
- See also: L1 — *Ventricular tachycardia*.

### Q: How does the vagus-ventilation link appear in both lectures?
- L1: **sinus arrhythmia** — inspiration ↓vagal tone → HR ↑.
- L2: **rapid respiratory compensation** — medullary chemoreceptors drive ventilation to change CO₂ → pH.
- Same physiological axis, different monitored output.
- See also: L1 — *Sinus arrhythmia*.

### Q: Why do the 4-step ABG and 7-step ECG procedures share a meta-skill?
- Both are numbered bedside algorithms.
- Both reward **systematic over holistic** reading.
- Meta-skill transfers to any investigation: CXR, PFT, echo, bloods.
- See also: L1 — *ECG reporting procedure*.

---

## Section 7 — Reusable reasoning pattern

### Q: The 6-beat pattern for any ABG in under 10 seconds.
1. pH — acidaemic, alkalaemic, or normal?
2. PaCO₂ — does it explain the pH? (CO₂ is acid.)
3. BE — does it explain the pH? (BE is base.)
4. Whichever explains = cause. Whichever opposes = compensation.
5. PaO₂ — hypoxaemia severity band?
6. Integrate with clinical story (acute vs chronic; COPD vs DKA vs vomiting).

---

## Section 8 — Interleaved SBAs

### Q: SBA 1 — 25-year-old hyperventilating from anxiety. pH 7.52, PaCO₂ 3.5, BE +1, PaO₂ 13. Diagnosis?
- **A.** Uncompensated respiratory acidosis
- **B. Uncompensated respiratory alkalosis** ✓
- **C.** Uncompensated metabolic alkalosis
- **D.** Partially compensated respiratory alkalosis
- **E.** Fully compensated respiratory alkalosis

**Answer: B.** pH ↑, PaCO₂ ↓ (explains), BE ↔ (uncompensated — acute). Metabolic alkalosis would show BE ↑. Partial compensation would show BE ↓.

### Q: SBA 2 — 68-year-old, known COPD, routine check. pH 7.37, PaCO₂ 7.8, BE +6, PaO₂ 8.5. Diagnosis?
- **A.** Uncompensated respiratory acidosis
- **B.** Uncompensated metabolic alkalosis
- **C. Fully compensated respiratory acidosis with mild hypoxaemia** ✓
- **D.** Partially compensated metabolic alkalosis
- **E.** Mixed disorder

**Answer: C.** pH in range (7.35–7.45). PaCO₂ and BE both ↑ → fully compensated chronic respiratory acidosis. Clinical story of COPD confirms direction. PaO₂ 8.5 = mild hypoxaemia.

### Q: SBA 3 — 20-year-old T1DM, drowsy, Kussmaul. pH 7.15, PaCO₂ 2.8, BE −20, PaO₂ 14. Mechanism of low CO₂?
- **A.** Incidental
- **B. Respiratory compensation via hyperventilation** ✓
- **C.** Renal compensation
- **D.** Anxiety-driven hyperventilation
- **E.** Mixed disorder

**Answer: B.** DKA = metabolic acidosis (ketoacids → ↓BE). Kussmaul breathing blows off CO₂ as rapid respiratory compensation. Partial (pH still ↓). Renal would take days.

### Q: SBA 4 — Reported ABG: pH 2.9, PaCO₂ 5.0, BE 0, PaO₂ 12. Most appropriate action?
- **A.** Start bicarbonate infusion
- **B. Repeat the sample — these values are physiologically impossible** ✓
- **C.** Intubate
- **D.** Adrenaline
- **E.** Diagnose compensated acidosis

**Answer: B.** pH 2.9 incompatible with life. Normal CO₂ and BE can't produce pH 2.9 anyway. Classic robot-trap; lecturer-flagged.

### Q: SBA 5 — Vomiting for 3 days. pH 7.52, PaCO₂ 6.2, BE +7, PaO₂ 12. Diagnosis?
- **A.** Uncompensated metabolic alkalosis
- **B. Partially compensated metabolic alkalosis** ✓
- **C.** Fully compensated metabolic alkalosis
- **D.** Respiratory alkalosis
- **E.** Mixed alkalosis

**Answer: B.** Vomiting → loses HCl → BE ↑ → pH ↑. PaCO₂ ↑ is the respiratory compensation (hypoventilation). pH still out of range → partial.

### Q: SBA 6 — Severe diarrhoea. pH 7.28, PaCO₂ 3.5, BE −10, PaO₂ 13. Aetiology and compensation?
- **A. Metabolic acidosis (HCO₃⁻ loss), partially compensated respiratory** ✓
- **B.** Metabolic alkalosis
- **C.** Respiratory acidosis
- **D.** Uncompensated mixed acidosis
- **E.** Fully compensated metabolic acidosis

**Answer: A.** Diarrhoea → HCO₃⁻ loss → BE ↓ → pH ↓. Hyperventilation ↓PaCO₂ = respiratory compensation. pH still out of range → partial.

### Q: SBA 7 — What percentage of total body acid is respiratory?
- **A.** 10%
- **B.** 50%
- **C.** 80%
- **D. ~99%** ✓
- **E.** ~25%

**Answer: D.** ~99%. Every mitochondrion produces CO₂. ~200 mL/min cleared via lungs. Explains why ventilation is the dominant acid-handling route.

### Q: SBA 8 — Heroin overdose, respiratory rate 4/min. Expected ABG?
- **A.** pH ↓, PaCO₂ ↑, BE ↔
- **B.** pH ↑, PaCO₂ ↓, BE ↔
- **C.** pH ↓, PaCO₂ ↔, BE ↓
- **D.** pH ↑, PaCO₂ ↔, BE ↑
- **E.** All normal

**Answer: A.** Opioid hypoventilation → CO₂ retention → acute respiratory acidosis. Uncompensated because acute (kidneys haven't had time).

### Q: SBA 9 — Pulmonary embolism, hyperventilating. Most likely ABG?
- **A. pH ↑, PaCO₂ ↓, PaO₂ ↓** ✓
- **B.** pH ↓, PaCO₂ ↑, PaO₂ ↓
- **C.** pH ↑, PaCO₂ ↑, PaO₂ ↓
- **D.** pH ↓, PaCO₂ ↓, PaO₂ ↑
- **E.** All values normal

**Answer: A.** PE causes hyperventilation (pain, hypoxia-driven) → respiratory alkalosis. V/Q mismatch from clotted vessels → hypoxaemia. Characteristic paired finding.

### Q: SBA 10 — Patient with metabolic acidosis. How long before renal compensation is complete?
- **A.** Seconds
- **B.** Minutes
- **C.** Hours
- **D. Days (3–5)** ✓
- **E.** Renal doesn't compensate for metabolic acidosis

**Answer: D.** Note: E is tempting but wrong — renal does compensate for metabolic disorders, just not as the *primary* rapid response (which is respiratory). Renal adjustments complete in 3–5 days. E would be true if asking about the *fast* compensator for metabolic disorders (answer then = respiratory).

---

## TILO check

- **CV & respiratory regulation** ✓ — acid-base homeostasis; respiratory and renal compensation; central chemoreceptor CO₂/[H⁺] sensing.
- **CV & respiratory integration** ✓ — pulmonary transit time, CO₂ flux at tissues, gas exchange time, cardiac output effect.
- **CV & respiratory investigations** ✓ — 4-step ABG interpretation, master grid, reference ranges, worked examples.

Full renal mechanism of acid-base compensation deferred to Renal module (spring term).
