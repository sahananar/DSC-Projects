# Recipes and Ratings

DSC 80 Project #3

By: Sahana Narayanan (sanarayanan@ucsd.edu)

# Introduction

This dataset contains information about recipes and the reviews and ratings submitted for them. The recipes dataset contains basic information about the name of the recipe, the cooking time, nutrition information, steps and a description. The ratings dataset contains information about the specific reviews given. 

The research question that I was the most interested in exploring was if there is a relationship between cooking time and the average rating of the recipes. I initially wondered if the average rating would be higher when the cooking time as more, as the food was prepared for longer, however this may also not necessarily be the case as some recipes simply may not require a longer cooking time and this wouldn't affect their rating, so I decided to investigate this topic further. 

The initial ratings dataset contained 731927 rows and 5 columns: 'user_id', 'recipe_id', 'date', 'rating', and 'review'. The initial recipes dataset contained 83782 rows and 12 columns: 'name', 'id', 'minutes', 'contributor_id', 'submitted', 'tags', 'nutrition', 'n_steps', 'steps', 'description', 'ingredients' and 'n_ingredients'. Once the datasets were merged together and cleaned (this will be further explained in the next section), the resulting dataset contained 234429 rows. While all columns from both datasets were kept, the ones that were most relevant were 'recipe_id', which identified the recipe, 'rating', which described how well the recipe was rated and 'minutes', indicating the cooking time. 

# Data Cleaning and EDA

**Data Cleaning**

The first step was to merge the ratings and recipes datasets together. I first had to rename the 'id' column of the recipes dataset to 'recipe_id', so that it would match the name of the column from the ratings dataset and the merge function would find a common column. The recipes dataset was then left merged with the ratings dataset. Next, all ratings of 0 were replaced with `np.nan`. This was a reasonable step as we can predict that instead of giving a recipe a 0 rating, it is more likely that the user did not submit their rating for that recipe and it had just been filled with 0 instead. 

Next, it was necessary to find the average rating per recipe, as this would be crucial to use for the analaysis. The table was grouped by 'recipe_id' and the mean of the ratings column for each recipe was found. Then, a new column was added to the dataframe ontaining these average ratings per recipe ID. 

The nutritional values for each recipe were stored in a format that resembled a list, however it was one large string. I thought it would be useful to have these individual values to investigate certain patterns for the bivariate analysis, so I split up the values and created a new column for each one, such as
'calories', 'total fat', 'sugar', 'sodium', 'protein', 'saturated fat', and 'carbohydrates'. 

Finally, while examining the `minutes` column which would be crucial for my analysis, I realized that several values were very large, the maximum such number being 1051200 minutes. These numbers are an unreasonable value for cooking time and it would not be logical to include values above a certain threshold in the analysis. Therefore, I decided to set the range to 600 minutes, or 10 hours. Any value larger than this would be replaced with np.nan as it is not reasonable a recipe would take significantly longer than this to prepare. 

Once this step was finished, I created a condensed dataframe which contained only the columns of 'name', 'recipe_id', 'minutes', 'n_steps', 'rating', 'avg_rating', 'calories', 'sugar', and 'protein'. Not all of these columns would be used later on however these were the ones I kept as I felt they were more relevant than columns such as 'description' or 'ingredients', which were irrelevant to my analysis and were also stretching out the size of the dataframe and making it look disproportionate. 

Here is the `head` of the cleaned and condensed dataframe:

| name                                 |   recipe_id |   minutes |   n_steps |   rating |   avg_rating |   calories |   sugar |   protein |
|:-------------------------------------|------------:|----------:|----------:|---------:|-------------:|-----------:|--------:|----------:|
| 1 brownies in the world    best ever |      333281 |        40 |        10 |        4 |            4 |      138.4 |      50 |         3 |
| 1 in canada chocolate chip cookies   |      453467 |        45 |        12 |        5 |            5 |      595.1 |     211 |        13 |
| 412 broccoli casserole               |      306168 |        40 |         6 |        5 |            5 |      194.8 |       6 |        22 |
| 412 broccoli casserole               |      306168 |        40 |         6 |        5 |            5 |      194.8 |       6 |        22 |
| 412 broccoli casserole               |      306168 |        40 |         6 |        5 |            5 |      194.8 |       6 |        22 |


Once all these steps were finished, the dataset had been cleaned and then I moved onto the analysis.

**Univariate Analysis**

Below is the histogram generated for the modified 'minutes' column of the dataset:

<iframe src="assets/minutes-histogram.html" width=800 height=600 frameBorder=0></iframe>

To further examine the distribution of the data in the first 100 minutes, where most of the data was clustered, I selected only those rows and then created another plot:

<iframe src="assets/minutes100-histogram.html" width=800 height=600 frameBorder=0></iframe>

The distribution is significantly skewed right, with most of the values lying in the 0-100 minutes range, as shown in more detail in the second plot. However, there are some outliers ranging until 500 to 600 minutes as well. From both plots, we can see that there are alternating 'spikes', where the bars get shorter and then taller again. Upon examination of the second plot, it seems like these 'spikes' occur at multiples of 5. This is most likely the case due to users deciding to 'round' their cooking times, for example if the actual cooking time of a recipe is 28 minutes, there is a likelihood of the user rounding this to 30 minutes as it is a more 'clean' number. 

Next, to examine the 'avg_rating' column, I decided to look at it using a boxplot:

<iframe src="assets/ratings-boxplot.html" width=800 height=600 frameBorder=0></iframe>

This plot is significantly skewed to the left, as it shows how most of the average ratings where on the higher side. The first quartile was at 4.5 stars and the third quartile was at 5 stars. It was rare that a recipe got an average or lower rating, as these values would be outliers. 

**Bivariate Analysis**

<iframe src="assets/scatterplot.html" width=800 height=600 frameBorder=0></iframe>

Here is a scatter plot of the 'minutes' and 'avg_rating' columns. The majority of the data is clustered in the top left corner of the dataset - where there is less cooking time and higher average ratings. This would seem natural based on the results of the univariate analyses conducted above - most of the data was in the range of 100 minutes of cooking time and most of the average ratings were 4 or 5 stars. However, there are still a significant number of data points in other parts of the plot, and I decided to investigate this relationship further later on. 

**Interesting Aggregates**

# Assessment of Missingness


# Hypothesis Testing

The topic I decided to investigate was the relationship between the cooking time and average rating of recipes. Specifically, I wanted to answer the question of whether recipes with a lower cooking time (under 100 minutes) would have a higher average rating than recipes with a cooking time of over 100 minutes. 

**Null Hypothesis** : The mean rating of recipes with a cooking time of under 100 minutes is equal to the mean rating of recipes with a cooking time of over 100 minutes. 

**Alternate Hypothesis** : The mean rating of recipes with a cooking time of under 100 minutes is greater than the mean rating of recipes with a cooking time of over 100 minutes. 

The significance level used here will be 1%. The test statistic used is the mean rating for recipes with under 100 minutes cooking time divided by 5 so it would be represented as a proportion, this value was 0.938. I simulated 100000 of the test statistic using the number of entries under 100 minutes as the sample size, which was 205218. 

The resulting p-value was 0.006915. Since this p-value is under the chosen significance level of 1%, this indicates we can reject the null hypothesis that the mean ratings of recipes with lower cooking times are equal to the main ratings of recipes with over 100 minutes cooking time. 
