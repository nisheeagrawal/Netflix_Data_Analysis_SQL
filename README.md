
-**Netflix-Data-Analysis by Nishee Agrawal**

**Tools Used:** Excel,PostgreSQL, Tableau

[Datasets Used](https://www.kaggle.com/datasets/victorsoeiro/netflix-tv-shows-and-movies?select=titles.csv)

[Netflix Dashboard - Tableau](https://public.tableau.com/app/profile/nishee.agrawal/viz/NetflixDashboard_17007982308780/NetflixDashboard)

- **Problem Statement:** Netflix aims to extract valuable insights from a massive dataset of approximately 82,000 rows on their shows and movies to enhance subscriber experience. The challenge lies in the need for a robust and scalable data analytics solution to effectively analyze the extensive data and reveal meaningful patterns and trends.

- **My Solution to 1the Problem:** 
- Firstly, I will start by importing all of the data from the CSV file into a SQL database and then do the following: 
1.Utilizing SQL and Tableau for insights on Netflix's movies and shows dataset.
2.Using SQL functions to reveal key metrics: viewer ratings, popularity trends, genre preferences, and viewership patterns.
3.Extracting and preparing data for presentation in Tableau.
4.Employing Tableau for interactive exploration through visually appealing charts, graphs, and visualizations.
5.Creating a dynamic Tableau dashboard for detailed exploration of movie genres, viewer demographics, and geographical regions.

Goal: Provide actionable insights for Netflix stakeholders.

## Questions Answered are as follows:

## 1. Which movies and shows on Netflix ranked in the top 10 and bottom 10 based on their IMDB scores?
- Top 10 Movies
```mysql
SELECT title, 
type, 
imdb_score
FROM shows_movies.titles
WHERE imdb_score >= 8.0
AND type = 'MOVIE'
ORDER BY imdb_score DESC
LIMIT 10
```


- Top 10 Shows
```mysql
SELECT title, 
type, 
imdb_score
FROM shows_movies.titles
WHERE imdb_score >= 8.0
AND type = 'SHOW'
ORDER BY imdb_score DESC
LIMIT 10
```


- Bottom 10 Movies
```mysql
SELECT title, 
type, 
imdb_score
FROM shows_movies.titles
WHERE type = 'MOVIE'
ORDER BY imdb_score ASC
LIMIT 10
```

- Bottom 10 Shows
```mysql
SELECT title, 
type, 
imdb_score
FROM shows_movies.titles
WHERE type = 'SHOW'
ORDER BY imdb_score ASC
LIMIT 10
```


IMDB scores serve as a widely recognized measure of a movie or show's quality and popularity.

The top 10 titles with exceptional IMDB scores are likely highly regarded and acclaimed, contributing to their prominence in the Netflix library.

The bottom 10 entries with lower IMDB scores may not resonate as strongly with audiences, influenced by factors like individual preferences, weak plot, poor acting, and low-quality production.

The project aims to uncover and highlight variations in audience reception, offering valuable insights for viewers seeking quality content and informing Netflix's audience recommendations.

Findings can serve as a basis for further analysis and decision-making, guiding viewers to well-received titles and identifying areas for improvement in lower-rated content.

## 2. How many movies and shows fall in each decade in Netflix's library?
```mysql
SELECT CONCAT(FLOOR(release_year / 10) * 10, 's') AS decade,
	COUNT(*) AS movies_shows_count
FROM shows_movies.titles
WHERE release_year >= 1940
GROUP BY CONCAT(FLOOR(release_year / 10) * 10, 's')
ORDER BY decade;
```


The SQL query results highlight the distribution of movies and shows across decades in Netflix's library.
A significant increase in content is observed from the 2000s onwards, indicating a notable shift over time.
Earlier decades (1940s-1980s) show a limited number of entries, while the 1990s and 2010s demonstrate substantial growth.
The 2010s stand out with 3,304 titles, showcasing Netflix's focus on contemporary content aligned with current trends.
Despite ongoing data for the 2020s, there are already 1,972 movies and shows, indicating a strong emphasis on recent years.
Netflix's strategy involves curating a diverse library spanning multiple decades, allowing audiences to explore varied content reflecting different eras.

## 3. How did age-certifications impact the dataset?
```mysql
SELECT DISTINCT age_certification, 
ROUND(AVG(imdb_score),2) AS avg_imdb_score,
ROUND(AVG(tmdb_score),2) AS avg_tmdb_score
FROM shows_movies.titles
GROUP BY age_certification
ORDER BY avg_imdb_score DESC
```



```mysql
SELECT age_certification, 
COUNT(*) AS certification_count
FROM shows_movies.titles
WHERE type = 'Movie' 
AND age_certification != 'N/A'
GROUP BY age_certification
ORDER BY certification_count DESC
LIMIT 5;
```

The first query on average IMDB scores reveals TV-14 as the age certification with the highest average score (6.71), indicating favorable ratings for content aimed at viewers aged 14 and older.
TV-G follows with an average score of 6.01, emphasizing appreciation for content suitable for all audiences.
Age certifications R and TV-Y, each with an average score of 6, show that, despite lower ratings, there is a substantial audience enjoying content in these categories.
The second query examines the distribution of titles across age certifications in Netflix's dataset.
R is the most prevalent certification (556 titles), followed by PG-13 (451 titles) for mature audiences, and PG (233 titles) for general audiences.
G has 124 titles for a younger audience, while NC-17 is the least represented with only 16 titles.
These findings highlight the diversity in age certifications on Netflix, offering insights into both audience preferences and content distribution. The higher average scores for TV-14, TV-MA, and TV-PG suggest positive resonance with viewers in these age categories.

## 4. Which genres are the most common? 
- Top 10 most common genres for MOVIES
```mysql
SELECT genres, 
COUNT(*) AS title_count
FROM shows_movies.titles 
WHERE type = 'Movie'
GROUP BY genres
ORDER BY title_count DESC
LIMIT 10;
```


- Top 10 most common genres for SHOWS
```mysql
SELECT genres, 
COUNT(*) AS title_count
FROM shows_movies.titles 
WHERE type = 'Show'
GROUP BY genres
ORDER BY title_count DESC
LIMIT 10;
```

- Top 3 most common genres OVERALL
```mysql
SELECT t.genres, 
COUNT(*) AS genre_count
FROM shows_movies.titles AS t
WHERE t.type = 'Movie' or t.type = 'Show'
GROUP BY t.genres
ORDER BY genre_count DESC
LIMIT 3;
```


In movies, the top 10 genres on Netflix are revealed, with Comedy being the most popular (384 movies), followed by Documentation (230) and Drama (224). Combinations like comedy + documentation and comedy + drama also feature prominently, emphasizing a preference for multi-genre movies.

For shows, Reality is the most common genre (113 shows), followed by Drama (104), Comedy (100), and Documentation (100). Combinations such as comedy + drama and drama + romance indicate viewer interest in multi-genre shows.

Combining movies and shows, the overall top three genres on Netflix are Comedy (484 entries), Documentation (329), and Drama (328). These findings highlight Netflix's commitment to offering a diverse range of genres to cater to a broad audience.

## Conclusion 

Top and bottom 10 movies and shows based on IMDB scores were analyzed, offering insights for informed viewing choices and identifying areas for potential content improvement.

The distribution of movies and shows across decades revealed a significant increase in content from the 2000s onwards, showcasing Netflix's commitment to featuring newer and trending content.

Age certifications played a crucial role, influencing both average IMDB scores and content distribution. TV-14 emerged as the most popular certification, indicating high viewer preference.

The analysis of age certifications highlighted the diverse range of content on Netflix, and the examination of common genres revealed Comedy as the dominant genre, followed by documentation and drama. Combinations of genres were also prevalent, indicating audience appreciation for multi-genre content. Overall, these insights provide a comprehensive understanding of Netflix's content landscape, showcasing its commitment to diversity and catering to viewer preferences.


