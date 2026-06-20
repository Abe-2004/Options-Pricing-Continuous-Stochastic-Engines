# Continuous-Time Derivatives Valuation: Analytical Black-Scholes vs. Vectorized Monte Carlo

## Executive Summary
This project constructs a financial engineering pipeline to price European derivatives using two distinct paradigms: an analytical closed-form partial differential equation (PDE) solution via the **Black-Scholes-Merton** framework, and a brute-force numerical simulation via a vectorized **Monte Carlo** asset simulator under **Geometric Brownian Motion (GBM)**.

## Mathematical Architecture
The underlying asset price path ($S_t$) is modeled as a continuous stochastic process governed by the classic Stochastic Differential Equation (SDE):

$$dS_t = r S_t dt + \sigma S_t dW_t$$

Where:
* **Analytical Solution (Black-Scholes):** Solved via Itô's Calculus to yield the deterministic pricing metric:
  $$\text{Call Price} = S_0 N(d_1) - K e^{-rT} N(d_2)$$
* **Numerical Solution (Monte Carlo):** Discretized over 100,000 parallel terminal paths utilizing a vectorized NumPy log-normal space transformation:
  $$S_T = S_0 \exp\left( \left(r - \frac{1}{2}\sigma^2\right)T + \sigma \sqrt{T} \cdot Z \right)$$

## Calibration & Numerical Verification
* **Market Inputs:** Spot Price ($S_0$) = 100.0, Strike Price ($K$) = 105.0, Horizon ($T$) = 1 Year, Risk-Free Rate ($r$) = 5%, Annual Volatility ($\sigma$) = 20%.
* **Analytical Ground Truth:** Exact Black-Scholes Call Price = **$8.0214**
* **Numerical Simulation Results:** 100,000 parallel paths generated an estimated option value of **$8.0416** with a microscopic absolute discrepancy of **$0.0203**.
* **Statistical Validity:** The simulation converged cleanly within a calculated Numerical Standard Error boundary of **+/- 0.0439**, mathematically confirming the Law of Large Numbers.
