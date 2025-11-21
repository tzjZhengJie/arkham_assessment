# arkham_assessment
# Arkham API Solana Token Rug Pull Risk Assessment

## Description
This Jupyter notebook implements a proof-of-concept risk scoring system for newly created Solana tokens using the Arkham Exchange API. It evaluates rug pull potential based on perpetual contract metrics (open interest for liquidity, funding rate for market sentiment, and price/mark gap for manipulation). The model computes a 0-100 composite risk score via normalized components and assigns tiers (HIGH RISK, MODERATE RISK, LOW RISK). Designed for the Arkham take-home challenge, it uses only Arkham API data, with a data-driven approach for objectivity and repeatability.

## Requirements
- Python 3.8+
- Libraries: `requests`, `json`, `pprint`, `pyspark` (install via `pip install requests pyspark`)
- Arkham API Key: Set in the notebook as `ARKHAM_API_KEY`.
- No external dependencies beyond the API; all data is fetched at runtime.

## Setup
1. Install dependencies: `pip install requests pyspark`.
2. Obtain an Arkham API key and set it in the notebook.
3. Run the notebook in Jupyter or Google Colab.

## How to Run
1. Execute cells sequentially to fetch Solana assets and contracts via the API.
2. The risk model query (in Spark SQL) computes scores—run the demonstration section for sample tokens (e.g., FARTCOIN, GRASS, POPCAT, MELANIA, PENGU).
3. Output: Table with individual risks, composite score (0-100), and tier.

## Assumptions
- Perp metrics proxy rug risks (low OI = illiquidity/easy dumps; high funding = traps).
- Focus on Solana-native tokens from API fetch.
- Normalization uses batch min/max for dynamic scaling—no fixed thresholds.
- Sample tokens are recent Solana memecoins (2024-2025 launches via Pump.fun/Raydium).

## Limitations
- Limited to Arkham API (no on-chain holder/dev wallet data for comprehensive rug detection).
- Small sample size; expand for statistical robustness.
- Simple average composite—could use ML for optimized weights in production.
- Assumes current batch represents market universe (trade-off for adaptability).

## Author
Zheng Jie - Take-Home Challenge  
Date: November 21, 2025
