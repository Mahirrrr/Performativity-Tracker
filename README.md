# 🎭 How Performative Is My Music Taste?

**Analyzing 152,000+ Last.fm Scrobbles to Measure Authenticity vs. Curation**

## Introduction

In online music communities, "performative listening" is the idea that people curate their music taste for social validation rather than genuine enjoyment. I got curious about my own habits, so I decided to put my listening data under the microscope and see what the numbers actually say.

I started by exporting my full Last.fm scrobble history as a CSV file, which gave me 152,000+ rows of timestamped listening data going back to August 2021. From there I cleaned the data in Python, handling missing timestamps and album names, then engineered time-based features like year, month, hour, and day of week to enable temporal analysis.

The core challenge was figuring out how to actually define and measure "performativity" with data. I went back to the Reddit discussions that inspired the idea and identified distinct archetypes of performative listening: the critic-bro who only plays acclaimed artists for credibility, the guy curating a "green flag" playlist for girls, the terminally online Drain Gang listener building an identity around internet music, and the tough-guy who exclusively plays hard rap to project masculinity. I manually built artist categorization lists for each archetype and then wrote scoring functions that measure things like canon overlap percentage, listening depth ratios (unique tracks vs. total plays per artist), trend chasing patterns (how spikey vs. sustained listening is over time), and discovery rate trends.

Each dimension gets scored 0 to 100 and then feeds into a weighted composite score. I also built a track-level performativity metric so I could identify which specific songs in my library are the most and least "performative." The whole analysis runs in a single Jupyter Notebook with 15+ visualizations including radar charts, heatmaps, scatter plots, and time series breakdowns.

The verdict: **46.8 / 100** — Mostly Authentic. I engage deeply and explore beyond the canon, though there are some performative patterns in there.

## The Dataset

