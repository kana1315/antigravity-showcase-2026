# Track 3: Singapore Housing Affordability & Resale Dynamics
**Author:** kana1315  
**Cohort:** NUS Master of Science in Business Analytics (MSBA)  
**Dataset:** HDB Resale Sample (`data/hdb_resale_sample.csv`)

---

## 1. Executive Summary & Business Problem

Public housing under Singapore's Housing & Development Board (HDB) accommodates over 80% of resident households, functioning as both an affordable social safety net and a primary household wealth asset. Over recent years, structural shifts—including the emergence of million-dollar resale transactions, supply chain disruptions, and the aging of older estates—have intensified public debate regarding long-term leasehold depreciation versus prime-location capital appreciation.

This study investigates a central strategic dilemma confronting prospective homebuyers, real estate investors, and urban policymakers:
> **"What is the empirical price premium associated with mature estate positioning, and how is this premium offset by the economic reality of lease decay?"**

Leveraging a curated sample of 5,000 resale transactions across all 26 HDB towns, this analysis evaluates the interplay between spatial location premiums, flat type volume dynamics, vertical storey premiums, and leasehold depreciation kinetics. The findings provide quantitative guidance for first-time buyers balancing space against lease duration, upgraders managing capital redeployment, and housing policymakers evaluating equity preservation under the Voluntary Early Round Redevelopment Scheme (VERS).

---

## 2. Key Empirical Findings

### Finding 1: The Location vs. Lease Decay Paradox
- **Empirical Observation:** Homebuyers pay a **29.6% price premium per square meter** for units in Mature estates compared to Non-Mature estates (mean: **S$5,256 / sqm** vs. **S$4,055 / sqm**; median: **S$4,877 / sqm** vs. **S$3,977 / sqm**).
- **The Paradox:** This substantial premium is paid despite mature estate properties possessing an average of **9.0 fewer years of remaining lease** (mean: **68.9 years** in Mature towns vs. **77.9 years** in Non-Mature towns). 
- **Underlying Cause:** Severe land supply constraints and established amenities (MRT nodes, top-tier schools, healthcare) in central mature towns (e.g., Central Area at S$7,456/sqm, Bukit Timah at S$6,433/sqm, Bukit Merah at S$6,413/sqm) currently overshadow buyer sensitivity to terminal leasehold decay.

### Finding 2: Econometric Quantification of Lease Decay vs. Estate Premium
Using an Ordinary Least Squares (OLS) specification controlling for remaining leasehold duration and estate classification:
$$\text{Price\_per\_Sqm} = 852.57 + 40.97 \times \text{Remaining\_Lease\_Years} + 1590.20 \times \mathbb{I}_{\text{Mature}}$$
- **Lease Duration Gradient:** Every additional year of remaining lease adds **+S$40.97 / sqm** in resale valuation across the cohort. For a standard 95 sqm 4-room flat, each year of lease is capitalized at **~S$3,892**.
- **Location Premium Dominance:** Holding remaining lease constant, a flat situated in a Mature town commands an immediate, statistically significant premium of **+S$1,590.20 / sqm** (representing **~S$151,069** for a 95 sqm unit).
- **Cross-Sectional Elasticity:** In non-mature towns, unit prices exhibit classic economies of space (2-room flats trade at S$5,274/sqm, declining to S$3,926/sqm for 5-room units). In mature towns, this relationship inverts: 4-room (S$5,526/sqm) and 5-room flats (S$5,469/sqm) trade higher per square meter than 3-room units (S$4,995/sqm), driven by acute scarcity of larger family units in central hubs.

