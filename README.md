# Data Collection Overview

This repository contains details about the data accompanying the paper [Algorithmic Behaviors Across Regions: A Geolocation Audit of YouTube Search for COVID-19 Misinformation between the United States and South Africa](https://arxiv.org/abs/2409.10168).

The data was collected through our geolocation audit experiment. Through the audit experiment, we investigate and compare the prevalence of COVID-19 misinformation surfaced by YouTube's search engine between the United States and South Africa, the countries heavily affected by the pandemic in the Global North and Global South, respectively. For each country, we selected 3 geolocations, placed twin sock-pupets (bots emulating real users) that collected the top-50 search results for 48 search queries belonging to 8 globally persistent COVID-19 misinformation topics, such as "Bill Gates Claims." To gain deeper insights into the platform's sorting algorithm, we sorted the search results across 4 search filters "Relevance" (default filter), "Upload Date," "View Count," and "Rating." The audit was conducted over 10 days from January 30th, 2023 to February 9th, 2023, resulting in 915K search results (of which 10,139 videos were unique). 

We scored the videos based on their stance toward COVID-19 misinformation and compared the amount of misinformation present in search results between the US and SA. The videos were initially labeled along a 7-point scale: "Opposing COVID-19 Misinformation (-1),' "Neutral COVID-19 Information (0)," "Supporting COVID-19 Misinformation (1)," "On the COVID-19 origins in Wuhan, China (2)," "Irrelevant (3)," "Video in a language other than English (4)," and "URL not accessible (5)" (See Appendix Table 7 in the paper). However, we normalized the annotations to a 3-point scale based on their stance on COVID-19 misinformation: supporting, neutral, and opposing (see subsection "Consolidating from 5-classes to 3-classes" in the paper for more information). 

# Data Description
Below, we describe each data and their fields.

**1. Search Queries** (`queries.csv`): The file consists of a complete list of 48 search queries used in the audit study. It contains the following fields:
- `Query`: name of the search query
- `Topic`: name of the COVID-19 misinformation topic

A snippet:
```html
Query, Topic                                                                                  
bill gates exposed, COVID-19 Bill Gates Claims
```

**2. Ground-Truth Annotations** (`manual-annotation/youtube-audit-ground-truth-annotated-video-dataset.csv.zip`): The file contains a dataset of 3,075 YouTube videos that have been annotated for COVID-19 misinformation. The annotations were conducted by the first author and Amazon Mechanical Turk (AMT). For detailed information on the annotation process, please refer to the section "Creating the Ground-Truth Dataset" in the paper. The dataset contains the following fields:
- `Video ID`: ID of the YouTube Video; This code is extracted from the Video URL
- `Video URL`: URL of the YouTube Video
- `Video Title`: Title of the YouTube Video
- `Video Description`: Description of the YouTube Video
- `Transcript`: Transcript from the YouTube Video
- `Tag`: Tags from the YouTube Video
- `Channel Title`: Name of Channel that uploaded the YouTube Video
- `Channel ID`: ID of the Channel that uploaded the YouTube Video
- `Publish Date`: Publish Date of the YouTube Video
- `Thumbnail (Default)`: YouTube Video Thumbnail URL 
- `Default language`: Default Language Metadata indicated by the YouTube Video
- `Duration`: Duration of the YouTube Video
- `Caption Available`: Metadata on whether caption was available or not on the YouTube Video (TRUE/FALSE)
- `Video Views`: View Count of the YouTube Video
- `Like`: Like Count of the YouTube Video
- `Favorite Count`: Favorite Count of the YouTube Video
- `# of Comments`: Number of Comments on the YouTube Video
- `Annotation`: Annotation label of the YouTube Video (Used the 7-point scale; `Data Collection Overview` section above or Appendix Table 7 in the paper for more information)
- `Top 100 Comments`: Top 100 Comments on the YouTube Video

A snippet: 
(Note: Empty fields are indicated by a blank space, and excessively long data entries are abbreviated with "...")
```html
Video ID, Video URL, Video Title, Video Description, Transcript, Tag, Channel Title, Channel ID, Publish Date, Thumbnail (Default), Default language, Duration, Caption Available, Video Views, Like, Favorite Count, # of Comments, Annotation, Top 100 Comments
x-wj8AXLDUI, https://www.youtube.com/watch?v=x-wj8AXLDUI, COVID 19 VACCINES BEING TESTED IN AFRICA AFTER ALL THE NOISE WE MADE., COVID 19 VACCINES ARE CURRENTLY BEING TESTED IN SENEGAL..., ..., ..., ..., ..., 2020-04-15 00:46:24+00:00, https://i.ytimg.com/vi/x-wj8AXLDUI/default.jpg, , PT21M56S, FALSE, 66.0, 18.0, 0.0, 0.0, 1, ,
```

**3. Non-English Video Annotations** (`manual-annotation/non-english-video-annotations.csv.zip`): The file contains 784 non-English videos from our audit data, manually annotated for COVID-19 misinformation. Please see section "Handling Videos in Non-English Languages" for more information. The dataset contains the following fields:
- `Annotation`: Annotation label of the YouTube Video (Used the 7-point scale; `Data Collection Overview` section above or Appendix Table 7 in the paper for more information).
- `Video ID`: ID of the YouTube Video; This code is extracted from the Video URL
- `Video URL`: URL of the YouTube Video
- `Video Title`: Title of the YouTube Video
- `Video Description`: Description of the YouTube Video
- `Transcript`: Transcript from the YouTube Video
- `Tag`: Tags from the YouTube Video
- `Channel Title`: Name of Channel that uploaded the YouTube Video
- `Channel ID`: ID of the Channel that uploaded the YouTube Video
- `Publish Date`: Publish Date of the YouTube Video
- `Thumbnail (Default)`: YouTube Video Thumbnail URL 
- `Default language`: Default Language Metadata indicated by the YouTube Video
- `Duration`: Duration of the YouTube Video
- `Caption Available`: Metadata on whether caption was available or not on the YouTube Video (TRUE/FALSE)
- `Video Views`: View Count of the YouTube Video
- `Like`: Like Count of the YouTube Video
- `Favorite Count`: Favorite Count of the YouTube Video
- `# of Comments`: Number of Comments on the YouTube Video


A snippet: 
(Note: Empty fields are indicated by a blank space, and excessively long data entries are abbreviated with "...")
```html
Annotation, Video ID, Video URL, Video Title, Video Description, Transcript, Tag, Channel Title, Channel ID, Publish Date, Thumbnail (Default), Default language, Duration, Caption Available, Video Views, Like, Favorite Count, # of Comments
-1, s6f9DJY6aqM, https://www.youtube.com/watch?v=s6f9DJY6aqM, Prevention the Spread of Covid-19 抑制新冠肺炎的扩散, Since the outbreak of Covid-19 in December 2019..., , , ..., ..., 2021-09-08T17:06:55Z, https://i.ytimg.com/vi/s6f9DJY6aqM/default.jpg, , PT9M3S, FALSE, 27.0, 3.0, 0.0, 0.0,
```

**4. Unique Video Annotations** (`manual-annotation/unique-video-annotations-normalized.csv.zip`)**: The file contains 10,139 unique videos collected during the audit. Approximately one-third of the videos were annotated by humans from the datasets in#2 (Ground-Truth Annotations) and #3 (Non-English Video Annotations), while the rest were annotated by a classifier (see Section 5 in the paper for more details). The annotation labels have been normalized to a 3-point scale based on their stance on COVID-19 misinformation: supporting (1), neutral (0), opposing (-1). See subsection "Consolidating from 5-classes to 3-classes" in the paper for more information. The dataset contains the following fields:
- `Index`: Index number associated with the particular YouTube video
- `Video ID`: ID of the YouTube Video; This code is extracted from the Video URL
- `Video URL`: URL of the YouTube Video
- `Video Title`: Title of the YouTube Video
- `Video Description`: Description of the YouTube Video
- `Transcript`: Transcript from the YouTube Video
- `Tag`: Tags from the YouTube Video
- `Channel Title`: Name of Channel that uploaded the YouTube Video
- `Channel ID`: ID of the Channel that uploaded the YouTube Video
- `Publish Date`: Publish Date of the YouTube Video
- `Thumbnail (Default)`: YouTube Video Thumbnail URL 
- `Default language`: Default Language Metadata indicated by the YouTube Video
- `Duration`: Duration of the YouTube Video
- `Caption Available`: Metadata on whether caption was available or not on the YouTube Video (TRUE/FALSE)
- `Video Views`: View Count of the YouTube Video
- `Like`: Like Count of the YouTube Video
- `Favorite Count`: Favorite Count of the YouTube Video
- `# of Comments`: Number of Comments on the YouTube Video
- `Annotation`: Normalized annotation label of the YouTube Video. A 3-point scale based on their stance on COVID-19 misinfo: supporting (1), neutral (0), opposing (-1)

A snippet: 
(Note: Empty fields are indicated by a blank space, and excessively long data entries are abbreviated with "...")
```html
Index, Video ID, Video URL, Video Title, Video Description, Transcript, Tag, Channel Title, Channel ID, Publish Date, Thumbnail (Default), Default language, Duration, Caption Available, Video Views, Like, Favorite Count, # of Comments, Annotation
0, X2VIcb0VeQg, https://www.youtube.com/watch?v=X2VIcb0VeQg, Man denies Pfizer COVID vaccine claims he told Project Veritas | Morning in America, ..., ..., ..., NewsNation, UCCjG8NtOig0USdrT5D1FpxQ, 2023-02-03T15:53:21Z, https://i.ytimg.com/vi/X2VIcb0VeQg/default.jpg, , PT3M17S, TRUE, 48983.0, 484.0, 0.0, 336.0, 1,
```

**5. Geolocation Audit Search Results** (`search-results/*`): As outlined in the `Data Collection Overview`, the audit experiment deployed twin sock-puppet bots in three different geolocations within both the United States and South Africa. These bots collected the top-50 search results for 48 search queries across 4 search filters. The `search-results/` directory contains 12 files, each corresponding to one of the twin bots at a particular geolocation. The file are named using the format: {*geolocation*}-bot{*number*}-top50-search-results.csv.zip, where the bots are identified by either number 1 or 2. Each file contains the following fields:
- `Run #`: Index (1-10) representing the day of the data collection
- `Search Query`: The query entered
- `Search Filter Type`: The type of the search filter. Note: always going to be value "Video"
- `Search Filter Sort-By`: The filter used for sorting the search results (e.g. Relevance, Upload Date, View Count, Rating)
- `Video Title`: Title of the YouTube Video
- `Video URL`: URL of the YouTube Video
- `Video ID`: ID of the YouTube Video; This code is extracted from the Video URL
- `Search Result Rank`: The rank of the video in the search results
- `Channel Name`: Name of channel that uploaded the YouTube Video
- `Channel URL`: URL of the channel that uploaded the YouTube Video
- `Date Published`: Publish Date of the YouTube Video
- `annotation`: Normalized annotation label of the YouTube Video. A 3-point scale based on their stance on COVID-19 misinfo: supporting (1), neutral (0), opposing (-1)

A snippet: 
(Note: Empty fields are indicated by a blank space, and excessively long data entries are abbreviated with "...")
```html
Run #, Search Query, Search Filter Sort-By, Video Title, Video URL, Video ID, Search Result Rank, Channel Name, Channel URL, Date Published, annotation
1, lab_leak_theory, Video, Relevance, Why the China Covid lab-leak theory is being taken seriously - BBC News, youtube.com/watch?v=pktSL5kL3ZI, pktSL5kL3ZI, 1, BBC News, , 1 year ago, 0,
```

All the search results CSV files are sorted based on the `Video Title`, so users may need to sort and organize the data as needed (e.g., using Python's Pandas library). For example, if a user wants to extract search results for the query *lab_leak_theory* with the search filter *Relevance* on run #5, they can use a command like:

```html
df.loc[(df["Run #"] == 5) & (df["Search Query"] == "lab_leak_theory") & (df["Search Filter Sort-By"] == "Relevance")].sort_values("Search Result Rank")
```

This will return the top-50 search results, sorted by rank from 1 to 50. Since our analysis focused on the top-10 search results, which are most likely to capture viewers' attention, users can filter the data further to include only the top-10 search results by adding a condition for `Search Result Rank`:

```html
df.loc[(df["Run #"] == 5) & (df["Search Query"] == "lab_leak_theory") & (df["Search Filter Sort-By"] == "Upload Date") & (df["Search Result Rank"] <= 10)].sort_values("Search Result Rank")
```

This will return the top-10 search results, sorted based on their search result rank.

# Citation
If you used this dataset in your research, please cite our work at:

```bibtex
@misc{jung2024algorithmicbehaviorsregionsgeolocation,
      title={Algorithmic Behaviors Across Regions: A Geolocation Audit of YouTube Search for COVID-19 Misinformation between the United States and South Africa}, 
      author={Hayoung Jung and Prerna Juneja and Tanushree Mitra},
      year={2024},
      eprint={2409.10168},
      archivePrefix={arXiv},
      primaryClass={cs.CY},
      url={https://arxiv.org/abs/2409.10168}, 
}
```
