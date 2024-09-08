# Ingredients to Insights

> This website is the work of Aahil Rupsi

In the world of cooking, one might wonder: Is there a relationship between how long it takes to cook a recipe and how highly it’s rated by those who prepare it? This research explores this very question, analyzing the connection between cooking time and recipe ratings to uncover whether the amount of time spent in the kitchen affects how much people enjoy the final dish.

Understanding this relationship is valuable for both home cooks and culinary professionals alike. Whether you’re looking to maximize efficiency in the kitchen or aiming to cook the most highly-rated recipes, this research sheds light on how time investment may influence culinary satisfaction.

## Introduction

The dataset used for this analysis contains 83,782 rows of data, each representing a unique recipe. The dataset includes a variety of information about each recipe, providing insights into the cooking process and the recipe's overall reception. Key columns include:

- `id`: An identification number for the recipe
- `minutes`: The total time required to prepare and cook the recipe in minutes
- `n_steps`: The number of steps needed to prepare the recipe
- `ingredients`: A list of the ingredients needed to prepare the recipe
- `n_ingredients`: The total number of ingredients needed to prepare the recipe
- `average_rating`: The average rating of the recipe
- `calories (#)`: The total number of calories in the recipe
- `total fat (PDV)`: The percentage of the daily value of total fat needed by the average person
- `sugar (PDV)`: The percentage of the daily value of sugar needed by the average person
- `sodium (PDV)`: The percentage of the daily value of sodium needed by the average person
- `protein (PDV)`: The percentage of the daily value of protein needed by the average person
- `saturated fat (PDV)`: The percentage of the daily value of saturated fat needed by the average person
- `carbohydrates (PDV)`: The percentage of the daily value of carbohydrates needed by the average person
- `rating_missing`: A binary value indicating whether the value of rating is missing or not
- `cooking_time_binned`: This is a transformation of the continuous cooking_time into discrete bins
- `coooking_time_category`: This variable is used to provide more descriptive labels for different ranges of cooking time (Short, Medium, Long, Very Long)

This rich dataset provides the foundation for our exploration of the relationship between cooking time and recipe ratings, helping us better understand how these factors may be connected.

## Data Cleaning and Exploratory Data Analysis

### Data Cleaning





