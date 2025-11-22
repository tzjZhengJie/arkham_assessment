# Arkham API Solana Token Rug Pull Risk Assessment

## Description
This Jupyter notebook implements a proof-of-concept risk scoring system for newly created Solana tokens using the Arkham Exchange API. It evaluates **rug pull potential** via two complementary approaches:

1. **Perpetual Contract Metrics (Perp Risk Model):**  
   - **Open Interest (OI):** Proxy for liquidity; low OI indicates thin markets and easy dumps.  
   - **Funding Rate:** Market sentiment; extreme values can indicate retail traps or squeezes.  
   - **Price/Mark Gaps:** Thin order book levels; repeated gaps signal structural fragility.  

2. **Wallet Concentration Risk Model (Holder-Based Risk):**  
   - **Top-10 Wallet Concentration (45% weight):** Measures systemic risk from a few wallets controlling the token supply.  
   - **Unknown Wallets (30% weight):** Highlights opacity and potential hidden manipulation.  
   - **Largest Holder (25% weight):** Focuses on whale risk; a single wallet can trigger cascades.

Both models compute a **0-100 composite risk score** and assign tiers: HIGH RISK, MODERATE RISK, LOW RISK, VERY LOW RISK.  

Designed for the Arkham take-home challenge, the notebook uses **only Arkham API data**, ensuring objectivity and repeatability.

---

## Requirements
- **Python:** 3.8+  
- **Libraries:** `requests`, `json`, `pprint`, `pyspark`  
  ```bash
  pip install requests pyspark
  
| Token Name     | Symbol | Solana Chain Address                         |
| -------------- | ------ | -------------------------------------------- |
| Jupiter        | JUP    | JUPyiwrYJFskUPiHa7hkeR8VUtAeFoSYbKedZNsDvCN  |
| Pudgy Penguins | PENGU  | 2zMMhcVQEXDtdE6vsFS7S7D5oUodfJHE8vd1gnBouauv |
| Fartcoin       | FART   | 9BB6NFEcjBCtnNLFko2FqVQBq8HHM13kCyYcdQbgpump |
| Bonk           | BONK   | DezXAZ8z7PnrnRJjz3wXBoRgixCa6xjnB7YaB1pPB263 |
| Samoyed Coin   | SAMO   | 7xKXtg2CW87d97TXJSDpbD5jBkheTqA83TZRuJosgAsU |
| Wrapped Solana | SOL    | So11111111111111111111111111111111111111112  |
| USD Coin       | USDC   | EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v |
