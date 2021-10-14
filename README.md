# A2: Bias in Data

## Overview
The goal of this project is to explore potential bias in Wikipedia articles. In particular, we are interested in Wikipedia articles on politial figures of each country. We will use Wikipedia article data, population data, and a machine learning service called ORES to examine the coverage and quality of articles across differentc countries and regions.

## Data
For this project we have three sources to retrieve our data.
* Wikipedia politicians articles by country dataset: https://figshare.com/articles/dataset/Untitled_Item/5513449. This dataset is posted on figshare and licensed under the CC-BY-SA 4.0: https://creativecommons.org/licenses/by-sa/4.0/. Terms of use: https://wikimediafoundation.org/wiki/Terms_of_Use/en. The data is included in this repository in the file page_data.csv. It contains the following attributes:
  * page: name of Wikipedia article
  * country: name of the country
  * rev_id: revision id of the article. This will be used to retrieve quality score from an API later.

* Population dataset: https://www.prb.org/international/indicator/population/table/ by Population Reference Bureau. No license information found. This dataset is in this repository in the file WPDS_2020_data.csv. It contains the following attributes:
  * FIPS: abbreviation of country/gergraphical region
  * Name: name of country/gergraphical region
  * Type: indicate the type of region: world, sub-region, or country
  * TimeFrame: 2019 for this dataset
  * Data (M): population of country in million
  * Population: population of country

* Wikipedia article score. This is data is available through the machine learning API ORES (Objective Revision Evaluation Service). Description: https://www.mediawiki.org/wiki/ORES. API: https://ores.wikimedia.org/v3/#!/scoring/get_v3_scores_context_revid_model. It rates each article into one of the six qualities: FA, GA, B, C, Start, Stub. Here we consider FA (featured article) and GA (good article) as high quality articles.
  * Note that this API takes in revision ids of articles as input for evaluation, and some revision ids from the articles dataset do not have a rating. These articles are excluded from analysis and their revision ids are listed in the file articles_with_no_ores_scores.

## Data processing and analysis
The code for data cleaning, processing, and analysis, including getting ORES scores from API, is included in hcds-a2-bias.ipynb. For data cleaning and preprocessing, there are a few articles from the article dataset that do not match any country in the population dataset. There are also a few countries in the population dataset that do not match any article. In either case, the data is excluded from analysis and these rows are shown in wp_wpds_countries-no_match.csv.
The other data with good matches are output in the wp_wpds_politicians_by_country.csv. Both of these csv files have the following schemas:
* country: name of the country
* article_name: name of Wikipedia article
* revision_id: revision id of the article
* article_quality_est.: the ORES rating of article quality
* population: population of the country

## How to run the notebook
Run the following commands in terminal.
1. Clone this repository: git clone https://github.com/zhangjunhao0/data-512-a2.git
2. (Optional): create a virtual environment and activate it. See https://docs.python.org/3/tutorial/venv.html. Feel free to skip this step.
3. Install packages (if you do not have them installed): pip3 install pandas tqdm requests
4. Open hcds-a2-bias.ipynb and run all cells.
