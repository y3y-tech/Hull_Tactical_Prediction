# Hull_Tactical_Prediction
Kaggle Competition for Hull Tactical Prediction


# Getting Started

```bash
python -m .venv

source .venv/bin/activate 

pip install -r requirements.txt

```

## Files

### train.csv

Historic market data. The coverage stretches back decades; expect to see extensive missing values early on.

#### Columns

- **`date_id`** - An identifier for a single trading day
- **`M*`** - Market Dynamics/Technical features
- **`E*`** - Macro Economic features
- **`I*`** - Interest Rate features
- **`P*`** - Price/Valuation features
- **`V*`** - Volatility features
- **`S*`** - Sentiment features
- **`MOM*`** - Momentum features
- **`D*`** - Dummy/Binary features
- **`forward_returns`** - The returns from buying the S&P 500 and selling it a day later (Train set only)
- **`risk_free_rate`** - The federal funds rate (Train set only)
- **`market_forward_excess_returns`** - Forward returns relative to expectations. Computed by subtracting the rolling five-year mean forward returns and winsorizing the result using a median absolute deviation (MAD) with a criterion of 4 (Train set only)

---

### test.csv

A mock test set representing the structure of the unseen test set. The test set used for the public leaderboard is a copy of the last 180 date IDs in the train set. **As a result, the public leaderboard scores are not meaningful.** The unseen copy of this file served by the evaluation API may be updated during the model training phase.

#### Columns

- **`date_id`** - An identifier for a single trading day
- **`[feature_name]`** - The feature columns are the same as in `train.csv`
- **`is_scored`** - Whether this row is included in the evaluation metric calculation. During the model training phase this will be true for the first 180 rows only (Test set only)
- **`lagged_forward_returns`** - The returns from buying the S&P 500 and selling it a day later, provided with a lag of one day (Test set only)
- **`lagged_risk_free_rate`** - The federal funds rate, provided with a lag of one day (Test set only)
- **`lagged_market_forward_excess_returns`** - Forward returns relative to expectations. Computed by subtracting the rolling five-year mean forward returns and winsorizing the result using a median absolute deviation (MAD) with a criterion of 4, provided with a lag of one day (Test set only)

---

### kaggle_evaluation/

Files used by the evaluation API. See the demo submission for an illustration of how to use the API.

---

## Important Notes

### Data Characteristics

- **Missing Values**: Expect extensive missing values in early historical data
- **Lagged Features**: Test set provides features with a one-day lag to simulate real-world prediction scenarios
- **Target Variable**: `market_forward_excess_returns` (train) vs `lagged_market_forward_excess_returns` (test)

### Feature Categories

| Prefix | Category | Description |
|--------|----------|-------------|
| `M*` | Market Dynamics | Technical market indicators |
| `E*` | Macro Economic | Economic indicators |
| `I*` | Interest Rate | Interest rate and yield data |
| `P*` | Price/Valuation | Price and valuation metrics |
| `V*` | Volatility | Volatility measures |
| `S*` | Sentiment | Market sentiment indicators |
| `MOM*` | Momentum | Momentum indicators |
| `D*` | Dummy/Binary | Binary indicator features |
