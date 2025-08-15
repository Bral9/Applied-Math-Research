# Cameroon Population Modeling (Malthus vs. Logistic)

## Overview
This study asks: *Which model, Malthus or Verhulst, is more reliable for estimating when Cameroon reaches its maximum sustainable population?*  
I modeled 2007–2022 population figures and evaluated model fit with EAMP. Visualizations were produced in Python.

## Data
Annual population counts for Cameroon (2007–2022), summarized in **Table 1**, were used to fit model parameters and compute errors.

## Methods

### Models
- **Malthus (exponential):** $P(t)=P_0 e^{\beta t}$  
- **Verhulst (logistic):**
  $P(t)=\frac{K P_0}{\,P_0 + (K-P_0)e^{-rt}\,}$

### Parameter estimation
- **Exponential model:** Estimate $\beta$ via **least squares** on $\log P(t)=\log P_0+\beta t\cdot \log e$.  
  From the fit: $P_0 \approx 18{,}730{,}000$, $\beta \approx 0.026663$, yielding $P(t)=18{,}730{,}000\,e^{0.026663t}$.
- **Logistic model:** Solve for $r$ and $K$ using a **two-point** method with $t=T=7$ and $t=2T=14$ (years since 2007). This gave $K\approx 104{,}875{,}664$ and $r\approx 0.034042$.

### Error metric
- **EAMP (mean absolute percentage error):**
  $\mathrm{EAMP}=\frac{1}{N}\sum_{t=1}^{N}\left|\frac{X_t - \hat X_t}{X_t}\right|\times 100$

### Projection to saturation
Using **implicit Euler** on $f(P)= rP \left(1-\frac{P}{K}\right)$ with $P_0=18{,}730{,}000$ found $t=666$ years after 2007 → **year 2673**.

## Results
- **Fit quality (2007–2022):**
  - Malthus EAMP ≈ **0.245%**
  - Logistic EAMP ≈ **0.241%**

- **Chosen model:** Logistic (slightly lower error and more realistic long-run behavior under resource limits).
