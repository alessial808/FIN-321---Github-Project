**FX Hedging Model – Technical Specification**

**Created by:** Alessia Loperfido  
**Updated by:** Alessia Loperfido  
**Date Created:** 04/21/2026  
**Date Updated:** 04/21/2026  
**Version:** 1.0  
**LLM Used:** OpenAI

**Role:** Financial Analyst / Treasury Analyst  
**Audience:** CFO / Director of Treasury

**Purpose:** Provide a structured, quantitative specification for evaluating FX hedging strategies on a EUR-denominated receivable, enabling reproducible analysis and improved model design.

**1\. Problem Statement**  
The firm expects to receive €20,000,000 in one year, creating transaction exposure to fluctuations in the EUR/USD exchange rate. If the euro depreciates relative to the U.S. dollar, the firm’s USD proceeds will decline, negatively impacting revenue and cash flow. The objective is to protect the USD value of the receivable, evaluate trade-offs between certainty, cost, and upside potential, and provide a quantitative comparison of hedging strategies to support treasury decision-making

**2\. Inputs (Known Variables)**

| Variable | Description | Unit | Value | Source |
| ----- | ----- | ----- | ----- | ----- |
| FC\_AMT | Foreign-currency receivable | EUR | 20,000,000 | Company Data |
| S0\_in | Spot exchange rate | USD/EUR | 1.1605 | Market Data |
| F0\_in | Forward rate (1-year) | USD/EUR | 1.0935 | S0 × (1+R\_USD)/(1+R\_GBP) |
| R\_USD | USD interest rate | Annual % | 5.0% | Macro Benchmark |
| R\_FC | EUR interest rate | Annual % | 3.0% | Macro Benchmark |
| T\_YRS | Time to maturity | Years | 1 | Derived |
| K\_PUT | Put option strike | USD/EUR | 1.16 | Analyst Choice |
| PREM\_PUT | Put premium | USD per EUR | 0.019 | Scenario |
| S\_T | Future spot rate | USD/EUR | Variable | Modeled |

**3\. Assumptions & Constraints**

* Interest rates are assumed, based on macro benchmarks rather than market quotes  
* Exchange rates are quoted as USD per EUR  
* Covered interest rate parity holds, implying a forward ≈ money market hedge  
* No transaction costs, taxes, or bid-ask spreads are included  
* No credit or counterparty risk is considered  
* The option is European-style, exercisable only at maturity  
* Premium is paid upfront in USD and not financed  
* Market liquidity is assumed to be perfect  
* Model is static, using a single terminal exchange rate (S\_T)

**4\. Calculation Flow**  
Forward Hedge

1. Lock in the forward exchange rate (F0\_in)  
2. Multiply the foreign currency amount by the forward rate  
3. Output fixed USD proceeds

   Result: eliminates FX uncertainty entirely

Money Market Hedge

1. Discount the EUR receivable using the EUR interest rate  
2. Borrow equivalent present value in EUR  
3. Convert borrowed EUR to USD at the spot rate  
4. Invest USD at the USD interest rate until maturity  
5. Compare the resulting USD value to the forward hedge  
   	Expected outcome: matches forward hedge due to parity

Option Hedge

1. Calculate total premium cost:  
2. premium × FC amount  
3. At maturity:  
   1. If (S\_T \< K\_PUT): exercise put  
   2. If (S\_T ≥ K\_PUT): sell at market rate  
4. Subtract the premium from the final USD proceeds

		Result: downside protection with retained upside

**5\. Outputs**  
 

| Output | Description | Format | Purpose |
| ----- | ----- | ----- | ----- |
| USD\_forward | Forward hedge proceeds | Numeric | Baseline certainty |
| USD\_mm | Money market proceeds | Numeric | Validation check |
| USD\_option | Option hedge proceeds | Table | Sensitivity analysis |
| Sensitivity\_Table | USD vs. S\_T across strategies | Table | Risk comparison |
| Chart\_Comparison | Strategy payoff curves | Line chart | Visual analysis |
| Summary\_Output | Key results | Dashboard-style | Decision support |

**6\. Sensitivity Plan**  
The sensitivity analysis evaluates the firm’s exposure to exchange rate uncertainty by varying the terminal spot rate S\_T​ over a ±5% range around the current spot rate in 1% increments. For each scenario, USD proceeds are calculated across all hedging strategies, enabling direct comparison of outcomes under different market conditions. This approach provides a structured range estimate of transaction exposure and highlights how each strategy responds to currency movements, with forward and money market hedges producing fixed outcomes and the option hedge exhibiting asymmetric payoffs. Sensitivity analysis is a standard tool in FX risk management used to assess how financial results change under alternative exchange rate scenarios

**7\. Limitations & Next Steps**  
The model is subject to several limitations, including the exclusion of exchange rate volatility, dynamic hedging strategies, transaction costs, and credit risk considerations. It also relies on a static, single-period framework and does not incorporate stochastic modeling or advanced option pricing techniques, which may affect the precision of results. Despite these constraints, the model provides a clear and practical foundation for evaluating hedging strategies. The next step is to translate this specification into a structured AI-driven framework that enhances the model’s analytical depth, incorporates additional scenario analysis, and supports the development of a data-driven hedge recommendation aligned with the firm’s risk management objectives.