# Decision-Theoretic SCADA Agent

This repository contains the core implementation and evaluation of a
decision-theoretic agent for SCADA systems, developed as part of a master's
thesis at the Western Norway University of Applied Sciences (HVL).

The agent performs probabilistic inference under uncertainty using explicitly
defined likelihoods and utility-based decision-making.

## Structure

### Core agent (`code/`)

- `stateless_agent.ipynb` — Stateless variant: independent posterior update per observation window.
- `sequential_agent.ipynb` — Sequential variant: posterior propagated within each day.

These notebooks contain the likelihood specification, posterior inference, and
expected-utility decision rule. They assume that required input data
(`merged_15`: aggregated SCADA observations, `ft`: function table) has already
been constructed.

### Experiments (`experiments/`)

- `stateless_injection_experiments.ipynb`
- `sequential_injection_experiments.ipynb`

These notebooks contain controlled evidence injection, baseline vs injected
comparisons, and analysis of posterior and decision behaviour. They are
intentionally kept in a less structured form and are provided for transparency
and reproducibility, not as polished implementations.

### Data (`data/`)

An anonymised function table is included in
`data/function_table/Funksjonstabell.xlsx` (referred to as the "function table"
in the thesis). It contains structural and utility-related metadata used by the
agent, including topology, component relationships, and utility dimensions.

Raw SCADA measurements and event logs are not included due to confidentiality
constraints.

## Running the notebooks

The core agent notebooks (`code/`) contain the model implementation and can be
inspected independently of the experimental setup.

The experiment notebooks (`experiments/`) require preprocessed data and
intermediate structures (`merged_15`, `ft`) to be available. These are
constructed as part of the data preprocessing pipeline described in the thesis.
The experiment notebooks are therefore intended primarily for analysis and
reproduction of results, rather than as standalone scripts.

## Methodology

The model is based on classical decision theory:

- **Hypotheses:** Normal, SensorFault, CommFault
- **Actions:** Ignore, Inspect, Isolate
- **Decision rule:** The agent selects the action that maximises expected utility
  given the posterior belief over hypotheses:
  
  EU(a) = Σ P(h | E) · U(a, h)

Likelihoods and utilities are explicitly defined based on domain knowledge,
without data-driven parameter estimation.

## Author

Jonny Hugøy — Master's thesis, HVL, 2026
