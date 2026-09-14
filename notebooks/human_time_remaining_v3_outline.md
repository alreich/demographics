# `human_time_remaining_v3.ipynb` — Outline

**Working title:** Catastrophe Pathway Fault Tree + Robust-Bayes Reference-Class Synthesis

This extends v2 (three reference-class outside-view estimates + Gott delta-t + Carter-Leslie)
with (1) an explicit fault tree for catastrophic extinction pathways, and (2) a formal
robust-Bayes treatment across the reference classes instead of picking or softly averaging one.

---

## 0. Abstract
Same convention as v1/v2: 1 paragraph stating what's new in this notebook relative to v2,
and the headline result once you have it (e.g. "adding catastrophe pathways shifts the
combined median from X to Y; robust bounds across reference classes span [lo, hi]").

## 1. Recap of v1/v2 state (short, mostly loaded not re-derived)
- Reload the three reference-class posteriors from v2: All Mammalia (median 5.2 Myr),
  Primates (median 3.5 Myr), Large-bodied ≥10kg (median 3.9 Myr)
- Reload Gott delta-t and Carter-Leslie posteriors (using N_past ≈ 79.4B, 95% CI [70.5B, 89.4B])
- One paragraph noting the framing shift: v1/v2 modeled a *background* hazard (evolutionary/
  ecological turnover, "no privileged position" reasoning); v3 adds a *foreground* hazard
  (acute catastrophe) that was explicitly excluded from that scope. State this framing
  change explicitly in the notebook so the two hazard types aren't implicitly conflated.

## 2. Part D — Catastrophe fault tree

### 2.1 Tree structure
- Top event: "extinction-causing catastrophe by time *t*"
- First pass: OR-gate, pathways treated as independent competing risks
- Note (for a v4, not implemented here): shared-cause refinement — ecological collapse can
  be triggered by pandemic-driven societal collapse or an asteroid winter — would need
  AND/OR logic instead of a pure product; flag as a known simplification

### 2.2 Sub-model: asteroid / comet impact
- Data: NASA/ESA NEO survey size-frequency counts; crater-count record as a cross-check
- Model: marked Poisson process — rate λ(size) fit from survey data, civilization-ending
  lethality probability p(size) as a step/logistic function of impactor diameter
  (Tunguska/Chelyabinsk-scale vs. Chicxulub-scale threshold)
- PyMC sketch:
  ```
  with pm.Model():
      log_rate = pm.Normal("log_rate", mu=..., sigma=...)  # per size bin, from survey data
      threshold = pm.Normal("lethal_diam_km", mu=10, sigma=2)  # weakly informative
      # posterior predictive: P(lethal impact in next t years)
  ```
- This is the best-constrained pathway — treat it as the "sanity check" sub-model

### 2.3 Sub-model: pandemic
- Data: historical pandemic frequency (plague, 1918 flu, COVID) as partial data;
  zero historical events at extinction-level severity
- Model: hierarchical — emergence rate × P(extinction-level | emergence), the latter
  built from R0, case-fatality rate, intervention-effectiveness sub-parameters
- Zero-event tail: use Laplace's rule of succession / Jeffreys prior to bound
  P(extinction-level | emergence) rather than assuming a point value
- Optional informative prior source: Ord (2020, *The Precipice*) elicited estimates,
  used as a prior mean with inflated uncertainty rather than taken at face value

### 2.4 Sub-model: ecological collapse
- Least data-rich pathway — treat as time-*varying* hazard tied to an anthropogenic
  driver trajectory (e.g. logistic-increasing hazard keyed to a warming or
  biodiversity-loss proxy trend) rather than constant-rate
- Priors here are the most subjective in the notebook — say so explicitly and consider
  a structured-elicitation-style prior (a small set of named scenarios with assigned
  weights) rather than a single smooth functional form, so the subjectivity is visible
  and auditable rather than hidden in a parametric choice

### 2.5 Combining the three pathways
- S_catastrophe(t) = S_asteroid(t) · S_pandemic(t) · S_ecological(t)
- Plot combined catastrophe-only survival curve; report combined median/CI
- Diagnostic: report each pathway's marginal contribution to short-horizon risk
  (e.g. next 1,000 / 10,000 / 1M years) since they operate on very different timescales

## 3. Part E — Combining background (v1/v2) with catastrophe (Part D)
- S_total(t) = S_background(t) · S_catastrophe(t), computed separately per reference class
  and per background method (outside-view / Gott / Carter-Leslie)
- Expect catastrophe pathways to dominate the *short*-horizon tail and background hazard
  to dominate the *long*-horizon tail — show this as a single combined-hazard plot with
  both components visible, not just the product curve, so the crossover point is legible

## 4. Part F — Robust Bayes across reference classes
### 4.1 Define the prior class Γ
- Γ = the 3 reference classes × 2 parametric forms (Kaplan-Meier empirical, log-logistic)
  already built in v1/v2 — six posteriors, no new fitting required

### 4.2 Robust interval
- For a quantity of interest Q (e.g. P(T < 1 Myr), or median T), compute
  min over Γ and max over Γ of the posterior value of Q
- Report as an interval, explicitly *not* collapsed to a point — this is the
  "class of priors" / Berger-style sensitivity analysis, distinct from BMA

### 4.3 Soft-BMA comparison (secondary, for contrast)
- Also compute a single blended posterior weighting the 3 reference classes by
  out-of-sample predictive fit (WAIC/LOO) or by phylogenetic proximity to humans
- Present side-by-side with 4.2's interval so the notebook shows both "our best
  single number" and "how much that number depends on an unresolved modeling choice"

## 5. Sensitivity / diagnostics
- Vary each catastrophe sub-model's most subjective prior (esp. ecological collapse)
  and show how much the combined median shifts — same spirit as v2's reference-class
  narrowing sensitivity check (24-40% shift reported there)

## 6. Pros / cons
- Same convention as v1/v2. Cons should explicitly include: independence assumption
  between catastrophe pathways, subjectivity of the ecological-collapse prior, and the
  framing tension between "background" and "foreground" hazard noted in §1

## 7. Conclusions
- Standard summary; headline should report both the combined point estimate(s) and
  the robust interval width from Part F, not just a single number

## 8. References
- Existing v1/v2 bibliography, plus: NASA/ESA NEO survey data sources, Ord (2020)
  *The Precipice*, PRA/fault-tree methodology references (e.g. WASH-1400 lineage),
  Berger — robust Bayesian analysis overview, Walley — imprecise probability

## 9. Appendix — new data provenance
- Document sources/access dates for NEO survey data and any pandemic/ecological
  datasets pulled in, matching the existing PBDB/NOW provenance notes from v1
