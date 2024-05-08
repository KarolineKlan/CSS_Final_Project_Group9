---
title: Network analysis
prev: data-description
next: text-analysis
---

In the network analysis we will delve into details giving us insights into consumer behavior in terms of how food item are purchased together. As an overview we are going to investigate the following:
1. The network properties to understand the overall structure that the foods-network follow by looking at the degree distribution. 
2. Investigate Assortativity to see if there is a tendency that some nodes in the network connect to other nodes that are similar in degree or based on other attributes like whether they are ecological.
3. 
4. 


Each node represents a food item in one of 8 different categories:

<figure>
    <img src="/images/Categories_overview.png" width="80%" alt="Scraping">
    <figcaption style="text-align:center;font-style: italic;"></figcaption>
</figure>

Each link between the nodes represent if a product is in the top 10 list of frequently bought items with another product. When using the [frequently bought together endpoint](https://developer.sallinggroup.com/api-reference#frequently-bought-together) from the [Salling Group API](https://developer.sallinggroup.com/api-reference) every time an item is called a list of the 10 items that most often is bought together with the product is returned and is  ordered by descending relevance. After filtering the data and creating the network as an undirected graph as explained in the data description section we see the following: 
>  <center>The network is fully connected and has 9.755 nodes and 74.180 links<center>



# __1. Degree distribution__


The degree of a node describes how many edges are connected to a node. We take a look at the degree distribution of the network in order to investigate if it has properties of a real-world social network. To do this we use a randomized network that has the same amount of nodes and links as the food-network but where the nodes are randomly linked with the same propability *p* as in the food-network. Go to the explainer notebook to get more insights into the theory behind the creation of this random-network as a baseline. The degree distribution of a network, P(k), tells us the probability that a randomly chosen node will have degree k.



<figure>
    <img src="/images/Degree_Distribution_Plot.png" width="90%" alt="Scraping">
    <figcaption style="text-align:center;font-style: italic;font-size:smaller;">Figure. 3: The degree distribution of the Food-network compared to the random network with logarithmic binding. </figcaption>
</figure>

From the degree distribution it appears that the Foods Network (in green) resembles a power law distribution after degree 10 as the distribution approximately resembles a straight line in log-log scale. This is a property of real-world social networks that suggest that there are a few highly connected nodes (hubs) in the food-items network. The reason this happens after degree 10 is because every node is forced to have at least 10 neighbors as this is what is returned from the API call. In the data cleaning all neighboring items that does not belong in the foods-category is removed, which results in some nodes getting a degree less than 10.
 The average degree of the foods network is affected by these major hubs, which is why the median is a better sample estimate for the population of a heavy-tailed network like this. Comparing the foods network to the random network (in red) we see that the random network model is more symmetrically distributed and predicts a larger number of nodes around the average degree ‹k› than seen in the Foods-network.

 The high-degree nodes in the Foods Network likely represent items that are versatile or have broad appeal, causing them to appear frequently on the "frequently bought together" list across various other items. For example, common ingredients like milk, bread, or eggs might be expected to have higher degrees. We delve further into the specific items in the next sections.

# __2. Assortativity__
Assortativity can help give insights in what items tend to get bought together, as it gives insights into the tendency of how nodes connect to other nodes that are similar or dissimilar in some defined way. In this section we will look into degree assortativity and assortativity that is related to specific attributes, in our case we will be looking at the attributes 'Category', 'Ecology' and 'Price'.

In order to compare if the assortativity of the food-network is significant from random we compare it to 100 different random networks, where the assortativity has been broken by a configuration model that uses the _double edge swap_ algorithm to ensure each node retains its original degree but with altered connections.

The results from the analysis is shown in the table below, and the details can be seen in the explainer notebook:

| **Assortativity Coefficient**                     | **Food Network** | **Average Random Network** |
|---------------------------------------------------|:--------------:|:------------------------:|
| Degree Assortativity Coefficient                  | 0.054        | -0.034                 |
| Category Assortativity Coefficient                | 0.494        | -0.001                 |
| Ecology Assortativity Coefficient                 | 0.595        | -0.002                 |
| Price Assortativity Coefficient                   | 0.087        | -0.000                 |
<div style="text-align:center;font-style: italic;font-size:smaller;">Table 1. Assortativity coefficients of the food network compared to the average of the 100 random networks </div>

Our findings show that the assortativity coefficients of the random network is very low, close to zero which we would expect.

When considering the attribute assortativity on the category and the ecology attribute it is apparent that these values are very significant different than the random. This suggest that products within the same categories tend to get purchased together. Additionally eco products tend to get purchased with other eco products as well, which is also what we could expect considering what we anticipate from certain consumer behaviours.

We selected a random example of an eco-product with the product ID 

<figure>
    <img src="/images/Ecology_assort.png" width="70%" alt="Scraping">
    <figcaption style="text-align:center;font-style: italic;font-size:smaller;">Figure. 4:  . </figcaption>
</figure>


# __3. Communities__



<figure>
    <img src="/images/Graph_communities.png" width="60%" alt="Scraping">
    <figcaption style="text-align:center;font-style: italic;font-size:smaller;">Figure. 5: . </figcaption>
</figure>

| **Community ID** | **Community label (made in textanalysis)**      | **Number of Nodes** |
|:--------------:|:---------------------------------------------:|:-----------------:|
| 16           | <span style="color:blue;">Everyday</span>       | 1742            |
| 24           | <span style="color:darkorange;">Organic</span> | 1367        |
| 18           | <span style="color:forestgreen;">Beverages</span> | 948       |
| 19           | <span style="color:magenta;">Indulgence</span> | 899             |
| 3            | <span style="color:cyan;">Entertaining</span>       | 595             |

<div style="text-align:center;font-style: italic;font-size:smaller;">Table 2. Overview of the size of the top 5 largest communities in the dataset with labels that are made in the NLP-text analysis section</div>




# __4. Centrality__

