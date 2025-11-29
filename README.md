# Hull_Tactical_Prediction
Kaggle Competition for Hull Tactical Prediction


# Getting Started

```bash
python -m .venv

source .venv/bin/activate 

pip install -r requirements.txt

```

## Data

``train.csv`` contains training set of 98 variables. The variable of particular interest is ``forward_returns``, which is renamed to ``target``. We are using the other 96 variables (excluding ``risk_free_rate`` and ``market_forward_excess_returns`` to predict ``target``)

``test.csv`` contains testing set of 10 rows, and 99 features. 