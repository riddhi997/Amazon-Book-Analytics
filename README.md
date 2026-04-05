# Amazon-Book-Analytics
### Pricing, Trends & Historical Context

An end-to-end data engineering and analytics project on 700,000+ Amazon 
book and review records — investigating how book pricing, category 
popularity, and author gender dynamics have evolved across 12 decades 
of publishing (1900s–2020s).

Built with a database-first approach: all analysis executed via SQL 
queries on a DuckDB columnar database, with external API integration 
for author gender inference.

📊 [View Full Presentation](presentation.pdf)

---

## Research Questions

**Q1** — Which books and categories were most popular by decade, 
and how did popularity evolve over time?

**Q2** — Which book categories command premium prices, and how 
stable are these price hierarchies across decades?

**Q3** — How does author gender distribution vary across categories, 
and does gender composition correlate with pricing?

---

## Key Findings

- **Post-1990 inflection point:** digital reviewing created a 10× 
  signal shift in what "popular" means in the dataset
- **Technical categories command a 3× price premium** over leisure 
  content — Technology & Engineering ($52.54) vs Pets ($8.76)
- **Price stability ≠ price level:** Poetry (CV 0.037) is cheap and 
  stable; Design (CV 0.365) is similarly priced but volatile
- **Scarcity premium:** female authors command higher prices in 
  Computers, Law, and Language Arts — all statistically significant
- **Sample size is the critical lens:** several apparently large 
  gender price gaps are statistically insignificant (p > 0.05) 
  due to tiny female author counts

---

## Project Structure

**Phase 1: Data Preparation**

| Notebook | Description | Output |
|----------|-------------|--------|
| `01_data_cleaning.ipynb` | Clean prices, scores, extract year/decade/author fields | `books_clean.csv`, `reviews_clean.csv` |
| `02_api_gender_data.ipynb` | Genderize.io API integration — gender inference for top 50 authors | `author_genders.csv` |
| `03_database_setup.ipynb` | Build DuckDB database (3-table schema) | `amazon_books.ddb` |

**Phase 2: Analysis** *(all read from `amazon_books.ddb`)*

| Notebook | Research Question |
|----------|-------------------|
| `04_popularity_analysis.ipynb` | Which books and categories were most popular by decade? |
| `05_price_stability_analysis.ipynb` | Which categories command premium prices, and how stable are they? |
| `06_gender_price_analysis.ipynb` | How does gender distribution vary across categories and correlate with pricing? |

**Other files**

| File | Description |
|------|-------------|
| `amazon_books.ddb` | DuckDB database — skip Phase 1 and use directly |
| `database_schema.md` | Full schema documentation |
| `requirements.txt` | Python dependencies |
| `presentation.pdf` | Full project presentation |

## Quick Start

> **Skip to Phase 2** if you're using the included `amazon_books.ddb` 
> file directly.

### Phase 1: Data Preparation

**Step 1: Get the raw data**

Download from Kaggle and place in a folder called 
`amazon_books_raw_data/`:
- [Books dataset](https://www.kaggle.com/datasets/mohamedbakhet/amazon-books-reviews?select=books_data.csv) 
  — `books_data.csv` (165,744 records)
- [Reviews dataset](https://www.kaggle.com/datasets/mohamedbakhet/amazon-books-reviews?select=Books_rating.csv) 
  — `Books_rating.csv` (481,164 records)

**Step 2: Install requirements**
```bash
pip install -r requirements.txt
```

**Step 3: Run notebooks in order**
1. `01_data_cleaning.ipynb`
2. `02_api_gender_data.ipynb` 
3. `03_database_setup.ipynb`

### Phase 2: Analysis

Run in any order — all read from `amazon_books.ddb`:

4. `04_popularity_analysis.ipynb`
5. `05_price_stability_analysis.ipynb`
6. `06_gender_price_analysis.ipynb`

---

## Database Schema

| Table | Rows | Description |
|-------|------|-------------|
| `books` | 165,744 | Core catalog — titles, categories, authors, dates |
| `reviews` | 481,164 | Ratings and pricing data |
| `author_genders` | 50 | Gender inference via Genderize.io API |

**Total records: 647,858 | Period: 1900s–2020s**

Full schema documentation: [database_schema.md](database_schema.md)

---

## Data Sources

- [Amazon Books Dataset — Kaggle](https://www.kaggle.com/datasets/mohamedbakhet/amazon-books-reviews?select=Books_rating.csv)
- [Genderize.io API](https://genderize.io/) — author gender inference

---

## Tech Stack

Python · DuckDB · SQL · REST API · Pandas · Matplotlib · Seaborn · 
Jupyter Notebooks

---

## Author

**Riddhi Kedia**  
MSc Data Science & AI — Barcelona Technology School  
[linkedin.com/in/rkedia97](https://linkedin.com/in/rkedia97) · 
riddhi997@gmail.com
