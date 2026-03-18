# Investigation on the Relationship Between Cooking Time and the Average Rating of Recipes

Author: Lex Hou

## Overview

This data science projected focuses on exploring the relationship between the cooking time and the average rating of recipes.

## Introduction

The idea of food to many is simply just the basic necessity that we need to survive. However, food has always meant more than that to me. From eating food, to watching professionals cook, to even cooking myself, I have always found an interest in the culinary world. With that being said, I have wondered what exactly makes a dish so good? It could be a variety of different things, but here I want to investigate the relationship between the cooking time and the average rating of various recipes. Do people need to spend hours to make a great dish, or could they achieve that goal in a shorter amount of time? To conduct this investigation, I am analyzing two datasets that contain cooking times and ratings posted on [food.com](https://www.food.com).

The first dataset, `recipes`, contains 83782 rows, each containing a unique recipe. Each recipe has 10 attributes which include the following information:

| Column             | Description                                                                                                                                                                                       |
| :----------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `'name'`           | Recipe name                                                                                                                                                                                       |
| `'id'`             | Recipe ID                                                                                                                                                                                         |
| `'minutes'`        | Minutes to prepare recipe                                                                                                                                                                         |
| `'contributor_id'` | User ID who submitted this recipe                                                                                                                                                                 |
| `'submitted'`      | Date recipe was submitted                                                                                                                                                                         |
| `'tags'`           | Food.com tags for recipe                                                                                                                                                                          |
| `'nutrition'`      | Nutrition information in the form [calories (#), total fat (PDV), sugar (PDV), sodium (PDV), protein (PDV), saturated fat (PDV), carbohydrates (PDV)]; PDV stands for “percentage of daily value” |
| `'n_steps'`        | Number of steps in recipe                                                                                                                                                                         |
| `'steps'`          | Text for recipe steps, in order                                                                                                                                                                   |
| `'description'`    | User-provided description                                                                                                                                                                         |
| `'ingredients'`    | Text for recipe ingredients                                                                                                                                                                       |
| `'n_ingredients'`  | Number of ingredients in recipe     

The second dataset,`interactions`,  contains 731927 rows which each contain a review from a user on a recipe. Each row's attributes contain:

| Column        | Description         |
| :------------ | :------------------ |
| `'user_id'`   | User ID             |
| `'recipe_id'` | Recipe ID           |
| `'date'`      | Date of interaction |
| `'rating'`    | Rating given        |
| `'review'`    | Review text         |

There are several key variable from the datasets that are relevant to our research question. The `id` column allowed us to merge the two data sets which led to grouping our ratings by recipe. The `minutes` column represents the amount of time for that recipe which serves as the explanatory variable in our analysis. The `rating` column contains the ratings given by users which we use to compute a new column, `avg_rating`, which represents the average rating for each recipe and is our response variable.

## Data Cleaning and Exploratory Data Analysis

The data cleaning steps below were taken to ensure a better analysis:

1. Left merge recipes and interactions on `id` and `recpie_id`.
  - This allows us to match the recipes to their ratings.
2. Fill all ratings of 0 with np.nan.
  - Ratings are based on a 1 to 5 scale, indicating that ratings of 0 are actually missing values. In order to avoid bias we can fill all the 0 ratings with np.nan.
3. Add `avg_rating` column into the merged table.
  - Since some recipes may have multiple ratings, we take the average of the ratings which will represent that recipe's rating.

Here are the first five rows of the cleaned dataframe. Since our investigation does not require all of the columns, only relevant data will be displayed.

| id      | minutes  | avg_rating |
| :------ | :------- | :--------- |
| 333281  | 40       | 4.0        |
| 453467	| 45       | 5.0        |
| 306168  | 40       | 5.0        |
| 286009  | 120      | 5.0        |
| 475785	| 90       | 5.0        |

### Univariate Analysis

For this analysis, we are taking a closer look at the distribution of the time(in minutes) that it takes for a recipe to be completed. As shown in the plot, the distribution is skewed to the right, telling us that most of the recipes in the dataframe have a lower cooking time.

<iframe
  src="assets/UnivariateGraph.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

### Bivariate Analysis

For this analysis, we are looking at the distribution of the cooking time when comparing it to the average rating. This graph shows that there a lot of recipes that take shorter cook time but also that a majority of the shorter cook times result in high ratings.

<iframe
  src="assets/BivariateGraph.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

### Interesting Aggregates

In this section, we are looking at the relationship is grouped cook times(bins) to the ratings of the recipe. From looking at the table, it is interesting to see that the mean across all the bins are fairly similiar and that the only differences between each other are the amount of recipes per bin. From this alone it seems that cook time really has no effect on rating but we will dive deeper into the question later.

| minutes   | mean  | median  | min  | max  | count  |
| :-------- | :---- | :------ | :--- | :--- | :----- |
| (0, 30]   | 4.64  | 5.0     | 1.0  | 5.0  | 36418  |
| (30, 60]	| 4.61  | 5.0     | 1.0  | 5.0  | 24570  |
| [60, 120] | 4.63  | 5.0     | 1.0  | 5.0  | 11840  |
| [120, 300]| 4.62  | 5.0     | 1.0  | 5.0  | 5139   |
| [300, 600	| 4.52  | 4.86    | 1.0  | 5.0  | 2235   |

## Assessment of Missingness

### MNAR Analysis

From the gathered information, it is believed that the `'avg_rating'` column is MNAR. The missingness of `'avg_rating'` is more than likely to be MNAR because it depends on the unobserved value itself. A recipe only receives an average rating if the user chooses to rate it. For example, recipes with poorer qualities are less likely to receive any rating at all, as users may avoid rating worse recipes simply because they just do not care. To better explain the missingness and make it MAR over MNAR, additonal data such as number of views, completed or incompleted recipes, or engagement metrics could be variable that could help push the missingness to be MAR.

### Missingness Dependency

Moving on, we are trying to examine the missingness of `'avg_rating'`, testing to see if its missingness depends on the cooking time of a recipe, `'minutes'`.

**Null Hypothesis:** The missingness of avg_rating does not depend on the cooking time of the recipe.

**Alternate Hypothesis:** The missingness of avg_rating does depend on the cooking time of the recipe.

**Test Statistic:** The difference in mean cooking time (minutes) between recipes with missing avg_rating and those without missing avg_rating.

**Significance Level:** 0.05






