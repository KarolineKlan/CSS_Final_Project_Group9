---
title: Network analysis
prev: data-description
next: text-analysis
---

The goal of this project is to investigate the real life network of food-items that are frequently bought together. Each node represents a food item in one of 8 different categories:

| **Danish Category**      | **English Translation**        |
|----------------------|----------------------------|
| kolonial             | Grocery                    |
| drikkevarer          | Beverages                  |
| mejeri-og-koel       | Dairy and Chilled          |
| slik-og-snacks       | Candy and Snacks           |
| broed-og-kager       | Bread and Cakes            |
| frost                | Frozen                     |
| frugt-og-groent      | Fruits and Vegetables      |
| koed-og-fisk         | Meat and Fish              |

Each link between the nodes represent if a product is in the top 10 list of frequently bought items with another product. When using the [frequently bought together endpoint](https://developer.sallinggroup.com/api-reference#frequently-bought-together) from the [Salling Group API](https://developer.sallinggroup.com/api-reference) every time an item is called a list of the 10 items that most often is bought together with the product ordered by descending relevance is returned. 




<figure>
    <img src="/images/Degree_Distribution_Plot.png" width="100%" alt="Scraping">
    <figcaption style="text-align:center;font-style: italic;">Figure. 3: </figcaption>
</figure>


127323
[129632, 129633, 19434, 71512, 92948, 87131, 19721, 18364, 91334, 41414]

71493
[38700, 38930, 16528, 117645, 20676, 105446, 115347, 91957, 115350, 104436]

19364
[19366, 19365, 115352, 59086, 89202, 69882, 77934, 110126, 106052, 110009]

19363
[73411, 19366, 93935, 75294, 104969, 69364, 91700, 19365, 39445, 81118]