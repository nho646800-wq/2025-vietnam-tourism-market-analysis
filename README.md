# 🇻🇳 Vietnam Tourism Market Analysis
### Strategic Market Intelligence for Abercrombie & Kent – Vietnam Territory

> **Role:** Lead Strategic Data Analyst & Consultant  
> **Stakeholder:** Mr. Shawn Johnson, Senior Vice President of Trade Sales, Abercrombie & Kent  
> **Deliverable:** Data-driven market entry and sales growth recommendations for A&K's Ho Chi Minh City branch

---

## 📁 Repository Contents

| File | Description |
|------|-------------|
| [`Vietnam_Tourism_Market_Analysis_Report.md`](Vietnam_Tourism_Market_Analysis_Report.md) | Full report |
| [`data/VNAT_International_Arrivals_2025.xlsx`](data/VNAT_International_Arrivals_2025.xlsx) | Macro dataset — VNAT international arrivals by country × month, 2025 |
| [`data/VNAT_Tableau_Data.xlsx`](data/VNAT_Tableau_Data.xlsx) | Long-format VNAT data restructured for Tableau |
| [`Detailed_Project_Excel_File.xlsx`](Detailed_Project_Excel_File.xlsx) | Full project Excel file with all sheets - pivot tables, visuals, raw, and clean datasets |
| [`Presentation Slides.pptx`](Presentation Slides.pptx) | Full PowerPoint Presentation slideshow created to accompany the meeting with the stakeholder |

---

## 🎯 Project Overview

Vietnam's tourism sector hit **21.5 million international arrivals in 2025** (+22% YoY), contributing ~8.8% of GDP. This analysis was scoped specifically to A&K's Vietnam branch — a luxury travel operator — to identify **where growth opportunity lies beyond their existing American and European clientele**.

### Business Questions Addressed

1. Which destinations are most popular among foreign visitors (outside the main hubs)?
2. How does seasonality affect destination popularity?
3. Which source countries send the most tourists, and when?
4. Which customer segments visit most frequently and are most satisfied?
5. Where do those customer segments travel within Vietnam?
6. What tour types and price points yield the highest satisfaction?

---

## 🗄️ Data Sources

