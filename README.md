# Stock Analysis

This repository contains two notebook workflows for working with stock-market data:

1. **`Dataanalysis.ipynb`** — use an LLM-powered pandas agent to analyze stock data conversationally.
2. **`stockanalysis.ipynb`** — train a deep-learning/reinforcement-learning model for future stock movement and trading-action prediction experiments.

The project is designed for students, AI/ML learners, and developers who want to upload a stock CSV file, understand the data, and then experiment with future stock prediction.

> **Disclaimer:** This project is for education and research only. Stock prediction is uncertain, and this repository does not provide financial advice or a production trading system.

## Repository Structure

```text
.
├── ADANIPORTS.NS.csv       # Sample stock dataset
├── Dataanalysis.ipynb      # LLM-based stock data analysis notebook
├── stockanalysis.ipynb     # Future stock prediction / trading model notebook
├── requirements.txt        # Python dependencies
└── README.md               # Project guide
```

## Notebook Purpose

### 1. `Dataanalysis.ipynb` — LLM Stock Data Analysis

Use this notebook first after you have stock data. It loads your CSV into a pandas dataframe and uses an LLM dataframe agent to answer questions about the dataset.

You can ask questions like:

- How many rows and columns are in the stock dataset?
- Are there missing values?
- What are the available columns?
- What is the date range of the data?
- What is the average closing price?
- Which day had the highest trading volume?
- Plot closing price over time.
- Summarize the trend in the stock data.

This notebook is useful for quickly understanding the dataset before building a prediction model.

### 2. `stockanalysis.ipynb` — Future Stock Prediction

Use this notebook after you understand the data. It preprocesses historical stock prices and uses a deep-learning workflow with LSTM layers and reinforcement-learning-style trading actions.

The notebook focuses on:

- Loading historical stock data.
- Scaling features such as `Open`, `High`, `Low`, `Close`, and `Volume`.
- Creating windowed time-series input from previous days.
- Training a model on historical movement patterns.
- Simulating future-oriented buy, sell, and hold decisions.
- Visualizing rewards, predictions, and trading behavior.

## Dataset Format

You need a stock CSV file before using the notebooks. The included sample file is:

```text
ADANIPORTS.NS.csv
```

Recommended CSV format:

```csv
Date,Open,High,Low,Close,Adj Close,Volume
2007-11-27,154.000000,207.000000,154.000000,191.800003,177.675140,27262365
```

Required columns for the prediction notebook:

| Column | Purpose |
| --- | --- |
| `Date` | Sorts the stock data in time order |
| `Open` | Opening stock price |
| `High` | Highest price for the day |
| `Low` | Lowest price for the day |
| `Close` | Closing stock price |
| `Volume` | Number of shares traded |

`Adj Close` is useful but not mandatory for the current prediction workflow.

## Step-by-Step Usage After You Have Stock Data

### Step 1: Clone the Repository

```bash
git clone <repository-url>
cd stockanalysis
```

### Step 2: Create a Virtual Environment

```bash
python -m venv .venv
source .venv/bin/activate
```

For Windows PowerShell:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

### Step 3: Install Requirements

```bash
pip install -r requirements.txt
```

### Step 4: Add Your Stock Data

Place your CSV file in the project folder, or upload it directly when running the notebook in Google Colab.

Example local project folder:

```text
stockanalysis/
├── ADANIPORTS.NS.csv
├── your_stock_data.csv
├── Dataanalysis.ipynb
└── stockanalysis.ipynb
```

### Step 5: Analyze the Data with `Dataanalysis.ipynb`

Open Jupyter Notebook:

```bash
jupyter notebook
```

Then open:

```text
Dataanalysis.ipynb
```

Use this notebook to inspect your stock CSV before prediction. Update the CSV path in the notebook if needed:

```python
df = pd.read_csv("your_stock_data.csv")
```

If you are using the LLM analysis workflow, set your Google API key as an environment variable instead of hardcoding it in the notebook:

```bash
export GOOGLE_API_KEY="your_api_key_here"
```

For Windows PowerShell:

```powershell
$env:GOOGLE_API_KEY="your_api_key_here"
```

After loading the dataframe, ask stock-analysis questions through the dataframe agent.

### Step 6: Run Future Prediction with `stockanalysis.ipynb`

After the dataset is clean and understood, open:

```text
stockanalysis.ipynb
```

Run the notebook cells in order. When prompted, upload the same stock CSV file or use the sample `ADANIPORTS.NS.csv` file.

The notebook will:

1. Load the stock data.
2. Convert `Date` into datetime format.
3. Sort records by date.
4. Select numerical stock features.
5. Scale the data.
6. Train the model.
7. Simulate buy, sell, and hold actions.
8. Show training and trading results.

### Step 7: Review Results Carefully

When training completes, review:

- Reward per episode.
- Final portfolio value.
- Buy and sell signals.
- Price charts.
- Model behavior over time.

Do not assume the model is ready for real trading. Validate on out-of-sample data and compare against simple baselines like buy-and-hold.

## Running in Google Colab

1. Open either notebook in Google Colab.
2. Upload your stock CSV file.
3. Install missing packages inside Colab if required:

```python
!pip install -r requirements.txt
```

4. Run `Dataanalysis.ipynb` first to understand the data.
5. Run `stockanalysis.ipynb` next for future prediction experiments.

## Recommended Workflow

```text
Get stock CSV
      ↓
Run Dataanalysis.ipynb
      ↓
Check columns, missing values, date range, trends
      ↓
Clean or replace the dataset if required
      ↓
Run stockanalysis.ipynb
      ↓
Train and evaluate future prediction / trading behavior
```

## Troubleshooting

### `FileNotFoundError`

Make sure your CSV file path is correct. If the file is in the same folder as the notebook, use:

```python
pd.read_csv("your_stock_data.csv")
```

### Missing required columns

The prediction notebook expects columns like `Date`, `Open`, `High`, `Low`, `Close`, and `Volume`. Rename your CSV columns or adjust the notebook feature-selection code.

### TensorFlow installation issues

Use Python 3.10 or 3.11 if TensorFlow does not install correctly in your environment. Google Colab is the easiest option for beginners.

### API key issues in LLM analysis

Make sure `GOOGLE_API_KEY` is set in your environment before running the LLM dataframe agent. Do not hardcode real API keys in notebooks.

## Future Improvements

- Convert notebook code into reusable Python modules.
- Add a clean data-validation script.
- Add prediction metrics such as RMSE, MAE, and directional accuracy.
- Add baseline models like moving average, ARIMA, Prophet, and simple LSTM regression.
- Add train/test split by date to reduce data leakage.
- Add transaction costs, slippage, and risk management.
- Add charts for predicted versus actual closing price.

## License

No license file is currently included. Add a license before public distribution or reuse.
