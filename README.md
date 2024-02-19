# LEDE Project 1: Swimming

This repository include the jupyter notebooks used to collect, clean and analyze data for the first project I've worked on as a part of the Lede program for Data Journalism, an intensive summer program from Columbia Graduate School of Journalism.

While working on this project I aimed at learning how to spot undocumented API and use them to collect structured data. By working on the World Aquatics undocumented API, I wanted to have enough historical data to spot interesting trends or undocumented facts about the evolution of this sport.

### [Read the story](https://marcodallastella.github.io/swimming)

## Summary of findings
The two years of 2008 and 2009 resulted in an unprecedented wave of world records in swimming due to the introduction of advanced technology in swimsuits. After those swimsuits were banned in 2010, average times among top-50 rankings increased, but soon started decrease again and by 2020 they were already around the times recorded during the tech-swimsuits era. While world records became scarcer, by 2021 the average time for a top-50 race in all disciplines is remarkely lower than 2009.


### Notebooks:

* [1. Getting the data](1_swimming_data.ipynb)
* [2. Cleaning the data](2_swimming_cleaning.ipynb)
* [3. Analyzing the data](3_swimming_analysis.ipynb)

## 1. Data Collection

This notebook uses the undocumented API the World Aquatics to collect information regarding the top-50 times registered for every individual race since 1972 to 2023.

Because not all four strokes have the same races, it is composed of three sections:

* 1. Common races: collect data for the 50, 100, 200 meters in the four strokes
* 2. Freestyle-specific races: collect data for the 400, 800 and 1500m freestyle.
* 3. Medley-specific races: collect data for the 200 and 400 meters medley.

Then save the results in the `1_output.csv` file.

## 2. Data Cleaning

I used this notebook to clean the data and extract what I needed for my analysis.

* From the `1_output.csv` file, only selects columns that I am interested in, and change the date to have only the year of each time.

* I wanted to format the `time` value in a way that I could use to do some math. To do so, I formatted it in a `timedelta` object and used it to calculate the seconds of each time.

* Fix a mistake in the dataset, which I noticed only after, that included eleven times wrongly categorized as 800m instead of 1500m.

Output: `2_output_clean.csv`

* Reduce the dataset to have a coherent set of entries for each year and for yeach discipline. I decided to choose 2003 as my starting year, since years before that had inconsistent data.

Output: `2_output_2003.csv` file.

## 3. Data Analysis

I used this notebook to analyze my dataset and see if I can spot some interesting trend.

* Create a pivot table counting how many times each country registered a top-50 time.
Output: `3_countries_pivot.csv` 

* Compare the average time for the top-50 times for each stroke, and focus on how this changed during the tech-swimsuit revolution of 2007 and 2008. To do so, I calculated average times in seconds for each discipline in each year, and then calculate the percentage change compared to the starting year of 1991. (This last passage was done on Excel).
Output: `3_average_times_fixed.csv`.

* Compare the average time for the top-50 times for each race and each stroke since 2003.
Output: `3_pivot_disciplines.csv` 

* Calculate how many world records were set each year.
Output: `3_pivot_strokes.csv`

### Tools, skills, approaches
* I used [this guide](https://inspectelement.org/apis.html) to find the undocumented API of [World Aquatics](https://www.worldaquatics.com/swimming/rankings?).
* I used nested `for loops` to get data for different strokes, in different disciplines and `append` to add them to a pandas dataframe object.
* I used `pandas` to clean the data and format it in a way that could serve my scope. In particular, i formatted the `time` value in a `timedelta` object to convert it into seconds and calculate the average. This passage was not as straigthforward as I hoped, as it required to assign all times to the same HH:MM:SS format.
* I used `pivot_table` and `matplotlib` to review my data, spot trends and errors.


### Missed Opportunities
Although I expected World Aquatics to provide a substantial and consistent I discovered that the data is much more inconsistent and noisy than I initially expected. Given more time, I would have explored alternative sources of data.

I think having more time at my disposal I would have changed the first graph in order to show not only the World Records, but also other types of records (such as National, Continental and Manifestation records). Because that value was expressed in code (ex. `[0 16]` for manifestation's record) I decided to leave it there for the moment.

Marco Dalla Stella

[md3934@columbia.edu](mailto:md3934@columbia.edu)
