# **FX Hedging Analysis & Recommendation**

**Created by:** Alessia Loperfido  
**Role:** Financial Analyst / Treasury Analyst  
**Audience:** CFO / Director of Treasury

## **A. Exposure Summary**

The firm expects to receive **€20,000,000 in one year**, creating transaction exposure to fluctuations in the EUR/USD exchange rate. If the euro depreciates, the USD value of the receivable declines, directly impacting revenue and cash flow. This exposure is significant given the size of the receivable and the sensitivity of USD proceeds to relatively small FX movements.

Foreign exchange hedging is used to mitigate this risk by locking in exchange rates or using financial instruments that offset adverse currency movements. The objective is to protect the firm’s USD cash flows while evaluating trade-offs between certainty, flexibility, and cost.

## **B. Summary of Hedge Outcomes**

### **Forward Hedge**

### The forward hedge locks in an exchange rate of 1.0935, resulting in guaranteed USD proceeds of approximately $21.87 million.

* Strength: Complete elimination of FX risk  
* Weakness: No participation in favorable EUR appreciation

Forward contracts provide certainty by fixing the exchange rate for a future transaction, ensuring predictable cash flows.

### **Money Market Hedge**

The money market hedge replicates a forward contract by borrowing EUR, converting at the spot rate, and investing USD.

* **Strength:** Produces nearly identical USD proceeds to the forward hedge  
* **Weakness:** Requires balance sheet usage and operational complexity

This outcome confirms covered interest rate parity, where synthetic hedges align with forward pricing.

### **Put Option Hedge**

The EUR put option (strike \= 1.16, premium \= $0.019) provides a minimum exchange rate floor while allowing upside participation.

* Strength: Protects against EUR depreciation  
* Weakness: Premium cost (\~$380,000) reduces net proceeds

Options differ from forwards because they provide the right, not obligation, to transact at a fixed rate, allowing firms to benefit from favorable movements.

### **No Hedge (Baseline)**

If unhedged, USD proceeds vary directly with (S\_T):

* EUR depreciation → significant loss in USD value  
* EUR appreciation → potential upside

This highlights the firm’s exposure to FX volatility.

## **C. Sensitivity Interpretation**

The sensitivity analysis evaluates outcomes across a ±5% range of exchange rates.

### **EUR Depreciation Scenario**

* Forward/MM: Stable at \~$21.87M  
* Option: Protected by strike price (floor)  
* No Hedge: Declining USD proceeds

Forward and MM provide full protection; the option hedge limits downside while retaining flexibility.

### **EUR Appreciation Scenario**

* Forward/MM: Fixed, no additional benefit  
* Option: Gains from higher spot rate (minus premium)  
* No Hedge: Maximum upside

The option hedge captures upside potential, unlike the forward hedge, which locks in opportunity cost.

### **Key Trade-Off**

* Forward/MM: Certainty and predictability  
* Option: Flexibility and asymmetric payoff  
* No Hedge: Maximum risk exposure

This aligns with corporate treasury practice, where forwards provide certainty, and options provide flexibility at a cost.

## **D. Strategic Recommendation**

**Recommended Strategy: Forward Hedge**

The forward hedge is the most appropriate strategy, given the firm’s objective of protecting USD cash flows and minimizing risk.

### **Supporting Rationale:**

* Guarantees \~$21.87M in proceeds  
* Eliminates downside risk entirely  
* No upfront cost  
* Aligns with predictable receivable exposure

While the option hedge provides upside potential, the premium cost reduces expected value and introduces uncertainty.

## **E. Executive Justification**

From a CFO perspective, the forward hedge is preferred due to:

* Cash Flow Certainty: Enables accurate budgeting and forecasting  
* Risk Elimination: Removes exposure to unfavorable FX movements  
* Cost Efficiency: No premium or upfront cost  
* Simplicity: Easy to implement and monitor

Although options provide flexibility, they function as “insurance” and may appear costly if not exercised, making them harder to justify in a cost-conscious treasury environment

Overall, the forward hedge aligns with the firm’s likely priority, which prioritizes stability over speculation.

## **F. Structured AI Prompt**

\# GOAL  
Create a professional Excel workbook that models and compares FX hedging strategies for a EUR-denominated receivable. The model must evaluate forward, money market, and option hedges, and produce clear outputs for decision-making.

\---

\# SCENARIO  
A firm expects to receive €20,000,000 in 1 year and is exposed to EUR/USD exchange rate risk. The objective is to protect USD cash flows while evaluating trade-offs between certainty, cost, and upside.

\---

\# INPUT VARIABLES (DEFINE AS NAMED RANGES)

\- FC\_AMT \= 20000000  \# EUR  
\- S0\_in \= 1.1605     \# USD/EUR  
\- F0\_in \= 1.0935     \# USD/EUR  
\- R\_USD \= 0.05       \# 5.0%  
\- R\_FC \= 0.03        \# 3.0%  
\- T\_DAYS \= 365  
\- K\_PUT \= 1.16  
\- PREM\_PUT \= 0.019

\---

\# SPREADSHEET STRUCTURE

\#\# 1\. Inputs Section  
\- Place all inputs in one section  
\- Highlight in \*\*Yellow\*\*  
\- Assign named ranges to each input

\#\# 2\. Assumptions Section  
\- Highlight in \*\*Blue\*\*  
\- Include notes on:  
  \- Interest rate conventions  
  \- No transaction costs  
  \- European option assumption  
  \- Covered interest parity

\#\# 3\. Calculations Section  
\- Highlight in \*\*Green\*\*  
\- Clearly separate each hedge strategy

