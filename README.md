# Financial Insights: Stock & Revenue Analysis


This project performs **data analytics and visualization** on historical stock prices and quarterly revenue data for companies such as **Tesla (TSLA)** and **GameStop (GME)**. The project combines **financial data extraction, data cleaning, and visualization** to provide insights into stock price trends and revenue performance.

---

## Table of Contents

- [Project Overview](#project-overview)  
- [Technologies Used](#technologies-used)  
- [Data Sources](#data-sources)  
- [Project Workflow](#project-workflow)  
- [Visualizations](#visualizations)  
- [Installation](#installation)  
- [Usage](#usage)  
- [Future Enhancements](#future-enhancements)  
- [License](#license)  

---

## Project Overview

The main goal of this project is to:

1. Extract historical stock price data using **Yahoo Finance API (`yfinance`)**.  
2. Scrape quarterly revenue data from **Macrotrends**.  
3. Clean and process financial data.  
4. Visualize the relationship between stock price trends and company revenue over time.  

By analyzing both stock prices and revenue, the project helps understand how a company’s financial performance aligns with its market valuation.

---

## Technologies Used

- Python 3.x  
- Libraries: 
  - `yfinance` – for fetching stock price data  
  - `pandas` – for data manipulation  
  - `requests` – for web scraping  
  - `matplotlib` – for data visualization  
- Tools:
  - Jupyter Notebook / IDE (for running Python scripts)

---

## Data Sources

- **Stock Price Data:** [Yahoo Finance](https://finance.yahoo.com/) via `yfinance`  
- **Revenue Data:** [Macrotrends](https://www.macrotrends.net/)  

**Companies Analyzed:**  
- Tesla (TSLA)  
- GameStop (GME)  

---

## Project Workflow

1. **Fetch Stock Data**
   ```python
   import yfinance as yf
   tesla = yf.Ticker("TSLA")
   tesla_data = tesla.history(period="max")
   tesla_data.reset_index(inplace=True)
Scrape Revenue Data

python
Copy code
import pandas as pd
import requests
from io import StringIO

url = "https://www.macrotrends.net/stocks/charts/TSLA/tesla/revenue"
headers = {"User-Agent": "Mozilla/5.0"}
html = requests.get(url, headers=headers).text
tables = pd.read_html(StringIO(html))
Clean and Prepare Data

python
Copy code
tesla_revenue = tables[0].iloc[:, :2]
tesla_revenue.columns = ["Date", "Revenue"]
tesla_revenue = tesla_revenue[tesla_revenue["Revenue"].str.contains("\$")]
tesla_revenue["Revenue"] = tesla_revenue["Revenue"].replace({'\$': '', ',': ''}, regex=True).astype(float)
Visualize Stock vs Revenue

python
Copy code
import matplotlib.pyplot as plt

def make_graph(stock_data, revenue_data, stock_name):
    fig, ax1 = plt.subplots(figsize=(14, 6))
    ax1.plot(stock_data['Date'], stock_data['Close'], label='Stock Price')
    ax1.set_ylabel('Stock Price', color='blue')
    ax1.set_title(f"{stock_name} Stock Price")
    ax2 = ax1.twinx()
    ax2.plot(revenue_data['Date'], revenue_data['Revenue'], label='Revenue', color='green')
    ax2.set_ylabel('Revenue (in USD)', color='green')
    plt.show()
Visualizations
Tesla (TSLA): Displays stock price and quarterly revenue trends over time.

GameStop (GME): Displays stock price and quarterly revenue trends over time.

The dual-axis plots allow comparison between stock price and revenue for each company.

Installation
Clone the repository:

bash
Copy code
git clone https://github.com/yourusername/stock-revenue-analytics.git
cd stock-revenue-analytics
Install dependencies:

bash
Copy code
pip install yfinance pandas matplotlib requests dash plotly
(Optional) Restart your Python kernel if using Jupyter Notebook.

Usage
Run the Python script or notebook to fetch stock and revenue data.

Clean and process data as shown in the workflow.

Generate visualizations using make_graph() function for each company.

Example:

python
Copy code
make_graph(tesla_data, tesla_revenue, "Tesla")
make_graph(gme_data, gme_revenue, "GameStop")
Future Enhancements
Add interactive visualizations using Dash or Plotly.

Extend analysis to multiple companies simultaneously.

Integrate financial ratios and other performance metrics.

Perform predictive analytics on stock price based on historical revenue trends.

License
This project is licensed under the MIT License.

yaml
