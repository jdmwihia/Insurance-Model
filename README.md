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
Python 3.10+
NumPy
Jupyter (to run the notebook)


## Sample output
Year:  1 | VaR Capital:   36,503,309.92 | Mean Capital:  115,591,933.16 
Year:  2 | VaR Capital:   67,747,771.91 | Mean Capital:  187,129,930.45 
...
Year: 50 | VaR Capital: 2,366,968,608.72 | Mean Capital: 8,664,213,904.11 

Final Probability of Ruin: 0.2540%

## Next steps
Replace normal claim frequency with Poisson distribution
Add gamma distribution for claim severity
Make all parameters configurable via dataclass
Add unit tests for each component
Generate visualizations of capital paths distribution