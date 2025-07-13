# Movie-Catalog-Analysis
---
## Objectives of the Analysis

With so much content on Netflix, ever wondered what truly makes up its catalog? What kinds of shows and movies are most common, where they come from, and how things have changed over the years? This analysis was done to help answer those questions and uncover meaningful patterns that can guide smarter content choices and business decisions.

To achieve this, the analysis focused on:

- Understanding how Netflix’s catalog has grown and changed over time.  
- Identifying dominant and underrepresented genres.  
- Exploring regional contributions to Netflix’s content.  
- Highlighting top-performing directors and actors.  
- Analyzing content maturity ratings and duration.  
- Translating these patterns into actionable insights to guide content curation and business decisions.
---
## Methodology

This analysis was conducted using a combination of tools and techniques to ensure comprehensive data exploration, cleaning, transformation, modeling, and visualization. The workflow prioritized data quality and analytical rigor to enable meaningful insights.

### Tools Used

- **Microsoft Excel**: For rapid initial data exploration and quality assessment, including identification of duplicates, missing values, incorrect data types, and formatting inconsistencies.  
- **Jupyter Notebook (Python)**: Utilized for detailed data exploration, cleaning, and preparation with libraries such as `pandas` for data manipulation, `chardet` for encoding detection, and `re` for pattern matching.  
- **Power BI and Power Query**: Employed for data transformation, data modeling using star schema, and interactive visualization/dashboard creation.

### Initial Dataset Overview

The original dataset comprised **8,807 rows** and **12 columns**. Upon initial review, three rows with empty duration values were found, which were mistakenly shifted into the rating column. These values were corrected by placing them back in the appropriate duration field.

Four duplicate rows, identified by matching title and release year, were removed to ensure unique records, reducing the dataset to **8,803 rows**.

### Missing Values Summary

The dataset had missing values concentrated mainly in descriptive fields:

| Column       | Missing Entries | Percentage Missing |
|--------------|-----------------|--------------------|
| Director     | 2,633           | 29.91%             |
| Cast         | 825             | 9.37%              |
| Country      | 830             | 9.43%              |
| Date Added   | 10              | 0.11%              |
| Rating       | 7               | 0.08%              |

These missing values were addressed where appropriate during data cleaning, with non-critical fields imputed with placeholders such as **“Unknown.”**

### Data Cleaning and Preparation

Key cleaning steps conducted in **Jupyter Notebook - Python**  included:

