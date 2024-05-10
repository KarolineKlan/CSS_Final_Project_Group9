---
title: Text analysis
prev: network-analysis
---

To gain insights into consumer buying patterns, we analyze the words that characterize certain natural communities within the frequently-bought-together network. The descriptions are a small text about each product typically explaining what the product tastes like, and what occasions/setting they are typically enjoyed in. This analysis helps us understand what underlying words characterize items that are frequently purchased together.

In order to do this, the text-analysis is made in 3 steps:

1. The product descriptions are tokenized and the distribution of the descriptions and the frequency of words are analysed. More details about this step can be found in the Explainer Notebook.
2. The TF-IDF scores are calculated and the most characterizing words for each community is visualized using wordclouds.
3. OpenAI's API is called using ChatGPT 3.5 to label the communites based on the top 100 TF-IDF words.

  
# __2. TF-IDF scores and Wordclouds__

These TF-IDF scores help us identify which words are specifically unique to each community. The result from the text-analysis and the top TF-IDF scores of words for the top 9 communities can be seen below:

| **Community 16 TF-IDF Words** | **Community 24 TF-IDF Words** | **Community 18 TF-IDF Words** |
|----------------------------|----------------------------|----------------------------|
| lækker  0.0126             | økologisk 0.0119           | gin 0.0129                |
| salling 0.0122            | salling 0.0113             | vinen 0.0115              |
| smag 0.0119               | smag 0.0112                | noter 0.0105              |
| prøv 0.0110               | økologiske 0.0112          | smag 0.0104               |
| nyd 0.0106                | kaffe 0.0110               | ved 0.0103                |
| frisk 0.0103              | brug 0.0110                | frisk 0.0098              |
| brug 0.0099               | prøv 0.0109                | vin 0.0096                |
| ved 0.0097                | øko 0.0108                 | nyd 0.0093                |
| lidt 0.0097               | retter 0.0106              | smagen 0.0092             |

| **Community 19 TF-IDF Words** | **Community 3 TF-IDF Words** | **Community 22 TF-IDF Words** |
|----------------------------|--------------------------|---------------------------|
| chokolade 0.0154           | oliven 0.0162            | smag 0.0140               |
| lakrids 0.0148             | lækker 0.0140            | desserter 0.0126          |
| mix 0.0141                 | salling 0.0123           | lækker 0.0126             |
| smag 0.0140                | ost 0.0118               | chokolade 0.0124          |
| mælkechokolade 0.0131      | nyd 0.0115               | kager 0.0123               |
| lækker 0.0126              | prøv 0.0112              | brug 0.0115               |
| søde 0.0125                 | smag 0.0110               | lave 0.0112               |
| nyd 0.0122                 | cremet 0.0106             | dine 0.0111               |
| lækre 0.0120               | sammen 0.0106             | is 0.0106                 |

| **Community 9 TF-IDF Words** | **Community 8 TF-IDF Words** | **Community 17 TF-IDF Words** |
|--------------------------|--------------------------|---------------------------|
| kaffe 0.0134             | lækker 0.0129            | retten 0.0152             |
| kondi 0.0126             | snack 0.0125             | lækker 0.0140             |
| faxe 0.0126              | smag 0.0124              | salaten 0.0133             |
| energidrik 0.0119        | nyd 0.0119               | smag 0.0132                |
| giver 0.0119             | vegansk 0.0113           | salling 0.0127             |
| lækker 0.0118            | skøn 0.0112              | velsmagende 0.0120         |
| frisk 0.0117             | velsmagende 0.0110       | nyd 0.0120                 |
| forfriskende 0.0117      | minutter 0.0110          | giver 0.0120               |
| mælk 0.0109              | økologisk 0.0109         | frisk 0.0117               |

<div style="text-align:center;font-style: italic;font-size:smaller;">Table 4. Overview of the top 9 words based in TF-IDF scores for all the top 9 communities.</div>

