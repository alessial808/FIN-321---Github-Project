[stage4-final-analysis-Loperfido.md](https://github.com/user-attachments/files/27298863/stage4-final-analysis-Loperfido.md)
# Stage 4 – Final Analysis, Prompt Engineering & Recommendation
**Prepared by:** Alessia Loperfido  
**Date:** April 2026  
**Version:** 1.0  
**Audience:** CFO / Director of Treasury  

---

## A. Exposure Summary

The firm holds a EUR 20,000,000 receivable due in one year, denominated in euros and creating transaction exposure to EUR/USD exchange rate movements. At the current spot rate of 1.1605 USD/EUR, the receivable is worth approximately **$23,210,000 USD** in today's terms. However, if the euro depreciates over the next twelve months, the realized USD proceeds at collection will be materially lower — eroding revenue and distorting cash flow projections.

This is a classic transaction exposure problem: the euro amount is fixed, but the USD value is a function of the future spot rate S_T, which is unknown. A 5% depreciation in the euro, for example, would reduce USD proceeds by over $1.1 million relative to today's spot value — a meaningful impact for budget planning and financial reporting.

The hedging decision is therefore not speculative; it is a risk management question about how much FX uncertainty the firm is willing to accept, and at what cost.

---

## B. Summary of Hedge Outcomes

All proceeds are calculated on a EUR 20,000,000 receivable. Key market inputs: S0 = 1.1605, F0 = 1.0935, R_USD = 5.0%, R_EUR = 3.0%, K_PUT = 1.16, PREM_PUT = 0.019 USD/EUR.

### Forward Hedge
**Locked-in USD proceeds: $21,870,000**

Multiplying the EUR receivable by the one-year forward rate (1.0935 USD/EUR) produces a fixed, guaranteed outcome of $21,870,000. This eliminates all FX uncertainty. The trade-off is opportunity cost: if the euro appreciates above 1.0935, the firm forgoes the upside. The forward rate reflects the interest rate differential between the USD (5%) and EUR (3%) — a 1.7% discount to the current spot rate — which is the cost of certainty in the current rate environment.

**Key insight:** The forward rate is below spot because USD rates exceed EUR rates. The firm is locking in a rate that is already discounted relative to today's market.

### Money Market Hedge
**Proceeds: ~$21,870,000 (matches forward)**

The money market hedge replicates the forward synthetically: discount the EUR receivable at R_EUR (3%) to find the present value of ~€19,417,476, borrow that amount today, convert to USD at spot (1.1605), and invest at R_USD (5%) for one year. The result converges to the forward hedge outcome due to covered interest rate parity. This equivalence serves as an important validation check for model consistency.

**Key insight:** While the economic outcome is identical to the forward, the money market hedge requires balance sheet activity — borrowing in EUR and investing in USD — which carries liquidity implications and may be operationally more complex for some treasury teams.

### Put Option Hedge
**Floor proceeds (if EUR depreciates below K_PUT = 1.16): ~$21,820,000 net**

The put option provides downside protection with retained upside. The total premium cost is $380,000 (0.019 × 20,000,000). If S_T falls below the strike of 1.16, the firm exercises the put and receives $23,200,000 gross, or **$22,820,000 net** of premium. If the euro appreciates above 1.16, the firm sells at the market rate and benefits from the upside, minus the $380,000 premium cost.

**Key insight:** The option hedge dominates the forward in upside scenarios and provides a meaningful floor in downside scenarios. The cost is $380,000 in upfront premium — effectively the price of preserving optionality.

### Call Option
A call option on EUR would benefit the firm if it had a euro *payable* rather than a receivable. For this exposure (long EUR), a call option is not the appropriate hedging instrument. It would only add to the firm's existing EUR exposure rather than offset it. It is included for completeness as a benchmark for understanding asymmetric payoffs.

### No Hedge (Baseline)
The unhedged position exposes the firm to the full range of possible S_T outcomes. At S_T = 1.1605 (spot unchanged), proceeds would be $23,210,000 — meaningfully above the forward hedge. At S_T = 1.04 (–10% EUR depreciation), proceeds would fall to approximately $20,800,000 — well below the hedged outcomes. The unhedged position is the highest-risk, highest-potential-reward strategy.

---

## C. Sensitivity Interpretation

The sensitivity analysis varies S_T over a ±5% range around the current spot (1.1605), at 1% increments, producing the following approximate USD proceeds across strategies:

| S_T (USD/EUR) | Change | Unhedged | Forward | Option (Net) |
|---|---|---|---|---|
| 1.102 | –5% | $22,040,000 | $21,870,000 | $22,820,000 |
| 1.125 | –3% | $22,500,000 | $21,870,000 | $22,820,000 |
| 1.148 | –1% | $22,960,000 | $21,870,000 | $22,820,000 |
| **1.160** | **0%** | **$23,210,000** | **$21,870,000** | **$22,830,000** |
| 1.183 | +1% | $23,660,000 | $21,870,000 | $23,280,000 |
| 1.206 | +3% | $24,120,000 | $21,870,000 | $23,740,000 |
| 1.219 | +5% | $24,380,000 | $21,870,000 | $24,000,000 |

*Note: Option net proceeds = max(S_T, K_PUT) × 20,000,000 – $380,000*

**EUR Depreciation Scenarios:** The forward and money market hedges provide certainty, locking in $21,870,000 regardless of how far the euro falls. The option hedge also provides a floor, with net proceeds of approximately $22,820,000 — actually *better* than the forward — because the put strike (1.16) is above the forward rate (1.0935). The unhedged position deteriorates in line with the exchange rate.

**EUR Appreciation Scenarios:** Here the forward hedge's opportunity cost becomes visible. The unhedged position and the option hedge (above the strike) both benefit from a rising euro. The forward hedge is capped at $21,870,000 and cannot participate in upside. The option hedge retains this upside while keeping the downside floor — the economic benefit of the premium paid.

**Key takeaway:** Across this ±5% range, the put option hedge consistently outperforms or matches both the forward and unhedged positions on a risk-adjusted basis, with the only cost being the $380,000 upfront premium.

---

## D. Strategic Recommendation

**Recommended Strategy: Put Option Hedge**

The put option hedge is the recommended strategy for managing this EUR 20,000,000 receivable.

The core rationale is as follows: the put strike of 1.16 USD/EUR is set above the current forward rate of 1.0935, meaning the option hedge establishes a floor that is actually *higher* than what the forward hedge locks in. This is an unusually favorable structure. In EUR depreciation scenarios, the put outperforms the forward. In EUR appreciation scenarios, the firm participates in the upside — which neither the forward nor money market hedge permits.

The cost of this advantage is a $380,000 upfront premium — approximately 1.6% of the hedged notional value. This is a defined, budgetable cost that can be treated as an insurance premium for FX risk.

**Supporting data:**
- Forward hedge floor: $21,870,000 (certain, no upside)
- Option hedge floor: ~$22,820,000 net (above forward floor, with upside retained)
- Premium cost: $380,000 (1.64% of $23,210,000 spot value)
- Break-even: The option underperforms only if the euro appreciates and the firm views the premium as "wasted" — but given current uncertainty, this is the appropriate trade-off

---

## E. Executive Justification

**Cash Flow Stability:** The put option establishes a minimum USD cash flow of approximately $22,820,000. This provides a reliable floor for financial planning and working capital projections without giving up the possibility of higher proceeds if market conditions improve.

**Budget Certainty:** Unlike the unhedged position, the option strategy allows treasury to set a conservative budget using the floor rate, with upside scenario planning above it. The forward hedge also enables budgeting but at a lower floor and with no upside flexibility.

**Liquidity Impact:** The $380,000 premium is paid upfront in USD, which is a known, immediate cash outflow. This should be factored into near-term liquidity planning but is manageable relative to the $23M exposure. The money market hedge, by contrast, requires EUR borrowing — a more complex and potentially more disruptive balance sheet action.

**Optionality Value:** The put option is the only strategy that allows the firm to benefit from EUR appreciation. Given current macroeconomic uncertainty — including potential shifts in ECB and Fed policy — maintaining this flexibility has genuine economic value that the sensitivity table quantifies.

**Premium Cost as Insurance:** The $380,000 premium should be framed for the CFO as an insurance cost, not a speculative expense. It is economically equivalent to purchasing downside protection on a $23M asset. The effective hedge ratio is 100%, and the cost per dollar protected is approximately 1.64 cents — a reasonable price in the current volatility environment.

---

## F. Structured AI Prompt (Appendix)

---

```
# GOAL

Generate a complete FX hedging model in Excel (.xlsx) that evaluates forward, money market,
and option hedging strategies for a EUR-denominated receivable. The model must include
named input ranges, color-coded sections, a sensitivity table, and verification checks.
Output a professionally formatted workbook with a summary dashboard.

---

# INPUT VARIABLES

Use the following values. Do not infer or substitute any variable. Label all inputs in a
dedicated "Inputs" section.

FC_AMT     = 20,000,000          # Foreign currency receivable (EUR)
S0_in      = 1.1605              # Spot rate (USD/EUR)
F0_in      = 1.0935              # 1-year forward rate (USD/EUR)
R_USD      = 0.05                # USD annual interest rate (5.0%)
R_FC       = 0.03                # EUR annual interest rate (3.0%)
T_YRS      = 1                   # Time to maturity (years)
K_PUT      = 1.16                # Put option strike (USD/EUR)
PREM_PUT   = 0.019               # Put option premium (USD per EUR)
K_CALL     = 1.16                # Call option strike (USD/EUR) — reference only
PREM_CALL  = 0.021               # Call option premium (USD per EUR) — reference only
T_DAYS     = 365                 # Days to maturity

---

# MODEL LOGIC

## Section 1: Forward Hedge
- USD_forward = FC_AMT × F0_in
- Output: fixed USD proceeds, labeled USD_forward
- Interpretation note: eliminates all FX risk; locked rate below current spot due to interest rate differential

## Section 2: Money Market Hedge
Step 1: Compute PV of EUR receivable
  PV_FC = FC_AMT / (1 + R_FC)^T_YRS

Step 2: Convert to USD at spot
  USD_borrowed = PV_FC × S0_in

Step 3: Invest at USD rate
  USD_mm = USD_borrowed × (1 + R_USD)^T_YRS

- Output: USD_mm
- Verification: USD_mm should equal USD_forward (parity check). Flag if difference > $100.

## Section 3: Put Option Hedge
- Total premium cost: PREM_COST = PREM_PUT × FC_AMT
- At maturity for each scenario:
  IF S_T < K_PUT: USD_option = (K_PUT × FC_AMT) - PREM_COST   [exercise put]
  IF S_T >= K_PUT: USD_option = (S_T × FC_AMT) - PREM_COST    [sell at market]
- Output: USD_option (varies with S_T)

## Section 4: Call Option (Reference)
- PREM_CALL_COST = PREM_CALL × FC_AMT
- Note in model: call option benefits a EUR payable, not a receivable; included for reference only

## Section 5: Unhedged Baseline
- USD_unhedged = S_T × FC_AMT
- Output: varies with S_T; serves as risk benchmark

---

# SENSITIVITY TABLE

Create a table with S_T ranging from S0_in × 0.95 to S0_in × 1.05, in 1% increments
(11 rows). For each S_T value, compute and display:
  - Unhedged USD proceeds
  - Forward hedge proceeds (constant)
  - Money market proceeds (constant)
  - Put option net proceeds
  - % difference: option vs. forward

Label columns clearly. Include a note row indicating the current spot rate and forward rate
within the table for visual reference.

---

# COLOR CODING

Apply the following color scheme consistently across ALL sections:
  - Yellow  (#FFFF00 or equivalent)  → Input cells (all FC_AMT, S0_in, etc.)
  - Blue    (#BDD7EE or equivalent)  → Assumption cells (interest rates, T_YRS)
  - Green   (#C6EFCE or equivalent)  → Formula output cells
  - Gray    (#D9D9D9 or equivalent)  → Summary/output section backgrounds

Use bold headers for each section. Include a color legend on the first sheet or in a footer.

---

# SPREADSHEET STRUCTURE

Sheet 1: Model
  - Row 1–2: Title block (firm name placeholder, date, analyst name)
  - Rows 4–15: Input section (named ranges, yellow)
  - Rows 17–30: Forward Hedge section
  - Rows 32–45: Money Market Hedge section (3-step layout)
  - Rows 47–60: Put Option Hedge section
  - Rows 62–70: Call Option reference block
  - Rows 72–85: Sensitivity Table
  - Rows 87–95: Verification Checks

Sheet 2: Summary Dashboard
  - Key outputs: USD_forward, USD_mm, USD_option (floor), option premium cost
  - Side-by-side strategy comparison table
  - Recommendation row (highlight preferred strategy)

---

# NAMED RANGES

Define the following named ranges in the workbook (Insert > Name Manager):
  FC_AMT, S0_in, F0_in, R_USD, R_FC, T_YRS, K_PUT, PREM_PUT, K_CALL, PREM_CALL, T_DAYS

All formulas in the model must reference named ranges, not hardcoded cell addresses.

---

# VERIFICATION CHECKS

Include the following checks in a dedicated verification block:
1. Parity Check: USD_mm vs. USD_forward — flag if |difference| > $100
2. Formula Consistency: Confirm that USD_forward = FC_AMT × F0_in
3. Option Floor Check: Confirm that (K_PUT × FC_AMT) – PREM_COST > USD_forward
   (i.e., option floor exceeds forward proceeds — flag if false)
4. Premium Reasonableness: PREM_COST as % of (S0_in × FC_AMT) — output as percentage

---

# EXPORT

Save the completed workbook as: FX_Hedging_Model_Loperfido.xlsx
Ensure all formulas are live (no hardcoded outputs).
Freeze the top row of each section header.
Apply print-ready formatting: 1-inch margins, landscape orientation, fit to page.
```

---

## Extra Credit: Areas for Further Study & Improvement

### 1. AI Skills & Automation

The model developed in this project is static — it uses fixed assumptions and requires manual updates whenever market data changes. AI tools like Claude Skills or Python-based Code Interpreter environments could transform this into a dynamic, on-demand system. A skill could be configured to pull live EUR/USD spot and forward rates from a market data API (such as Bloomberg or Refinitiv), substitute them into the named range inputs, and regenerate the full hedging model automatically. This would eliminate the manual re-entry step that currently limits the model's usefulness in an active treasury environment. More ambitiously, a Monte Carlo simulation layer could replace the static ±5% sensitivity range with a stochastic distribution of exchange rate paths — producing probabilistic outputs (e.g., 5th and 95th percentile USD proceeds) that better capture tail risk. The structured AI prompt in Section F is already written in a way that would support this extension: all variable names are explicit and standardized, which means a script could simply substitute new values and re-run the prompt without redesigning the model logic.

### 2. Multi-File Reasoning & GitHub Version Control

One of the practical challenges in financial modeling is maintaining consistency across multiple documents — a specification, a spreadsheet, an analysis memo, and a prompt — especially as inputs change over time. AI systems with multi-file context, such as those accessible via GitHub-linked repositories, can ingest the Stage 3 specification, the Stage 2 spreadsheet, and the Stage 4 prompt simultaneously and flag inconsistencies automatically (for example, if the forward rate in the spec differs from the rate used in the model). Committing each stage of this project to a GitHub repository creates a complete, timestamped audit trail: every change to the model inputs, formulas, or assumptions is logged with a commit message and is fully reversible. This is directly analogous to hedge documentation requirements under ASC 815 (FASB) or IFRS 9, where firms must demonstrate that a hedging relationship was designated and documented *at inception*. A GitHub commit at the point of hedge designation could serve as that documentation — providing an auditor with a verifiable record of what was known and decided at the time, with no possibility of retroactive alteration. This integration of version control and accounting rigor represents a genuinely novel application of developer tools to treasury practice.
