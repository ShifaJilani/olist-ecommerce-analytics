# Olist Marketing Funnel Analysis

## 1. Business Problem

Olist generates Marketing Qualified Leads (MQLs) through different acquisition channels and landing pages. Not all MQLs progress to a closed deal.

The purpose of this analysis is to understand how effectively leads move through the funnel and identify where conversion performance differs.

The analysis looks at the overall MQL-to-closed-deal conversion rate and compares performance across acquisition origin, landing pages, time periods, and other available sales attributes.

## 2. Objective

The objective is to:

- Measure the overall MQL-to-closed-deal conversion rate.
- Compare conversion performance across acquisition origins.
- Identify differences in landing-page performance.
- Examine whether landing-page performance changes across acquisition origins.
- Analyze how conversion changed over time.
- Measure the time taken for leads to become closed deals.
- Review closed-deal distribution across SDRs and lead types.
- Identify areas where the sales funnel may be improved.

## 3. Data Used

This analysis uses the Olist Marketing Funnel dataset, which contains information about leads and closed deals.

Two tables were used:

### Marketing Qualified Leads

**Table:** `marketing_qualified_leads_table`

- 8,000 MQL records
- One record per `mql_id`
- Contains:
  - `mql_id`
  - `first_contact_date`
  - `landing_page_id`
  - `origin`

### Closed Deals

**Table:** `closed_deals_table`

- 842 closed-deal records
- One record per `mql_id`
- Contains information about the seller, sales representatives, deal date, lead characteristics, and other attributes.

### Relationship

The two tables were connected using:

`mql_id`

The MQL table was treated as the starting point of the funnel. A closed deal was identified when the corresponding `mql_id` was present in the closed-deals table.

A validation check confirmed that all 842 closed deals had a matching MQL record and that `mql_id` was unique in both tables.

## 3.1 Initial Data Checks

Before loading the data into Microsoft Fabric, an initial review was carried out in Excel to check the structure and quality of the source data.

The checks included reviewing column names and data types, checking row counts, identifying missing values and duplicates, and looking for any obvious data inconsistencies.

After these initial checks, the data was moved to Microsoft Fabric, where the main data validation, SQL analysis, funnel calculations, and analysis were carried out.


## 4. Funnel Overview

The funnel starts with 8,000 Marketing Qualified Leads (MQLs).

Of these, 842 became closed deals.

This gives an overall MQL-to-closed-deal conversion rate of **10.53%**.

| Funnel Stage | Count |
|---|---:|
| Marketing Qualified Leads (MQLs) | 8,000 |
| Closed Deals | 842 |
| MQL-to-Closed-Deal Conversion Rate | 10.53% |

### Finding

The overall MQL-to-closed-deal conversion rate is **10.53%**, meaning that roughly 1 in 10 MQLs progressed to a closed deal.

This provides the baseline for comparing conversion performance across acquisition origins, landing pages, and other funnel characteristics.

## 5. Conversion by Acquisition Origin

The next step was to compare MQL-to-closed-deal conversion across the different acquisition origins.

| Origin | MQLs | Closed Deals | Conversion Rate |
|---|---:|---:|---:|
| organic_search | 2,296 | 271 | 11.80% |
| paid_search | 1,586 | 195 | 12.30% |
| social | 1,350 | 75 | 5.56% |
| unknown | 1,099 | 179 | 16.29% |
| direct_traffic | 499 | 56 | 11.22% |
| email | 493 | 15 | 3.04% |
| referral | 284 | 24 | 8.45% |
| other | 150 | 4 | 2.67% |
| display | 118 | 6 | 5.08% |
| other_publicities | 65 | 3 | 4.62% |
| NULL | 60 | 14 | 23.33% |

### Finding

Conversion performance varies considerably across acquisition origins.

`paid_search` had the highest conversion rate among the major identified acquisition sources at **12.30%**, followed closely by `organic_search` at **11.80%**.

`social` generated a large number of MQLs (1,350), but converted only **5.56%** of them. `email` generated 493 MQLs with a conversion rate of only **3.04%**.

