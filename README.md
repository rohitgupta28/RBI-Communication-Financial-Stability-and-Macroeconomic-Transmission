# 📊 RBI Communication & Macroeconomic Transmission
### Evidence from Sentiment Analysis of MPC Minutes (2010–2025)

![Python](https://img.shields.io/badge/Python-3.11-blue?logo=python)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter)
![License](https://img.shields.io/badge/License-MIT-green)
![Status](https://img.shields.io/badge/Status-In%20Progress-yellow)
![Documents](https://img.shields.io/badge/RBI%20Documents-62%20PDFs-red)
![Period](https://img.shields.io/badge/Period-2010--2025-blue)

---

## 📌 Overview

This project quantifies whether the **language and tone** of Reserve Bank of India (RBI)
Monetary Policy Committee (MPC) minutes can predict real macroeconomic outcomes in India.

> *"The words the RBI chooses matter as much as the decisions it makes."*

Using the **Loughran-McDonald Finance Dictionary** — the gold standard for financial text
analysis — sentiment scores are extracted from **62 RBI official documents** (31 MPC minutes
\+ 31 Financial Stability Reports) spanning **15 years from 2010 to 2025**.

Each MPC period is classified as **Hawkish 🦅**, **Dovish 🕊️**, or **Neutral ⚖️** and tested
against key economic variables using OLS regression, Granger causality, and VAR models.

---

## 🎯 Research Questions

1. Does RBI MPC tone **correlate** with CPI inflation, GDP growth, Nifty 50, and credit growth?
2. Does MPC sentiment **Granger-cause** changes in financial stability?
3. Can the Hawkish/Dovish stance derived from text **predict** future policy decisions?
4. How did tone shift around **COVID-19, demonetisation, and the 2022 rate hike cycle**?

---

## 🗂️ Project Structure

```
RBI_Sentiment_Project/
│
├── 📁 data/
│   ├── raw/
│   │   ├── LM_MasterDictionary.csv          # Loughran-McDonald Finance Dictionary
│   │   └── positive and negative data.xlsx  # Original custom word list
│   └── processed/
│       ├── mpc_sentiment.csv                # ✅ MPC sentiment scores (31 docs)
│       ├── fsr_sentiment.csv                # ✅ FSR sentiment scores (31 docs)
│       ├── combined_sentiment_lm.csv        # ✅ MPC + FSR combined
│       ├── policy_indices.csv               # FSSI + MPSI + Hawkish/Dovish
│       └── master_dataset.csv              # All sentiment + macro variables
│
├── 📓 notebooks/
│   ├── 01_setup_and_wordlist.ipynb          # LM Dictionary setup
│   ├── 02_sentiment_extraction.ipynb        # PDF scraping + scoring
│   ├── 03_stability_index.ipynb             # FSSI + MPSI construction
│   ├── 04_macro_data_collection.ipynb       # Economic indicators
│   ├── 05_econometric_analysis.ipynb        # Statistical tests
│   └── 06_visualizations.ipynb             # 7 publication-ready figures
│
├── 📊 output/
│   ├── figures/                             # fig1.png – fig7.png (300 DPI)
│   └── tables/                              # table1.csv – table7.csv
│
├── requirements.txt
└── README.md
```

---

## 🔬 Methodology

### Sentiment Index Formula
```
Sentiment Index  =  (Positive Words − Negative Words) / Total Words
```
- **Positive value** → Accommodative / Dovish language 🕊️
- **Negative value** → Restrictive / Hawkish language 🦅

### Financial Stability Sentiment Index (FSSI)
```
FSSI  =  100 × ( −FSR_Sentiment − min ) / ( max − min )
```
Higher score = more stable financial system tone in FSR reports.

### Hawkish / Dovish Classification
```
Dovish   →  Sentiment > mean + 0.3 × std
Hawkish  →  Sentiment < mean − 0.3 × std
Neutral  →  everything in between
```

---

## 📈 Sample Output

### MPC Sentiment Scores (Selected Periods)

| Period | Positive | Negative | Total Words | Sentiment Index | Stance |
|--------|----------|----------|-------------|-----------------|--------|
| Jul-10 | 40 | 33 | 4,964 | +0.001410 | 🕊️ Dovish |
| Jul-12 | 15 | 63 | 4,375 | −0.010971 | 🦅 Hawkish |
| Dec-16 | 18 | 50 | 4,957 | −0.006456 | 🦅 Hawkish |
| Jun-19 | 45 | 123 | 10,202 | −0.007646 | 🦅 Hawkish |
| Jun-20 | 48 | 130 | 8,907 | −0.009206 | 🦅 Hawkish |
| Dec-20 | 118 | 81 | 8,767 | +0.004220 | 🕊️ Dovish |
| Jun-21 | 69 | 56 | 7,470 | +0.001740 | 🕊️ Dovish |
| Jun-22 | 48 | 63 | 7,958 | −0.001885 | ⚖️ Neutral |
| Jun-24 | 50 | 36 | 7,091 | +0.001974 | 🕊️ Dovish |
| Jun-25 | 44 | 35 | 6,157 | +0.001462 | 🕊️ Dovish |

> **Dec-20** has the most positive MPC tone (+0.00422) — peak COVID accommodation period.
> **Jun-20** has the most negative MPC tone (−0.00921) — COVID emergency cut language.
> **Jul-12** is the most hawkish period (−0.01097) — peak inflation stress 2012.

---

### MPC vs FSR Sentiment Comparison

| Period | MPC Sentiment | FSR Sentiment | Interpretation |
|--------|--------------|---------------|----------------|
| Jul-10 | +0.001410 | −0.003694 | Policy confident, system cautious |
| Jul-12 | −0.010971 | −0.008530 | Both hawkish — peak inflation stress |
| Dec-20 | +0.004220 | −0.005678 | Policy easing, system still stressed |
| Jun-22 | −0.001885 | −0.005904 | Rate hike begins, stability weak |
| Jun-24 | +0.001974 | −0.003842 | Policy improving, system stabilising |
| Jun-25 | +0.001462 | −0.004256 | Gradual normalisation underway |

---

### Key Event Study Snapshot

| Event | Date | MPC Tone | Repo Rate | Signal |
|-------|------|----------|-----------|--------|
| Post-GFC Recovery | Jul-10 | 🕊️ +0.00141 | 5.75% | Accommodative |
| Peak Inflation | Jul-12 | 🦅 −0.01097 | 8.00% | Most hawkish in sample |
| Demonetisation | Dec-16 | 🦅 −0.00646 | 6.25% | Uncertainty spike |
| Pre-COVID Cuts | Jun-19 | 🦅 −0.00765 | 5.75% | Cautious easing |
| COVID Emergency | Jun-20 | 🦅 −0.00921 | 4.00% | Crisis language |
| COVID Recovery | Dec-20 | 🕊️ +0.00422 | 4.00% | Most dovish in sample |
| Rate Hike Cycle | Jun-22 | ⚖️ −0.00189 | 4.90% | Tightening begins |
| Rate Cut Restart | Dec-24 | 🦅 −0.00442 | 6.25% | Cautious pivot |

---

### Sentiment Timeline — ASCII Chart

```
MPC Sentiment Index (2010 → 2025)

+0.005 |                         ▓▓
+0.004 |                         ▓▓
+0.003 |                         ▓▓
+0.002 |▓▓                       ▓▓  ▓▓  ▓▓            ▓▓  ▓▓
+0.001 |▓▓  ▓▓                   ▓▓  ▓▓  ▓▓  ▓▓  ▓▓    ▓▓  ▓▓
 0.000 |────────────────────────────────────────────────────────→ time
-0.001 |        ▓▓                              ▓▓
-0.002 |        ▓▓  ▓▓      ▓▓  ▓▓
-0.003 |            ▓▓
-0.004 |                ▓▓              ▓▓              ▓▓
-0.005 |                ▓▓              ▓▓
-0.006 |        ▓▓      ▓▓      ▓▓
-0.007 |        ▓▓              ▓▓  ▓▓
-0.008 |
-0.009 |                                    ▓▓
-0.010 |
-0.011 |    ▓▓▓▓
       └────────────────────────────────────────────────────────
        10  11  12  13  14  15  16  17  18  19  20  21  22  25
                     ↑               ↑           ↑
                  Inflation      Demone-       COVID
                   Peak          tisation      Crisis
```

---

## 🧪 Econometric Tests

| Test | Purpose | Library |
|------|---------|---------|
| **ADF Unit Root** | Check stationarity before regression | `statsmodels` |
| **Pearson Correlation** | Linear association: sentiment ↔ macro | `pandas` |
| **OLS Regression** | Impact of sentiment on each macro variable | `statsmodels` |
| **Granger Causality** | Does past sentiment predict future macro? | `statsmodels` |
| **VAR Model** | Bidirectional sentiment-macro dynamics | `statsmodels` |
| **Impulse Response** | Effect of a sentiment shock over 8 periods | `statsmodels` |
| **Event Study** | Sentiment around 7 structural events | custom |

---

## 📊 Output Figures

| Figure | Description |
|--------|-------------|
| `fig1_mpc_sentiment_timeline.png` | MPC Sentiment 2010–2025 with Repo Rate overlay |
| `fig2_fssi_timeline.png` | FSSI and FSR sentiment with event markers |
| `fig3_correlation_heatmap.png` | Full 10×10 correlation matrix heatmap |
| `fig4_scatter_plots.png` | MPC Sentiment vs CPI, GDP, Nifty 50, Credit |
| `fig5_event_study.png` | Sentiment around 7 key policy events |
| `fig6_stance_distribution.png` | Hawkish/Dovish/Neutral pie + timeline |
| `fig7_impulse_response.png` | VAR Impulse Response to MPC sentiment shock |

> All figures saved at **300 DPI** — meets journal submission standards.

---

## 🚀 How to Run

### 1. Clone the repository
```bash
git clone https://github.com/yourusername/RBI_Sentiment_Project.git
cd RBI_Sentiment_Project
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

### 3. Add your existing data (if you have it)
```
Copy mpc_sentiment.csv and fsr_sentiment.csv into data/processed/
Notebook 02 will auto-detect and use them if direct download is blocked.
```

### 4. Run notebooks in order
```
01_setup_and_wordlist.ipynb       ←  1–2 min
02_sentiment_extraction.ipynb     ←  10–20 min (first run only)
03_stability_index.ipynb          ←  < 1 min
04_macro_data_collection.ipynb    ←  2–5 min
05_econometric_analysis.ipynb     ←  2–5 min
06_visualizations.ipynb           ←  1–2 min
```

---

## 📦 Requirements

```
Python >= 3.10
pandas · numpy · matplotlib · seaborn · scipy
statsmodels · yfinance · pysentiment2
PyPDF2 · pypdf · pdfplumber · requests · openpyxl
```

Install all at once:
```bash
pip install -r requirements.txt
```

---

## 📚 Key References

- Loughran, T. & McDonald, B. (2011). *When is a liability not a liability?* Journal of Finance.
- Tetlock, P. C. (2007). *Giving content to investor sentiment.* Journal of Finance.
- Blinder et al. (2008). *Central bank communication and monetary policy.* Journal of Economic Literature.
- Reserve Bank of India (2010–2025). *MPC Minutes & FSR Reports.* rbidocs.rbi.org.in

---


## 👤 Author

**Rohit Gupta**

---

## 📄 License

This project is licensed under the MIT License.

---
