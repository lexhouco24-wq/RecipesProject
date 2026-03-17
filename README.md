# Investigation on the Relationship Between Cooking Time and the Average Rating of Recipes

Author: Lex Hou

## Overview

This data science projected focuses on exploring the relationship between the cooking time and the average rating of recipes.

## Introduction

The idea of food to many is simply just the basic necessity that we need to survive. However, food has always meant more than that to me. From eating food, to watching professionals cook, to even cooking myself, I have always found an interest in the culinary world. With that being said, I have wondered what exactly makes a dish so good? It could be a variety of different things, but here I want to investigate the relationship between the cooking time and the average rating of various recipes. Do people need to spend hours to make a great dish, or could they achieve that goal in a shorter amount of time? To conduct this investigation, I am analyzing two datasets that contain cooking times and ratings posted on [food.com](https://www.food.com).

The first dataset, `recipes`, contains 83782 unique recipes. Each recipe has 10 attributes which include the following information:

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













