<p align="center">
🎧 🎶 🎼 🎤 🎹
</p>

## Project Goal

Analyze factors that influence Spotify song popularity and build a predictive model.

## Introduction

Music plays an important role in my daily life, and I am interested in understanding why some songs become more popular than others. In recent years, platforms such as TikTok, Instagram Reels, and Spotify have made it possible for songs to reach millions of listeners within a very short period of time. This raises an interesting question: are there measurable characteristics that make a song more likely to become popular?

For this project, I use the Spotify Music Tracks dataset, which contains information on more than 110,000 songs. The dataset includes popularity scores, audio features, genre labels, and other metadata. Because it contains both numerical and categorical variables, it is well suited for exploratory data analysis, hypothesis testing, missingness analysis, and predictive modeling.

My primary research question is: **Do songs with higher danceability tend to receive higher popularity scores on Spotify?** Danceability measures how suitable a song is for dancing based on rhythm, beat strength, tempo, and overall musical characteristics. Since many viral songs on social media platforms are highly danceable, I want to investigate whether higher danceability is associated with greater popularity.

In addition to exploring this relationship, I will build machine learning models to predict song popularity using a variety of audio features. I will compare a baseline model with a more advanced final model and evaluate whether the final model performs fairly across different groups of songs.

Relevant variables used throughout this project include:

* **popularity:** Spotify popularity score ranging from 0 to 100, where higher values indicate greater popularity.
* **danceability:** A score between 0 and 1 that measures how suitable a song is for dancing.
* **energy:** A measure of the intensity and activity level of a song.
* **tempo:** Estimated beats per minute (BPM) of a song.
* **valence:** A measure of musical positivity, where higher values generally correspond to happier and more cheerful songs.


## Data Cleaning and Exploratory Data Analysis

The Spotify dataset contains 114,000 songs and 22 variables.

After examining the dataset structure using `info()`, I found that most variables were complete. However, several metadata columns such as artist name, album name, and track name contained a very small number of missing values.

Summary statistics for two important variables are shown below.

| Variable | Mean | Median | Min | Max |
|----------|------|--------|------|------|
| Popularity | 33.24 | 35 | 0 | 100 |
| Danceability | 0.567 | 0.580 | 0.000 | 0.985 |

These results suggest that the average popularity score is relatively low, while danceability is centered around 0.57.

I inspected the dataset structure and checked for missing values before beginning the analysis. Most variables used in this project, including popularity and danceability, contain complete observations. However, the tempo column contains a noticeable number of missing values (22,114 missing entries). Since tempo is not the primary variable used to answer my research question, I focused on variables with complete information such as popularity and danceability. No additional cleaning was required for these key variables, making the dataset suitable for further exploratory analysis and hypothesis testing.

## Univariate Analysis: Popularity Distribution
To better understand the dataset, I first examined the distribution of Spotify popularity scores. The histogram below shows the distribution of song popularity across all tracks in the dataset.

<iframe
src="assets/popularity_distribution.html"
width="750"
height="550"
frameborder="0">
</iframe>

The histogram shows that most songs have low to moderate popularity scores, with relatively few songs achieving extremely high popularity. This right-skewed distribution suggests that viral or highly successful songs are uncommon compared to the overall Spotify catalog.

## Univariate Analysis: Danceability Distribution
Next, I examined the distribution of danceability scores across all songs in the Spotify dataset. Since danceability is the primary explanatory variable in my research question, understanding its distribution provides important context for later analyses.

<iframe
src="assets/danceability_distribution.html"
width="750"
height="550"
frameborder="0">
</iframe>

This histogram shows that danceability scores are approximately centered around 0.6. Most songs fall between 0.4 and 0.8, while very low and very high danceability scores are relatively uncommon. The distribution is roughly unimodal and concentrated in the middle range, suggesting that songs in the Spotify dataset tend to be moderately danceable. Overall, danceability does not appear to be evenly distributed across all possible values, with most observations clustered around the center of the scale. This distribution provides useful context for the analyses conducted later in the project.

## Bivariate Analysis: Danceability vs Popularity

