# Spotify Music Recommendation Project : Project Overview
* Created an unsupervised machine learning project that tends to make music recommendations according to a user's list of songs they used to listen to.
* Collected data to work with from kaggle (a dataset named `recommendation-system-spotify` within Datasets section).
* Cleaned data up and engineered features so they will help us in the prediction process like creating one hot encoded features.
* Connected to `Spotify` API and generated music recommendations according to my Playlist's list of songs using `cosine similarity` technique.

## Code and Resources used
<b>Python Version :</b> 3.9<br>
<b>Packages :</b> Numpy, Pandas, Matplotlib, Spotipy, PIL, Scikit-learn<br>
<b>For Web Framework Requirements :</b> `pip install -r requirements.txt`

## Data Collection
Collect data from kaggle website to get a dataset that has 170653 songs and another that has 28680 artists with songs' genres. So, we got the following :
* The musical positiveness conveyed by a track
* Track release year
* Whether the track is acoustic
* List of artists that contributed to a track
* How suitable a track is for dancing based on a combination of musical elements including tempo, rhythm stability, beat strength, and overall regularity
* The duration of a track in milliseconds
* A perceptual measure of intensity and activity
* Whether or not a track contains curse words that is generally deemed sexual, violent, or effensive in nature
* Track's id
* whether a track contains no vocals
* The key the track is in
* The presence of an audience in the recording
* The overall loudness of a track in decibels (dB)
* The modality (major or minor) of a track, the type of scale from which its melodic content is derived
* Track's name
* The total number of plays the track has had and how recent those plays are
* Track's release date
* The presence of spoken words in a track
* The overall estimated tempo of a track in beats per minute (BPM)
* Track's list of genres

## Data Cleaning
Clean the data up to make it ready for modeling process. I made the following changes:
* Changed the artists and genres features' types to a list
* Created a new feature that combines both track name and artists' names who have contributed in the realisation of that song and drop duplicates on this variable
* Exploded artists' column, merged it with artists related dataset and enriched spotify dataset with genres information extracted from the newly made dataframe that combines exploded artists, genres and tracks musical characteristics
* Created 5-point bucket for popularity feature
* Made dummy variables for year and popularity features
* Normalized float features using MinMax Scaler
* Generated TF-IDF features from genres list feature

## Connection to Spotify API
At first, I created a Spotify web app that'll manage my playlists, logged in my Spotify account and created some playlists to use in the recommendation phase based on the songs I used to listen to. Then, I extracted my secret token so I don't have to authentificate every time I want to connect to Spotify API. After that, I pulled out songs that belong to our spotify dataset because I'll make my recommendation system based on them.

## Recommendation System Building
This phase consists of two steps:
* <b>Creating Playlist Vector :</b> Summarize my playlist into a single vector created by multiplying Spotify numerical list of features already created in precedent steps by weight and summing up every row to create a single vector for all songs. Also, it's so important to note that weight factor is chosen so that so our system could recommend us the most recent songs that have been published so far.
* <b>Making recommendations :</b> Compare my playlists' vectors to other songs' vector in Spotify dataset using `Cosine Similarity` score and extract the most 24 similar tracks to it (Highest cosine similarity).
