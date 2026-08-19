# Group Project (3 members): Market Shock Resilience: FTSE 100 Sector Analysis Across Brexit and COVID-19

An event-study and unsupervised-learning analysis of how the ten major FTSE 100 sectors weathered two very different shocks — the **2016 Brexit referendum** and the **COVID-19 pandemic** — combining live data collection, volatility analysis, and a composite resilience score built from PCA and K-means.

The central finding: **sector resilience is crisis-dependent, not structural.** No single sector is reliably "safe" across shocks — the sectors that suffer most depend on the *nature* of the crisis. COVID-19 behaved as a systemic shock hitting nearly all sectors at once; Brexit behaved as an institutional shock concentrated in domestically-exposed sectors.

---

## Research question

Which FTSE 100 sectors are most resilient during market crises — and is resilience a fixed property of a sector, or does it change with the type of shock? The analysis compares sector return distributions, downside risk, and recovery around two structurally distinct events: a sudden policy-driven uncertainty shock (Brexit) and a prolonged global real-economy shock (COVID-19).

---

## Data

All data is collected programmatically from public sources at run time — no static files:

| Dataset | Source |
|---------|--------|
| EU Referendum results (regional leave/remain) | Greater London Authority — London Datastore |
| UK COVID-19 cases & deaths (daily) | UKHSA Data Dashboard API |
| FTSE 100 major sectors & weights | ftse100index.com |
| Ticker labels & company names | FTSE 100 Wikipedia page (scraped with BeautifulSoup) |
| Historical stock prices | Yahoo Finance (`yfinance`) |

The pipeline scrapes and joins sector/company/ticker metadata, then pulls historical prices for constituents across the ten major sectors, converting to daily log returns for analysis.

---

## Methods

The analysis moves from context → exploration → modelling:

1. **Crisis background** — Brexit polling distribution by region; UK COVID-19 case/death trajectories, to establish the timing and character of each shock.
2. **Return & cumulative-return analysis** — sector- and company-level cumulative returns over the full sample and in zoomed event windows around each crisis.
3. **Volatility analysis** — rolling volatility and a sector × crisis volatility heatmap.
4. **Event windows** — cumulative-return responses measured over symmetric ±30- and ±60-trading-day windows around each event.
5. **Resilience metrics** — for each sector and window, four crisis-response measures: **Impact** (net cumulative log return), **Volatility** (dispersion of daily log returns), **Worst Day** (most negative single-day return), and **Maximum Drawdown** (deepest peak-to-trough decline).
6. **Unsupervised learning** — **PCA** to visualise sectors in resilience-metric space, **K-means** to cluster sectors by crisis response, and a standardised **composite resilience score** ranking sectors per crisis.

---

## Key findings

**1 — Crisis type drives market behaviour.** Brexit produced modest, sector-specific declines; COVID-19 produced a sharp, near-simultaneous drop across almost all sectors. This frames **COVID-19 as a systemic shock** and **Brexit as an institutional shock** — a distinction that holds consistently across cumulative-return plots, the volatility heatmap, and PCA.

**2 — Resilience is crisis-dependent, not fixed.** The most-vulnerable sectors change with the shock:

| | Brexit (institutional shock) | COVID-19 (systemic shock) |
|---|---|---|
| **Most vulnerable** | Financials, Real Estate | Energy, Industrials |
| **Most resilient** | Healthcare, Telecoms | Healthcare, Technology, Consumer Goods |

**3 — Financials were the most volatile sector across both crises**, reflecting sensitivity to both regulatory uncertainty and systemic stress.

**4 — Healthcare and Consumer Goods are the closest to universally robust** — resilience tied to stable, essential demand. Healthcare is the standout, staying resilient across both shocks; AstraZeneca was the only company with positive cumulative returns across both COVID-19 windows.

**5 — Company-level responses vary within sectors.** Brexit losers clustered in domestically-exposed firms (BT, Lloyds, Barclays, British Land); resilient firms (Sage, AstraZeneca, Diageo, Unilever) often *gained* by ±60 days. Under COVID-19, capital-intensive and mobility-dependent firms (Rolls-Royce, Land Securities, Shell) took the deepest, most persistent losses.

---

## Repository contents

```
.
├── FTSE_Sector_Analysis.ipynb    # full analysis, top to bottom
└── README.md
```

The notebook is self-contained and documented throughout, moving from data collection through EDA to the modelling section, with written findings after each analysis and a synthesising conclusion.

---

## Tech stack

`pandas` · `numpy` · `yfinance` · `BeautifulSoup` · `requests` · `scikit-learn` (PCA, K-means, StandardScaler) · `matplotlib` · `seaborn` · `ipywidgets`