To investigate my research question, I created a scatter plot showing the relationship between danceability and popularity. Each point represents a song in the dataset.

<iframe
src="assets/danceability_vs_popularity.html"
width="750"
height="550"
frameborder="0">
</iframe>

This scatter plot shows the relationship between danceability and popularity for a sample of songs in the Spotify dataset. While songs with higher danceability scores appear across a wide range of popularity levels, there is no strong visual pattern indicating a clear relationship. The points are widely dispersed, suggesting that danceability alone may not fully explain differences in popularity. Additional analyses are needed to determine whether a statistically meaningful relationship exists between these two variables.

## Bivariate Analysis: Energy vs Popularity

I also examined energy because it is another audio feature that may be connected to how popular a song becomes.

<iframe
src="assets/energy_vs_popularity.html"
width="750"
height="550"
frameborder="0">
</iframe>

This scatter plot shows the relationship between energy and popularity for the sampled Spotify songs. The points are widely spread across different energy levels, suggesting that there is no strong visual relationship between energy and popularity. Popular songs appear at both moderate and high energy levels, while many high-energy songs still have low or moderate popularity. This suggests that energy alone is unlikely to explain song popularity.

## Interesting Aggregate: Average Popularity by Danceability Group

To better compare popularity across different levels of danceability, I divided songs into four danceability groups (Low, Medium-Low, Medium-High, and High) and calculated the average popularity score for each group.

<iframe
src="assets/average_popularity_by_danceability.html"
width="750"
height="550"
frameborder="0">
</iframe>

The bar chart shows that the average popularity scores are relatively similar across the four danceability groups. Songs in the Medium-Low and Medium-High groups have slightly higher average popularity scores than songs in the Low and High groups. This suggests that popularity does not increase consistently with danceability.

Overall, the differences between groups are fairly small, indicating that danceability alone is not a strong predictor of popularity. While moderate levels of danceability may be associated with slightly higher popularity, other audio features and external factors likely play a larger role in determining whether a song becomes successful on Spotify.

## Assessment of Missingness

NMAR Analysis

The <code>tempo</code> column contains a substantial number of missing values. Based only on the observed data, it is difficult to determine whether the missingness mechanism is NMAR (Not Missing At Random). One possible explanation is that tempo values may be unavailable for some songs because of limitations in Spotify's audio feature extraction process. Additional information about how Spotify generates audio features would be required to determine whether the missingness is truly NMAR.

Missingness Dependency Analysis

To investigate whether the missingness of the <code>tempo</code> column depends on other variables in the dataset, I performed permutation tests using both <code>popularity</code> and <code>explicit</code>.

<iframe
src="assets/tempo_missingness_popularity.html"
width="750"
height="550"
frameborder="0">
</iframe>

The boxplot above shows the distribution of popularity for songs with missing and non-missing tempo values. The two distributions appear very similar, with nearly identical medians and spreads.

A permutation test comparing popularity across the two groups produced a p-value of approximately <strong>0.734</strong>. Since this value is much larger than 0.05, I failed to reject the null hypothesis. This suggests that tempo missingness does not appear to depend on popularity.

Next, I investigated whether tempo missingness depends on whether a song is marked as explicit. The observed difference in explicit rates between songs with missing and non-missing tempo values was tested using a permutation test.

The permutation test produced a p-value approximately equal to <strong>0.000</strong>. Since this value is less than 0.05, I rejected the null hypothesis. This suggests that tempo missingness is associated with the <code>explicit</code> variable.

Overall, the results indicate that the missingness of <code>tempo</code> is not completely random. Because the missingness appears to depend on an observed variable (<code>explicit</code>), the missingness mechanism is more consistent with MAR (Missing At Random) rather than MCAR (Missing Completely At Random).


## Hypothesis Testing

Hypothesis Test 1: Danceability and Popularity

Research Question: Do songs with higher danceability tend to have higher popularity scores on Spotify?

<strong>Null Hypothesis:</strong> Songs with high danceability and songs with low danceability have the same average popularity.

<strong>Alternative Hypothesis:</strong> Songs with high danceability have higher average popularity than songs with low danceability.

