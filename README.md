# Box Office Analysis

**Authors**: Claire Sarraille, Sam Whitehurst & Nick Tjandra


![img](images/oldHollywood.jpg)

## Overview

Our company is seeking to enter the film making industry by opening a new movie studio. Specifically, our company is looking to make movies with a high return using a relatively lean budget. We will make our recommendations based on data analyzed from IMDb and The Numbers datasets. 

## Business Understanding

Our team has decided on three budget tiers and will make our recommendations around them. We have identified the top performing movie genres and top directors to make the movie with the highest possible return for each budget tier.

## The Data

The data explored for this task came from two sources:

- [The Numbers](https://www.the-numbers.com/): A film data website which provided production budgeting information and worldwide gross revenue estimations for the films we analyzed. This website is operated by [OpusData](https://www.opusdata.com/home.php), and it allows access to all the financial film data via its web-based API.
    - The data file from this website is stored in our repository for reference.

- [IMDb](https://www.imdb.com/): A website that functions to gather and present information about the success of films based on metrics like ratings, while also contributing categorical metrics such as attributing directors to films and connecting principal actors to their work. We utilized this website to categorize films into their appropriate genres as well as to identify the directors that worked on each of the films.
    - The data from IMDb is stored as a SQL database and can also be found in our repository as well.


## Data Preparation

We began the project by importing all necessary python libraries and reading in the data described above.

For the IMDb dataset, we reviewed the following ERD visual, which allowed us to recognize how each of the tables are connected via designated keys.

![ERD Diagram IMDB](https://raw.githubusercontent.com/learn-co-curriculum/dsc-phase-2-project-v3/main/movie_data_erd.jpeg)

### Data Cleaning
Through various functions outlined below, we cleaned data from diverse sources. This enabled smoother execution of aggregating functions in later data analysis stages. The Numbers dataset underwent cleaning via three key functions:

- **Function 1:** Cleaned the numbers column, removing unnecessary characters, and converting it to integers.
- **Function 2:** Cleaned column headers.
- **Function 3:** Cleaned comma-separated string values of a series into a list of strings.

## Data Analysis

### Analysis Overview:
1. Identify the most suitable metric for measuring a film's "success."
2. Explore options for categorizing films (e.g., genre classification or decade).
3. Develop a strategy for presenting data to stakeholders.
4. Group data by the range of initial investments, reflecting the level of risk incurred by the studio.

### Conducting the Analysis:

#### 1. Measuring Film Success
Utilizing The Numbers dataset, we identified 'Worldwide Gross' revenue and 'Production Budget' as key metrics. We engineered 'Profitability' and 'ARR' columns:

- 'Profitability': Money earned by subtracting the 'Production Budget' from 'Worldwide Gross.'
- 'ARR' (Average Return Ratio): Ratio of worldwide revenue to the cost of creating the movie.

Release Date Filter:
- Cleaned the Release Date column, isolating the release year.
- Eliminated films before 1990 as outliers.

#### 2. Exploring Categorization Options for Films and Merging our Datasets
In the IMDb dataset:

- Identified the 'genres' column in the 'movie_basics' table.
- Extracted director names associated with each film.
- Cleaned the 'genres' column, standardized it, and configured the dataset as a pandas DataFrame.
- Merged datasets based on common headers.

#### 3. Strategizing how to Present our Findings to the Stakeholders
Explored which film genres, on average, produce the highest return on investment. Created 4 investment risk levels based on quartiles of the 'Production Budget' column:

- Level 1: 0 - 5,575,000
- Level 2: 5,575,000 - 20,000,000
- Level 3: 20,000,000 - 45,000,000
- Level 4: 45,000,000+

Eliminated genres with insufficient data for accurate analysis.

#### 4. Determining Risk Level Ranges
Used IQR from The Numbers 'Production Budget' column to set risk levels.

#### Binning the Datasets Based off our Investment Risk Levels
After initial binning, examined film distribution at each risk level.

#### Setting the Median as a Parameter for Genres
Eliminated genres with a count equal to or less than the median at each level. Focused on the top ten genres with the most data points contributing to ARR.

#### Running a Linear Regression to Further Support our ARR Calculations
Calculated linear regression for each risk level. Identified top three genres as Mystery, Horror, and Thriller. (Note: Detailed logic for each risk level not repeated for brevity. Comments in code cells provide brief reminders.)

# Data Summary

- At Risk Level 1 ($0 - $5,575,000): the film genres with the highest ARR are: Mystery, Horror, Thriller. The relative order of these films is further supported by our linear regression analysis which produced coefficients with magnitudes that aligned with the ARR calculation ordering.

![Level One](images/risk_level_graphs/level_1.png)

If this new studio chooses to invest less than $5,575,000 then the data shows that the studio has an opportunity to make a return on their investment at a factor of 16.08 if they were to make a Mystery film.

- At Risk Level 2 ($5,575,000 - $20,000,000): the film genres with the highest ARR are: Horror, Mystery, Thriller. Our linear regression supported this conclusion again.

![Level Two ](images/risk_level_graphs/level_2.png)

If the new studio chooses to invest between $5,575,000 and $20,000,000, then the data shows the studio has an opportunity to make a return on their investment at a factor of 5.11 if they were to make a Horror film.

- At Risk Level 3 ($20,000,000 - $45,000,000): the film genres with the highest ARR are: Horror, Romance, Documentary. Our linear regression supported this conclusion again.

![Level Three ](images/risk_level_graphs/level_3.png)

If the new studio chooses to invest between $20,000,000 and $45,000,000, then the data shows the studio has an opportunity to make a return on their investment at a factor of 3.04 if they were to make a Horror film.

- At Risk Level 4 ($45,000,000+): the film genres with the highest ARR are: Animation, Sci-Fi, and Adventure. Our linear regression supported this conclusion again.

If the new studio chooses to invest more than $45,000,000, then the data shows the studio has an opportunity to make a return on their investment at a factor of 3.88 if they were to make an Animated film.


### Top Directors by Risk Level:
- When we drilled down into Risk Level One, looking at each of the top 10 films by ARR, we found that some of the top directors are all associated with the same studio that mae The Gallows, Paranormal Activity and insidious. 7/10 of these top 10 films are [horror/mystery/thriller] or horror.

#### Level 1:

![Top Directors: Risk Level 1](/images/top_directors_L1.png)

#### Level 2:

![Top Directors: Risk Level 2](/images/top_directors_L2.png)

#### Level 3:

![Top Directors: Risk Level 3](/images/top_directors_L3.png)


# Recommendations

- Produce Horror films at any of the first three budget levels.

- Top directors at the first Risk Level: Chris Lofing, William B. Bell, Jordan Peele 

- At higher risk levels, consider additional genres like Romance and Animation.

- At highest risk level, best performing genres are animation, sci-fi and adventure

# Next Steps

- Explore top genres in higher risk levels (>45 mill)

- Use multi-genre to fine-tune (i.e. horror-mystery-comedy)

- Identify winning actor/director combos

# Presentation and Additional Links:

- [Presentation Slide Deck](Presentation.pdf)

- [Tableau Dashboard](https://public.tableau.com/app/profile/claire.sarraille/viz/MovieBudgetRiskAnalysis/BudgetbyGenre?publish=yes)


#### Repository Structure Diagram
```
├── LICENSE
├── README.md
├── csv_exports_for_tableau
│   ├── directors.csv
│   ├── movie_basics.csv
│   ├── movie_genre_directors.csv
│   ├── movie_risk_NO_genre.csv
│   ├── movie_risk_genre.csv
│   └── persons.csv
├── images
│   ├── movie_data_erd.jpeg│   
    ├── risk_level_graphs│   
        ├── level_1.png
        ├── level_2.png
        ├── level_3.png
│   ├── oldHollywood.jpg
│   └── top_directors_L1.png
│   └── top_directors_L2.png
│   └── top_directors_L3.png
├── Final_Notebook.ipynb
├── notebooks
│   ├── EDA - Sam.ipynb
│   ├── EDA IMDB - Nick.ipynb
│   ├── EDA IMDB - Sam.ipynb
│   ├── EDA TN.MovieBudget - Nick.ipynb
│   ├── EDA TN.MovieBudget - Sam Risk Bins by Production Budget.ipynb
│   ├── OLD_Movie Budget Risk Analysis.ipynb
│   └── claire_dev
│       ├── imdb_persons_cleaning.ipynb
│       └── tableau_data_prep.ipynb
└── zippedData.zip
```
