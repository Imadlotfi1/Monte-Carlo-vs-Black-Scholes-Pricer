# European Option Pricing Engine: Monte Carlo vs. Black-Scholes

This project provides a comprehensive and validated pricing engine for European options, capable of calculating both option prices and their corresponding risk sensitivities (the Greeks). It serves as a practical demonstration of quantitative finance principles, comparing a numerical simulation method (Monte Carlo) against a closed-form analytical solution (Black-Scholes).

## 📊 Key Features

- **Dual Pricing Methods**: Implements both the analytical Black-Scholes formula and a vectorized Monte Carlo simulation.
- **Complete Greeks Calculation**: Computes all five major Greeks (Delta, Gamma, Vega, Theta, Rho) using both analytical formulas and numerical finite difference methods.
- **High Accuracy & Validation**: Achieves an average error of **<1%** for Monte Carlo Greeks compared to analytical benchmarks, with robust handling of second-order derivatives (Gamma).
- **Performance**: Leverages NumPy vectorization to perform over 100,000 simulations in approximately **0.013 seconds**.
- **Statistical Rigor**: Includes convergence analysis to verify the O(1/√N) behavior of the Monte Carlo method and statistical validation of results.

---

## 📈 Final Results Summary

The Monte Carlo engine was validated against the Black-Scholes model using a standard set of parameters for an at-the-money European call option.

| Parameter | Value |
|---|---|
| Spot Price (S0) | $100 |
| Strike Price (K) | $100 |
| Time to Maturity (T) | 1 year |
| Risk-Free Rate (r) | 5% |
| Volatility (σ) | 20% |

### Greeks Comparison (100,000 Simulations)

The numerical estimates from the Monte Carlo simulation align closely with the exact analytical values.

| Greek | Black-Scholes | Monte Carlo | Error (%) | Status |
|-------|---------------|-------------|-----------|--------|
| **Delta** | 0.6368 | 0.6394 | 0.40% | ✅ Excellent |
| **Gamma** | 0.0188 | 0.0186 | 0.86% | ✅ Excellent |
| **Vega** | 37.5240 | 37.8933 | 0.98% | ✅ Excellent |
| **Theta** | -0.0176 | -0.0177 | 0.69% | ✅ Excellent |
| **Rho** | 53.2325 | 54.0741 | 1.58% | ✅ Excellent |

_Note: The methodology correctly stabilizes the Gamma calculation by using a wider bump size, reducing the error from over 10% to less than 1%._


---

## 🛠️ Methodology Highlights

### 1. Model Dynamics
The underlying asset price is modeled using Geometric Brownian Motion (GBM):
$$ dS_t = r S_t dt + \sigma S_t dW_t $$

### 2. Numerical Greeks Calculation
The Greeks are estimated using the **Finite Difference Method** combined with the **Common Random Numbers (CRN)** variance reduction technique. This ensures that the noise from the simulation is minimized when calculating sensitivities.

- **First-Order Greeks (Delta, Vega, Rho, Theta)**: Calculated using a one-sided or central difference approach.
- **Second-Order Greek (Gamma)**: Stabilized using a wider bump size for the underlying price to ensure the curvature signal is stronger than the simulation noise, a critical adjustment for second-derivative stability in Monte Carlo.

### 3. Validation
The project's success is validated by:
- **Low Percentage Error**: All Greeks are estimated with less than 2% error.
- **Convergence Analysis**: The notebook visually confirms that the Monte Carlo estimates converge towards the analytical Black-Scholes values as the number of simulations (N) increases, following the theoretical O(1/√N) rate.

---

## 🚀 How to Use

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/Imadlotfi1/Monte-Carlo-vs-Black-Scholes-Pricer.git
    cd Monte-Carlo-vs-Black-Scholes-Pricer
    ```
2.  **Install dependencies:**
    ```bash
    pip install numpy pandas matplotlib seaborn scipy
    ```
3.  **Run the Jupyter Notebook:**
    ```bash
    jupyter notebook "Option Pricing : Monte Carlo vs Black-Scholes.ipynb"
    ```
    You can modify the parameters in the "Parameters Setup" section to price different options and analyze the results.

---
