# What Makes Magic: The Gathering Cards Expensive?

A data science project that uses the [Scryfall API](https://scryfall.com/docs/api) to collect and analyze Magic: The Gathering card data, with the goal of understanding what attributes drive card prices.

---

## Motivating Question

**What card attributes are apart of the most expensive Magic: The Gathering cards?**

Magic: The Gathering has been around since 1993 and has thousands of unique cards with prices ranging from a few cents to tens of thousands of dollars. This project explores what characteristics — rarity, color, mana cost, commander legality, and more — are associated with higher card prices.

---

## Repository Contents

```
├── mtg_analysis.ipynb       # Jupyter notebook with cleaning, analysis, and findings
├── mtg_top1000.csv          # Final cleaned dataset (top 1000 most expensive cards)
└── README.md                # This file
```

---

## Data Collection

Data was collected using the [Scryfall REST API](https://scryfall.com/docs/api), which is free and open — no API key or account required.

The API was queried for all English, non-digital cards with a listed USD price. Pagination was handled automatically using Scryfall's `next_page` field. A 100ms delay was used between requests to respect the API's rate limit guidelines.

**To collect the data yourself, run:**
```bash
pip install requests pandas
python mtg_data_collection.py
```

This will generate `mtg_top1000.csv` in your working directory.

---

## Dataset Overview

The final dataset contains the **1,000 most expensive Magic: The Gathering cards** with the following features:

| Column | Description |
|---|---|
| `card_name` | Name of the card |
| `card_price` | Non-foil market price in USD |
| `foil_price` | Foil market price in USD (not available for all cards) |
| `colors` | List of colors the card belongs to (W, U, B, R, G) |
| `mana_cost` | Converted mana cost (numeric) |
| `commander_legal` | Legality in the Commander format (legal / banned / not_legal) |
| `rarity` | Card rarity (common, uncommon, rare, mythic) |
| `card_type` | Full type line (e.g. "Legendary Creature — Dragon") |
| `release_year` | Year the card was first printed |

**Dataset shape:** 1,000 rows × 9 columns

---

## Key Findings

- The most expensive card in the dataset commands a price far above the median, driven largely by scarcity and age
- Commander-banned cards tend to have a higher average price than legal cards, reflecting their historically powerful effects
- Colorless cards (artifacts, lands) dominate the top prices
- Older cards (pre-2000) are disproportionately represented among the most expensive
- Foil versions of cards command a significant price premium on average

---

## Data Quality Notes

- `foil_price` has missing values for cards that do not have a foil printing
- `mana_cost` is `0` for lands and some colorless cards, which may skew CMC-based analysis
- Prices reflect market values at the time of collection and will change over time
- Cards with variable power/toughness (e.g. `*`) are stored as `NaN` in numeric power/toughness columns

---

## Ethics & API Usage

Scryfall's API is free and publicly accessible with no authentication required. Their [terms of service](https://scryfall.com/docs/api) permit data collection for personal and educational use. This project follows good API practices by:
- Adding a delay between requests to avoid overloading the server
- Not republishing bulk data in a way that would compete with Scryfall's own bulk data offering
- Crediting Scryfall as the data source

---

## Resources

- [Scryfall API Documentation](https://scryfall.com/docs/api)
- [Scryfall Search Syntax](https://scryfall.com/docs/syntax)
- [MTG Reserved List](https://magic.wizards.com/en/news/announcements/reserved-list) — explains why some old cards are so expensive
- [EDHREC](https://edhrec.com/) — Commander format popularity data

---

## Author

Created for STAT 386 — Data Science Process 
Seth Kelly | Brigham Young University