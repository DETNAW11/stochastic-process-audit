# Stochastic Process Audit & Memoryless Property Verification

An end-to-end empirical statistical audit conducted on a continuous stochastic time series ($n = 638$). The primary objective of this project is to rigorously evaluate whether the data-generating process follows an **independent and identically distributed (i.i.d.) bounded distribution** or exhibits first/second-order Markovian memory, serial autocorrelation, or temporal clustering.

---

## Executive Summary

A common misconception in bounded multiplier processes is the presence of "hot streaks" or "compensation effects" (Gambler's Fallacy). This study applies parametric maximum likelihood estimation, exact non-parametric hypothesis testing, Markov chain transition analyses, and Monte Carlo risk simulations to test for sequential independence.

**Key Finding:** The underlying process is strictly **memoryless and i.i.d.**, with an estimated house edge ($\hat{\varepsilon}_{MLE}$) of **4.08%** ($IC_{95\%}: [2.68\%, 5.91\%]$). All observed streak patterns conform precisely to a theoretical Geometric distribution driven purely by sample variance.

---

## Statistical Methodology & Results Summary

| Test / Metric | Evaluated Parameter | Sample Metric ($n=638$) | $p$-value / Threshold | Conclusion |
| :--- | :--- | :--- | :--- | :--- |
| **MLE Estimator ($\hat{\varepsilon}$)** | Implied Edge / Friction | $4.08\%$ ($26$ collapses at $1.00\text{x}$) | $IC_{95\%}: [2.68\%, 5.91\%]$ | Consistent with theoretical edge ($\varepsilon = 3\%$) |
| **Exact Binomial Test** | Success Rate $\ge 1.50\text{x}$ | $65.05\%$ ($415$ hits) | $p = 0.43817$ | $H_0$ Not Rejected; aligns with $P(X \ge 1.50) = 64.67\%$ |
| **Runs Test** | Sequential Independence | $299$ observed runs | $Z = 0.6876$ ($p = 0.49169$) | $H_0$ Not Rejected; sequence is i.i.d. |
| **Markov Transition ($\ge 2.00\text{x}$)** | First-Order Dependency | $P(G \mid G) = 47.77\%$ vs $P(G \mid P) = 50.77\%$ | $\chi^2 = 0.4607$ ($p = 0.49730$) | Absence of streak memory or momentum |
| **2nd-Order Chain ($\ge 2.00\text{x}$)** | Conditional Continuation | $P(X_t \ge 2 \mid X_{t-1} \ge 2, X_{t-2} \ge 2) = 45.33\%$ | $p = 0.85800$ | $H_0$ Not Rejected; no acceleration effect |
| **Ljung-Box Test (Lags 1-10)** | Serial Autocorrelation | $Q = 7.7221$ (Lag 10) | $p_{\text{min}} = 0.26815$ | Absence of temporal clustering or seasonality |
| **Gambler's Fallacy Test** | Rebound after 4 losses ($<2\text{x}$) | $P(5\text{th} \ge 2 \mid 4 \text{ losses}) = 52.94\%$ | $p = 0.40333$ | $H_0$ Not Rejected; outcome remains $50\%$ binomial |

---

## Main Analytical Insights

### 1. Verification of the Memoryless Property
The conditional probability of hitting a target multiplier $x$ remains invariant regardless of preceding outcomes:
$$P(X_t \ge x \mid X_{t-1}, X_{t-2}, \dots, X_{t-k}) = P(X_t \ge x)$$
Both win and loss streak lengths strictly follow a **Geometric Distribution** $P(K=k) = p^{k-1}(1-p)$, confirming that apparent clusters are standard sample fluctuations.

### 2. Expected Value ($EV$) & Risk of Ruin
For any fixed cashout target $x$, the theoretical and empirical expected value per unit bet is strictly negative:
$$EV(x) = \frac{1 - \varepsilon}{x} \cdot (x - 1) + \left(1 - \frac{1 - \varepsilon}{x}\right) \cdot (-1) = -\varepsilon$$
Monte Carlo simulations ($1,000$ iterations over $1,000$ rounds) demonstrate that due to $EV < 0$, the long-term asymptotic probability of bankruptcy approaches $100\%$ ($P(\text{Ruin}) \to 1$ as $N \to \infty$).

---

## Project Structure

```text
├── data/
│   └── dataset.xlsx                   # Time series observations (n = 638)
├── notebooks/
│   └── stochastic_process_audit.ipynb # Complete analytics pipeline & hypothesis tests
├── .gitignore
├── requirements.txt
└── README.md
```


## How to Run

1. **Clone the repository:**
```bash
git clone https://github.com/DETNAW11/stochastic-process-audit.git
cd stochastic-process-audit

```


2. **Set up the environment:**
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt

```


3. **Launch the analysis:**
```bash
jupyter notebook notebooks/stochastic_process_audit.ipynb

```



---

## Author

* **Luis Alejandro Prieto Torres** – *Statistician & Data Scientist / Data Engineer*
* Profile: Focus on Statistical Modeling, Time Series Analysis, and Data Platform Engineering.