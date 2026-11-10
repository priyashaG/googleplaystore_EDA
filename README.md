# App Insights Unlocked: Google Play Store Analytics

A data analytics case study on 10,841 Google Play Store app records (Kaggle `googleplaystore.csv`) plus 64,295 user reviews. It answers the 25 case-study questions (10 Basic, 10 Medium, 5 Advanced) and recommends what drives app success. The Python notebook `notebooks/Google_Play_Store_Analysis.ipynb` (Pandas, NumPy, Matplotlib, Seaborn) reproduces every answer below from the raw CSVs. Every figure comes from the data.

---

## Executive Summary

- **Apps analysed:** 9,659 unique apps (after removing 1 corrupted row and 1,181 duplicate app rows)
- **Average rating:** 4.17 (8,196 rated apps); 76.7% of rated apps score 4.0 or higher
- **Free vs paid:** 92.2% free (8,905) vs 7.8% paid (754)
- **Installs and rating:** correlation 0.04: more installs do not mean a higher rating, though apps with 10M to 100M installs average 4.36 vs 4.03 for 1K to 10K installs
- **Top categories by installs:** Game (13.5B lower-bound installs), Communication, Tools, Family, Productivity
- **Reviews:** free apps average 234K reviews vs 8.7K for paid (median 1,379 vs 89)
- **Users:** positive reviews are 68.5% for apps rated 4.4+ vs 54.0% for apps under 4.0; complaints centre on ads, updates and in-app money

---

## Dataset and Cleaning

- `googleplaystore.csv`: 10,841 rows x 13 columns. `googleplaystore_user_reviews.csv`: 64,295 rows (37,432 with a sentiment label, 865 apps).
- **Corrupted row removed:** 1 row (Life Made WI-Fi Touchscreen Photo Frame) had shifted columns (Category = 1.9).
- **Duplicates removed:** 1,181 repeated App names; the row with the most reviews was kept. **9,659 unique apps remain.**
- **Missing values:** Rating is blank for 1,463 apps (excluded from rating analyses, not filled in). The one missing Type had price 0, so it is Free. 1,228 apps list size as "Varies with device" and are excluded from size analyses.
- **Data types:** Installs (e.g. `1,000,000+`) became numbers using the lower bound of each band; Price lost the `$`; Size "k" values were divided by 1,024; Last Updated became a date; Category names were made readable.
- **Not in the data:** revenue, conversion, uninstall or retention figures, and per-app update history. Nothing in this repository claims results on those.
- Installs are bands, so install totals are lower bounds. The data is a snapshot to 8 Aug 2018.

---

## Answers to the Case-Study Questions

### Basic

| Question | Answer |
| :--- | :--- |
| Q1 Average rating | **4.17** across 8,196 rated apps (median 4.3) |
| Q2 Unique categories | **33** |
| Q3 Distribution of app sizes | Median 12 MB, mean 20.4 MB (8,431 apps with a size). 23.7% are 1 to 5 MB, 24.8% are 20 to 50 MB, 10.4% are 50 to 100 MB; none exceed 100 MB |
| Q4 Free vs paid | 8,905 free (92.2%) and 754 paid (7.8%) |
| Q5 Most common content rating | **Everyone**: 7,903 apps (81.8%), then Teen 1,036 and Mature 17+ 393 |
| Q6 Top 5 most installed apps | 20 apps share the top band (1,000,000,000+). Top 5 by reviews within it: Facebook, WhatsApp Messenger, Instagram, Messenger, Subway Surfers |
| Q7 Rated 4.0 and above | **6,287 apps** (76.7% of rated apps) |
| Q8 Average reviews, free vs paid | Free 234,421; paid 8,748 (medians 1,379 vs 89): free apps get about 27 times more reviews |
| Q9 Average size by category | Largest: Game 41.7 MB, Family 27.3, Travel and Local 24.2. Smallest: Tools 8.8, Libraries and Demo 10.6, Personalization 11.2 |
| Q10 Updated in 2018 | **6,287 apps** (65.1%); the newest date in the file is 8 Aug 2018 |

### Medium

