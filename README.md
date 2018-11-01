# data-512-a2 Bias in Data
Use ORES API to examine English wikipedia article quality on politicians around the world for DATA512 Assignment2

Name: Yumeng Ding	

Date: November 1st, 2018

## Objective

The goal of this assignment is to use ORES API to evaluate english wikipedia articles on politicans and analyze their quality of articles, quantity of articles and in comparison with corresponding population data on countries around the world. Through the examination, we started seeing differences in terms of percentage of articles per population and percentage of high quality articles based on total number of articles. This helps us understand the potential bias behind Wikipedia article compostions by country, in particular articles about politicians, and understand the implications and consequences of usage of these data based the differences in coverage and quality.

## Input Data

We used three data sources for our analysis:

* **Wikipedia dataset** from Figshare.com: https://figshare.com/articles/Untitled_Item/5513449

This dataset is downloaded from Figshare.com. <br/>
The dataset is titled "Politicians by Country from the English-language Wikipedia", of which are data extracted from Wikimedia thru API calls. <br/>
Both the dataset and the code used to extract the data are under CC-BY-SA 4.0 license. <br/>
It is downloadable as a csv file titled "page_data.csv", and there are three columns and 47,197 rows in the csv file. <br/>

    page: article title of the page for political figures, not cleaned yet
    country: cleaned version of country name from which the category the political figure is under
    rev_id: unique identifier for revision tracking


* **Population dataset** from Dropbox: https://www.dropbox.com/s/5u7sy1xt7g0oi2c/WPDS_2018_data.csv?dl=0

This dataset is downloaded from Dropbox. <br/>
The dataset is originally from Population Reference Bureau under International Indicators <br/>
and it is population data for all countries from mid-2018 in millions of population. <br/>
It is downloadable as a csv file titled "WPDS_2018_data.csv", and there are two columns and 207 rows in the csv file. <br/>

    Geography: country and continent names 
    Population mid-2018 (millions): population data from mid-2018 in millions


* **ORES article quality prediction data**

For the article quality predictions, we will be using ORES API calls by passing in each articles' rev_id and getting their 'prediction' values from the json file.

For ORES documentation, please refer to this website: https://ores.wikimedia.org/v3/#!/scoring/get_v3_scores_context

For prediction values in ORES, there are 6 quality categories, in later analysis, we will mainly focus on the first two categories for high quality article percentage calculation.

    FA - Featured article
    GA - Good article
    B - B-class article
    C - C-class article
    Start - Start-class article
    Stub - Stub-class article


## Output Data

* **final_data.csv**

All three data sources are individually cleaned and merged together using the common columns in page_data(rev_id, country), population_data(Geography), article_quality(revision_id), the final dataset have 5 columns and 44,973 rows after removing all data point that don't have a match.

    country: country column from page_data
    article_name: page column from page_data
    revision_id: revision_id column from article_quality
    article_quality: article_quality column from article_quality
    population: Population mid-2018 (millions) column from population_data which will be in millions


## Resources used

