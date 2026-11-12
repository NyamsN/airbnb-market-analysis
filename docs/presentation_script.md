# Recorded presentation script (about 7 minutes)

Show the report PDF or notebook on screen while speaking.

**1. Introduction (0:00–0:45).** "Hi, I'm Nelson Nyamweya, Track B Data Science on the AnalystLab Africa Airbnb Market Intelligence project. My question was: which listing characteristics are associated with higher advertised prices within each of ten cities, and does review activity tell us anything about ratings?"

**2. Data and quality (0:45–2:00).** Show Section 2. "I used 279,712 listings and 5.37 million review records. listing_id is a clean primary key and every review links to a listing. The 160 repeated review IDs turned out to be 11 pairs of Rome listings from 2 hosts that share carried-over reviews, so I kept them and used listing_id plus review_id as the key. I removed 113 zero or negative prices, flagged about 5,000 extreme prices, and did not impute missing host data because it is missing far more in some cities than others."

**3. Currency (2:00–2:30).** "There is no currency field, so I never compared raw prices across cities. Every test runs inside one city, and the cross-city charts use price divided by the city median."

**4. EDA highlights (2:30–3:45).** Show Figures 2, 3, 6, 7. "Paris dominates with 23% of listings. Prices are right-skewed in every city, so I used medians and rank-based tests. Price climbs with capacity everywhere. Review activity peaked in 2019 and collapsed in March 2020."

**5. Hypotheses (3:45–5:30).** Show the hypothesis summary table. "H1: room type matters in all ten cities; an entire place is 1.5 to 2.6 times a private room, with large effects in Sydney, New York, Mexico City and Hong Kong. H2: capacity is positively associated with price in every city, about 7 to 23% per extra guest after controlling for room type and bedrooms. H3: the review–rating link is small and negative, because listings with few reviews have very noisy ratings. H4: host responsiveness differs across cities, but the effect is small. I reported effect sizes, used Holm correction, and re-ran the price tests without extreme prices: nothing changed."

**6. Limitations (5:30–6:15).** "These are advertised prices, not revenue; review counts are not occupancy; and everything is association, not causation. The data is from the COVID period."

**7. Recommendations and contribution (6:15–7:00).** "I recommend segmented price benchmarks by city, room type and capacity; showing ratings only above a review threshold; and focusing host support on Paris and Sydney. My cleaned dataset and currency rules can feed the dashboard and the ML price model. Thank you."