This project uses **151,811 personal Last.fm scrobbles** from **August 2021 to March 2026** across **3,023 unique artists** and **13,632 unique tracks**. The data was exported from my Last.fm profile using [benjaminbenben.com/lastfm-to-csv](https://benjaminbenben.com/lastfm-to-csv).

## Who Do I Actually Listen To?

Before getting into the performativity analysis, here is a look at the raw listening data. JPEGMAFIA dominates with 7,596 plays, followed by Kanye West at 7,061 and Kendrick Lamar at 3,716. The top 5 artists alone make up 16.9% of all listening.

#### Top 20 Most Played Artists
![Top 20 Most Played Artists](Images/Top%2020%20Most%20Played%20Artists.png)

The most played songs paint a slightly different picture. Frank Ocean's "Nights" sits at 337 plays, followed by Mac Miller's "Blue World" and Kendrick Lamar's "PRIDE."

#### Top 20 Most Played Songs
![Top 20 Most Played Songs](Images/Top%2020%20Most%20Played%20Songs.png)

## The Performativity Framework

I built an 8-dimension scoring system where each dimension captures a different flavor of performative listening. Each one is scored 0 to 100 and then combined into a weighted composite.

| Dimension | Weight | What It Captures |
|-----------|--------|-----------------|
| Girl-Appeal Index | 20% | Artists guys listen to that signal sensitivity to women (Laufey, Keshi, Clairo, Sabrina Carpenter) |
| Tough Guy Rap | 20% | Aggressive rap that projects toughness and masculinity (Playboi Carti, Future, Chief Keef) |
| Drain / Internet-Core | 15% | Terminally online identity music (Bladee, Death Grips, JPEGMAFIA, 100 gecs) |
| Listening Depth | 15% | Whether you explore full discographies or just replay the same hits |
| Critical Canon | 10% | Overlap with universally praised "essential" artists (Kendrick, Radiohead, Frank Ocean) |
| Trend Chasing | 10% | Binge-then-drop patterns vs. sustained long-term listening |
| Mainstream Balance | 5% | Whether taste skews entirely mainstream or entirely underground |
| Discovery Decline | 5% | Whether new artist exploration has slowed over time |

## Key Findings

### Girl-Appeal Performativity (12.6% of listening)

The Marías top this category at 2,392 plays, followed by Magdalena Bay, Verzache, and FKA twigs. 12.6% of my library falls into the "green flag" category, which scored as moderate. Not enough to say I am curating for romantic appeal, but it is a noticeable chunk.

#### Top "Girl-Appeal" Artists
![Top Girl Appeal Artists](Images/Top%20Girl%20Appeal%20Artists.png)

### Drain / Internet-Core Performativity (12.2% of listening)

JPEGMAFIA alone accounts for most of this at 7,596 plays, making up nearly half the category. Denzel Curry, Freddie Gibbs, Injury Reserve, and Bladee round out the top five. The 12.2% scored as moderate, meaning I am plugged in but it is not my whole identity.

#### Top "Drain / Internet-Core" Artists
![Top Drain-Internet People Artists](Images/Top%20Drain-Internet%20People%20Artists.png)

### Tough Guy Rap Performativity (8.3% of listening)

Travis Scott leads this one at 2,280 plays, followed by Drake and XXXTENTACION. At only 8.3%, this was my lowest performativity signal. The "Masculinity Balance Check" showed a 0.7x ratio of tough-rap to girl-appeal listening, meaning my library actually leans slightly more toward the soft side than the hard side.

#### "Tough Guy Rap" vs "Girl-Appeal" Listening Over Time
![Tough Guy Rap vs Girl Appeal Comparison](Images/Top%20Tough%20Guy%20Rap%20Artists%20%2B%20Tough%20Rap%20Vs%20Girl%20Appeal%20Comparison.png)

### Discovery Rate

My rate of finding new artists has been declining. The first half of my listening history averaged a 2.06% discovery rate compared to 1.17% in the second half. This suggests my taste is starting to calcify around familiar favorites rather than continuing to explore.

#### New Artist Discoveries Per Month
![New Artist Discoveries Per Month](Images/New%20Artist%20Discoveries%20Per%20Month.png)

### The Full Tier Breakdown

Every single scrobble categorized into its performativity tier. Critical Canon takes the largest performative slice at 23.9%, followed by Girl-Appeal at 12.6% and Drain/Internet-Core at 12.2%. About 35% of listening falls outside any performative category entirely.

#### Listening Breakdown by Performativity Tier
![Listening by Performativity Categorized](Images/Listening%20by%20Performativity%20Categorized.png)

## Listening Habits

#### When I Listen (Day of Week × Hour)
![Listening Activity Heatmap](Images/Listening%20Activity%20Heatmap.png)

#### Monthly Listening Volume Over Time
![Monthly Listening Volume Over Time](Images/Monthly%20Listening%20Volume%20Over%20Time.png)

## Final Score

#### Performativity Radar (8 Dimensions)
![Performativity Profile](Images/Performativity%20Profile.png)

```
============================================================
       PERFORMATIVITY SCORE BREAKDOWN
============================================================
  Canon Overlap:           50.7 / 100  (weight: 10%)
  Listening Depth:         90.7 / 100  (weight: 15%)
  Trend Chasing:           56.7 / 100  (weight: 10%)
  Discovery Decline:       42.9 / 100  (weight:  5%)
  Mainstream Imbalance:    92.9 / 100  (weight:  5%)
  Girl-Appeal Index:       31.4 / 100  (weight: 20%)
  Drain/Internet-Core:     34.9 / 100  (weight: 15%)
  Tough Guy Rap:           20.7 / 100  (weight: 20%)
============================================================
  OVERALL PERFORMATIVITY:  46.8 / 100
============================================================

  🎵 MOSTLY AUTHENTIC
```

The highest flag was **Listening Depth at 90.7**, meaning I tend to replay the same tracks from artists rather than exploring their full catalogs. KIDS SEE GHOSTS, for example, has 614 plays across only 8 unique tracks, which comes out to about 77 plays per track. **Mainstream Imbalance at 92.9** was also high, but that is because my library is heavily skewed toward either canon or underground artists with very little "neutral" mainstream listening.

On the other hand, **Tough Guy Rap scored only 20.7** and **Girl-Appeal scored 31.4**, meaning neither of those performative archetypes dominates my taste. The strongest signal is that I listen deeply but narrowly to artists I like, which is more of a habit pattern than a performative one.

## Tier Summary

| Tier | Scrobbles | % of Total |
|------|-----------|-----------|
| Uncategorized | 53,039 | 34.9% |
| Critical Canon | 36,258 | 23.9% |
| Girl-Appeal | 19,085 | 12.6% |
| Drain / Internet-Core | 18,539 | 12.2% |
| Tough Guy Rap | 12,598 | 8.3% |
| Underground | 6,193 | 4.1% |
| Mainstream | 6,099 | 4.0% |
| **Total** | **151,811** | **100%** |

Total "performative" listening: **57.0%**
Total "neutral" listening: **43.0%**

## Methodology and Limitations

The artist categorization lists (canon, girl-appeal, drain, tough-rap) are manually curated, which is inherently subjective. A more robust version would pull listener counts from the Spotify or Last.fm API for objective popularity measurement. Some artists fall into multiple categories, and the priority system (tough rap > drain > girl-appeal > canon > mainstream > underground) affects the final numbers.

Scrobble data does not distinguish between active and passive listening. Having a playlist on shuffle is very different from intentionally putting on an album, and this analysis treats both the same.

Most importantly, enjoying critically acclaimed music or any specific genre does not make someone fake. This analysis is exploratory and meant to provoke reflection, not pass judgment on anyone's taste.

## Future Work

I would like to integrate the Spotify or Last.fm API for real-time artist popularity data instead of manual categorization. Sentiment analysis on Last.fm tags could help classify "aesthetic" vs. "substance" listening more objectively. I am also planning to build an interactive Tableau dashboard from these findings and potentially apply the framework to other users for comparative analysis.

## Tools

Python (Pandas, NumPy, Matplotlib, Seaborn) · Jupyter Notebook · Last.fm Data Export

## Project Structure

```
📂 Performativity-Tracker/
├── 📓 LastFM_Performativity_Analysis.ipynb
├── 📄 Last_fm_Data.csv
├── 📄 README.md
└── 📂 Images/
    ├── Listening Activity Heatmap.png
    ├── Listening by Performativity Categorized.png
    ├── Monthly Listening Volume Over Time.png
    ├── New Artist Discoveries Per Month.png
    ├── Performativity Profile.png
    ├── Top 20 Most Played Artists.png
    ├── Top 20 Most Played Songs.png
    ├── Top Drain-Internet People Artists.png
    ├── Top Girl Appeal Artists.png
    └── Top Tough Guy Rap Artists + Tough Rap Vs Girl Appeal Comparison.png
```

---

*Built by Mahir Abdullah · March 2026*
