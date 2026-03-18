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

<iframe
  src="assets/DensityGraph.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

We found that the p_value is 0.0, and since it is less than the 0.05 significance level, we reject the null hypothesis. Therefore the missingness of `'avg_rating'` does depend on the cook time `'minutes'`.

We also tested whether or not the missingness depended on a randomly generated column, `'random_group'`, where each recipe was randomly assigned to group A or group B.

**Null Hypothesis:** The missingness of avg_rating does not depend on the random group assignment.

**Alternate Hypothesis:** The missingness of avg_rating does depend on the random group assignment.

**Test Statistic:** The difference in the proportion of recipes assigned to group “A” between those with missing avg_rating and those without missing avg_rating.

**Significance Level:** 0.05

To test this, we performed a permutation test by shuffling the missingness indicator 1000 times and computing the difference in each proportion.

<iframe
  src="assets/GroupAProp.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The bar chart above clearly shows that there is no relationship between missingness and the random grouping variable since the proportions are nearly identical. We found that the resulting p-value extremely large, far great than the 0.05 significance level meaning that we fail to reject the null hypthesis and can conclude that the missingness of `'avg_rating'` does not depend on `'random_group'`.

## Hypothesis Testing

As previously stated, we are interested in determining if there is a difference in average ratings between short and long recipes.

**Null Hypothesis:** There is no difference in average recipe ratings between short and long recipes.

**Alternate Hypothesis:** There is a difference in average recipe ratings between short and long recipes.

**Test Statistic:** The difference in mean average rating between long and short recipes (mean rating of long recipes minus mean rating of short recipes).

**Significance Level:** 0.05

A permutation test was chosen because we are comparing the averages of two groups without assuming any distribution for the ratings. The difference in means is an interpretable test statistic for this question as it measures how much the average rating differs between each group.

#### Conclusion of Permutation Test

The observed test statistic is -0.027. The p-value of 0.03 that we found is less than oour 0.05 significance level, meaning we reject the null hypothesis. There is statistically significant evidence to suggest that the average ratings of short and long recipes are different. With a negative observed test statistic, we can conclude that on average, long recipes tend to have slightly lower ratings than shorter recipes.

## Framing a Prediction Problem

The goal of the prediction task is to **predict the average rating** of a recipe based on its characteristics. Since the response variable is continuous, this is a **regression problem**. The response variable is `'avg_rating'`, which represents the average rating of a recipe.

At the time of prediction, it is assumed that we only have access to information available before users submit their ratings. Because of this, the model uses features that include the cooking time(`'minutes'`), number of ingredients(`'n_ingredients'`), and contributor ID(`'contributor_id'`).

In order to evaluate the performace of the model, MSE and R^2 will be implemented. 
  - MSE will measure the average squared difference between the predicted and the actual ratings which will be useful for capturing the magnitude of prediction errors
  - R^2 will measure how well the model explains the variability of the response variable.

## Baseline Model

For my baseline model, a linear regression model was used within a single sklearn Pipeline. The features included in the model are `'minutes'` and `'n_ingredients'`, which are quantitative variables, and `'contributor_id'`, which is a nominal categorical variable.

To prepare the data, a one-hot encoding to the `'contributor_id'` column was applied to standardize the quantitative features which allowed the model to interpret categorical information.

The performance of the model on the test gave us an MSE of 0.46 and an R^2 score of -0.107. The negative R^2 tells us that the model performs worse than if we were to simply predict the ean rating for all recipes. This suggests that the current model is not that effective in capturing the relationship between the features and our target variable.

Overall, this baseline model is not very strong.

## Final Model

For the final model, I wanted to improve upon the baseline model by introducing more informative features as well as using a far more flexible modeling approach. In addition to the three original features used in the baseline model, two new features were engineered: `'log_minutes'` and `'n_steps'`. The `'log_minutes'` feature is a log transformation of the cooking time which will help reduce the skewness in the distribution of recipe cook times, making it easier for the model to learn patterns. The `'n_steps'` feature has the number of steps in a recipe which captures how complex the recipe is and how they may influence user ratings.

For the modeling algorithm, a Random Forest Regressor was used, which captured the nonlinear relationships and interactions between features the the linear model failed to do. GridSearchCV was also used, focusing on the max_depth parameter in order to control the complexity.

The final model ended up achieving a better performace than the baseline model. The MSE was 0.415 and the R^2 was 0.0018. The lower MSE and higher R^2 indicates that the moodel is better at capturing patterns in the data and generalize it to new recipes. The improvement is definitely attributed to the addition of more informative features and the use of a more powerful model.












