# Storm-to-Quote
**Florida wind parametric · hypothetical event set · $10M limit (assume)**

I built a hypothetical replica of the "Florida 2nd stochastic event set" structure. <BR>

**Historical_HURDAT** — 150 synthetic storm records in a HURDAT-style layout (storm ID, season, wind speed, category, pressure, FL region), spanning an illustrative 1851–2024 window. This is what I'd use to calibrate frequency and severity <br>

**Stochastic_YLT_49999** a 49,999-row Year Loss Table, the standard cat-model output format. Each row is one simulated year: number of storms, the worst storm's peak intensity, its distance of closest approach to a single reference site, the resulting site-level wind speed, category, and payout.<br>

**On methodology:** since a single point can't just inherit a whole storm's peak wind (a Cat 5 passing 200 miles away barely grazes one site), I added a wind-field decay step — each storm's peak intensity is attenuated to the site using Site_Wind = Peak_Wind × exp(−distance/75mi), with distance of closest approach drawn from an Exponential(mean 120mi). That's what separates "150 storms hit Florida somewhere" from "what did this one location actually feel." <br>
Frequency comes from a Poisson process calibrated to the historical set (λ≈0.86 storms/yr); severity within each category is Beta(2,4)-shaped, skewed toward the category's lower bound as real climatology tends to show. <br>
For the payout ladder,I interpreted it as Cat1-or-below → 0%, Cat2 → 50%, Cat3+ → 100% <BR>

**Result** on this hypothetical catalog, $10M limit: EL ≈ 4.32% of limit (~$431.7k), std dev ≈18.4% (CV≈4.3, typical of a low-frequency/high-severity cat layer), attachment probability ≈5.8%/yr, full-payout probability ≈2.8%/yr. <Br>
