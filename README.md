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

<iframe
  src="my_plot.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

### Bivariate Analysis

The second scatter plot illustrates the relationship between the number of carbohydrates (measured as a percentage of daily value) and the total number of calories in recipes. As expected, there is a positive correlation: recipes with higher carbohydrate content tend to have more calories. However, there are some outliers, such as a few recipes with extremely high carbohydrate content but relatively fewer calories. This plot demonstrates the general trend that carbohydrate-rich recipes are also higher in calories.

<iframe
  src="my_plot2.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

### Interesting Aggregates

The table below presents the average nutritional values grouped by the number of ingredients in each recipe. Specifically, it shows the mean values for calories, carbohydrates, and total fat content across recipes with different ingredient counts. This analysis highlights potential relationships between the complexity of a recipe, in terms of the number of ingredients, and its nutritional profile.

| n_ingredients | calories (#) | carbohydrates (PDV) | total fat (PDV) |
| --- | --- | --- | --- |
| 1.0 | 714.65 | 11.357142857142858 | 91.0 |
| 2.0 | 331.98340026773764 | 11.21954484605087 | 25.550200803212853 |
| 3.0 | 306.11165670367205 | 10.617847993168231 | 22.244235695986337 |
| 4.0 | 336.0086810979692 | 11.957598750278956 | 23.704753403258202 |
| 5.0 | 347.8010182370821 | 12.111854103343465 | 25.438297872340424 |

Note that the first five rows of the grouped table have been displayed.

## Assessment of Missingness

In this section, the relationship between missing values in the `average_rating` column and other variables in the dataset was explored. Specifically, a permutation test was performed to assess whether the missingness of `average_rating` is dependent on `cooking_time_binned` and `cooking_time_category`.

### NMAR (Not Missing At Random) Considerations:
The missingness in the `average_rating` column **does not appear to be NMAR** (Not Missing At Random). This is because the missing values in the `average_rating` column are unlikely to depend on the actual values of the ratings themselves, but rather on other variables like cooking time or other recipe characteristics. If the missingness were NMAR, it would imply that the reason for the missing values is directly related to the missing ratings, which doesn’t seem to be the case here.

### P-Value for the Missingness-Dependent Column:
When testing for dependency between the missingness of `average_rating` and `cooking_time_category`, the observed test statistic was **0.00394**, and the p-value was **0.322**. Since the p-value is greater than the commonly used significance level of 0.05, we **fail to reject the null hypothesis**, indicating that there is **no significant relationship** between the missingness of `average_rating` and cooking time categories. This suggests that whether a recipe's rating is missing or not does not depend on its cooking time category.

### P-Value for the Missingness-Independent Column:
Similarly, the permutation test for the `cooking_time_binned` variable yielded a p-value greater than 0.05, which further supports the conclusion that the missingness in `average_rating` is **not dependent on cooking time** (whether binned or categorized).

Overall, the results of the permutation tests indicate that the missing values in `average_rating` are likely missing at random (MAR) with respect to the cooking time variables. This means the missingness of the rating data does not seem to be driven by cooking times, allowing for more flexible analysis without having to account for NMAR conditions.

## Hypothesis Testing

In this section, a permutation test was conducted to assess the relationship between cooking time and the average rating of recipes. The goal was to determine whether there is a significant difference in the average ratings of recipes based on their cooking time categories.

### Null Hypothesis (H₀):
There is no significant difference in the average ratings of recipes across different cooking time categories. Any observed differences in ratings are due to random chance.

### Alternative Hypothesis (H₁):
There is a significant difference in the average ratings of recipes across different cooking time categories.

### Significance Level:
A significance level of **0.05** was chosen for this test.

### Test Statistic and P-Value:
- **Observed difference in average ratings**: 0.012
- **P-value**: 0.176

Since the p-value (0.176) is greater than the significance level of 0.05, we **fail to reject the null hypothesis**. This means that there is no statistically significant difference in the average ratings of recipes across different cooking time categories. Any differences observed in the average ratings are likely due to random variation rather than a meaningful relationship between cooking time and ratings.

## Framing a Prediction Problem

**Prediction Problem**: The goal of this project is to **predict the calorie content of recipes based on the number of ingredients and total fat content**. This is a regression problem because the response variable, `calories (#)`, is a continuous numeric value that we are trying to estimate.

**Response Variable**: The response variable for this prediction problem is **`calories (#)`**. This variable corresponds to the prediction problem because we are interested in predicting the exact number of calories a recipe contains, making it the key target for our regression model.

**Evaluation Metric**: The model is evaluated using the **Root Mean Squared Error (RMSE)**. RMSE was chosen as the evaluation metric because it provides an interpretable estimate of how much, on average, the predicted calorie content deviates from the actual calorie content. RMSE is preferred over other metrics because it penalizes larger errors more heavily, making it a good fit for regression problems where outliers or large deviations are undesirable.

The features used in this report include:
- **n_ingredients**: The number of ingredients in a recipe.
- **total fat (PDV)**: The total fat content in the recipe.

These features are readily available at the time of prediction since both the number of ingredients and fat content are known when the recipe is created. These variables are also strong predictors of calorie content, as recipes with more ingredients and higher fat content are likely to have more calories.

## Baseline Model

- **n_ingredients**: Quantitative (number of ingredients)
- **total fat (PDV)**: Quantitative (total fat content)

The RMSE score of our model came out to be approximately **269.42**, which indicates that, on average, the model’s predictions deviate from the actual values of calorie content of recipes by **269.42 units**. Since this number is too high, we would classify the performance of this model as **average**.

## Final Model

- **n_ingredients**: This feature was included because the number of ingredients directly affects the complexity of a recipe, which in turn influences its calorie content. Recipes with more ingredients tend to have more calories, making this a valuable predictor.
- **total fat (PDV)**: Total fat content is an essential feature for predicting the calorie content of a recipe, as fat is one of the macronutrients contributing directly to calorie count. Including this feature improves the model's ability to estimate the calorie content accurately.

The final model used is a **RandomForestRegressor**, which is a powerful ensemble method that works well for regression tasks by building multiple decision trees and averaging their predictions.

- **Number of Estimators (`n_estimators`)**: This refers to the number of trees in the forest. The model tested with a value of 100.
- **Maximum Depth (`max_depth`)**: This controls how deep each tree in the forest can grow. The model tested with both `None` (no limit) and `10` as values.

### Best Hyperparameters:
- **Best number of estimators**: 100
- **Best maximum depth**: 10

The hyperparameters were selected using **GridSearchCV**, a method that exhaustively tests combinations of hyperparameters through cross-validation to find the best performing ones based on the root mean squared error (RMSE).

The final model showed an RMSE of **359.04**, which is higher than the baseline model’s RMSE of 269.42. Although the RandomForestRegressor model added complexity and hyperparameter tuning, it did not outperform the baseline linear regression model in this specific case. This result highlights that more complex models do not always guarantee better performance, particularly if the features or the data do not support the added complexity.

## Fairness Analysis

- **Group X**: Recipes whose number of ingredients is less than or equal to the median number of ingredients in the training dataset.
- **Group Y**: Recipes whose number of ingredients is greater than the median.

- **Root Mean Squared Error (RMSE)**: Used for evaluating prediction error.
- **R² Score**: Assesses the proportion of variance in the dependent variable that is predictable from the independent variable(s).

- **Null Hypothesis**: The model is fair for a low number of ingredients vs high number of ingredients and low fat vs high fat.
- **Alternate Hypothesis**: The model is unfair for a low number of ingredients vs high number of ingredients and low fat vs high fat.

The test statistic is the difference in RMSE and R² scores between the two groups.

The significance level is 0.05.

The p-value is 0.0438

Based on the analysis, there appears to be evidence enabling us to **reject the null hypothesis**, suggesting that the model may not be fair according to the defined metrics.

Unlocking the recipe for success, this project showed how ingredient data can dish out powerful predictions, revealing the balance between simplicity, accuracy, and fairness.
