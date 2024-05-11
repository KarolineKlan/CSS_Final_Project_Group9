---
title: Network analysis
prev: data-description
next: text-analysis
---

In the network analysis we will delve into details giving us insights into consumer behavior in terms of how food item are purchased together. As an overview we are going to investigate the following:
1. The network properties to understand the overall structure that the foods-network follow by looking at the degree distribution. 
2. Investigate Assortativity to see if there is a tendency that some nodes in the network connect to other nodes that are similar in degree and other attributes.
3. The network is partitioned into communities to can gain insights into how consumers group certain types of food together when shopping. 
4. The most central nodes in the network is investigated in order to find the product that acts as hubs between communities.


Each node represents a food item in one of 8 different categories:

<figure>
    <img src="/images/Categories_overview.png" width="80%" alt="Scraping">
    <figcaption style="text-align:center;font-style: italic;"></figcaption>
</figure>

Each link between the nodes represent if a product is in the top 10 list of frequently bought items with another product. When calling the [frequently bought together endpoint](https://developer.sallinggroup.com/api-reference#frequently-bought-together) from the [Salling Group API](https://developer.sallinggroup.com/api-reference) a list of the 10 items most often bought together with each product is returned, ordered by descending relevance. After filtering the data and creating the network as an undirected graph we see the following: 
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
Assortativity can help give insights in what items tend to get bought together, as it explains a preference for a network's nodes to attach to others that are similar. In this section we will look into degree assortativity and assortativity that is related to specific attributes, in our case we will be looking at the attributes 'Category', 'Ecology' and 'Price'.

In order to compare if the assortativity of the food-network is significant from random we compare it to 100 different random networks, where the assortativity has been broken by a configuration model that uses the _double edge swap_ algorithm to ensure each node retains its original degree but with altered connections.

The results from the analysis is shown in the table below, and the details can be seen in the explainer notebook:

| **Assortativity Coefficient**                     | **Food Network** | **Average Random Network** |
|---------------------------------------------------|:--------------:|:------------------------:|
| Degree Assortativity Coefficient                  | 0.054        | -0.034                 |
| Category Assortativity Coefficient                | 0.494        | -0.001                 |
| Ecology Assortativity Coefficient                 | 0.595        | -0.002                 |
| Price Assortativity Coefficient                   | 0.355        | -0.001                 |
<div style="text-align:center;font-style: italic;font-size:smaller;">Table 1. Assortativity coefficients of the food network compared to the average of the 100 random networks </div>

Our findings show that the average assortativity coefficients of the random network is very low, close to zero which is also what we would expect.

If the degree assortativity coefficient is high it means that nodes tend to be connected with other nodes with similar degree values. In our results we found this value to be very small. Although it is modest it is still dsignificant from random indicating that there might be a slight preference for items with similar degrees of connectivity to be purchased together. For example popular items might commonly appear in the same baskets. These results however is not as convincing as for the Category and Ecology Assortativity.

When considering the attribute assortativity on the category and the ecology attribute it is apparent that these values are very significant different than the random. This suggest that products within the same categories tend to get purchased together. One possible reason for this is the physical proximity of products within the same category in the store, which makes it more convenient for shoppers to buy them together. Additionally, eco products tend to be purchased with other eco products, which aligns with our expectations based on certain consumer behaviors. Shoppers who prioritize ecological products are likely to seek out and purchase multiple eco-friendly items together. The same applies to the Price assortativity where the value is pretty high, indicating that expensive products tend to get purchased with other expensive and vice versa. However considering that all prices in the dataset is kilo-prices these findings might be a bit misleading as the price does not reflect the acutal price paid in the store when shopping.

We selected a random example of an eco-product to inspect its neighbors. The Ecological minced chicken with the product ID 71136 and its neighbors is seen below:

<figure>
    <img src="/images/Ecology_assort.png" width="70%" alt="Scraping">
    <figcaption style="text-align:center;font-style: italic;font-size:smaller;">An example of an ecological product and its 10 neighbors. </figcaption>
</figure>
Above image illustrates how an ecological product is connected to other eco-products, as all its neighbors in this example are also ecological. Additionally, this demonstrates that many neighbors of this product within the meat category are also in the same category. 
This example supports the conclusions drawn from the assortativity analysis, indicating a general trend in the entire network where items within the same category and eco-products tend to be purchased together.

# __3. Communities__

By identifying communities, we are able to gain insights into how the certain types of foods are grouped together by the consumers. This helps in understanding purchasing patterns and preferences that consumers make when going grocery shopping. When partitioning the network into communities we use the Louvain Community Detection Algorithm because we want to investigate the underlying and naturally existing structures, and this algorithm finds the non-overlapping communities.

 Because the food-network with its 9.755 nodes is very cluttered to visualize, below the top 5 biggest communities including a total of 5551 nodes is shown:

<figure>
    <img src="/images/Graph_communities.png" width="60%" alt="Scraping">
    <figcaption style="text-align:center;font-style: italic;font-size:smaller;">Figure. 4: The top 5 communities in the network, colored by the ID and labeled in the text-analysis. </figcaption>
</figure>

| **Community ID** | **Community label (made in textanalysis)**      | **Number of Nodes** |
|:--------------:|:---------------------------------------------:|:-----------------:|
| 16           | <span style="color:blue;">Everyday</span>       | 1742            |
| 24           | <span style="color:darkorange;">Organic</span> | 1367        |
| 18           | <span style="color:forestgreen;">Beverages</span> | 948       |
| 19           | <span style="color:magenta;">Indulgence</span> | 899             |
| 3            | <span style="color:cyan;">Entertaining</span>       | 595             |

<div style="text-align:center;font-style: italic;font-size:smaller;">Table 2. Overview of the size of the top 5 largest communities in the dataset with labels that are made in the NLP-text analysis section</div>

The communities are labeled and investigated further in the text-analysis section.


# __4. Centrality__

The centrality measure give us insight in which nodes play a more dominant role in the network. We use two different centrality measures; closeness and betweenness centrality. Closeness centrality rank each node in the network by how "far" it has to travel to reach other nodes in the network, meaning nodes that do not need to travel far is more central in the network. The score itself is not that relevant for us, as we would like to focus on which nodes that acts as the central hubs in our network. 

The betweenness centrality tell us how many times each node act as a part of the shortest path between two nodes in the network. The nodes with high betweenness score fall in the shortest path between alot of nodes in the network and is therefore considered central. 
We would like to match the 14 highest scoring nodes from each of the two metrics to see if it is the same nodes that score highest. 

| **Rank** | **Closeness Centrality**       | **Betweenness Centrality**               |
|----------|--------------------------------|------------------------------------------|
| 1    | agurk                               | agurk                                    |
| 2    | agurk øko                           | smørbar                                  |
| 3    | finvalsede havregryn øko            | mørk pålægschokolade 53% kakao øko       |
| 4    | æg m/l øko                          | agurk øko                                |
| 5    | smørbar                             | æg m/l øko                               |
| 6    | hvedemel øko                        | finvalsede havregryn øko                 |
| 7    | hakkede tomater øko                 | skrabeæg m/l                             |
| 8    | bananer 4 pak øko                   | remoulade øko                            |
| 9    | skrabeæg m/l                        | hvedemel øko                             |
| 10   | rosiner øko                         | bananer                                  |
| 11   | peberfrugter røde                   | hakkede tomater øko                      |
| 12   | bananer                             | bananer 4 pak øko                        |
| 13   | remoulade øko                       | peberfrugter røde                        |
| 14   | mørk pålægschokolade 53% kakao øko  | tonic                                    |
<div style="text-align:center;font-style: italic;font-size:smaller;">Table 3. Top 14 food-items based on closeness centrality and betweenness centrality</div>

As seen in the table, many nodes re-appear, with the only difference being 'rosiner øko' (raisins eco) and 'tonic'.

Since these nodes act as central hubs, we want to investigate how many, and which communities each node connects with, as it will give insights as to how these products are used in different ways. In our text analysis we create community labels,  which is used to clarify the essence of each community. We use the resulting table here to illustrate how the different betweenness hubs bridge accros communities:
<figure>
    <img src="/images/betweenness.png" width="80%" alt="Scraping">
    <figcaption style="text-align:center;font-style: italic;font-size:smaller;">  Table. 4: A dataframe showing the top betweeness centrality products in the network and the communities they link.  </figcaption>
</figure>

The dataframe is sorted such that the products on the left, are ordered from highest betweenness centrality to lowest of the top 14 highest betweenness centrality in the entire frequently-bought-together network.
A higher betweenness centrality means that this product is likely to be a bridge between different grocery shopping categories. This mean that these products are likely for a consumer to get bought together with a varity of goods. A reason why the cucumber ranks highest could be its versatility. It is used in a variety of dishes, can be a snack, and is often one of the first items customers see when entering a supermarket. Additionally, its affordability makes it more likely to be added to a basket with a wide range of other products.

Based on the dataframe, we can see that several products have high betweenness centrality, meaning they are often bought together with products from other communities. These products include:

- Cucumbers (agurk)
- Butter (smørbar)
- Organic cucumbers (agurk øko)
- Organic eggs (æg m/l øko)
- Grated oatmeal (finvalsede havregryn øko)
- Remoulade (remoulade øko)
- Wheat flour (hvedemel øko)

These products could be considered "bridge" products that connect different shopping categories. For example, organic cucumbers (agurk øko) appear in the "Healthy", "Organic", "Everyday", and "Beverages" communities. This suggests that organic cucumbers are often bought together with a variety of other products, such as healthy snacks, other organic items, everyday stables, and beverages.

Next, we will explore the text analysis in greater detail to explain how the communities are labeled.