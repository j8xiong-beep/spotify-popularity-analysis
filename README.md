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

Univariate Analysis: Popularity Distribution
To better understand the dataset, I first examined the distribution of Spotify popularity scores. The histogram below shows the distribution of song popularity across all tracks in the dataset.

<iframe
src="assets/popularity_distribution.html"
width="900"
height="550"
frameborder="0">
</iframe>


## Step 3: Assessment of Missingness

...

## Step 4: Hypothesis Testing

...

## Step 5: Prediction Problem

...

## Step 6: Baseline Model

...

## Step 7: Final Model

...

## Step 8: Fairness Analysis

...