The `unknown` category had a relatively high conversion rate of **16.29%** and 179 closed deals. However, because the source is not identified, this category should be treated separately when evaluating acquisition-channel performance.

### Business Interpretation

The results show that generating a high number of MQLs does not necessarily lead to a high number of closed deals. Some sources produce substantial lead volume but convert at a much lower rate.

This suggests that acquisition performance should be evaluated using both **lead volume and conversion rate**, rather than MQL volume alone.

## 6. Landing Page Performance

Landing-page performance was analyzed to determine whether some pages generated more effective leads than others.

Because there are many landing pages, the analysis focused on pages that generated at least 20 MQLs. This avoids giving too much importance to pages with very small numbers of leads.

| Landing Page | MQLs | Closed Deals | Conversion Rate |
|---|---:|---:|---:|
| LP-357 | 912 | 171 | 18.75% |
| LP-62 | 883 | 174 | 19.71% |
| LP-123 | 330 | 67 | 20.30% |
| LP-395 | 394 | 59 | 14.97% |
| LP-160 | 495 | 27 | 5.45% |
| LP-263 | 445 | 31 | 6.97% |
| LP-469 | 310 | 21 | 6.77% |
| LP-444 | 291 | 10 | 3.44% |

### Finding

Landing-page performance varies considerably.

Several high-volume landing pages, including **LP-62, LP-123, and LP-357**, converted around **19–20%**. These pages also generated a large number of MQLs.

In contrast, other high-volume pages performed much worse. **LP-160** converted at **5.45%**, **LP-469** at **6.77%**, and **LP-444** at only **3.44%**.

This shows that high MQL volume does not necessarily mean strong funnel performance. Some landing pages generate substantial lead volume while producing relatively few closed deals.

### Business Interpretation

Landing-page performance appears to be an important area for further investigation.

The data identifies clear differences between high-volume, high-converting pages and high-volume, low-converting pages. However, the dataset does not contain information about the actual content, design, or user experience of these pages, so the analysis cannot determine why these differences exist.

The landing-page aliases (`LP-1` to `LP-495`) are used only to make the analysis easier to read. They do not represent meaningful page names.

## 7. Origin and Landing Page Performance

The analysis was then extended to both acquisition origin and landing page together.

This was done to determine whether a landing page performed consistently across different acquisition sources or whether its performance changed depending on how the lead arrived.

The analysis focused on origin and landing-page combinations with at least 20 MQLs.

### Selected Findings

| Origin | Landing Page | MQLs | Closed Deals | Conversion Rate |
|---|---|---:|---:|---:|
| organic_search | LP-62 | 495 | 112 | 22.63% |
| organic_search | LP-357 | 116 | 24 | 20.69% |
| organic_search | LP-469 | 197 | 13 | 6.60% |
| organic_search | LP-444 | 109 | 4 | 3.67% |
| paid_search | LP-123 | 241 | 50 | 20.75% |
| paid_search | LP-62 | 124 | 20 | 16.13% |
| paid_search | LP-116 | 33 | 1 | 3.03% |
| direct_traffic | LP-395 | 46 | 11 | 23.91% |
| direct_traffic | LP-62 | 105 | 18 | 17.14% |
| social | LP-263 | 413 | 30 | 7.26% |
| social | LP-160 | 464 | 24 | 5.17% |
| social | LP-259 | 84 | 1 | 1.19% |
| unknown | LP-357 | 656 | 134 | 20.43% |

### Finding

Landing-page performance can vary substantially within the same acquisition origin.

For example, within `organic_search`, LP-62 converted **22.63%**, while LP-469 converted **6.60%** and LP-444 converted **3.67%**.

The differences are also visible across origins for the same landing page. LP-62 converted at **22.63%** for organic search, **16.13%** for paid search, **17.14%** for direct traffic, **17.86%** for referral, but only **3.03%** for social.

### Business Interpretation

The results suggest that landing-page performance should not be evaluated separately from acquisition origin.

