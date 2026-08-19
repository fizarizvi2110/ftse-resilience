# Market Shock Resilience: FTSE 100 Sector Analysis Across Brexit and COVID-19

## Research Question
How did FTSE 100 sectors differ in resilience across two fundamentally different crises — the Brexit referendum (policy uncertainty shock) and COVID-19 (global demand shock)?

## Data
- Yahoo Finance daily stock data for major FTSE 100 sector constituents
- UK Government COVID-19 API (cases and deaths)
- EU Referendum results (Greater London Authority)

## Methods
- Cumulative returns and volatility computed within ±30 and ±60 day event windows around each crisis onset
- PCA on multi-dimensional resilience metrics to identify latent structure in sector responses
- K-Means clustering (validated by silhouette score) to group sectors by shock absorption and recovery profiles
- Composite resilience score constructed and ranked across sectors

## Key Findings
Sectors exhibited significantly heterogeneous resilience profiles across the two crises, with defensive sectors showing consistent outperformance and cyclical sectors amplifying downside risk differently under policy vs demand shocks.

## Tools
Python, pandas, numpy, scikit-learn, yfinance, matplotlib, UK Gov API, BeautifulSoup
