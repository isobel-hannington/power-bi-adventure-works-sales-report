# 📊 Power BI: Adventure Works sales report

**A three-page sales report built across Microsoft's PL-300 guided labs, from Power Query cleaning to DAX measures.**

From Week 2 of my bootcamp. Adventure Works is a fictional bike company, and the report gives its sales team an overview of sales and margin, a profit summary by financial year, and one salesperson's performance against target. These were guided labs, so I followed set instructions and the design and choice of visuals were the lab's.

## 🔎 At a glance

| | |
|---|---|
| **Tools** | Power BI Desktop (Power Query and DAX) |
| **Dataset** | Adventure Works reseller sales sample: 57,851 order lines from July 2017 to May 2020, with product, region, reseller, salesperson and target tables |
| **Bootcamp week** | Week 2, Days 3 and 4 (September 2026), Level 3 Data Technician Skills Bootcamp, Leep Talent |
| **Labs completed** | Lab 1: Get data · Lab 2: Clean, transform and load data · Lab 3: Configure a semantic model · Lab 4: Create DAX calculations · Lab 8: Design a report |
| **Type** | Guided labs from Microsoft's PL-300 course |
| **Report file** | [`adventure-works-sales-report.pbix`](adventure-works-sales-report.pbix) is the completed Lab 8 file supplied by Leep Talent.|

## 💡 Skills demonstrated

**✔️ Getting and transforming data (Power Query)**
- Connecting to source tables, removing columns and filtering rows (Labs 1 and 2)
- Expanding related tables, merging and renaming columns, and replacing an inconsistent value ("Ware House" to "Warehouse")
- Adding a custom Cost column that fills gaps with the product's standard cost
- Unpivoting a targets file from one column per month to one row per salesperson per month

**✔️ Data modelling**
- A Sales table linked to lookup tables for product, region, reseller and salesperson (Lab 3)
- A bridging table, so one salesperson can cover several regions

**✔️ DAX**
- Calculated columns that turn dates into Adventure Works' financial year, using `YEAR`, `MONTH`, `IF` and `FORMAT` (Lab 4)
- Measures with `SUM`, `DIVIDE`, `DISTINCTCOUNT` and `HASONEVALUE` for profit, margin, orders, targets and variance

**✔️ Report design**
- A combined line and column chart with two axes, stacked column, bar and clustered charts, a matrix and a multi-row card (Lab 8)
- Dropdown and list slicers and a page-level filter, so choosing a year or region updates every chart on the page

## 📗 Exercises covered

| Lab | What I did |
|---|---|
| Lab 1: Get data | Connected to Microsoft's AdventureWorksDW2020 sample database and a sales targets file, giving eight source queries in Power Query |
| Lab 2: Clean, transform and load | Shaped each table in Power Query and loaded seven tables with business-friendly names |
| Lab 3: Configure a semantic model | Set up the relationships between the Sales table and its lookup tables |
| Lab 4: Create DAX calculations | Added financial year columns and the report's measures |
| Lab 8: Design a report | Built the Overview, Profit and My Performance pages |

## 🧩 Highlights
**DAX for the financial year and profit (Lab 4)**

```dax
Year = "FY" & YEAR('Date'[Date]) + IF(MONTH('Date'[Date]) > 6, 1)

MonthKey = (YEAR('Date'[Date]) * 100) + MONTH('Date'[Date])

Profit = SUM('Sales'[Sales]) - SUM('Sales'[Cost])

Profit Margin = DIVIDE([Profit], SUM('Sales'[Sales]))

Target =
IF(
    HASONEVALUE('Salesperson (Performance)'[Salesperson]),
    SUM(Targets[TargetAmount])
)
```

`MonthKey` makes the text month labels sort in date order. `DIVIDE` returns a blank rather than an error if a total is zero, and `HASONEVALUE` means a target only shows when one salesperson is selected.

**Overview page** (filtered to FY2020)

![Overview page](images/overview.png)

Sales (columns) and margin (line) sit on separate axes, so a busy month with a poor margin stands out. Year and Region slicers update every chart.

**Profit page**

![Profit page](images/profit.png)

A matrix of orders, sales, cost, profit and margin for each financial year, with a Region slicer.

**My Performance page** (Michael Blythe, FY2019)

![My Performance page](images/my-performance.png)

A card with the year's headline numbers, and sales against target month by month.

## 📈 Results

Financial years run from July to June, and the data ends in May 2020, so FY2020 covers 11 months. All amounts are US dollars from sample data.

- **Three years in total:** sales of $77,548,570 and a profit of $999,495, a margin of 1.29%. FY2019 had the best margin, at 4.33%.
- **FY2020 grew but lost money:** sales rose to $33,139,748, but cost was higher, giving a loss of $343,416 (−1.04%). The margin was negative in July, August and September 2019, then positive from October to April.
- **Bikes drive sales but not margin:** bikes made 83% of sales but ran at a small loss, while accessories had the highest margin.
- **The US dominates:** it made $19.2 million of FY2020's $33.1 million in sales.
- **Michael Blythe beat his FY2019 target by $8,484:** sales of $8,658,484 against $8,650,000. He beat his monthly target in 5 of the 12 months.

## 🎓 Key learning outcomes

- **Compare like with like.** FY2020 has 11 months of data, so its total sales can't be compared fairly with FY2019's 12. The margins are a fairer comparison.
- **A margin is a measure, not a column.** It's recalculated for whatever is selected, so adding up monthly margins would give a meaningless total.
- **Know what "Sales" includes.** Sales reach a salesperson through the table linking them to their regions. Michael Blythe's figure is all sales in his three US regions, not only the orders he took himself, and the Director of Sales, who covers all 10 regions, shows the company total.

## 🛠️ Tools and technologies

- **Power BI Desktop:** the data model and the three report pages
- **Power Query Editor:** connecting to, cleaning and loading the data
- **DAX:** calculated columns and measures

## 📁 Repository contents

| File or folder | What it is |
|---|---|
| `adventure-works-sales-report.pbix` | The completed Lab 8 report, supplied by Leep Talent. Open it in Power BI Desktop (free, Windows). |
| `images/` | Screenshots of my lab work and the three report pages |