And the top 3 most frequently bought togehter products for each of those communities are seen in the tables below:
<figure>
    <img src="/images/TopProducts.png" width="80%" alt="Scraping">
    <figcaption style="text-align:center;font-style: italic;font-size:smaller;">Figure. 7: Top 3 products for each of the Top 9 communities. All images are taken from the BilkaToGo website using the product ID's.  </figcaption>
</figure>


We see some distinct patterns that that differentiate each community. For instance, community 24 is clearly associated with ecological products, while community 19 appears to be centered around candy, with prominent words like 'mix,' 'liquorice,' and 'milk-chocolate.' To gain a better understanding of the defining characteristics of each community, we will examine the top TF-IDF words in word clouds for the top 9 communities.

<figure>
    <img src="/images/wordcloud_9.png" width="80%" alt="Scraping">
    <figcaption style="text-align:center;font-style: italic;font-size:smaller;">Figure. 8: Worldcloud showing the top TF-IDF word for the top 9 communities with the top 3 most frequently bought together products above them.  </figcaption>
</figure>

Here, we can distinguish between the top 9 communities based on the words specific to each community. This enables us to pinpoint distinct buying patterns for customers visiting a Salling store. To further help with the distinguishing of each community we made an API call for chatGPT 3.5 to classify each community based on the top 100 TF-IDF words for that specific community (see specifics in the next section). The classifications for each community are:


1. Community 16: 'Everyday'
> This community's top TF-IDF words include: 'Salling', 'Delicious', 'taste', 'enjoy', 'together'. This makes sense that this is the largest community within the frequently-bought-together network, as one could imagine that consumers often buy groceries in bulk for weekly meal plans. According to [this study](https://ijbnpa.biomedcentral.com/articles/10.1186/s12966-017-0461-7) [[5](#chapter5)] at least 57% of families plan their meals weekly (across the US). This wordcloud indicates that the majority of consumers purchase a diverse range of foods for everyday shopping, which is why this community is the largest. The products with the highest degrees within this community are two different brands of (agurk) cucumbers, and normal eggs (skrabeæg), which makes sense as these products are used in a lot of different dishes.

2. Community 24: 'Organic'
> This community's top TF-IDF words include: 'Salling', 'Ecological', 'Taste', 'Coffee'. This community represents a lot of what community 16 does of everyday bought items, but include ecological items. It aligns with the idea that consumers buying for meal plans as explained in community 16 but here organic options are chosen consistently. People who purchase some organic items tend to buy all organic items together, as supported ealier by our assortativity analysis. The products with the highest degrees in this community are eco oatmeal, eco eggs, and eco tomatoes.

3. Community 18: 'Beverages'
> This community's top TF-IDF words include: 'Gin', 'Wine', 'notes', 'taste'. This community describes consumers buying beverages, possibly for social gatherings, as indicated by the word 'Together', suggesting that these drinks are meant to be enjoyed with company.  This community is also large because when buying drinks consumers tend to buy things together because drinks are a combination of different products mixed together. Hence, why the word 'Gin' is the largest in the wordcloud, as Gin & Tonic is a very common drink especially in Denmark. This is further shown by the top 3 products with higest degree in this community which is two types of tonic water and London dry gin.

4. Community 19: 'Indulgence'
> This community's top TF-IDF words include: 'liquorice', 'Mix', 'Milkchocolate', 'Chocolate'. As the fourth largest community in the network, it makes sense because stores often place candy and other indulgent treats together. The tendency with the urge of eating and purchasing various sugary snacks for movie nights or parties contributes to the size of this community. The top products in this community are 'liquorice hard candy', 'tappsy', and 'chocofants'.

5. Community 3: 'Gourmet' / 'Tapas'
> This community was classified by ChatGPT as 'Gourmet' but we thought that 'Tapas' was a more fitting category. This community's top TF-IDF words include: 'Olives', 'Cheese', 'Taste' and 'delicious'. Although this community is smaller and more niche, it represents items commonly bought together for tapas. The top frequently bought together items in this community are 'Bell pepper', 'Italian bresaola', and 'Italian serrano ham'.

