# data-512-a2 Bias in Data
Use ORES API to examine English wikipedia article quality on politicians around the world for DATA512 Assignment2

Name: Yumeng Ding	

Date: November 1st, 2018

## Goal

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



## Resources used
This analysis was prepared using Python 3.5 running in a Jupyter Notebook environment.  
Documentation for Python can be found here: https://docs.python.org/3.5/  
Documentation for Jupyter Notebook can be found here: http://jupyter-notebook.readthedocs.io/en/latest/  

The following Python packages were used and their documentation can be found at the accompanying links:

## Files Created
This notebook creates N CSV files of data extracted and compiled as part of this analysis.

The first file...

The Nth file...

## Visualizations Created

## License

This assignment code is released under...

The data sources are licensed under...