# 🏅 Olympics Analytics Dashboard

An end-to-end data analytics project built on 128 years of Olympic Games data (1896–2024), including Paris 2024. All data cleaning and analysis is done purely in SQL. Python is used only for rendering the interactive dashboard.

## 📋 What This Project Does

Combines two Kaggle datasets — historical Olympic medals from 1896 to 2022, and the complete Paris 2024 dataset — into a unified SQLite database. From there, SQL views handle all cleaning, deduplication, and standardisation. Nine analytical queries power an interactive Plotly Dash dashboard with real-time filters.

## 📁 Project Structure

```
SQL PROJECT/
├── olympics_sql_dashboard.ipynb   # Main notebook
├── historical/                    # Historical medals 1896–2022 (CSVs)
├── paris2024/                     # Paris 2024 full dataset (CSVs)
│   └── results/                   # Per-sport detailed results (45 disciplines)
├── README.md                      # This file
└── kaggle.json                    # Kaggle API credentials (not committed)
```

## 🛠️ Stack

- **Data:** 📊 Kaggle API (piterfm datasets)
- **Storage:** 🗄️ SQLite in-memory database
- **Cleaning & Analysis:** 🔍 Pure SQL (`CREATE VIEW`, `WITH`, `ROW_NUMBER()`, `CASE`, `UNION ALL`)
- **Dashboard:** 🎨 Python + Plotly Dash
- **Charts:** 📈 Plotly Express + Plotly Graph Objects

## 🎛️ Dashboard Features

**8 KPI Cards**  
Total medals, unique athletes, countries, sports, editions, and gold/silver/bronze counts across all time.

**5 Interactive Filters**  
Year range slider (1896–2024), country dropdown, sport dropdown, medal type, and season (Summer/Winter). All filters update in real-time.

**9 Charts:**
1. 📅 **Medals over time** — Stacked bar by medal type
2. 🌍 **Medal share by country** — Donut chart (top 8)
3. 🏆 **Top 15 countries** — Stacked gold/silver/bronze breakdown
4. 🏋️ **Top 15 sports by medals** — Colored by country diversity
5. 👫 **Gender participation trend** — Area chart over time
6. ☀️❄️ **Summer vs Winter medals** — Line chart
7. 🥇 **Medal type distribution** — Donut
8. 🗼 **Paris 2024 country medal table** — Current games spotlight
9. 🗼 **Paris 2024 medals by sport** — Per-discipline breakdown

## 💡 SQL Design Decisions

All data cleaning happens in `CREATE VIEW` statements, not in Python. This keeps the transformation layer declarative and auditable. Key techniques used:

- **Deduplication:** `ROW_NUMBER() OVER (PARTITION BY ...)` to identify and keep only the first occurrence of each medal record
- **Null handling:** `COALESCE` to provide sensible defaults
- **Text standardisation:** `UPPER(TRIM(...))` for consistent formatting
- **Year extraction:** `SUBSTR(slug_game, -4)` to pull the year from game slugs like `'paris-2024'`
- **Data unification:** `UNION ALL` combining historical and Paris 2024 data into a single `all_olympics` view
- **Security:** Parameterized queries (`?` placeholders) in all Dash callbacks to prevent SQL injection

Three main views power everything:
- `clean_historical` — Deduplicated, standardised historical medals
- `clean_paris2024` — Cleaned Paris 2024 medals with matching schema
- `all_olympics` — UNION of both for unified querying

## 📥 Data Sources

- [**Paris 2024 Olympic Summer Games**](https://www.kaggle.com/datasets/piterfm/paris-2024-olympic-summer-games) — Athletes, medals, events, schedules, venues
- [**Olympic Games Medals 1896–2018**](https://www.kaggle.com/datasets/piterfm/olympic-games-medals-19862018) — Historical medals and results

## 🚀 Setup & Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/sql-olympics-dashboard.git
   cd sql-olympics-dashboard
   ```

2. **Get your Kaggle API token**
   - Go to [kaggle.com](https://www.kaggle.com) → **Profile** → **Settings** → **API** → **Create New Token**
   - This downloads `kaggle.json`

3. **Place your credentials**
   ```bash
   cp ~/Downloads/kaggle.json ~/.kaggle/kaggle.json
   chmod 600 ~/.kaggle/kaggle.json
   ```

4. **Install dependencies**
   ```bash
   pip install kaggle dash plotly pandas
   ```

5. **Run the notebook**
   - Open `olympics_sql_dashboard.ipynb` in Jupyter
   - Run all cells in order
   - The dashboard will be available at `http://localhost:8050`

## 📊 Key Insights

The dashboard reveals patterns across 128 years:

- **Participation growth:** More countries and sports as Olympics evolved
- **Gender inclusion:** Sharp increase in female medal counts post-2000
- **Winter vs Summer:** Clear seasonal split in medal distribution
- **Host advantage:** Paris 2024 showed competitive depth across 45 sports
- **Dominant nations:** Historical leadership and emerging powerhouses

## 🔒 Security Notes

- Kaggle credentials are excluded from version control (`.gitignore`)
- All database queries use parameterized statements to prevent injection
- SQLite runs in-memory; no data persists after the notebook session ends

## 📝 License

This project is for educational purposes. Data sourced from Kaggle under their dataset licenses.

---

Built with ❤️ for data enthusiasts who love the Olympics 🏅