- **Encoding Correction**: Resolved mojibake issues caused by inconsistent character encoding using encoding detection and standardization.  
- **Duplicate Removal**: Removed four exact duplicate records based on title and release year.  
- **Missing Value Imputation**: Filled missing values in non-essential fields with placeholder text to maintain dataset consistency.
See the cleaning and transformation Python code [here](https://github.com/Chiagoziemchidera/Movie-Catalog-Analysis/blob/main/Netflix_Dataset_Cleaning.ipynb).

To enable detailed frequency and categorical analysis, columns containing multivalued entries such as `listed_in` (genres), `country`, `director`, and `cast` were *exploded* into separate dimension tables. This normalization expanded the dataset as follows:

- **Genres Table**: 19,313 rows  
- **Countries Table**: 10,837 rows  
- **Directors Table**: 9,608 rows  
- **Cast Table**: 64,918 rows
See the fully cleaned data [here](https://github.com/Chiagoziemchidera/Movie-Catalog-Analysis/blob/main/netflix_fully_cleaned.xlsx).

### Data Transformation and Modeling

Further transformations were performed in **Power Query within Power BI**, including:

- Parsed the `duration` column to extract numerical values and categorize content length.  
- Created a dedicated **date dimension table** to support time-based analysis.  
- Structured the dataset into a **star schema** model consisting of fact and dimension tables for optimized querying and visualization.  
  > For the model diagram, see *Figure 2 below.

### Analysis and Visualization

Data analysis and dashboard development were completed in **Power BI**, using the following approach:

- **Card visuals** to display key summary metrics at a glance.  
- **Bar, column, and donut charts** to illustrate categorical distributions for content addition date, genre, country, and maturity rating.  
- **Interactive slicers** allowing exploration by content type, country, and date added to enhance user-driven insights.
---
## Analysis and Insights

Netflix’s content strategy has evolved significantly over time, revealing patterns in genre preferences, regional contributions, audience targeting, and content types. Below are key insights derived from the dataset:

### Content Growth & Catalog Composition

<img width="1056" height="336" alt="Screenshot 2025-07-13 083951" src="https://github.com/user-attachments/assets/592c7443-fdc8-43bd-bbfa-27c8ecce9f52" />


- Netflix's content library comprises **8,803 titles**, with **Movies accounting for 70% (6,128)** and **TV Shows for 30% (2,675)**.  
- Content acquisition started slowly in **2014** but accelerated in **2016** with an **81% year-over-year increase**, peaking in **2019** with **2,013 new titles**.  
- The onset of **COVID-19** may explain the drop in additions during **2020 and 2021**, likely due to production and acquisition challenges.  
- The **Movies-to-TV Show ratio** has remained relatively stable over time, consistently favoring movies.  

**Business Insight**: The peak in 2019 followed by a decline highlights the need for **adaptive content sourcing strategies**, possibly favoring **local productions or co-productions** during global disruptions.

### Genre Evolution & Preferences

<img width="1459" height="631" alt="Screenshot 2025-05-16 130436" src="https://github.com/user-attachments/assets/74a43ddd-636e-4899-af28-f77101579521" />


- The most dominant genres are **International Movies (2,751)**, **Drama (2,424)**, **Comedies (1,673)**, and **International TV Shows (1,350)**.  
- In early years (**2014–2015**), **Documentaries** led content additions, but from **2016 onward**, **International Movies** and **Drama** took over, reflecting Netflix's growing global footprint.  
- Least-represented genres include **TV Thrillers (57)**, **Stand-Up Comedies & Talk Shows (56)**, and **Classic & Cult TV (28)**.

**Business Insight**: The shift to international genres indicates **successful localization efforts**. Continued investment in **underrepresented yet growing genres** like **Stand-Up Comedy** or **Thriller** could help tap niche markets.

### Release Year vs. Add-to-Catalog

- The most common release years for content are **2018 (1,144)**, **2017 (1,032)**, and **2019 (1,029)**.  
- Interestingly, **TV Shows from 2020** and **Movies from 2017** dominate their respective categories.

<img width="1427" height="598" alt="Screenshot 2025-05-16 130351" src="https://github.com/user-attachments/assets/b6b69d16-9615-4a25-8759-a699dbdaef9c" />

**Business Insight**: Netflix could improve **exclusive offerings** by shifting toward **earlier or simultaneous releases** through **original productions** or **first-rights partnerships**.

### Geographic Distribution & Cultural Diversity

<img width="1445" height="622" alt="Screenshot 2025-05-16 130638" src="https://github.com/user-attachments/assets/9e0e837c-1a98-44d3-841f-fba2c4bbb993" />

- The top content-producing countries are:  
  - **United States**: 3,689 titles  
  - **India**: 1,048 titles  
  - **United Kingdom**: 806 titles  
  - **Canada**: 445 titles  
  - **France**: 393 titles  
- Content labeled as **“Unknown Country”** is high (**830 entries**), often tied to **International TV Shows** and **Children & Family** content.  
- Countries with the fewest titles are primarily from **Asia**, **South America**, parts of **Europe**, **Africa**, and the **Caribbean**, typically contributing only **one to three titles** each.  
- **Country-specific genre dominance**:  
  - **US**: Drama, Comedies, Documentaries  
  - **India**: International Movies, Drama, Action & Adventure  

**Business Insight**: India’s rising presence signals a **high-growth market**. However, the large number of **"Unknown" countries** suggests **metadata quality issues** that could hamper **regional recommendation accuracy**.

### Audience Targeting via Ratings

- The most frequent maturity ratings are:  
  - **TV-MA (3,204)** – targeting mature audiences  
  - **TV-14 (2,155)** – suitable for teens and adults  
  - **TV-PG (861)**, **R (796)**, and **PG-13 (490)**  
- Rarely used or outdated ratings include **NC-17 (3)** and **TV-Y7-FV (6)**.

<img width="1483" height="634" alt="Screenshot 2025-05-16 130712" src="https://github.com/user-attachments/assets/35154eeb-cec7-4913-86c9-489eadaf1675" />

**Business Insight**: Netflix’s content is skewed toward **older teens and adults**. Expanding **family-friendly content** could improve engagement among **younger users and shared accounts**.

### Duration Patterns

- **Movies** average **1hr 40mins**, with the longest being **5h 12mins** ("*Black Mirror: Bandersnatch*") and the shortest **3 mins** ("*Silent*").  
- **TV Shows** average **2 seasons**, with outliers like "*Grey’s Anatomy*" (17 seasons) and "*Supernatural*" and "*NCIS*" (15 seasons).  
- **1-season shows** dominate, making up over **1,792 titles** — possibly mini-series or underperforming series.

**Business Insight**: Short-duration content can drive **binge-watch behavior**, but may also indicate **high content churn**. Better **promotion and continuity strategies** can retain **long-form series viewers**.

### Talent Distribution – Actors & Directors

- **Top Actors**:  
  - “Unknown” (825)  
  - **Anupam Kher** (43)  
  - **Shah Rukh Khan** (35)  
  - **Julie Tejwani** (33)  

- **Top Directors**:  
  - “Unknown” (2,633)  
  - **Rajiv Chilaka** (22)  
  - **Jan Suter** (21)  

**Business Insight**: The high count of **unknown actors/directors** indicates **missing metadata**. Addressing this could enhance **personalization**, **content credits**, and **talent partnerships**.

### Cross-Dimensional Relationships

- Cross-analysis reveals that **Drama** and **International Movies** consistently intersect across top countries, suggesting **strong global appeal**.  
- Countries like **India** and the **US**, while both highly represented, favor **slightly different content genres**, underlining **regional content preferences**.  
- **Duration and Genre**: TV Shows in **Drama** and **Romance** tend to have longer seasons (up to 17), whereas **Comedy** and **Children’s** shows usually have shorter runs.

---

## Recommendations

Based on the data, here’s what I would suggest to help Netflix strengthen its catalog and user experience:

### 1. Fill in the Gaps in Metadata
A significant portion of the catalog is missing key information like **director**, **cast**, and **country of origin**. This affects how well content is recommended and discovered. It’s worth investing in cleaning this up — either by cross-referencing internal production records or using external data providers.  
> For a platform that relies so heavily on personalization, **complete metadata is non-negotiable**.

### 2. Reignite Content Growth in a Strategic Way
After a strong spike in content additions in **2019**, the pace has clearly slowed. While this may have been intentional, it's important to keep the catalog feeling fresh — especially with competitors like **Prime Video** and **Disney+**.  
Rather than just adding more, focus on bringing in **diverse content** that fills current gaps, like **thrillers**, **classic TV**, or **regional stories** from underserved markets.

### 3. Balance the Mix Between Movies and Series
Currently, about **70% of the catalog is movies**. But **TV shows** — especially short, bingeable series — tend to keep users coming back.  
Consider building out **limited series** and **anthologies**, especially in popular categories like **crime**, **romance**, and **drama**. These are cost-effective and great for engagement.

### 4. Double Down on Regional Relevance
The data shows Netflix content is dominated by the **U.S.** and **India**. That’s not surprising, but other regions like **Africa**, **Latin America**, and parts of **Europe** are underrepresented.  
As Netflix pushes for global growth, a **stronger local content pipeline** will be key.  
> It’s not just about adding titles — it’s about making sure there’s content that feels “**made for me**” wherever the user is.

### 5. Use Genre Insights to Guide Originals Strategy
**International films** and **dramas** are popular everywhere, which is an important insight. Creating original shows and movies in these categories — designed to match **local tastes** — can boost viewer interest.  
Rather than focusing only on expensive global blockbusters, Netflix should invest more in **local-language Originals** that connect with what audiences actually want.

### 6. Pay Attention to Content Duration Trends
Most **movies average 1 hour 40 minutes**, and most **TV shows last just one or two seasons**.  
As Netflix continues to develop Originals, it’s worth validating whether viewers finish longer content and **adjusting episode or season length accordingly**.

### 7. Show More Love to Niche Genres
Genres such as **stand-up comedy**, **cult classics**, and **thrillers** have smaller but **dedicated audiences**.  
While they may not appeal to the masses, they play a key role in keeping **loyal viewers engaged**.  
Netflix can strengthen **user retention** by:
- Creating **curated collections**  
- Highlighting these genres in **recommendations**  
- Testing new content to give subscribers more reasons to **stick around**

---

## Limitations & Assumptions

As with most data projects, a few limitations and assumptions shaped how far the analysis could go:

### Data Gaps and Quality Issues

- Some key information was missing — especially for **directors (almost 30%)**, **cast members**, and **countries of origin**. This made it harder to tell a complete story about who’s behind the content and where it’s coming from.  
- A few minor issues were found and fixed, like **misplaced duration values** and **four duplicate rows**. Nothing alarming, but worth noting.  
- “**Unknown**” had to be used frequently to fill in gaps, especially for fields like **cast** and **country**, which reduces how precise we can be in those areas.

### Analytical Constraints

- The dataset only reflects content **available at the time it was collected**, so we can’t speak to recent changes or removals.  
- How genres, actors, and countries showed up were examined, but we couldn’t measure **popularity or viewer engagement**, only presence.

### Assumptions Made

- **Multivalued fields** like `genre` and `country` were treated as **separate attributes** to get more meaningful insights.  
- “**Unknown**” entries were kept in the analysis to **preserve row integrity** and avoid losing potentially useful data.

## The Missing Piece: User Engagement

- One major gap is the lack of **user behavior data** — things like **views**, **time spent watching**, **likes**, or **completion rates**.  
- With engagement data, analysis could go a step further to understand what people actually **enjoy watching**, not just what’s available.  
- This would help connect **catalog data to audience impact**, guiding smarter **content investments**, **marketing**, and **personalization strategies**.

<img width="1385" height="661" alt="Screenshot 2025-05-16 164711" src="https://github.com/user-attachments/assets/9e86761e-8e4e-48a3-bf57-92c74d0ce55e" />


<img width="940" height="701" alt="Screenshot 2025-05-16 003410" src="https://github.com/user-attachments/assets/35c35bc9-e5cf-41be-8de8-ff3874e469a7" />

---

## Key DAX Formulas

This section includes the main DAX formulas used in the Power BI dashboard to calculate important metrics and support the analysis.

// Formula 1: Date Dimension Table
```dax
Dim_Date = 
ADDCOLUMNS(
    CALENDAR(DATE(2014, 4, 1), DATE(2021, 9, 21)),
    "Year", YEAR([Date]),
    "Month Number", MONTH([Date]),
    "Month Short", FORMAT([Date], "MMM"),
    "Month Year", FORMAT([Date], "MMM yyyy"),
    "Quarter Number", QUARTER([Date]),
    "Quarter Text", "Q" & QUARTER([Date]),
    "Day", DAY([Date]),
    "Week of Year", WEEKNUM([Date], 2),
    "Day of Week", WEEKDAY([Date], 2),
    "Day Name", FORMAT([Date], "dddd"),
    "Is Weekend", IF(WEEKDAY([Date], 2) > 5, TRUE(), FALSE())
)


// Formula 2: Content Length (Calculated Column)
ContentLength = 
VAR Raw = 'Fact_Main'[duration]
RETURN
    VALUE(LEFT(Raw, FIND(" ", Raw & " ") - 1))


// Formula 3: Total Contents
Total Contents = COUNTROWS('Fact_Main')


// Formula 4: Total Movies
Total Movies = 
CALCULATE(
    COUNTROWS('Fact_Main'),
    'Fact_Main'[type] = "Movie"
)


// Formula 5: Total TV Shows
Total TV Shows = 
CALCULATE(
    COUNTROWS('Fact_Main'),
    'Fact_Main'[type] = "TV Show"
)


// Formula 6: Average Movie Duration
AverageMovieDuration = 
VAR AvgMins = 
    CALCULATE(
        AVERAGE('Fact_Main'[ContentLength]),
        'Fact_Main'[type] = "Movie"
    )
VAR Hrs = INT(AvgMins / 60)
VAR Mins = ROUND(MOD(AvgMins, 60), 0)
RETURN
    FORMAT(Hrs, "0") & "h " & FORMAT(Mins, "0") & "min"


// Formula 7: Average TV Show Duration (Seasons)
AverageTVSeasons = 
VAR AvgSeasons = 
    CALCULATE(
        AVERAGE('Fact_Main'[ContentLength]),
        'Fact_Main'[type] = "TV Show"
    )
RETURN
    FORMAT(AvgSeasons, "0") & IF(AvgSeasons = 1, " Season", " Seasons")
