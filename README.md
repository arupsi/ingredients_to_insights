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

To ensure the dataset was ready for analysis, several steps were carried out to clean and preprocess the data:

1. **Merging Datasets**: The recipes and interactions datasets were merged using a common identifier (`id`), combining the recipe information with user interactions such as ratings.
   
2. **Handling Missing and Zero Ratings**: Ratings of `0` were replaced with missing values (`NaN`) to avoid bias in the analysis. The average rating for each recipe was then calculated and added as a new column (`average_rating`).

3. **Dropping Unnecessary Columns**: To focus on the most relevant information, columns such as `name`, `contributor_id`, `submitted`, `tags`, `description`, `user_id`, `date`, `review`, `steps`, and individual `rating` were removed from the dataset.

4. **Processing Nutrition Data**: The `nutrition` column, which contained a list of nutritional values, was split into individual columns for calories, total fat, sugar, sodium, protein, saturated fat, and carbohydrates. This allowed for a more detailed analysis of the nutritional content of each recipe.

5. **Removing Duplicates**: Any duplicate entries based on the recipe ID were removed to ensure each recipe appeared only once in the dataset.

This process helped ensure that the dataset was clean, consistent, and ready for further analysis of recipe ratings and cooking times.

Below is a preview of the first few rows of the dataset, showcasing the cleaned and processed data used for analysis.

| id | minutes | n_steps | ingredients | n_ingredients | average_rating | calories (#) | total fat (PDV) | sugar (PDV) | sodium (PDV) | protein (PDV) | saturated fat (PDV) | carbohydrates (PDV) | rating_missing | cooking_time_binned | cooking_time_category |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 333281 | 40 | 10 | ['bittersweet chocolate', 'unsalted butter', 'eggs', 'granulated sugar', 'unsweetened cocoa powder', 'vanilla extract', 'brewed espresso', 'kosher salt', 'all-purpose flour'] | 9 | 4.0 | 138.4 | 10.0 | 50.0 | 3.0 | 3.0 | 19.0 | 6.0 | 0 | 0 | Medium |
| 453467 | 45 | 12 | ['white sugar', 'brown sugar', 'salt', 'margarine', 'eggs', 'vanilla', 'water', 'all-purpose flour', 'whole wheat flour', 'baking soda', 'chocolate chips'] | 11 | 5.0 | 595.1 | 46.0 | 211.0 | 22.0 | 13.0 | 51.0 | 26.0 | 0 | 0 | Medium |
| 306168 | 40 | 6 | ['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions'] | 9 | 5.0 | 194.8 | 20.0 | 6.0 | 32.0 | 22.0 | 36.0 | 3.0 | 0 | 0 | Medium |
| 286009 | 120 | 7 | ['butter', 'sugar', 'eggs', 'all-purpose flour', 'whole milk', 'pure vanilla extract', 'almond extract'] | 7 | 5.0 | 878.3 | 63.0 | 326.0 | 13.0 | 20.0 | 123.0 | 39.0 | 0 | 0 | Long |
| 475785 | 90 | 17 | ['meatloaf mixture', 'unsmoked bacon', 'goat cheese', 'unsalted butter', 'eggs', 'baby spinach', 'yellow onion', 'red bell pepper', 'simply potatoes shredded hash browns', 'fresh garlic', 'kosher salt', 'white pepper', 'olive oil'] | 13 | 5.0 | 267.0 | 30.0 | 12.0 | 12.0 | 29.0 | 48.0 | 2.0 | 0 | 0 | Long |

### Univariate Analysis

The plot shows the distribution of calories across various recipes in the dataset. Most recipes contain between 0 and 1000 calories, with a significant spike around the lower calorie range. A small number of recipes exceed 1000 calories, but they are less common. This visualization highlights how most recipes in the dataset tend to be lower in calories, which may suggest that the dataset includes many healthy or low-calorie options.



### Bivariate Analysis

The second scatter plot illustrates the relationship between the number of carbohydrates (measured as a percentage of daily value) and the total number of calories in recipes. As expected, there is a positive correlation: recipes with higher carbohydrate content tend to have more calories. However, there are some outliers, such as a few recipes with extremely high carbohydrate content but relatively fewer calories. This plot demonstrates the general trend that carbohydrate-rich recipes are also higher in calories.

