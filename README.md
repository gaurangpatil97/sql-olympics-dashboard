# 🏅 Olympics Analytics Dashboard

An end-to-end data analytics project built on **128 years of Olympic Games data (1896–2024)**, including a dedicated spotlight on **Paris 2024**. This project demonstrates a **"SQL-First" architecture**, where all data transformation, cleaning, and analysis are performed within the database layer, while Python serves purely as the visualization engine.

## 📘 Project Presentation

> 🎥 For a detailed walkthrough of the methodology, visuals, and insights, view the [PROJECT DEMO PPT](./Olympics_Analytics_Dashboard.pdf)

---

## 📋 Project Overview

This dashboard unifies two massive Kaggle datasets into a single, high-performance analytical tool:
1. **Historical Olympics (1896–2022):** Medals, athletes, and host information.
2. **Paris 2024:** Real-time data including medals, events, and schedules.

All data is ingested into an **in-memory SQLite database**, cleaned via **SQL Views**, and presented through an interactive **Plotly Dash** application.

## 🛠️ The Tech Stack

- **Data Ingestion:** Programmatic Kaggle API Integration
- **Database:** SQLite (Stateless In-Memory execution)
- **Transformation:** Pure SQL (`CREATE VIEW`, `WITH`, `ROW_NUMBER()`, `UNION ALL`)
- **Visualization:** Python + Plotly Dash
- **Security:** Parameterized SQL queries to prevent injection attacks

## 📁 Repository Structure

```text
SQL PROJECT/
├── historical/                        # Local folder for 1896–2022 CSVs (Git ignored)
├── paris2024/                         # Local folder for Paris 2024 CSVs (Git ignored)
├── .gitignore                         # Prevents large datasets & API keys from being pushed
├── Olympics_Analytics_Dashboard.pptx  # Project presentation deck
├── olympics_sql_dashboard.ipynb       # Main source code (ETL, SQL, and Dashboard)
└── README.md                          # Project documentation
```

## 🔍 SQL Engineering Highlights

Unlike traditional "Pandas-heavy" notebooks, this project pushes all logic to the database layer to ensure scalability and auditability:

- **Deduplication:** Uses `ROW_NUMBER() OVER (PARTITION BY ...)` to ensure medal records are unique across both datasets.
- **Standardisation:** Unifies inconsistent gender labels (`MALE`, `MEN`, `M`) and country codes across 100+ years of data.
- **Year Extraction:** Uses `SUBSTR(slug_game, -4)` to reliably parse game years from slugs like `cortina-d-ampezzo-1956`.
- **Unified Schema:** Uses `UNION ALL` to merge disparate historical and modern tables into a single `all_olympics` view.
- **Data Security:** Parameterized queries (`?` placeholders) in all Dash callbacks to safely handle user-driven filters.

## 📊 Dashboard Features

The application features **8 KPI Cards** and **9 Interactive Charts**:

1. 📅 **Medals Over Time** — Stacked bar chart showing the growth of the Games from 1896 to 2024
2. 🌍 **Medal Share** — Donut chart of top-performing nations all-time
3. 🏆 **Global Rankings** — Stacked breakdown of Gold, Silver, and Bronze by country
4. 🏋️ **Sports Diversity** — Top 15 sports mapped against country participation breadth
5. 👫 **Gender Trends** — Area chart showing the historic rise of female participation post-2000
6. ☀️❄️ **Seasonality** — Comparison of Summer vs. Winter Games medal volumes
7. 🥇 **Medal Distribution** — Overall Gold / Silver / Bronze split
8. 🗼 **Paris 2024 Spotlight** — Dynamic medal table for the most recent Games
9. 🏊 **Paris 2024 Sports** — Medal distribution by discipline across all 45 sports

**5 Interactive Filters:** Year range slider (1896–2024), Country, Sport, Medal type, Season — all updating every chart in real-time.

## 🚀 Setup & Installation

1. **Clone the repo**
```bash
   git clone https://github.com/patilgaurang0907/sql-olympics-dashboard.git
   cd sql-olympics-dashboard
```

2. **Configure Kaggle API**
   - Go to [kaggle.com](https://www.kaggle.com) → Settings → API → Create New Token
   - Place `kaggle.json` at `~/.kaggle/kaggle.json`
   - On Windows: `C:\Users\YourName\.kaggle\kaggle.json`

3. **Install dependencies**
```bash
   pip install kaggle dash plotly pandas
```

4. **Launch**
   - Open `olympics_sql_dashboard.ipynb` and run all cells
   - Access the dashboard at `http://localhost:8050`

## 📝 License

This project is for educational purposes. Data is sourced from Kaggle under the licenses provided by the dataset authors.

---

Built by **Gaurang Patil**