| Dataset | Source | Type | Method |
|---------|--------|------|--------|
| Customer booking transactions | [Kaggle – Vietnam Tour Bookings](https://www.kaggle.com/datasets/ngchno/vietnam-tour-bookings) | Micro-level synthetic dataset | Downloaded |
| International arrivals by market | [VNAT Official Statistics](https://vietnamtourism.gov.vn/en/statistic/international) | Macro government data | Scraped via Java |

---

## 🧹 Data Cleaning Methodology

**Micro dataset (Kaggle):**
- Removed non-analytical columns (booking ID, customer ID, payment method, booking date)
- Eliminated duplicates using Excel's Remove Duplicates function
- Standardized destination naming inconsistencies (e.g., encoding errors like `"H√† N·ªôi"` → `"Hà Nội"`) via Find & Replace
- Normalized discount rate formatting to 2-decimal percentage
- Identified missing `satisfaction` values as **Missing at Random (MAR)** — always co-occurring with `Booking Status: Cancelled` and `Revenue: 0` → applied **listwise deletion**
- Imputed remaining categorical nulls (`customer segment`, `channel`, `destination`, `tour type`) using **Last Observation Carried Forward (LOCF)**, appropriate given the time-series structure of the dataset

**Macro dataset (VNAT):**
- Restructured wide-format scraped table into long format for Tableau compatibility
- Validated totals against published VNAT monthly reports

---

## 📊 Key Findings

### Seasonality & Destinations
- **Top 3 destinations (2022–2025):** Phu Quoc, Da Nang, Nha Trang — all coastal cities
- Coastal areas peak **June–October**; Ho Chi Minh City peaks in **Q1 and Q4**

### Market Sources (2025 VNAT Data)
| Market | Share | Peak Month |
|--------|-------|-----------|
| China | ~25% | March (11.9%) |
| Republic of Korea | ~10% | February (10.8%) |
| Taiwan | ~6% | February (10.3%) |
| USA | ~4% | January (10.9%) |
| Japan | ~4% | August (11.1%) |
| India | ~3.5% | December (12.1%) |
| Southeast Asia (combined) | ~13% | Dec–Jan |
| Major European nations | ~5% | March–April |

### Customer Segments
- **Families** and **young professionals** make up the bulk of the market
- **Students** have the highest satisfaction rate: **66.24%** gave a 4–5/5 rating
- Families and young professionals gravitate toward **Phu Quoc**; students prefer **Da Nang**

### Tour Types & Pricing
- Most booked: **beach** and **cultural** tours
- Highest satisfaction conversion: **adventure tours** (68.85% rated 4–5)
- Optimal price point: **~$90.66 USD/person/day** (after ~13% discount from ~$106.60 base) → higher prices correlated with better experience ratings

---

## 💡 Strategic Recommendations

**1. DMC-as-a-Service Model**  
Shift from B2C to B2B by formalizing A&K Vietnam as a **Destination Management Company** — contracting stable, recurring revenue from Chinese, Korean, and Taiwanese travel advisors whose clients already peak in Q1.

**2. Seasonal Campaign Calendar**  
- Q1: City hubs (HCM, Hanoi) — targets Chinese New Year and East Asian arrivals
- Q2: Countryside/highlands
- Q3: Coastal focus (Phu Quoc, Da Nang, Nha Trang) — peak season
- Q4: HCM Christmas/NYE experience — targets European and American arrivals

**3. Cross-branch Collaboration**  
Coordinate with A&K's China branch on dual-market cultural itineraries (e.g., *"Hong Kong to Hanoi: The Interwoven Cultures"*) to drive revenue across both branches simultaneously.

**4. Segment-Specific Product Development**  
- Families: Eco-coastal itineraries, kid-friendly beach packages
- Young professionals: MICE, "bleisure," luxury cruising, workation packages
- Students: Faculty-led study treks at MICE pricing — buy loyalty at scale

**5. Market Expansion Targets**  
India (wedding/MICE demand) and Russia (rerouted tours post-suspension) are emerging growth markets with December–January peak travel to Vietnam.

---

## Additional Links

| Asset | Link |
|-------|------|
| Excel Database | [View on SharePoint](https://purdue0-my.sharepoint.com/:x:/g/personal/nguy1462_purdue_edu/IQBURPkndi0HSLbdBjILJkcuAQ6elPsq5K-rbgGmlmiZG2Q?e=5Hb9by) |
| Presentation Slides | [View on SharePoint](https://purdue0-my.sharepoint.com/:p:/g/personal/nguy1462_purdue_edu/IQBcbo2S1dO6QYF7EHv4TEyNAenRjOXM6OKkCT0QJOFzDLk?e=1wa9ED) |
| Stakeholder Meeting Recording | [Watch on Google Drive](https://drive.google.com/file/d/11N9kEV_vHFABT3HaQroR4Q_5E27vxMds/view?usp=sharing) |
| Interactive Inbound Visitors by Source Markets Tableau Viz | [View and Interact in Tableau Public](https://public.tableau.com/app/profile/hoang.nguyen2871/viz/InternationalVisitorstoVietnambyMajorSourceMarkets2025/Dashboard1) |

---

## Tools Used

`Microsoft Excel` · `Tableau` · `Java (web scraping)` · `VNAT Open Data` · `Kaggle` · `Microsoft PowerPoint`

---

## Authors

**Hoang Nguyen**  
Business Analytics · Purdue University  
nguy1462@purdue.edu

**Minh Quang Nguyen**  
Computer Science · Purdue University  
nguy1426@purdue.edu
