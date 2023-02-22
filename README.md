# Recipes and Ratings

DSC 80 Project #3

By: Sahana Narayanan (sanarayanan@ucsd.edu)

# Introduction

This dataset contains information about recipes and the reviews and ratings submitted for them. The recipes dataset contains basic information about the name of the recipe, the cooking time, nutrition information, steps and a description. The ratings dataset contains information about the specific reviews given. 

The research question that I was the most interested in exploring was if there is a relationship between cooking time and the average rating of the recipes. I initially wondered if the average rating would be higher when the cooking time as more, as the food was prepared for longer, however this may also not necessarily be the case as some recipes simply may not require a longer cooking time and this wouldn't affect their rating, so I decided to investigate this topic further. 

The initial ratings dataset contained 731927 rows and 5 columns: 'user_id', 'recipe_id', 'date', 'rating', and 'review'. The initial recipes dataset contained 83782 rows and 12 columns: 'name', 'id', 'minutes', 'contributor_id', 'submitted', 'tags', 'nutrition', 'n_steps', 'steps', 'description', 'ingredients' and 'n_ingredients'. Once the datasets were merged together and cleaned (this will be further explained in the next section), the resulting dataset contained 234429 rows. While all columns from both datasets were kept, the ones that were most relevant were 'recipe_id', which identified the recipe, 'rating', which described how well the recipe was rated and 'minutes', indicating the cooking time. 

# Data Cleaning and EDA

**Cleaning**

The first step was to merge the ratings and recipes datasets together. I first had to rename the 'id' column of the recipes dataset to 'recipe_id', so that it would match the name of the column from the ratings dataset and the merge function would find a common column. The recipes dataset was then left merged with the ratings dataset. Next, all ratings of 0 were replaced with `np.nan`. This was a reasonable step as we can predict that instead of giving a recipe a 0 rating, it is more likely that the user did not submit their rating for that recipe and it had just been filled with 0 instead. 

Next, it was necessary to find the average rating per recipe, as this would be crucial to use for the analaysis. The table was grouped by 'recipe_id' and the mean of the ratings column for each recipe was found. Then, a new column was added to the dataframe ontaining these average ratings per recipe ID. 

The nutritional values for each recipe were stored in a format that resembled a list, however it was one large string. I thought it would be useful to have these individual values to investigate certain patterns for the bivariate analysis, so I split up the values and created a new column for each one, such as
'calories', 'total fat', 'sugar', 'sodium', 'protein', 'saturated fat', and 'carbohydrates'. 

Here is the `head` of the cleaned dataframe including some of the more relevant columns. Not all columns may be used later on but I decided not to include colums such as 'description' or 'ingredients' as they were irrelevant to my analysis and were also stretching out the size of the dataframe and making it look disproportionate. 

| name                                 |   recipe_id |   minutes |   n_steps |   rating |   avg_rating |   calories |   sugar |   protein |
|:-------------------------------------|------------:|----------:|----------:|---------:|-------------:|-----------:|--------:|----------:|
| 1 brownies in the world    best ever |      333281 |        40 |        10 |        4 |            4 |      138.4 |      50 |         3 |
| 1 in canada chocolate chip cookies   |      453467 |        45 |        12 |        5 |            5 |      595.1 |     211 |        13 |
| 412 broccoli casserole               |      306168 |        40 |         6 |        5 |            5 |      194.8 |       6 |        22 |
| 412 broccoli casserole               |      306168 |        40 |         6 |        5 |            5 |      194.8 |       6 |        22 |
| 412 broccoli casserole               |      306168 |        40 |         6 |        5 |            5 |      194.8 |       6 |        22 |


Once all these steps were finished, the dataset had been cleaned and then I moved onto the analysis.

**Univariate Analysis**


# Assessment of Missingness


# Hypothesis Testing