\#\# 4\. Outputs Section  
\- Highlight in \*\*Gray\*\*  
\- Include summary metrics and key results

\---

\# MODEL LOGIC

\#\# Forward Hedge  
\- Compute USD proceeds:  
  USD\_forward \= FC\_AMT × F0\_in  
\- Output as fixed value

\---

\#\# Money Market Hedge  
Step 1: Discount foreign currency receivable    
  PV\_FC \= FC\_AMT / (1 \+ R\_FC)

Step 2: Convert to USD at spot    
  USD\_today \= PV\_FC × S0\_in

Step 3: Invest USD    
  USD\_mm \= USD\_today × (1 \+ R\_USD)

\---

\#\# Option Hedge (Protective Put)  
Step 1: Compute premium cost    
  Premium\_total \= FC\_AMT × PREM\_PUT

Step 2: At maturity:  
  IF S\_T \< K\_PUT:  
      Use K\_PUT  
  ELSE:  
      Use S\_T

Step 3: Compute USD proceeds    
  USD\_option \= MAX(K\_PUT, S\_T) × FC\_AMT − Premium\_total

\---

\# SENSITIVITY ANALYSIS

\- Create a range of S\_T values:  
  From 0.95 × S0\_in to 1.05 × S0\_in  
\- Increment in 1% steps  
\- For each S\_T:  
  \- Compute USD\_forward (constant)  
  \- Compute USD\_mm (constant)  
  \- Compute USD\_option (variable)

\---

\# OUTPUT REQUIREMENTS

\#\# Tables  
\- Summary table with:  
  \- USD\_forward  
  \- USD\_mm  
  \- USD\_option (base case)  
\- Sensitivity table:  
  USD proceeds vs. S\_T across strategies

\#\# Chart  
\- Line chart comparing:  
  \- Forward hedge  
  \- Money market hedge  
  \- Option hedge  
\- X-axis: S\_T  
\- Y-axis: USD proceeds

\---

\# VERIFICATION CHECKS

\- Forward hedge ≈ Money market hedge (within rounding)  
\- Option payoff increases as S\_T increases  
\- Premium reduces option payoff consistently  
\- No calculation inconsistencies

\---

\# FORMATTING RULES

\- Yellow \= Inputs  
\- Blue \= Assumptions  
\- Green \= Calculations  
\- Gray \= Outputs  
\- Use clean labels and avoid hardcoding values inside formulas  
\- Use named ranges consistently

\---

\# EXPORT

\- Output file name:  
  fx\_hedge\_model.xlsx  
\- Include:  
  \- Main model tab  
  \- "Notes & Assumptions" tab  
\- Ensure model is readable, auditable, and presentation-ready

## **G. Areas for Further Study & Improvement (Extra Credit)**

**1\. AI Skills & Automation**

AI tools can significantly enhance the functionality and scalability of this FX hedging model. For example, an AI system could automatically pull live market data, which includes spot rates, forward curves, interest rates, and implied volatility, and update the model in real time, eliminating reliance on static assumptions. More advanced implementations could incorporate Monte Carlo simulations to model thousands of potential exchange rate paths, providing probabilistic distributions of USD outcomes rather than a simple sensitivity range. This would allow treasury teams to quantify downside risk (e.g., Value-at-Risk) and make more informed hedging decisions. Additionally, AI could regenerate the entire Excel model from the structured prompt, ensuring consistency and reducing manual errors.

**2\. Multi-File Reasoning & Model Integration**

This project demonstrates how multiple artifacts, such as the Stage 1 memo, Stage 2 Excel model, and Stage 3 technical specification, can be integrated into a unified analytical workflow. AI systems capable of multi-file reasoning could read all three documents simultaneously to ensure consistency in assumptions, variable definitions, and outputs. For example, the AI could verify that all named ranges in the specification match those used in the spreadsheet and automatically flag discrepancies. It could also generate dashboards or executive summaries directly from the model outputs, streamlining reporting. This capability is particularly valuable in corporate finance environments where models must be updated frequently while maintaining alignment across documentation.

**3\. GitHub & Version Control**

Using GitHub to store the memo, model, and technical specification creates a fully auditable and reproducible workflow. Each stage of the project represents a version-controlled artifact, allowing analysts to track changes, revert to prior versions, and document the evolution of assumptions and methodologies. This is especially important in financial modeling, where transparency and traceability are critical. In a professional setting, GitHub enables collaboration among treasury, FP\&A, and audit teams, ensuring that all stakeholders work from the same validated model. It also supports automation pipelines, in which updates to the specification or inputs can trigger the model's regeneration using AI.

**4\. Accounting & Audit Integration**

In practice, FX hedging decisions must align with hedge accounting standards (e.g., ASC 815 or IFRS 9), which determine how gains and losses are recognized in financial statements. For example, qualifying hedges may defer gains/losses to Other Comprehensive Income (OCI) rather than immediate recognition in profit and loss. This introduces additional requirements, such as formal documentation, effectiveness testing, and audit trails. The structured specification and version-controlled model developed in this project could serve as supporting documentation for auditors, demonstrating how hedge effectiveness is measured and ensuring compliance with accounting standards. Integrating these considerations would elevate the model from a decision tool to a fully compliant financial reporting framework.

## **Conclusion**

This analysis demonstrates that while multiple hedging strategies are available, the optimal choice depends on the firm’s priorities. Given the importance of cash flow certainty and risk mitigation, the forward hedge provides the most reliable and cost-effective solution. The model and structured prompt together establish a reproducible framework for ongoing FX risk management and future automation.

