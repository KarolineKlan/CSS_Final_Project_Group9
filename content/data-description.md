---
title: Data collection and description
prev: "/"
next: network-analysis
---


# __Data collection__

The data used in the project was collected from the [BilkaToGo website](https://www.bilkatogo.dk/) using the python webscraping libraries [Beautiful Soup](https://pypi.org/project/beautifulsoup4/) and [Selenium](https://selenium-python.readthedocs.io/) because of the site's heavy reliance on JavaScript. The scraping was done in 2 steps.

1. The Product Id's, the Categories and the Price of all products on the site was collected. 
2. The Product Id's was used to collect the product descripstions for each item of the food-products only. 

The below figure shows what specific attributes was collected in the scraping:

<figure>
    <img src="/images/Scraping.png" width="100%" alt="Scraping">
    <figcaption style="text-align:center;font-style: italic;font-size:smaller;">Figure. 1: Visual representation of the process of collecting the data using webscraping tools on BilkaToGo</figcaption>
</figure>


Each attribute was collected and saved to CSV files, whereafter data cleaning and preprocessing was utilized. The items scraped from the [BilkaToGo website](https://www.bilkatogo.dk/) included a total of 32.285 data points across 21 categories as seen in the distribution below.



<figure>
    <img src="/images/concated_chart_categories.png" width="90%" alt="Distribution of the products in the different categories">
    <figcaption style="text-align:center;font-style: italic;font-size:smaller;">Figure 2: Distribution of the products in the different categories</figcaption>
</figure>



For the scope of this project, it was decided to focus solely on the 10.269 collected data points that belonged to the Foods category. Product descriptions were scraped exclusively for this category.

# __Data cleaning__
When collecting the product descriptions, it was discovered that some items did not have any descriptions at all. Additionally, some descriptions contained generic information about the brand or retailer rather than the product itself, which was not useful for our textual analysis. Furthermore, some items had very short descriptions with minimal meaningful information. Therefore, **it was decided to strip all product descriptions of long, generic brand information and filter out any descriptions that were less than 30 words long.** 

The [Salling Group API](https://developer.sallinggroup.com/api-reference), specifically the [frequently bought together endpoint](https://developer.sallinggroup.com/api-reference#frequently-bought-together) was used to create the network linking two items if they were on the same 'frequently bough together' list. In this process **any connection of frequently bought together items where one of the nodes did not belong to the foods category was not included in the network.**

See the [**Explainer Notebook**](explainer-notebook.html) for more details in how the data was scraped and preprocessed in order to be used and analysed in the project.

# __The final preprocessed and cleaned data__

After the cleaning process, the dataset consists of 9,755 food products, with each product constituting a node in a network containing 74,180 links. The dataset can be downloaded from [**this link**](https://drive.google.com/drive/folders/1AuX2D92FGSTjIBpWor3D7acklpOoaa6C?usp=sharing). It is important to note that the items on BilkaToGo are continuously updated and changed, so some of the items collected in the dataset on **April 17, 2024** might no longer be available on the website today.