<strong>Significance Level:</strong> α = 0.05

<iframe
src="assets/danceability_hypothesis_test.html"
width="1200"
height="550"
frameborder="0">
</iframe>

The observed difference in mean popularity between songs with high danceability and songs with low danceability was approximately <strong>0.531</strong>. The permutation test produced a p-value smaller than <strong>0.001</strong>.

Because the p-value is below the significance level of 0.05, I rejected the null hypothesis. This provides statistical evidence that songs with higher danceability tend to have slightly higher popularity scores on Spotify.

However, the observed difference is relatively small, so danceability alone is not enough to strongly explain song popularity. This result suggests that danceability may be associated with popularity, but other audio features and external factors likely also play an important role.

Hypothesis Test 2: Energy and Popularity

Research Question: Do songs with higher energy tend to have higher popularity scores on Spotify?

<strong>Null Hypothesis:</strong> Songs with high energy and songs with low energy have the same average popularity.

<strong>Alternative Hypothesis:</strong> Songs with high energy have higher average popularity than songs with low energy.

<strong>Significance Level:</strong> α = 0.05

<iframe
src="assets/energy_hypothesis_test.html"
width="750"
height="550"
frameborder="0">
</iframe>

The observed difference in mean popularity between songs with high energy and low energy was approximately <strong>-1.04</strong>.

The permutation test produced a p-value of <strong>1.0</strong>.

Because the p-value is much larger than 0.05, I failed to reject the null hypothesis.

The data do not provide evidence that songs with higher energy tend to have higher popularity scores on Spotify.

Interestingly, songs with higher energy had slightly lower average popularity in this dataset. However, this difference was not statistically significant and may simply be due to random variation.

Interpretation

Unlike danceability, energy did not show a statistically significant relationship with popularity. This suggests that energy alone is not a strong predictor of song popularity on Spotify.


## Framing Prediction Problem

The goal of this project is to predict a song's popularity score on Spotify using audio features and song characteristics available in the dataset.

The response variable is:

- popularity

Popularity is a numerical variable ranging from 0 to 100, representing how popular a song is on Spotify.

Because the response variable is continuous, this is a **regression problem** rather than a classification problem.

## Why Popularity?
Popularity is a key measure of a song’s success on Spotify. It summarizes listener engagement and overall performance on the platform. Throughout the exploratory data analysis and hypothesis testing sections, I examined how audio characteristics such as danceability and energy relate to popularity. Predicting popularity allows me to investigate whether these audio features can be used to explain and forecast a song’s success.

## Features Available at Time of Prediction

At the time a song is released, Spotify audio features can already be calculated. Therefore, I will use features such as:

- danceability
- energy
- loudness
- speechiness
- acousticness
- instrumentalness
- liveness
- valence
- tempo
- duration_ms
- explicit

These variables are available when a song is released and do not depend on future popularity outcomes. Therefore, they can reasonably be used as predictors without introducing data leakage.

I will not use popularity itself or any variables that directly depend on popularity.

## Evaluation Metric

I will evaluate model performance using Root Mean Squared Error (RMSE).

RMSE measures the typical magnitude of prediction errors while placing a larger penalty on large mistakes. Since popularity is a continuous numerical variable ranging from 0 to 100, RMSE is an appropriate metric for assessing regression performance.
Lower RMSE values indicate that predicted popularity scores are closer to the true popularity scores.


## Baseline Model

Response Variable:
- popularity

Features Used:
- danceability
- energy

Both predictors are quantitative variables, so no encoding was required.

These features were selected because they were explored in the hypothesis testing section and are related to song popularity.

## Performance

Evaluation Metric:
- RMSE

RMSE = 22.24

This indicates that predictions are typically about 22 popularity points away from the true popularity values.

## Assessment

The baseline model captures some information about popularity but its prediction error remains relatively large.

This suggests that popularity depends on additional song characteristics beyond danceability and energy alone.

For the final model, I plan to include additional features such as loudness, valence, acousticness, speechiness, tempo, and explicit status, as well as explore feature engineering techniques.

## Step 7: Final Model

...

## Step 8: Fairness Analysis

...
