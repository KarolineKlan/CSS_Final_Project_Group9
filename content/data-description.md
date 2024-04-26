---
title: Data collection and description
prev: "/"
next: network-analysis
---


# __Data collection__

The data used in the project was collected from the [BilkaToGo website](https://www.bilkatogo.dk/) using the python webscraping libraries [Beautiful Soup](https://pypi.org/project/beautifulsoup4/) and [Selenium](https://selenium-python.readthedocs.io/). The below figure shows what specific attributes was collected in the scraping:

![](/images/Scraping.png)
*Figure. 1 - Visual representation of the process of collecting the data using webscraping tools on [BilkaToGo](https://www.bilkatogo.dk/).*

Each attribute was collected and saved to CSV files, whereafter data cleaning and preprocessing was utilized. The items scraped from the [BilkaToGo website](https://www.bilkatogo.dk/) included a total of 32.285 data points across 21 categories




 Finally the [Salling Group API](https://developer.sallinggroup.com/api-reference), specifically the [frequently bought together endpoint](https://developer.sallinggroup.com/api-reference#frequently-bought-together) is used to create the network linking two items 

See the [**Explainer Notebook**](explainer-notebook.html) for more details in how the data was scraped and preprocessed in order to be used and analysed in the project.

# __Description of the final cleaned data__

In the collection