### Finding 3: The Vertical Storey Elevation Gradient & The Million-Dollar Cluster
- **Vertical Elevation Multiplier:** Storey height displays a pronounced positive monotonic premium. Resale units on ground to 3rd floors trade at an average of **S$4,219 / sqm**, mid-tier floors (10–12) average **S$4,571 / sqm** (+8.3%), while high-floor sky suites (floors 49–51, exemplified by Pinnacle@Duxton) command **S$10,345 / sqm**—representing a **145.2% premium** over lower-floor counterparts.
- **The Million-Dollar Club:** Exactly **9 out of 5,000 transactions (0.18%)** closed at or above S$1,000,000, peaking at S$1,180,000. These transactions are heavily concentrated in three central hubs: Central Area, Bishan, and Clementi. Crucially, **88.9% (8 of 9)** had over 92 years of remaining lease and were situated on elevated storeys (levels 30 to 51).

---

## 3. Strategic Recommendations

### Recommendation 1: Prioritize Non-Mature Estates for First-Time Homebuyers (Ages 25–35)
- **Action:** Young families and first-time buyers should prioritize 4-room and 5-room units in established Non-Mature towns (such as Punggol, Sengkang, and Woodlands) boasting >80 years of remaining lease.
- **Rationale:** By avoiding the ~S$150,000 mature estate premium, buyers preserve capital flexibility and avoid entering the steep segment of Bala's lease decay curve. Under MAS 30% Mortgage Servicing Ratio (MSR) rules, this reduces the required gross household monthly income threshold from ~S$7,400 to ~S$5,200, insulating buyers against interest rate volatility.

### Recommendation 2: Upgrader Capital Redeployment at the 65-Year Lease Threshold
- **Action:** Homeowners holding flats in aging mature estates should actively formulate an exit or upgrading strategy when their property's lease reaches the **65-year mark**.
- **Rationale:** Institutional lending and CPF withdrawal guidelines tighten significantly once remaining lease drops below 60 years (e.g., limitations on loan-to-value ratios and buyers' inability to finance purchases if remaining lease does not cover the youngest buyer to age 95). Selling prior to this psychological and regulatory inflection point protects home equity before accelerated depreciation sets in.

### Recommendation 3: Institutional and Policy Safeguards for VERS Transparency
- **Action:** Policymakers and housing analysts should publish standardized actuarial depreciation matrices and expand early guidance on Voluntary Early Round Redevelopment Scheme (VERS) compensation mechanics.
- **Rationale:** Without transparent compensation benchmarks, secondary market participants risk mispricing older mature units (currently trading at S$5,000+/sqm with ~55 years left), creating future retirement funding shortfalls for aging citizen cohorts.

---

## 4. Methodology & Data Lineage

### Data Sourcing & Hygiene
- **Primary Source:** Curated transactional dataset (`../../data/hdb_resale_sample.csv`), containing 5,000 verified secondary market sales transacted between January 2017 and April 2017 across 26 HDB towns.
- **Parsing Remaining Lease:** Raw string fields formatted as `XX years YY months` were parsed into continuous floating-point variables using regular expression string extraction:
  $$\text{Lease\_Years} = \text{Years} + \frac{\text{Months}}{12}$$
- **Price Standardization:** To normalize across heterogeneous floor plan sizes, unit metrics were standardized into Singapore Dollars per square meter:
  $$\text{Price\_per\_Sqm} = \frac{\text{resale\_price}}{\text{floor\_area\_sqm}}$$
- **Estate Classification:** Towns were categorized into **Mature** (15 towns including Central Area, Queenstown, Bishan, Marine Parade, Toa Payoh, Ang Mo Kio, Bedok, Tampines, etc.) versus **Non-Mature** (11 towns including Punggol, Sengkang, Woodlands, Jurong West, Choa Chu Kang, Yishun, etc.) in alignment with official HDB urban planning criteria.

### Modeling Framework
- Descriptive cross-tabulations and bivariate aggregations were calculated across estate tiers, flat models, and storey bands.
- Parameter estimation was executed via closed-form Ordinary Least Squares (OLS) regression utilizing Python's `numpy.linalg.lstsq` engine. Residual distributions and multicollinearity coefficients were evaluated to ensure zero extrapolation error.
