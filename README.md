# Sentiment Analysis of Human-Arthropod Interactions

## Purpose
These are the .rmds containing the code used in my Master's thesis, *Sentiment Analysis of Human-Arthropod Interactions (2021)*. .jp2 format figures are collected in figures.zip.

## Requirements
* [Census API key](https://api.census.gov/data/key_signup.html)
* iNaturalist account
* Twitter account with developer access + premium API subscription
* Twitter dev environment
* R libraries and dependencies
* [GeoDa](https://geodacenter.github.io/)

## Summary of steps
* Downloading iNaturalist data

1. Select your genera (or other taxa) of interest
1. Export observations using the [Export Observations tool on iNaturalist](https://www.inaturalist.org/observations/export) (alternatively, you can export directly from [GBIF's "iNaturalist Research-grade Observations" occurrence dataset](https://www.gbif.org/dataset/50c9509d-22c7-4a22-a47d-8c48425ef4a7))

* Processing iNaturalist data

1. If multiple, merge resulting data tables
1. Remove any observations that are not usable (not research-grade, coordinates unlisted due to being marked as private, etc.)
1. Convert tabular entries to points using latitude/longitude
1. Ensure CRS match, check for spatial overlap with a basemap, and clip to area of interest
1. Normalize by census data
1. Create maps/graphs; if your results are off you can return to the previous steps and re-examine your dataset
1. Export data from R and import to GeoDa for running Moran's I spatial autocorrelation

* Downloading Twitter data

1. Install libraries and update packages
1. Authenticate Twitter access and check token
1. Get tweets using your parameters (use as few parameters as possible; it is better to have more data and cut down your dataset than to not have enough)
1. Save tweets to CSV
1. Read in CSV (may need to break original CSV into parts and rbind if dataset is large)

* Processing Twitter data

1. Check for and remove duplicate tweets (using isUnique on text column; should visually examine duplicates before removing)
1. Remove any tweets that are not relevant to your topic (using grepl on text column to find key words)
1. Get latitude/longitude from bounding box coordinates (separate bbox coords column, delete unnecessary new columns, transform new columns to numeric, get centroids of bbox using (minlong+maxlong)/2 and (minlat+maxlat)/2, check for and drop any entries where is.na=”TRUE”)
1. Get state names by determining which entries do not have them, adding a projection to the coordinates from the previous step, checking for spatial overlap with a basemap, and using over to copy states to a new column
1. Normalize by census data
1. Create maps/graphs and perform sentiment analysis; if your results are off you can return to the previous steps and re-examine your dataset
1. Export data from R and import to GeoDa for running Moran's I spatial autocorrelation

* Combination

1. For multi-layered analysis, you can overlay the results from processing the iNaturalist data and the Twitter data. You can also choose to incorporate Google Trends data

In the future these steps might change to require more/less due to addition or deprecation of various features or attributes by Twitter post-v1.1 API.

## Questions/comments

@ me on [Twitter](https://twitter.com/easternhercules) or email `julianholman96 at gmail dot com`.
