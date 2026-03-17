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













