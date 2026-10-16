# llm-forecaster

Probabilistic forecasting with LLMs: calibrated probabilities, leakage-controlled backtesting, and Bayesian updating.

> **Status:** work in progress. No results are reported yet; this README will be updated with real numbers as each milestone is completed.

## Goal

Turn vague verbal assessments ("likely", "a real possibility") into explicit, testable probabilities.
Given a question about a future geopolitical or macroeconomic event, the system:

1. Retrieves only the information that was available **as of the question date**.
2. Uses an LLM to produce a probability with a structured rationale (base rate, key evidence).
3. Updates the probability as new evidence arrives.
4. Is scored after the fact against what actually happened.

## How quality is measured

- **Brier score** and **log score** (proper scoring rules).
- **Calibration**: do events forecast at 70% happen about 70% of the time?
- **Baselines**: always-50%, historical base rate, and the community forecast.
- **Leakage control**: an LLM may already "know" the outcome of past events from its training data, which makes naive backtests look better than they are. Every backtest documents how this was handled.

## Roadmap

| Milestone | Description | Status |
|---|---|---|
| 0 | Data loading and exploratory analysis of resolved forecasting questions | In progress |
| 1 | LLM forecaster v0: structured output, logging, automated evals | Planned |
| 2 | Backtesting harness: Brier score, calibration, baselines, leakage control | Planned |
| 3 | Bayesian evidence updating and leading indicators | Planned |
| 4 | Interactive demo and write-up | Planned |

## Project layout

```
src/forecaster/   Python package (the system itself)
tests/            Automated tests (run with: pytest)
notebooks/        Exploratory analysis
data/             Datasets (raw and processed data are not committed)
docs/             Design notes and write-ups
```

## Setup

```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
cp .env.example .env             # then put your API key in .env (never commit it)
pytest
```

## References

- Tetlock & Gardner, *Superforecasting* (2015)
- Gneiting & Raftery, "Strictly Proper Scoring Rules, Prediction, and Estimation", *JASA* (2007)
- Halawi et al., "Approaching Human-Level Forecasting with Language Models" (2024), [arXiv:2402.18563](https://arxiv.org/abs/2402.18563)
- Karger et al., "ForecastBench: A Dynamic Benchmark of AI Forecasting Capabilities" (2024), [arXiv:2409.19839](https://arxiv.org/abs/2409.19839)

## License

MIT
