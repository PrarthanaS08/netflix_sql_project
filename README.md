# Netflix Movies and TV Shows Data Analysis using SQL

![Netflix Logo](https://github.com/PrarthanaS08/netflix_sql_project/blob/main/netflix-logo.png)

## Objective

● **Analyze the distribution of content types** (Movies vs. TV Shows)  
● **Identify the most common ratings** for both movies and TV shows  
● **List and analyze content** based on release year, country, and duration  
● **Explore and categorize content** using specific criteria and keywords  


## Dataset
The data for this project is sourced from the Kaggle dataset:  
◦ **Dataset Link:** [Movies Dataset](https://www.kaggle.com/datasets/shivamb/netflix-shows?resource=download)


## Schema
```sql
DROP TABLE IF EXISTS netflix;
CREATE TABLE netflix
(
	show_id VARCHAR(6),
	type VARCHAR(10),
	title VARCHAR(150),
	director VARCHAR(208),
	casts VARCHAR(1000),
	county VARCHAR(150),
	date_added VARCHAR(50),
	release_year INT,
	rating VARCHAR(10),
	duration VARCHAR(15),
	listed_in VARCHAR(100),
	description VARCHAR(250)
);
```

## Business Problems and Solutions

### 1. Count the Number of Movies vs TV Shows

```sql
SELECT 
	type,
	COUNT(*) as total_content
FROM netflix
GROUP BY type
```

**Objective:** Determine the distribution of content types on Netflix.

### 2. Find the Most Common Rating for Movies and TV Shows
```sql
SELECT
	type,
	rating
FROM
(
	SELECT
		type,
		rating,
		COUNT(*),
		RANK() OVER(PARTITION BY type ORDER BY COUNT(*) DESC) as ranking
	FROM netflix
	GROUP BY 1, 2
) as t1
WHERE
	ranking = 1
```

**Objective:** Identify the most frequently occurring rating for each type of content.

### 3. List All Movies Released in a Specific Year (e.g., 2020)

```sql
SELECT * FROM netflix
WHERE
	type = 'Movie'
	AND
	release_year = 2020
```

**Objective:** Retrieve all movies released in a specific year.

## Findings and Conclusion

● **Content Distribution:**  
  The dataset includes a diverse range of movies and TV shows with varying ratings and genres.

● **Common Ratings:**  
  Identifying the most frequent ratings helps understand the target audience for different content types.

● **Geographical Insights:**  
  Top contributing countries and the average number of releases from India highlight regional content trends.

● **Content Categorization:**  
  Categorizing content based on specific keywords reveals patterns in the type of shows and movies available on Netflix.

Overall, this analysis provides a comprehensive view of Netflix’s content library and supports informed decision-making for content strategy.
