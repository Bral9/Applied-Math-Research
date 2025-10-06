# Cameroon Population Modeling — Malthus vs Logistic (2007–2022) 🇨🇲📈
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
![Python](https://img.shields.io/badge/Python-3.10+-blue)
![Methods](https://img.shields.io/badge/Models-Malthus%20%7C%20Logistic-green)

## Overview
**Question.** Which growth model—**Malthus (exponential)** or **Logistic (Verhulst)**—better fits Cameroon’s population (2007–2022) and provides a credible long-run projection toward carrying capacity?

**Answer (summary).** The **Logistic model** fits slightly better (lower error) and its residuals are more consistent with **decelerating growth toward a finite carrying capacity**, so it was selected for forecasting.

---

## Data
Annual population counts for **Cameroon, 2007–2022**.  
All computations and plots were implemented in **Python/Matplotlib**.

---

## Models
- **Malthus (exponential)**  
  $P(t)=P_0e^{\beta t}\$
- **Verhulst (logistic)**  
  $P(t)=\frac{KP_0}{P_0+(K-P_0)e^{-r t}}\$

Here t is years since 2007; $P_{0}\$ is the 2007 population; $\beta\$ the exponential rate; $r\$ the logistic growth rate; $K$ the carrying capacity.

---

## Parameter Estimation
- **Exponential:** estimate $\beta\$ via **least squares** on $\log P(t)\$.  
  Result: $P_0 \approx 18{,}730{,}000\$, $beta \approx 0.026663\$.
- **Logistic:** estimate $r, K\$ via a **two-point method** using $t=7\$ and $t=14\$.  
  Result: $K \approx 1.0488\times 10^8\$, $r \approx 0.034042\$.

---

## Error Metric
**EAMP (MAPE)**  
$\mathrm{EAMP}=\frac{1}{N}\sum_{t=1}^{N}\left|\frac{X_t-\hat X_t}{X_t}\right|\times 100\$

---

## Results (2007–2022)
| Model     | EAMP / MAPE | Notes |
|-----------|-------------:|------|
| Malthus   | **0.245%**   | Slightly higher error; residuals suggest persistent exponential drift. |
| Logistic  | **0.241%**   | **Best** fit; residuals look closer to white noise and align with finite \(K\). |

**Selected model:** **Logistic** — because of (i) lower EAMP and (ii) residuals consistent with saturation dynamics.

---

## Projection (Logistic)
Using **implicit Euler** on $\dot P = rP(1 - P/K)\$ with the fitted parameters above:
- **Approach to saturation:** ~**year 2673** (≈ 666 years after 2007)
- **Interpretation:** horizon is illustrative; it reflects the model’s long-run equilibrium under a finite $K\$.

---

## Reproducibility
- Language: **Python 3.10+**
- Libraries: `matplotlib`

---

## Takeaways
- **Logistic** is preferred for both **fit quality** (slightly lower MAPE) and **theory** (resource-constrained growth).  
- Exponential growth can approximate short windows but **overstates** long-run population under capacity limits.

---

## License
MIT — see `LICENSE` for details.
