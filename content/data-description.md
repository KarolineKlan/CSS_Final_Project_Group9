---
title: Data collection and description
prev: "/"
next: network-analysis
---


# __Data collection__

The data used in the project was collected from the [BilkaToGo website](https://www.bilkatogo.dk/) using the python webscraping libraries [Beautiful Soup](https://pypi.org/project/beautifulsoup4/) and [Selenium](https://selenium-python.readthedocs.io/). The scraping was done in 2 steps. Firstly the Product Id's, the Categories and the Price of the products was collected. Secondly the Product Id's was used to collect the product descripstions for each item. 
The below figure shows what specific attributes was collected in the scraping:

<figure>
    <img src="/images/Scraping.png" width="100%" alt="Scraping">
    <figcaption style="text-align:center;font-style: italic;">Figure. 1: Visual representation of the process of collecting the data using webscraping tools on BilkaToGo</figcaption>
</figure>


Each attribute was collected and saved to CSV files, whereafter data cleaning and preprocessing was utilized. The items scraped from the [BilkaToGo website](https://www.bilkatogo.dk/) included a total of 32.285 data points across 21 categories as seen in the distribution below.



<figure>
    <img src="/images/concated_chart_categories.png" width="90%" alt="Distribution of the products in the different categories">
    <figcaption style="text-align:center;font-style: italic;">Figure 2: Distribution of the products in the different categories</figcaption>
</figure>



For the scope of this project it was decided only to focus on the 10.269 colleced datapoints that belonged to the Foods category, and it was only for this category that the product descriptions were scraped.

# __Data cleaning__
When collecting the product descriptions it was discovered that some items did not have any descriptions. Additionally it was discovered that some descriptions involved generic descriptions of the brand or retailer of the product. This brand discription did not include any information of the product itself, and therefore it is not of interest for the textual analysis. Additionally some items had a very short description with very little meaningful information. It was decided that **all product descriptions got striped from long generic brand descriptions and any product description less than 30 words long were filtered out**. 

The [Salling Group API](https://developer.sallinggroup.com/api-reference), specifically the [frequently bought together endpoint](https://developer.sallinggroup.com/api-reference#frequently-bought-together) was used to create the network linking two items if they were frequently bought together. In this process **any connection of frequently bought together items where one of the nodes did not belong to the foods category was not included in the network.**

See the [**Explainer Notebook**](explainer-notebook.html) for more details in how the data was scraped and preprocessed in order to be used and analysed in the project.

# The final preprocessed and cleaned data

After the cleaning proces a dataset consisting of 9.755 food products where each product constitute a node in a network with 74.180 links. The data can be downloaded from [**INDSÆT LINK TIL DATASET**]()