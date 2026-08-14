# 🍫 Wonka's Sweet Distribution Co. — Sales & Profitability Analysis

A multi-page Power BI project analyzing sales, profit, and target performance for a candy distribution business, built on **10,194 transaction records** across 5 factories, 15 products, and 3 product divisions in the US and Canada. The project was built for a contest/class assignment and includes a 10-minute board-style presentation walkthrough.

---

## 🎯 Business Problem

A candy distributor needs a single source of truth to answer:

- Are we hitting revenue targets, and by how much are we over or under?
- Which division, product, region, and factory drive the most revenue and profit?
- How does performance break down geographically, down to the city level?
- How efficiently is production load distributed across our 5 factories?
- What does profitability look like month over month, and by country?

---

## 🧰 Tools Used

- **Power BI Desktop** — data modeling, DAX, and multi-page report design
- **Power Query** — table relationships and load
- **DAX** — KPI and profit-margin measures
- **Power BI AI visuals** — Key Influencers and Smart Narrative

---

## 🗂️ Data Model

Star-schema style model built from 5 source tables plus a supporting geography table:

| Table | Role |
|---|---|
| `Candy_Sales` | Fact table — 10,194 order line items (Sales, Units, Gross Profit, Cost, Order/Ship Date, Region, City) |
| `Candy_Products` | Dimension — 15 products, linked to Division, Factory, Unit Price, Unit Cost |
| `Candy_Factories` | Dimension — 5 factories with Latitude/Longitude for mapping |
| `Candy_Targets` | Dimension — revenue Target per Division |
| `uszips` | Supporting geography table for mapping city-level revenue |

**Relationships:** `Candy_Products` → `Candy_Sales` (one-to-many on Product ID), `Candy_Products` → `Candy_Factories` (many-to-one on Factory), `Candy_Sales` → `Candy_Targets` (many-to-one on Division), `Candy_Sales` → `uszips` (many-to-one for geographic mapping).

---

## 📊 Report Pages

**1. Executive Summary**
Top-level KPI cards (Total Revenue, Total Units, Profit Margin %, Target Variance, Total Cost, Total Target, Total Profit, Target Variance %), Actual Revenue vs. Target by Division chart, and two Power BI AI visuals — **Key Influencers** (what drives Total Profit up or down) and **Smart Narrative** (auto-generated text summary of top findings), plus button navigation to every other page.

**2. Deep Dive Analysis**
A **Decomposition Tree** that lets a viewer drill Total Revenue down interactively — Country/Region → Division → City — without needing to build a separate chart for every combination.

**3. Geographic Sales Analysis**
Total Revenue by Region bar chart, a **Customer Revenue by Location** map (bubble-sized by revenue), and a separate **Factory Locations** map, alongside city/country/factory count KPIs.

**4. Financial Profile Analysis**
Total Revenue and Total Profit by Month (dual-axis trend), Total Profit by Region, Total Profit by Month, and a Division × Country matrix breaking out Revenue, Profit, and Profit Margin % side by side for Canada vs. United States.

**5. Factory Operations & Load Distribution**
Factory Load Distribution donut and Revenue by Factory bar chart, showing how order volume and revenue are concentrated across the 5 factories.

**6. Dashboard**
A restyled, single-page executive summary in a distinct purple/gold "Maven Analytics" theme — condenses the KPIs, revenue-vs-target, factory load, location map, sales-vs-target gauge, and a top-products table into one boardroom-ready view.

**7. Tooltip**
A dedicated tooltip page (Total Revenue by Product Name pie chart) that appears on hover across other visuals, giving product-level context without cluttering the main pages.

---

## 📐 Key Measures

```DAX
Total Revenue = SUM(Candy_Sales[Sales])
Total Profit = SUM(Candy_Sales[Gross Profit])
Total Cost = SUM(Candy_Sales[Cost])
Profit Margin % = [Total Profit] / [Total Revenue]
Total Target = SUM(Candy_Targets[Target])
Target Variance = [Total Revenue] - [Total Target]
Target Variance % = [Target Variance] / [Total Target]
```

---

## 📈 Key Insights

- **Total Revenue reached 141.78K against a 45K target** — a variance of **+96.78K (215.07%)**, meaning the business more than tripled its target.
- **Chocolate is the dominant division**, generating **131.7K in revenue (92.9% of total)** and **88.8K in profit**, dwarfing Other (9.7K) and Sugar (just 427).
- **Overall profit margin sits at 65.9%**, on total revenue of 141.78K against 48.3K in cost.
- **The United States drives 97.9% of revenue** (138.8K) versus Canada's 2.95K — the business is heavily US-concentrated.
- **Pacific is the strongest region** (46.3K revenue), followed by Atlantic (41.2K), Interior (32.0K), and Gulf (22.2K) — a roughly 2x spread between the strongest and weakest region.
- **Wonka Bar - Triple Dazzle Caramel is the top-selling product** (28.5K revenue), narrowly ahead of Scrumdiddlyumptious (27.9K) and Milk Chocolate (26.9K) — the top 5 chocolate bars together account for the large majority of total revenue.
- **Factory load is highly concentrated**: Wicked Choccy's handles 55.4% of volume and Lot's O' Nuts 41.0%, while the remaining three factories combined handle under 4% — a potential single-point-of-failure risk worth flagging operationally.
- **Revenue and Total Target are negatively correlated** (per the AI Key Influencers visual) — divisions with the steepest revenue growth are pulling further ahead of their fixed targets rather than tracking them.

---

## ⚙️ Power BI Concepts Demonstrated

- Star-schema data modeling across 5 related tables
- DAX measures for KPIs, margins, and variance
- Decomposition Tree for ad-hoc interactive drill-down
- AI visuals: Key Influencers and Smart Narrative
- Filled/bubble map visuals for geographic analysis
- Button-based page navigation (custom nav bar on Executive Summary)
- Custom tooltip page
- Multiple report themes across pages (default theme vs. Maven Analytics purple/gold executive dashboard)
- Cross-filtering matrix (Division × Country with nested Total Revenue/Profit/Margin columns)

---

## 📁 Repository Contents

| File | Description |
|---|---|
| `Contest.pbix` | Power BI project file |
| `Candy_Sales.csv` | Fact table — order-level transactions |
| `Candy_Products.csv` | Product dimension table |
| `Candy_Factories.csv` | Factory dimension table with coordinates |
| `Candy_Targets.csv` | Division-level revenue targets |
| `candy_distributor_data_dictionary.csv` | Field-level data dictionary for all source tables |

---

## 👤 Author

**Sai Sagar**
