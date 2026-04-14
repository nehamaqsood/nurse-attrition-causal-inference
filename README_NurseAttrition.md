# Nurse Attrition Policy Evaluation — Causal Inference Analysis

A causal inference study evaluating the impact of two nurse retention policies at a Southern California hospital network (Optum), using Synthetic Control, Synthetic Difference-in-Differences, and Causal Random Forest methods.

**Duke Fuqua | Section C, Team 2**
Xinghan Shen, Alexander Lim, Jessica Xiong, Neha Maqsood, John Saleeb

---

## Background

Since the pandemic, nurse attrition has risen sharply at Optum's 50+ hospital network, driving up training costs and straining patient care. To respond, Optum introduced two retention policies:

1. **Seniority Bonus** — a financial bonus for nurses with 10+ years of tenure
2. **Management Training Program** — a hospital-level program offering career development and leadership pathways

This project answers three questions posed by the client:
- What was the causal impact of each policy on nurse attrition?
- How did attrition change at treated hospitals relative to untreated ones over time?
- Do these policies work equally well across all subgroups, or do some nurses benefit more than others?

---

## Data

Data is simulated at the nurse-month level across 52 hospitals over 36 months, designed to reflect realistic workforce dynamics. The simulation incorporates:

- **Hospital-level factors:** bed size, region (Metro/Coastal/Inland), for-profit status, operational strain
- **Nurse-level factors:** age, tenure, education level (ADN/BSN/MSN+), unobserved resilience
- **Treatment assignment:** seniority bonus (rule-based, tenure ≥ 10 years) and management training (staggered adoption based on hospital strain)
- **Outcome:** binary nurse attrition per month, modeled via a logistic probability function

Simulating the data was an intentional methodological choice — it allows precise control over the true treatment effect, enabling rigorous validation of the causal methods used.

---

## Methods

Three econometric and machine learning techniques were applied in sequence:

**1. Synthetic Control (SC)**
Constructs a weighted combination of untreated hospitals to serve as a counterfactual for early training adopters. Allows visual and quantitative estimation of hospital-level treatment effects.

**2. Synthetic Difference-in-Differences (SDiD)**
Estimates the average treatment effect on treated hospitals while relaxing the parallel trends assumption required by standard DiD. More robust to pre-existing differences between treated and control hospitals.

**3. Causal Random Forest (HTE)**
Estimates Conditional Average Treatment Effects (CATEs) at the nurse level to identify which subgroups benefit most from each policy. Captures heterogeneity by age, tenure, and education that average effects would miss.

---

## Results

- Hospitals adopting the management training program saw meaningfully lower attrition rates relative to the synthetic control
- The seniority bonus reduced attrition among eligible nurses, though effects were more uniform across subgroups
- HTE analysis found that **mid-career nurses (5–15 years tenure)** respond most strongly to the management training program
- High-turnover hospitals benefit disproportionately from targeted intervention

**Recommendation:** Expand management training at high-turnover hospitals and prioritize retention bonuses for mid-career nurses rather than applying programs uniformly across the network.

---

## Files

- `Team02-24Feb2026-1.qmd` — full analysis in R (data simulation, EDA, SC, SDiD, and Causal Random Forest)
- `Team02-24Feb2026-1.html` — rendered output with all visualizations and results (open in browser)

---

## Tools & Libraries

R — `tidyverse`, `MatchIt`, `Synth`, `synthdid`, `grf`, `ranger`, `ggplot2`, `sandwich`