The same landing page can produce different conversion rates depending on the source of the MQL. This indicates that the relationship between acquisition channel and landing page is worth considering when evaluating funnel performance.

The available data does not contain enough information about the landing-page content, campaign messaging, or user behaviour to determine the reason for these differences.

## 8. Conversion Trend Over Time

Conversion was analyzed by the month in which each MQL first made contact.

| Month | MQLs | Closed Deals | Conversion Rate |
|---|---:|---:|---:|
| Jun 2017 | 4 | 0 | 0.00% |
| Jul 2017 | 239 | 2 | 0.84% |
| Aug 2017 | 386 | 9 | 2.33% |
| Sep 2017 | 312 | 7 | 2.24% |
| Oct 2017 | 416 | 14 | 3.37% |
| Nov 2017 | 445 | 18 | 4.04% |
| Dec 2017 | 200 | 11 | 5.50% |
| Jan 2018 | 1,141 | 152 | 13.32% |
| Feb 2018 | 1,028 | 149 | 14.49% |
| Mar 2018 | 1,174 | 167 | 14.22% |
| Apr 2018 | 1,352 | 183 | 13.54% |
| May 2018 | 1,303 | 130 | 9.98% |

### Finding

MQL-to-closed-deal conversion increased substantially from mid-2017 through early 2018.

Conversion rose from **0.84% in July 2017** to **14.49% in February 2018**. It remained above 13% through April before falling to **9.98% in May 2018**.

The increase suggests that the funnel was converting a much larger proportion of MQLs in 2018 than during the earlier months of the dataset.

However, the most recent months need to be interpreted together with the sales-cycle analysis. A lead does not necessarily become a closed deal immediately after first contact.

## 9. Sales Cycle Analysis

The time between an MQL's first contact date and its won date was calculated for closed deals.

The average time taken to close a deal was **48.44 days**.

The results also showed that most deals were closed relatively early in the sales process, while a smaller number of deals took several months to close. The longest observed sales cycle was **427 days**.

One record had a sales cycle of **-2 days**, meaning the recorded won date was two days before the first contact date. This is a data-quality issue and was retained as part of the original data rather than changed during the analysis.

### Finding

The sales cycle has a wide range, from same-day conversions to deals taking more than a year.

The average of **48.44 days** shows that conversion does not necessarily happen immediately after an MQL is created. This is important when interpreting monthly conversion rates, particularly for the latest months in the dataset.

### Business Interpretation

Monthly conversion should be interpreted together with the sales cycle. Recent MQLs may not have had enough time to complete the sales process and become closed deals.

This means the lower conversion observed in May 2018 should not automatically be treated as a deterioration in funnel performance.

## 10. SDR Analysis

The closed-deals data was reviewed to understand how closed deals were distributed across Sales Development Representatives (SDRs).

The analysis showed that **33 SDRs** were associated with closed deals.

The number of closed deals varied considerably across SDRs. The highest-volume SDR was associated with **140 closed deals**, while several SDRs were associated with only one or a few closed deals.

### Finding

There is a clear difference in the number of closed deals handled by individual SDRs.

However, an SDR-level conversion rate could not be calculated from the available data. The `sdr_id` is recorded in the closed-deals table, but it is not available for all MQLs.

As a result, the data does not tell us how many MQLs were assigned to each SDR before the deals were closed.

### Business Interpretation

The SDR analysis can be used to describe the distribution of closed deals across the sales team, but it cannot be used to rank SDR performance based on conversion rate.

A higher number of closed deals may simply reflect that an SDR handled more leads. Additional assignment or activity data would be required to measure SDR-level conversion performance.

## 11. Lead Type Analysis

The closed-deals data was reviewed to understand the distribution of successful deals across lead types.

| Lead Type | Closed Deals |
|---|---:|
| online_medium | 332 |
| online_big | 126 |
| industry | 123 |
| offline | 104 |
| online_small | 77 |
| online_beginner | 57 |
| online_top | 14 |
| NULL | 6 |
| other | 3 |

