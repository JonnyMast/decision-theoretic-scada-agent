# Decision-Theoretic SCADA Agent

This repository contains the core implementation and evaluation of a decision-theoretic agent for SCADA systems, developed as part of a master's thesis.

The agent performs probabilistic reasoning under uncertainty using explicitly defined likelihoods and utility-based decision-making. No machine learning models are used.

---

## Structure

### Core agent (model implementation)

- `code/stateless_agent.ipynb`  
  Stateless variant: independent posterior update per observation window.

- `code/sequential_agent.ipynb`  
  Sequential variant: posterior propagated within each day.

These notebooks contain:
- likelihood specification  
- posterior inference  
- expected-utility decision rule  

They assume that required input data (e.g. `merged_15`, `ft`) has already been constructed.

---

### Experiments (evaluation)

- `experiments/stateless_injection_experiments.ipynb`  
- `experiments/sequential_injection_experiments.ipynb`

These notebooks contain:
- controlled evidence injection
- baseline vs injected comparisons
- analysis of posterior and decision behaviour

These are used to evaluate the agent and are not part of the core implementation.

---

## Running the notebooks

The core agent notebooks (`code/`) contain the model implementation and can be inspected independently of the experimental setup.

The experiment notebooks (`experiments/`) require preprocessed data and intermediate structures (e.g. `merged_15`, `ft`) to be available. These are constructed as part of the data preprocessing pipeline described in the thesis.

As a result, the experiment notebooks are intended primarily for analysis and reproduction of results, rather than as standalone scripts.

---

## Methodology

The model is based on classical decision theory:

- Hypotheses:
  - Normal
  - SensorFault
  - CommFault

- Actions:
  - Ignore
  - Inspect
  - Isolate

- Decision rule:
  The agent selects the action that maximizes expected utility:
  
  EU(a) = Σ P(h | E) · U(a, h)

Likelihoods and utilities are explicitly defined based on domain knowledge.

---

## Notes

- The repository focuses on model transparency and interpretability.
- All inference and decision logic is explicitly specified.
- Injection experiments are used to analyse behaviour under controlled conditions.

---

## Author

Jonny Hugøy  
Master's thesis – HVL