Python 3.7 was used to produce the Jupyter Notebook in this repo, please see documentations for [Python 3.7](https://docs.python.org/3.7/) and [Jupyter Notebook](http://jupyter-notebook.readthedocs.io/en/latest/) at their respective links. 

The following Python packages were used and their documentation can be found at the accompanying links:

* [Pandas](https://pandas.pydata.org/pandas-docs/stable/): used for data processing
* [requests](http://docs.python-requests.org/en/master/): used for API calls
* [json](https://docs.python.org/3/library/json.html): used for json format decoding


## Results

We evaluated the Wikipedia articles on politician from two perspective:

* The **percentage of articles-per-population** for each country: this measure will be calculated by taking the total number of articles in a particular country and divide it by the total population of the corresponding country. This requires us to sum the total number of articles by country and to represent population number normally.

* The **percentage of high-quality-articles** for each country: this measure will be calculated by taking the total number of articles in a particular country that qualifies as being either "FA" or "GA" and divide it by the total number of articles about politicians of the corresponding country.

We then ranked the highest and lowest 10 countries in terms of these 2 measures:

  1. 10 highest-ranked countries in terms of **pcnt_articles_per_population**

| country                        | article_count | population | pcnt_articles_per_population |
|--------------------------------|---------------|------------|------------------------------|
| Tuvalu                         | 55            | 10000.0    | 0.550000                     |
| Nauru                          | 53            | 10000.0    | 0.530000                     |
| San Marino                     | 82            | 30000.0    | 0.273333                     |
| Monaco                         | 40            | 40000.0    | 0.100000                     |
| Liechtenstein                  | 29            | 40000.0    | 0.072500                     |
| Tonga                          | 63            | 100000.0   | 0.063000                     |
| Marshall Islands               | 37            | 60000.0    | 0.061667                     |
| Iceland                        | 206           | 400000.0   | 0.051500                     |
| Andorra                        | 34            | 80000.0    | 0.042500                     |
| Federated States of Micronesia | 38            | 100000.0   | 0.038000                     |


  2. 10 lowest-ranked countries in terms of **pcnt_articles_per_population**

| country      | article_count | population   | pcnt_articles_per_population |
|--------------|---------------|--------------|------------------------------|
| India        | 986           | 1.371300e+09 | 0.000072                     |
| Indonesia    | 214           | 2.652000e+08 | 0.000081                     |
| China        | 1135          | 1.393800e+09 | 0.000081                     |
| Uzbekistan   | 29            | 3.290000e+07 | 0.000088                     |
| Ethiopia     | 105           | 1.075000e+08 | 0.000098                     |
| Zambia       | 25            | 1.770000e+07 | 0.000141                     |
| Korea, North | 39            | 2.560000e+07 | 0.000152                     |
| Thailand     | 112           | 6.620000e+07 | 0.000169                     |
| Bangladesh   | 323           | 1.664000e+08 | 0.000194                     |
| Mozambique   | 60            | 3.050000e+07 | 0.000197                     |


  3. 10 highest-ranked countries in terms of **pcnt_high_quality_articles**

| country                  | high_quality_article_count | article_count | pcnt_high_quality_articles |
|--------------------------|----------------------------|---------------|----------------------------|
| Korea, North             | 7                          | 39            | 17.948718                  |
| Saudi Arabia             | 16                         | 119           | 13.445378                  |
| Central African Republic | 8                          | 68            | 11.764706                  |
| Romania                  | 40                         | 348           | 11.494253                  |
| Mauritania               | 5                          | 52            | 9.615385                   |
| Bhutan                   | 3                          | 33            | 9.090909                   |
| Tuvalu                   | 5                          | 55            | 9.090909                   |
| Dominica                 | 1                          | 12            | 8.333333                   |
| United States            | 82                         | 1092          | 7.509158                   |
| Benin                    | 7                          | 94            | 7.446809                   |


  4. 10 lowest-ranked countries in terms of **pcnt_high_quality_articles**

| country      | high_quality_article_count | article_count | pcnt_high_quality_articles |
|--------------|----------------------------|---------------|----------------------------|
| Tanzania     | 1                          | 408           | 0.245098                   |
| Peru         | 1                          | 354           | 0.282486                   |
| Lithuania    | 1                          | 248           | 0.403226                   |
| Nigeria      | 3                          | 682           | 0.439883                   |
| Morocco      | 1                          | 208           | 0.480769                   |
| Fiji         | 1                          | 199           | 0.502513                   |
| Bolivia      | 1                          | 187           | 0.534759                   |
| Brazil       | 3                          | 551           | 0.544465                   |
| Luxembourg   | 1                          | 180           | 0.555556                   |
| Sierra Leone | 1                          | 166           | 0.602410                   |

One caveat on the lowest-ranked countries in terms of pcnt_high_quality_articles, we only included countries that have at least 1 article qualified as "GA" or "FA" and didn't include countries that don't have any high quality articles about politicians. Therefore, as a separate group of countries that don't have any high quality articles written about politicians, we've listed below in alphabetical order. There are 37 countries that dont have any articles qualified as "GA" or "FA".

	'Andorra', 'Angola', 'Antigua and Barbuda', 'Bahamas', 'Barbados', 'Belgium', 'Belize', 'Cameroon', 'Cape Verde', 'Comoros', 'Costa Rica', 'Djibouti', 'Federated States of Micronesia', 'Finland', 'Guyana', 'Kazakhstan', 'Kiribati', 'Lesotho', 'Liechtenstein', 'Macedonia', 'Malta', 'Marshall Islands', 'Moldova', 'Monaco', 'Mozambique', 'Nauru', 'Nepal', 'San Marino', 'Sao Tome and Principe', 'Seychelles', 'Slovakia', 'Solomon Islands', 'Switzerland', 'Tunisia', 'Turkmenistan', 'Uganda', 'Zambia'

## Reflection

First bias I was expecting come from the language aspect of the page dataset. The page dataset is collected on articles in English Wikipedia only, which means some countries that don't have their primary Wikipedia articles in English might have an article on a specific politician in their native language only. This bias might skew the percentage representation in terms of both population and high quality articles.

The second bias I was expecting come from usage of Wikipedia in general. Countries like United States or Iceland might have a lot more heavy users of Wikipedia than countries like China and North Korea. Less users would potentially result in less articles and worse quality. So unless we adjust for users of Wikipedia instead of just population, we will get skewed percentages.

I wasn't expecting country like Brazil to have so few high quality articles due to the high article counts in general. I would like to look up articles on politician of Brazil and get a better sense of why they are not rated as high quality articles.


## License

This assignment code and data is released under MIT License.