### Finding

`online_medium` was the largest lead type among closed deals, accounting for **332 of the 842 closed deals**.

The remaining closed deals were distributed across several other lead types, with `online_big`, `industry`, and `offline` being the next largest groups.

### Business Interpretation

The analysis shows which lead types are most represented among successful deals.

However, this does not measure conversion performance by lead type. The `lead_type` field is available in the closed-deals data rather than across the full MQL population, so we cannot determine what proportion of MQLs within each lead type became closed deals.

Therefore, the results are used as a **closed-deal distribution**, not as a lead-type conversion analysis.

## 12. Key Findings

The analysis identified several important differences in funnel performance.

### 1. Overall funnel conversion

The funnel converted **842 of 8,000 MQLs**, resulting in an overall conversion rate of **10.53%**.

### 2. Acquisition origin matters

Conversion rates differed considerably across acquisition origins. Paid search and organic search had relatively strong conversion rates, while social and email produced substantial MQL volume but had much lower conversion rates.

### 3. Landing-page performance varies

Landing pages showed large differences in conversion performance, even among pages with high MQL volumes. For example, LP-62 converted at **19.71%**, while LP-444 converted at only **3.44%**.

### 4. Origin and landing page should be considered together

The same landing page did not perform equally across all acquisition origins. LP-62, for example, converted at **22.63% through organic search** but only **3.03% through social**.

### 5. Conversion improved over time

The monthly conversion rate increased substantially from mid-2017 into early 2018, reaching **14.49% in February 2018**. It then declined to **9.98% in May 2018**.

### 6. The sales cycle affects how recent results should be interpreted

The average time from first contact to closed deal was **48.44 days**. Therefore, recent MQLs may not have had enough time to complete the sales process.

### 7. Some analyses are limited by the available data

SDR-level conversion and lead-type conversion could not be measured because those attributes are not available across the full MQL population. They were therefore used only for descriptive analysis.

## 13. Business Recommendations

Based on the analysis, the following areas should be prioritized:

### 1. Review high-volume, low-converting landing pages

Landing pages such as LP-160, LP-469, and LP-444 generated substantial MQL volume but had relatively low conversion rates.

These pages should be reviewed to understand whether their content, targeting, or user experience can be improved.

### 2. Investigate acquisition sources with high volume but low conversion

Social generated 1,350 MQLs but converted at only 5.56%. Email generated 493 MQLs with a 3.04% conversion rate.

The business should investigate whether these channels are attracting the right type of leads and whether lead quality differs from higher-converting sources.

### 3. Examine successful origin and landing-page combinations

Combinations such as organic search with LP-62 and paid search with LP-123 showed strong conversion performance.

These combinations should be investigated further to understand what characteristics may be contributing to their stronger results.

### 4. Avoid judging recent funnel performance without considering the sales cycle

Because the average sales cycle was 48.44 days, recent MQL cohorts should be given sufficient time to progress through the sales process before their final conversion performance is evaluated.

### 5. Improve tracking of acquisition and sales information

The presence of `unknown` and NULL origins, along with the lack of SDR information for the full MQL population, limits the ability to measure performance accurately.

Improving lead-source and sales-assignment tracking would allow more complete performance analysis.

## 14. Limitations

The analysis has several limitations based on the available data.

- The landing-page IDs do not contain meaningful page names or information about page content, design, or user experience.
- Acquisition origin contains both `unknown` and NULL values, which limits the accuracy of channel-level analysis.
- `sdr_id` is available only for closed deals, so SDR-level conversion rates cannot be calculated.
- `lead_type` is available only for closed deals, so the total number of MQLs for each lead type is unknown. Therefore, lead-type conversion rates cannot be calculated.
- One closed deal has a negative sales-cycle duration, with the recorded `won_date` occurring two days before the first contact date.
- Recent MQL cohorts may have incomplete conversion results because leads can take time to progress through the sales process.

These limitations were retained rather than artificially corrected so that the analysis reflects the actual characteristics of the source data.