| Question | Answer |
| :--- | :--- |
| M1 Installs vs rating | Pearson correlation **0.04** (Spearman 0.03): essentially no relationship |
| M2 Highest-rated categories | Events 4.44, Art and Design 4.36, Education 4.35, Books and Reference 4.35, Personalization 4.33 (lowest: Dating 3.98, Maps and Navigation 4.04, Tools 4.04) |
| M3 Price vs rating (paid) | Up to $1: 4.30; $1-2: 4.29; $2-5: 4.26; $5-10: 4.26; over $10: 4.13. Correlation -0.11; paid apps average 4.26 vs 4.17 for free |
| M4 Rating by content rating | Averages: Everyone 4.17, Everyone 10+ 4.23, Teen 4.23, Mature 17+ 4.12. Medians are 4.2 to 4.3 for all groups |
| M5 Genres with most 1M+ install apps | Tools 274, Action 180, Photography 173, Entertainment 154, Productivity 147 (3,398 apps have 1M+ installs) |
| M6 Average time between updates | **Not possible as asked:** each app has one Last Updated date. Alternative: average 281 days (median 96) since last update; 49% updated within 90 days, 25% not for over a year |
| M7 Size vs installs | Pearson 0.13, Spearman 0.31. Median installs rise with size: 10,000 (up to 10 MB), 100,000 (20 to 30 MB), 1,000,000 (50 to 100 MB). Size does not hurt installs |
| M8 Most reviewed apps | Facebook 78.2M (4.1), WhatsApp 69.1M (4.4), Instagram 66.6M (4.5), Messenger 56.6M (4.0), Clash of Clans 44.9M (4.6) |
| M9 Content rating, free vs paid | Everyone: 81.4% of free vs 86.6% of paid. Teen: 11.0% vs 6.9%. Mature 17+: 4.2% vs 2.4% |
| M10 Top 5 categories by installs | Game 13.5B, Communication 11.0B, Tools 8.1B, Family 6.2B, Productivity 5.8B (lower bounds) |

### Advanced

| Question | Answer |
| :--- | :--- |
| A1 Top-rated apps, reviews and installs | 271 apps are rated exactly 5.0, with a median of 4 reviews and 100 installs, so 5.0 is not a reliable quality signal. With at least 1,000 reviews, the top rated are JW Library 4.9 (923K reviews, 10M+ installs), Six Pack in 30 Days 4.9 (272K) and Tickets + PDA 2018 Exam 4.9 (197K) |
| A2 Update trend over time | Apps by last-updated year: 2014 203, 2015 448, 2016 779, 2017 1,792, 2018 6,287. Monthly counts climb through 2018 (May 690, June 911, July 2,318). This reflects the snapshot date, so no clean seasonal pattern can be separated |
| A3 Rating by install band | Up to 1,000+: 4.20; 1K-10K: 4.03; 10K-100K: 4.10; 100K-1M: 4.20; 1M-10M: 4.27; 10M-100M: 4.36; 100M+: 4.30 |
| A4 Sentiment of reviews | 35,934 labelled reviews for 816 rated apps: 64.2% positive, 13.5% neutral, 22.3% negative. Positive share rises with app rating: 54.0% (under 4.0), 61.8% (4.0 to 4.3), 68.5% (4.4+). Praise: great, love, easy, best, fun. Complaints: ads, updates, money, levels, "can't", "useless" |
| A5 Genre vs rating | Highest means (20+ rated apps): Events 4.44, Puzzle 4.37, Art and Design 4.36, Books and Reference 4.35. Lowest: Educational 3.87 (32 apps), Dating 3.98, Maps and Navigation 4.04, Tools 4.04 |

---

## Recommendations

- **Go free first:** free apps get about 27 times the reviews and nearly all installs; monetise through ads or in-app purchases.
- **Protect the rating early:** apps with 1K to 10K installs rate lowest (4.03); fix quality before pushing acquisition.
- **Prioritise demand:** Game, Communication and Tools lead installs; Education, Books and Reference and Art and Design combine high ratings with fewer apps.
- **Size is not the barrier:** the biggest apps (games) also have the most installs; keep apps lean without cutting features.
- **Keep updating and read reviews:** ads, update bugs and in-app money drive negative reviews.

---

## Repository Structure

```text
├── data/
│   ├── googleplaystore.csv
│   ├── googleplaystore_user_reviews.csv
│   └── googleplaystore_cleaned.csv
├── notebooks/
│   └── Google_Play_Store_Analysis.ipynb
├── screenshots/
│   └── google_play_dashboard.png
├── presentation/
│   └── Google Play Store Analytics.pptx
└── README.md
```


---

## Limitations

- **Association, not causation.** Results describe patterns in an August 2018 snapshot.
- **Installs are bands,** so totals and averages are approximate.
- **Sentiment covers 816 apps** (about 8% of the catalogue) and may not represent the rest.
- **Medium Q6 cannot be answered as asked:** one update date per app.
- **Small groups are noisy:** for example Events (45 rated apps), Educational (32) and Beauty (42).
- **Dashboard image:** `google_play_dashboard.png` is drawn in Python (Matplotlib) from the cleaned data.
