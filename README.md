# Insurance Portfolio Risk Simulation

A Monte Carlo simulation of an insurance company's capital adequacy over a 50-year time horizon, incorporating premium growth, policy retention with price elasticity, claims severity modeling, and disaster scenarios.

## Overview

This model simulates 100,000 parallel paths of an insurance portfolio's evolution, tracking capital adequacy and calculating ruin probability. It was built as an independent learning project after discovering that simulation modeling is far more engaging to me than traditional application development.

## Key Results

| Metric | Value |
|--------|-------|
| Ruin probability (50 years) | 0.25% |
| 95% VaR Capital (Year 50) | 2.37B |
| Mean Capital (Year 50) | 8.66B |

## Model Features

| Feature | Description |
|---------|-------------|
| **Premium growth** | Lognormal distribution with configurable drift and volatility |
| **Policy growth** | Lognormal distribution with base growth rate |
| **Price elasticity** | Premium increases reduce retention rate (normal distribution around mean elasticity) |
| **Claim types** | Small claims (85-95% of events) and large claims (5-15%) |
| **Claim limits** | Deductibles and caps applied to both claim types |
| **Inflation** | Annual escalation on caps and deductibles |
| **Disaster scenarios** | 5% annual probability, triggers 2-year recovery period with adjusted growth rates |
| **Risk metrics** | 95th percentile Value-at-Risk (VaR) and ruin probability |

## Limitations (and why they exist)

This is a first-attempt prototype. Known limitations:

| Limitation | Comment |
|------------|--------|
| Claim frequency uses normal approximation | Poisson distribution would have been computationally inefficient |
| Elasticity can become negative | Should be truncated or lognormal |
| Hardcoded parameters | Should use config files or dataclasses |
| Systemic not idiosyncratic risk | Wanted to simulate multiple versions of the same world |

These reflect the learning process, not oversight. Each will be addressed in future iterations.

## Quick Start

### Clone and setup

```bash
git clone https://github.com/jdmwihia/Insurance-Model.git
cd Insurance-Model
python -m venv simEnv
source simEnv/bin/activate  # On Windows: simEnv\Scripts\activate
pip install -r requirements.txt
jupyter notebook insuranceModel.ipynb
```

### Dependencies
- Python 3.10+
- NumPy
- Jupyter (to run the notebook)


## Sample Output

| Year | VaR Capital (KES) | Mean Capital (KES) |
|------|-------------------|--------------------|
| 1 | 36,503,309.92 | 115,591,933.16 |
| 10 | 282,273,845.96 | 957,509,564.70 |
| 20 | 647,712,071.95 | 2,361,862,601.64 |
| 30 | 1,159,515,544.18 | 4,179,766,977.52 |
| 40 | 1,798,894,031.30 | 6,341,298,826.43 |
| 50 | 2,366,968,608.72 | 8,664,213,904.11 |

**Final Probability of Ruin:** 0.2540%

## Next steps
- Replace normal claim frequency with Poisson distribution
- Add gamma distribution for claim severity
- Make all parameters configurable via dataclass
- Add unit tests for each component
- Generate visualizations of capital paths distribution
