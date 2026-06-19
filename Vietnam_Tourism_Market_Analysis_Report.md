# Vietnam Tourism Market Analysis Report
**By Hoang Nguyen** · nguy1462@purdue.edu

> 📊 **Excel Database** → [View on SharePoint](https://purdue0-my.sharepoint.com/:x:/g/personal/nguy1462_purdue_edu/IQBURPkndi0HSLbdBjILJkcuAQ6elPsq5K-rbgGmlmiZG2Q?e=5Hb9by)  
> 📽️ **Presentation Slides** → [View on SharePoint](https://purdue0-my.sharepoint.com/:p:/g/personal/nguy1462_purdue_edu/IQBcbo2S1dO6QYF7EHv4TEyNAenRjOXM6OKkCT0QJOFzDLk?e=1wa9ED)  
> 🎥 **Stakeholder Meeting Recording** → [Watch on Google Drive](https://drive.google.com/file/d/11N9kEV_vHFABT3HaQroR4Q_5E27vxMds/view?usp=sharing)

---

## Table of Contents
1. [Background](#1-background)
2. [Challenges & Business Questions](#2-challenges--business-questions)
3. [Approach](#3-approach)
4. [Data Gathering](#4-data-gathering)
5. [Data Cleaning](#5-data-cleaning)
6. [Descriptive Analysis & Pivot Tables](#6-descriptive-analysis--pivot-tables)
7. [Data Visualization](#7-data-visualization)
8. [Strategic Recommendations](#8-strategic-recommendations)
9. [Limitations & Enhancement Ideas](#9-limitations--enhancement-ideas)
10. [References](#10-references)

---

## 1. Background

Vietnam's tourism sector has grown into one of the country's most significant economic pillars, achieving a landmark **"triple growth"** across its three core pillars — international visitors, domestic travel, and revenue.

**2025 highlights:**
- **21.5 million** foreign arrivals (+22% YoY — 5% above the global average, 8% above Asia-Pacific)
- **135.5 million** domestic trips served
- Revenue exceeding **1 quadrillion VND (~$38 billion USD)**
- Tourism now contributes **~8.8% of GDP**, with a 2030 target of 13–14%

The growth was driven by effective state management, timely policy advisory, and strategic direction from the Vietnam National Authority of Tourism (VNAT), alongside notable milestone events: the 50th anniversary of National Reunification, the 80th anniversary of National Day, and the 95th founding anniversary of the Communist Party of Vietnam.

Vietnam also saw international recognition, with **Lo Lo Chai** and **Quynh Son** named among the world's Best Tourism Villages by the UN.

**2026 national targets:** 25 million foreign arrivals · 150 million domestic tourists · 1.12 quadrillion VND in revenue

---

## 2. Challenges & Business Questions

### Industry-Level Challenges
- Underinvestment in secondary destinations beyond HCM, Hanoi, and Da Nang
- Workforce gaps in language proficiency and professional service skills
- Outdated 2017 Tourism Laws restricting investment, new accommodation types, and community-based tourism
- Environmental pressure: overcrowding, pollution, restrictions on cultural sites
- Complex regulations creating friction for online booking platforms and foreign investors

### Business Questions — Scoped to A&K's Ho Chi Minh City Branch

| # | Question | Method |
|---|----------|--------|
| 1 | Which destinations are most popular (beyond the central hubs)? | Pivot Table 1 — rank by traveler count |
| 2 | How does seasonality affect destination popularity? | Pivot Table 1 — min/max by month |
| 3 | Which countries send the most visitors, and in which months? | Pivot Table 2 — market × month |
| 4 | Which customer types visit most often and are most satisfied? | Pivot Table 3 — segment × satisfaction |
| 5 | Where do those customer types travel within Vietnam? | Pivot Table 6 — segment × destination |
| 6 | What tour types generate the highest satisfaction? | Pivot Table 4 — tour type × satisfaction |
| 7 | What is the ideal trip budget? | Pivot Table 5 — price × satisfaction |

---

## 3. Approach

**Step 1 — Customer & transaction analysis:** Scrape and analyze booking data to identify which destinations, activities, and services generate the most revenue and satisfaction — pinpointing where further investment would yield returns.

**Step 2 — Market dynamics analysis:** Compare destination popularity, seasonality, and source market trends to determine when and where to direct marketing spend and what services to prioritize.

**Step 3 — Strategic output:** Translate findings into data-driven sales and marketing proposals aligned with both government tourism targets and A&K's growth objectives in the Vietnam territory.

---

## 4. Data Gathering

Two complementary datasets were used — one micro-level and one macro-level:

### Micro Dataset — Customer Booking Transactions
**Source:** [Vietnam Tour Bookings — Kaggle (Jax Teller)](https://www.kaggle.com/datasets/ngchno/vietnam-tour-bookings)

A synthetic, public-domain dataset simulating tour booking records. Used for customer segment, destination preference, tour type, pricing, and satisfaction analysis. Commercial booking data from agencies is proprietary, so this synthetic dataset was chosen to align with the data pipeline and dashboard architecture standards used by real tour operators.

### Macro Dataset — International Arrivals by Market
**Source:** [VNAT Official Statistics Portal](https://vietnamtourism.gov.vn/en/statistic/international?year=2025&period=t1)

Monthly international arrival counts by country for all of 2025, scraped from VNAT's published government reports using Java in collaboration with a Computer Science major. This dataset was used to identify market segments and macro-level seasonality trends to inform market diversification and targeted outreach strategies.

---

## 5. Data Cleaning

> 📎 Full cleaned database: [Excel File on SharePoint](https://purdue0-my.sharepoint.com/:x:/g/personal/nguy1462_purdue_edu/IQBURPkndi0HSLbdBjILJkcuAQ6elPsq5K-rbgGmlmiZG2Q?e=5Hb9by)

### Micro Dataset (Kaggle)

**Column removal:** Dropped `booking_date`, `booking_id`, `customer_id`, and `payment_method` — none contributed to answering the tourism trend questions.

**Duplicate removal:** Used Excel's built-in Remove Duplicates to eliminate repeat records and prevent skewed metrics.

**Destination name inconsistencies:** City names had encoding errors and inconsistent naming conventions introduced during the Kaggle download (e.g., `"Hà Nội"` rendered as `"H√† N·ªôi"`; `"TP HCM"` vs `"TP. HCM"`). Corrected systematically using Excel's Find & Replace.

**Discount rate formatting:** Standardized all discount values to a uniform percentage format rounded to 2 decimal places.

**Missing data — `satisfaction` column:**
- Missing values always co-occurred with `Booking Status: Cancelled` and `Revenue: 0`
- Since missingness correlates to an observed variable (booking status), not to the satisfaction score itself → classified as **Missing at Random (MAR)**
- Resolution: **Listwise deletion** — no meaningful satisfaction value can be imputed for trips that were never taken
- After deletion, `booking_status` contained only `"Completed"` and was itself dropped as a now-redundant column

**Missing data — categorical columns** (`customer_segment`, `channel`, `destination`, `tour_type`):
- All gaps were categorical → numerical imputation methods (mean, median, mode, interpolation) were not applicable
- The dataset follows a time-series structure ordered by `travel_date`
- Resolution: **Last Observation Carried Forward (LOCF)** — preserves trend consistency across adjacent time periods

### Macro Dataset (VNAT)

Restructured the wide-format scraped table (market × month columns) into a long format (`Market`, `Date`, `Month`, `Visitors`) for Tableau compatibility.

---

## 6. Descriptive Analysis & Pivot Tables

### Pivot Table 1 — Destination Popularity & Seasonality
**Structure:** Rows = destinations · Columns = months · Values = traveler count · Filter = year (All / 2022–2025)

**Findings:**
- Top 3 destinations across all years: **Phu Quoc, Da Nang, Nha Trang** — all coastal cities
- Conditional formatting (green = peak month, yellow = lowest month) confirmed that **seasonality significantly affects coastal popularity**
- Coastal areas (Phu Quoc, Da Nang, Nha Trang, Ha Long) peak **June–October**; Ho Chi Minh City peaks in **Q1 and Q4**

### Pivot Table 2 — Source Markets by Month
**Structure:** Rows = source countries · Columns = months · Values = arrival count (VNAT data)

**Findings:**
- Most visitors from **Asia** arrive in **March**
- **Americas and Oceania** peak in **January**
- **Europeans** peak in **November**
- **Africans** peak in **August**

### Pivot Table 3 — Customer Segments by Satisfaction
**Structure:** Rows = satisfaction bands (2–3, 3–4, 4–5) filtered to returning customers · Columns = customer segments

**Findings:**
- **Families** and **young professionals** are the most frequent visitor segments
- **Students** showed the highest enjoyment rate: **66.24%** rated their trip 4–5 out of 5

### Pivot Table 6 — Customer Segments by Destination
**Structure:** Rows = customer segments · Columns = destinations · Values = traveler share %

**Findings:**
- **Families (~12%)** and **young professionals (~13%)** most frequently visit **Phu Quoc**
- **Students (~13.5%)** prefer **Da Nang**
- **Corporate travelers (~12.8%)** concentrate in **Phu Quoc** for business trips

### Pivot Table 4 — Tour Types by Satisfaction
**Structure:** Rows = satisfaction bands · Columns = tour types

**Findings:**
- Most booked: **beach** and **cultural** tours
- Highest satisfaction conversion: **adventure tours** at **68.85%** rated 4–5

### Pivot Table 5 — Pricing vs. Satisfaction
**Structure:** Rows = satisfaction bands · Columns = avg. base price, avg. discount rate, avg. discounted price

**Findings (highest-rated trips):**
- Base price: **2,771,428 VND (~$106.60 USD/person/day)**
- Discount rate: **13.07%**
- Discounted price: **2,356,958 VND (~$90.66 USD/person/day)**

> **Notable insight:** Trips with lower prices and higher discount rates received *worse* ratings — suggesting that in today's tourism market, **experience quality outweighs cost savings** as a satisfaction driver.

---

## 7. Data Visualization

Six charts were built using Excel's Recommended Charts and Format Pane to visually communicate each finding set. No chart was produced for the pricing section, as the multi-digit VND values across many categories would have made a single visual difficult to interpret clearly.

The key Tableau visualization — an **interactive choropleth map of Vietnam's 2025 inbound tourism flows** segmented by source market and equipped with a dynamic month-range filter — is available via the links at the top of this report.

---

## 8. Strategic Recommendations

**Stakeholder:** Mr. Shawn Johnson, Senior Vice President of Trade Sales, Abercrombie & Kent USA — responsible for revenue from third-party travel advisors, territory ROI, and global brand expansion across A&K's luxury portfolio.

**Core message to stakeholder:** Vietnam's inbound tourism market extends far beyond A&K's current American and European client base. The data shows significant, underserved demand from Chinese, Korean, Taiwanese, and Southeast Asian markets — demand that, in aggregate, could exceed the luxury segment in volume and potentially in revenue. Capturing it requires the right product, the right timing, and the right partnerships.

### Narrative & Action Table

| Key Question | Insight | Recommended Actions |
|---|---|---|
| **Which destinations are most popular?** | Coastal cities dominate: Phu Quoc, Da Nang, Nha Trang, Ha Long, Hoi An | Specialize coastal itineraries over broad cross-country trips. Proposed tour: *"Vietnam: Coastal Sanctuary"* — a focused coastal version of the "Highlights of Vietnam" format. Scale beach/bay content across social media. Recruit experienced local guides from coastal cities. |
| **How does seasonality affect popularity?** | Coastal areas peak Jun–Oct; HCM peaks Q1 and Q4 | **Seasonal campaign calendar:** Q1 → city hubs (HCM, Hanoi); Q2 → countryside/highlands; Q3 → coastal region (peak push); Q4 → HCM Christmas/NYE atmosphere. Proposed tour: *"The Christmas Hymn of Saigon Notre Dame Cathedral."* Incorporate off-season deals for shoulder periods. |
| **Where do visitors come from?** | China (~25%), East Asia (~30%), Southeast Asia (~13%), USA (~4%), Europe (~5%) | Adopt a **DMC-as-a-Service model** — shift from B2C to B2B by formalizing contracts with travel advisors in top source markets for stable recurring revenue. Coordinate with A&K's China branch on dual-market itineraries (e.g., *"Hong Kong to Hanoi: The Interwoven Cultures"*). Leverage Vietnam's 45-day visa-free extension to create longer European itineraries. Use Phu Quoc's 30-day visa exemption to ease the American booking process. Target India (wedding/MICE demand) and Russia (rerouted tours) as emerging growth markets. |
| **Which customer types visit most?** | Families (bulk), young professionals (growing), students (highest satisfaction) | Launch *"Vietnam Family Adventure"* and *"Southeast Asia Family Adventure"* packages with UGC-driven social content. Design urban, modern tours for young professionals at premium prices (MICE, bleisure, luxury cruising). Explore faculty-led study treks for students at MICE-adjacent pricing — not discounted, but sized to build loyalty and recurring bookings. |
| **Where do those segments travel?** | All top segments gravitate toward coastal cities | Coastal family packages: eco-focused, nature-escape, beach-friendly. Young professional packages: *bleisure*, workation, sound-proof conference facilities, high-end F&B, cruising. |

---

## 9. Limitations & Enhancement Ideas

- **Kaggle dataset quality:** Origins are unclear and some category distributions show unusual patterns → future versions should source licensed, real-world datasets from industry providers
- **Dashboard completeness:** Current charts are standalone → combine into a unified branded dashboard using A&K's brand color kit; separate stacked area graphs by market for clarity
- **"Young professional" segment is too broad** → segment further by industry, company type, and trip purpose to better personalize product design
- **Student segment reach:** Difficult for a luxury brand like A&K to connect authentically with students → research specialized Vietnam student tour providers and identify high-demand universities/high schools as institutional partners
- **No predictive layer** → build revenue forecast models to estimate the impact of these proposals before committing to full implementation

---

## 10. References

Bao Chinh Phu. "Viet Nam targets to lure 25 million foreign visitors in 2026." *SOCIALIST REPUBLIC OF VIET NAM Government News*, 26 December 2025. https://en.baochinhphu.vn/viet-nam-targets-to-lure-25-million-foreign-visitors-in-2026-111251226144713535.htm

Singh, Sudhanshu. "Vietnam's Tourism Industry: Growth Trajectory, Policies, And Opportunities." *Vietnam Briefing*, 24 September 2025. https://www.vietnam-briefing.com/news/vietnams-tourism-growth-policies-opportunities.html/

VNA. "Vietnam targets 25 million international visitors for 2026." *Vietnam+ (VietnamPlus)*, 24 December 2025. https://en.vietnamplus.vn/vietnam-targets-25-million-international-visitors-for-2026-post334882.vnp
