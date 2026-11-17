# Papua Tourism

### Dynamic Dashboard for Papua Tourism: Unveil the Beauty of Eastern Indonesia

![Papua landscape](backdrop.jpg)

A tourism monitoring dashboard for Papua, Indonesia, built on sentiment analysis of traveller reviews from Google Maps and TripAdvisor. The goal is to help policymakers and tourism managers see what visitors love, what frustrates them, and where to focus improvements: attractions, accessibility, or amenities.

> 🇮🇩 Proyek ini adalah dashboard pemantauan pariwisata Papua berdasarkan analisis sentimen ulasan wisatawan, untuk membantu pemegang kebijakan mengambil keputusan secara efisien dan efektif.

## Table of Contents

- [Overview](#overview)
- [Destinations Covered](#destinations-covered)
- [Pipeline](#pipeline)
- [Repository Structure](#repository-structure)
- [Dataset](#dataset)
- [Getting Started](#getting-started)
- [Roadmap](#roadmap)

## Overview

Papua has some of Indonesia's most remarkable destinations, but there is little structured data on how visitors experience them. This project:

1. **Collects** public reviews of Papuan destinations from Google Maps and TripAdvisor.
2. **Cleans and merges** them into a single dataset, with an English-translated version.
3. **Labels sentiment** for each review, both overall and per aspect:
   - **Attraction**: the destination itself (scenery, activities, experience)
   - **Accessibilities**: getting there (roads, transport, distance)
   - **Amenities**: facilities on site (toilets, food, lodging, cleanliness)
4. **Shows** the results in an interactive dashboard for decision-makers.

## Destinations Covered

| Destination | Location | Sources |
|---|---|---|
| Raja Ampat | Raja Ampat, Papua Barat Daya | TripAdvisor |
| Teluk Cenderawasih National Park | Nabire, Papua Tengah | Google Maps, TripAdvisor |
| Pantai Tanjung Kasuari | Sorong, Papua Barat | Google Maps, TripAdvisor |
| Pantai Bosnik | Biak Numfor, Papua | TripAdvisor |
| Pantai Batu Picah | Manokwari, Papua Barat | TripAdvisor |
| Bukit Teletubbies | Jayapura, Papua | TripAdvisor |

## Pipeline

```
 Google Maps / TripAdvisor
          │  scraping (Selenium + BeautifulSoup)
          ▼
   data/scrap/*.csv          raw reviews, one file per destination
          │  cleaning, merging, translation
          ▼
   data/pre-process/         merged dataset (Indonesian & English)
          │  sentiment labelling (overall + per aspect)
          ▼
   data/*.xlsx               labelled database + recap
          │
          ▼
       Dashboard
```

## Repository Structure

```
papua-tourism/
├── data/
│   ├── scrap/                      # Raw scraped reviews
│   │   ├── gmap-*.csv              #   from Google Maps
│   │   └── trip-*.csv              #   from TripAdvisor
│   ├── pre-process/
│   │   └── Merged Data (Translated to English).csv
│   ├── Merged Data (Indonesia).xlsx
│   └── Database Pariwisata Papua.xlsx   # Full labelled database ("All" + "Recap" sheets)
├── notebooks/
│   └── Scraping_Trip_Advisor.ipynb      # Review scraper (Selenium)
├── backdrop.jpg
└── README.md
```

## Dataset

The merged dataset (`data/pre-process/Merged Data (Translated to English).csv`) has these columns:

| Column | Description |
|---|---|
| `Place Name`, `Province`, `City` | Where the review is about |
| `User Name`, `User Profile`, `User Avatar`, `User Location` | Reviewer info |
| `Rating` | Star rating (1–5) |
| `Review Title`, `Review Text` | Review content, translated to English |
| `Trip Type` | e.g. Solo, Couples, Family, Friends |
| `Helpful Votes`, `Published Date` | Review metadata |
| `Sentiment` | Overall sentiment: `positif` / `netral` / `negatif` |
| `Attraction`, `Accessibilities`, `Amenities` | Aspect sentiment: `positif` / `netral` / `negatif` |

> **Note:** Reviews are publicly available user content, collected for research and educational purposes only.

## Getting Started

```bash
git clone https://github.com/cesinata/papua-tourism.git
cd papua-tourism
pip install beautifulsoup4 selenium pandas tqdm
```

Open `notebooks/Scraping_Trip_Advisor.ipynb` to run the scraper. You need Google Chrome and a matching ChromeDriver installed. The scraper uses XPath/CSS selectors that can break when the site's layout changes, so you may need to update them.

## Roadmap

- [x] Scrape reviews from Google Maps and TripAdvisor
- [x] Merge and translate the review data
- [x] Label overall and aspect-based sentiment
- [ ] Add more destinations across Papua's provinces
- [ ] Automate sentiment classification with an NLP model
- [ ] Build and publish the interactive dashboard
