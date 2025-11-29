# Copilot / AI Agent Instructions for Hull_Tactical_Prediction

This file contains concise, actionable guidance for AI coding agents working in this repository.

Keep guidance short and specific to this project. Reference files and examples by path.

1. Project purpose
- This repo holds code and data artifacts for the Kaggle "Hull Tactical Prediction" competition. See `README.md` for dataset column descriptions.

2. Environment & common commands
- Create a Python venv at repo root: `python -m venv .venv` and activate: `source .venv/bin/activate`.
- Install dependencies: `pip install -r requirements.txt`.
- Developers sometimes use Conda; prefer the repository venv for reproducible runs unless the author requests otherwise.

3. Important files and directories
- `train.csv`, `test.csv` — primary datasets. Do not change column names or the structure of these CSVs.
- `kaggle_evaluation/` — evaluation helpers used by the scoring API and demo submissions. Check it before changing evaluation code.
- `main.ipynb` and `playground.ipynb` — exploratory and demo notebooks. Use them to reproduce experiments; prefer adding small runnable scripts for productionable changes.
- `requirements.txt` — canonical dependencies for running experiments.

4. Data and modeling conventions (project-specific)
- Target variable in training is `market_forward_excess_returns`. The test set exposes a lagged version `lagged_market_forward_excess_returns`.
- Feature prefixes are meaningful: `M*` (market), `E*` (economic), `I*` (interest rates), `P*` (price), `V*` (volatility), `S*` (sentiment), `MOM*` (momentum), `D*` (dummy). Use these prefixes when writing feature grouping, selection, or visualization code.
- Early historical rows have extensive missing values — preprocessing code should be robust to long runs of NaNs and avoid imputations that leak future information.
- The README documents winsorization used for `market_forward_excess_returns` (rolling 5-year mean + MAD with criterion 4). If reproducing target transformations, follow that method and reference `README.md` in the commit message.

5. Changes & PR guidance for AI agents
- When modifying modeling code or data transforms, include a short reproducible snippet (script or notebook cell) demonstrating the change on a small slice of `train.csv`.
- Do not modify `kaggle_evaluation/` without explicit tests showing identical or improved metric behavior. Add a demo script showing evaluation output differences.
- Keep changes minimal and localized. Note dataset invariants in PR descriptions (e.g., "keeps original column names", "no lookahead introduced").

6. Examples of common tasks (use these templates)
- Run quick experiment: `source .venv/bin/activate && python -c "import pandas as pd; print(pd.read_csv('train.csv', nrows=5))"`
- Compute simple group by by prefix: `df[[c for c in df.columns if c.startswith('M')]].describe()`

7. What not to do
- Don't rename dataset columns, change CSV layouts, or remove columns used by the evaluation API.
- Avoid heavy refactors across many files in a single patch; prefer incremental, tested changes.

8. Where to look for more context
- `README.md` — dataset descriptions and preprocessing notes (canonical source).
- Notebooks (`main.ipynb`, `playground.ipynb`) — examples of data loading and experimentation.

If anything above is unclear or you want the guidance expanded (e.g., example unit tests or a demo script), ask and I will iterate.