6. Community 22: 'Baking' 
> This community's top TF-IDF words include: 'Desert', 'Cake', 'Oetker' and 'Delicious'. This community would be associated with a buying patterns of a consumer that wants to bake.'Oetker' is a well-known brand for baking products, reinforcing this association. Baking often requires specific ingredients for recipes, which are typically bought together.  This conclusion is further enforced when looking at the top products in this community which is 'powdered sugar', 'gelatin' and 'sugar'.

7. Community 9: 'Energy'
> This community's top TF-IDF words include: 'Energydrink', 'Faxe kondi', Rerfreshing'. It is characterized by the need for refreshments or energy-boosting drinks like energy drinks or sodas. A reason why this community is rather large might include the hypothesis that consumers typically buys refreshments to multiple people, such as guests, who have different preferences. However, a reason that it is not as large of a community might be because sometimes people visit the supermarket to buy just a single refreshment and not many other products. The top products in this community include: 'Gum with fruit flavor', 'Coca Cola', and 'Sportsdrink'

8. Community 8: 'Vegan' 
> This community's top TF-IDF words include: 'Vegan', 'Delicious', 'Ecology' and 'Enjoy'. This community is distinguished by the vegan aspect. People who are vegan tend to buy other vegan and organic groceries together. A reason for the relative smaller size of this community might be due to the limited selection of vegan foods available in grocery stores and the tendency of vegan consumers to buy exclusively vegan products. The top products in this community are: 'vegan butter', 'vegan toppings' and 'creme fraiche dressing'.

9. Community 17: 'Healthy'
> This community's top TF-IDF words include: 'Salad', 'The dish', 'Enjoy'. This community is classified as a healthy community reflecting consumers who buy nutritious products like salads and healthy juices.The word 'innocent'—a brand known for healthy juices—also appears frequently. The top purchased products in this community are 'orange juice', and 'blackcurrants' and 'orange marmalade'. This suggests a pattern of buying items that contribute to a health-conscious diet.

# __Labeling of communities using OpenAI's API__

We set up a loop classifying each community based on the top 100 TF-IDF words with OpenAI's ChatGPT using their API to call the gpt-3.5-turbo model. We chose to use GPT-3.5 for this task because it is a highly capable model for such low-level tasks and is cost-effective. We ran a simple prompt with instructions to use a single word to classify each community, and we use the top 100 words because of token limits and at some point the TF-IDF score for these word become too low. We realize that chatGPT does not have a way of setting a seed, so the output could vary when running this code again. To mitigate this we put the 'temperature' variable that controls creativity in the llm to 0. However, this still didn't give consistent results. To avoid spending excessive time on this part of the project, we used the most consistent community mappings from multiple outputs. The mapped categories for each community can be seen in the below table:

| **Community Number** | **Community Label** |
|:------------------:|:----------------:|
| 0                | Convenience    |
| 1                | Beer           |
| 2                | Coffee         |
| 3                | Gourmet        |
| 4                | Healthy        |
| 5                | Everyday       |
| 6                | Snacks         |
| 7                | Indulgence     |
| 8                | Vegan          |
| 9                | Energy         |
| 10               | Snacks         |
| 11               | Organic        |
| 12               | Asian          |
| 13               | Meat           |
| 14               | Italian        |
| 15               | Tea            |
| 16               | Everyday       |
| 17               | Organic        |
| 18               | Beverages      |
| 19               | Indulgence     |
| 20               | Cooking        |
| 21               | Mexican        |
| 22               | Baking         |
| 23               | Coffee         |
| 24               | Organic        |


This approach provided an unbiased label for each community based on the top 100 words, a task that would be challenging and longsome for a human to do. Additionally, this method allowed us to quickly identify products that link communities, as seen in the network analysis part 4. You can see a wordcloud for all the 25 different communities and read more about this analysis in the [**Explainer Notebook**](explainer-notebook.html) under the text-analysis.
 
<!-- <figure>
    <img src="/images/betweenness.png" width="80%" alt="Scraping">
    <figcaption style="text-align:center;font-style: italic;font-size:smaller;">  Figure. 4: A dataframe showing the top betweeness centrality products in the network and the communities they link.  </figcaption>
</figure> -->

