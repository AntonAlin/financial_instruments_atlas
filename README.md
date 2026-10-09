# Financial Instruments Atlas

One Jupyter notebook that covers **209 financial instruments**: definitions, payoff mechanics, pricing math, risk profiles and portfolio risk tooling. Plain Python (numpy, pandas, scipy, matplotlib), so it runs in Google Colab and Microsoft Fabric without extra setup.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/AntonAlin/financial_instruments_atlas/blob/main/financial_instruments_atlas.ipynb)

## What's inside

| Part | Content |
|---|---|
| Catalog | 209 instruments in 15 asset classes: cash and money market, government and corporate bonds, securitized, equities, funds, futures, options, forwards and swaps, structured products, commodities, real assets, crypto, loans, insurance and Swedish wrappers |
| Risk profile | SRI 1 to 7 (PRIIPs-style), five 1 to 5 risk dimensions (market, credit, liquidity, leverage, complexity), composite score 0 to 100, indicative volatility |
| Calculations | 70 working demos wired to 172 instruments: bond math and BDT callable tree, convertibles, CoCo, CDS, MBS/IO/PO, Vasicek tranches, cost of carry, CTD, Nordic power and EPADs, IRS/CCS/inflation/variance swaps, BSM and Greeks, Black-76, CRR, caps and swaptions, Monte Carlo exotics, autocallables, crypto perps, ISK tax |
| Portfolio risk | Parametric and fat-tailed Monte Carlo VaR/ES, risk contributions, stress scenarios, Kupiec backtest |
| Export | CSV/XLSX, optional Delta table in a Fabric Lakehouse (`WRITE_TO_LAKEHOUSE = True`) |

## Quick use

```python
describe("autocall")                           # full card + live calculation
find("swap")                                   # fuzzy search
filter_catalog(max_sri=3, venue="Exchange")    # screener
```

## Validation

The notebook checks itself where a closed form exists: the BDT tree reprices the zero curve, put-call parity holds to ~1e-14, barrier and spread option Monte Carlo land within 2 standard errors of the analytical prices, and swaption payer minus receiver equals the forward swap.

## Caveats

* Risk scores are expert judgement on a typical instance of each instrument, not a regulatory SRI for a specific product.
* Market data (curves, spots, vols) is illustrative. Replace it before using any number for a decision.
* Swedish tax parameters (ISK) change yearly. Verify on skatteverket.se.

---

# Option Pricing Atlas

Companion notebook: **58 option pricing models and methods** with when they are used, pros and cons, scores (accuracy, speed, flexibility, smile, ease), 40 working pricers and 23 charts.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/AntonAlin/financial_instruments_atlas/blob/main/option_pricing_atlas.ipynb)

| Part | Content |
|---|---|
| Catalog | Models (BSM, Heston, SABR, Dupire, rough Bergomi, Hull-White...), methods (trees, PDE, Monte Carlo, FFT, COS) and approximations (BAW, Bjerksund-Stensland, Kirk, Vanna-Volga) |
| Validation | Every pricer checked against a closed form or an independent method (series vs Fourier, MC vs closed form, local vol MC repricing its own surface) |
| Visuals | Scorecard heatmap, smile gallery, Heston parameter effects, implied vs local vol surfaces, rough vs classical skew, convergence charts, exercise boundary, calibration shoot-out, speed vs accuracy benchmark |
| Helpers | `describe("heston")` for a model card + live demo, `recommend(...)` for a shortlist given product features |

Runtime about 2 minutes, mostly Monte Carlo. scikit-learn is optional (neural surrogate demo only).
