---
title: Text analysis
prev: network-analysis
---

We would like to get an insight in the consumer buying patterns and we could get this insight by analyzing the the words that characterize certain natural communities within the frequently-bought-together network. Here, we might get som insight in what makes products frequently bought together. In order to do this, we use the TF-IDF scores on the tokenized product descriptions.
These TF-IDF scores of words help us identify what words specifically are unique for each community.
The TF-IDF scores of words for the top 9 communities can be seen below:

| Community 16 TF-IDF Words | Community 24 TF-IDF Words | Community 18 TF-IDF Words |
|----------------------------|----------------------------|----------------------------|
| lækker 0.0126             | økologisk 0.0119           | gin 0.0129                |
| salling 0.0122            | salling 0.0113             | vinen 0.0115              |
| smag 0.0119               | smag 0.0112                | noter 0.0105              |
| prøv 0.0110               | økologiske 0.0112          | smag 0.0104               |
| nyd 0.0106                | kaffe 0.0110               | ved 0.0103                |
| frisk 0.0103              | brug 0.0110                | frisk 0.0098              |
| brug 0.0099               | prøv 0.0109                | vin 0.0096                |
| ved 0.0097                | øko 0.0108                 | nyd 0.0093                |
| lidt 0.0097               | retter 0.0106              | smagen 0.0092             |

| Community 19 TF-IDF Words | Community 3 TF-IDF Words | Community 22 TF-IDF Words |
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

| Community 9 TF-IDF Words | Community 8 TF-IDF Words | Community 17 TF-IDF Words |
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

And the top 3 most frequently bought togehter product for each of those communities

| Community 16 top products | Community 24 top products | Community 18 top products |
|----------------------------|----------------------------|----------------------------|
| agurk                      | finvalsede havregryn øko   | tonic                      |
| agurk                      | æg m/l øko                 | london dry gin             |
| skrabeæg m/l              | hakkede tomater øko        | indian tonic water         |

| Community 19 top products  | Community 3 top products  | Community 22 top products |
|---------------------------- |-------------------------- |---------------------------|
| lakridsbolcher             | fyldte røde peberfrugter m. flødeost  | husblas                    |
| tappsy                     |  lufttørret italiensk bresaola i skiver             | flormelis                  |
| chocofant                  | serranoskinke, salchichon og chorizo    | sukker                     |


| Community 9 top products  | Community 8 top products  | Community 17 top products |
|-------------------------- |-------------------------- |---------------------------|
| tyggegummi m. frugtsmag   | smørepålæg vegansk        | appelsinjuice fra   koncentrat      |
| coca cola                  | vegetarpålæg i skiver m. peber     |       solbærmarmelade          |
| sportssodavand sukkerfri  |    creme fraiche dressing                |       appelsinmarmelade     |


We see some different patterns that we can associate from each other in each communities. We some clear ones in e.g. community 24 that has ecology, and community 19 which has a lot of top words that can make this community be interperated like a candy-like community with top words like 'mix', 'liquorice', 'milk-chocolate' etc. But to get a better overview of the top words within each community, let's look at the top TF-IDF words in word clouds for the top 9 communities:

<figure>
    <img src="/images/wordcloud_9.png" width="80%" alt="Scraping">
    <figcaption style="text-align:center;font-style: italic;font-size:smaller;">Figure. 3: Worldcloud showing the top TF-IDF word for the top 9 communities with the top 3 most frequently bought together products above them.  </figcaption>
</figure>

Here we can distinguish betwween the top 9 communities for the words that are specif for each community. Which makes us able to pinpoint each buying pattern when visiting a Salling store. To further help with the distinguishing of each community we made an API call for chatGPT 3.5 to classify each community based on the top 100 TF-IDF words for that specific community. The classifications for each community are:


1. Community 16: 'Everyday'
> This community's top TF-IDF words include: 'Salling', 'Delicious', 'taste', 'enjoy', 'together'. This makes sense that this is the biggest community within the frequently-bought-together network, as when a consumer buys food, they usually buys in bulk in mealplans for the whole week, and [this study](https://ijbnpa.biomedcentral.com/articles/10.1186/s12966-017-0461-7) showed that atleast 57% of families buy after weekly mealplans (across the US). This means that atleast the majority buy a lot of diverse foods for the 'everyday' shopping, and is why this community is the largest. The products with the highest degrees within this community are two different brands of (agurk) cucumbers, and normal (skrabeæg) eggs, which makes sense as these products are used in a lot of different dishes.

2. Community 24: 'Organic'
> This community's top TF-IDF words include: 'Salling', 'Ecological', 'Taste', 'Cofee'. This community represents a lot of what community 16 does of everyday bought items, but include ecological items. This community makes sense, as it is still the same reasoning with consumers buying for mealplans, but people who buy some ecological items, tend to buy all ecological items together, you can read more about the assortativity analysis in the explainer notebook. The products with the highest degrees in this community is eco oatmeal, eco eggs, and eco tomato.

3. Community 18: 'Beverages'
> This community's top TF-IDF words include: 'Gin', 'Wine', 'notes', 'taste'. This community describes a consumer buying drinks or wine for a maybe a night with guests, indicated by one of the top words 'Together' that would indicate that the drinks are to be enjoyed with company. This community is also large because when buying drinks consumers tend to buy things together because drinks are a comibnation of different products mixed together. Hence, why the word 'Gin' is the largest in the wordcloud, as Gin & Tonic is a very common drink especially in denmark. This is further shown by the top 3 products with higest degree in this community which is two types of tonic water and London dry gin.

4. Community 19: 'Indulgence'
> This community's top TF-IDF words include: 'liquorice', 'Mix', 'Milkchocolate', 'Chocolate'. This is the 4th largest community in the network, and makes sense because shops put Candy and other indulgences together in the same spot, and together with the urge of eating a lot of sugary stuff for a movienight or party, makes the indulgence community rather large. The top products in this community are 'liquorice hard candy', 'tappsy' and 'chocofants'.

5. Community 3: 'Gourmet' / 'Tapas'
> This community was classified as 'Gourmet' but we thought that 'Tapas' was a more fitting category for this community. This community's top TF-IDF words include: 'Olives', 'Cheese', 'Taste' and 'delicious'. This community is less large as it is more of a niche category. But for tapas certain things are tend to be bought together like the top frequently-bought-together items in this community: 'Bell pepper', 'Italian bresaola', and 'italian serrano ham'.

6. Community 22: 'Baking' 
> This community's top TF-IDF words include: 'Desert', 'Cake', 'Oetker' and 'Delicious'. This community would be associated with a buying patterns of a consumer that wants to bake. This is shown by the top words in the community and 'Oetker' is a brand that is used for baking. These things are often bought together as you typically need specific things for a recipe when baking. This conclusion is further enforced when looking at the top products in this community which is 'powdered sugar', 'gelatin' and 'sugar'.

7. Community 9: 'Energy'
> This community's top TF-IDF words include: 'Energydrink', 'Faxe kondi', Rerfreshing'. This community is identified by the need of a refreshment or energy like some energy drink or soda. The reason why this community is rather large is that consumers typically buys refreshments to more people likes guests where people prefer different things to drink. A reason why it is not higher up in size, is that sometimes people just go to the supermarket to buy a single refreshment and not a lot of other products. The top products in this community include: 'Gum with fruit flavor', 'Coca Cola', and 'Sportsdrink'

8. Community 8: 'Vegan' 
> This community's top TF-IDF words include: 'Vegan', 'Delicious', 'Ecology' and 'Enjoy'. This community is distinguished by the vegan aspect. People who are vegan tend to buy other vegan and ecology groceries together. A reason for the not so large community here is that there are not such a vast selection of vegan foods in the grocery shops yet and vegan consumers usually only stick to buying vegan groceries and not other non-vegan products. The top products in this community are: 'vegan butter', 'vegan toppings' and 'creme fraiche dressing'.

9. Community 17: 'Healthy'
> This community's top TF-IDF words include: 'Salad', 'The dish', 'Enjoy'. This community is classified as a healthy community. Here a conclusion to this community would be that certain consumers buy very healthy products like salads and healthy juices as indicated by the word 'innocent' which is a type of brand for healthy juices. The top bought products in this community is: 'orange juice', blackcurrants- and orange marmelade.  

We set up a loop classifying each community based on the top 100 TF-IDF words with OpenAI's ChatGPT using their API to call the gpt-3.5-turbo model. We chose to use GPT-3.5 because this is a very cableable model at this low level task and because it is cheap in operation. We run a simple prompt with instructions to use a single word to classify each community, and we use the top 100 words because of token limits and at some point the TF-IDF score for these word become too low. We realize that chatGPT does not have a way of setting a seed, so the output could vary when running this code again. To mitigate this we put the 'temperature' variable that controls creativity in the llm to 0. However, this still didn't give consistent results so without spending the majority of the timeframe in this project and throughout the analysis we use this mapping of the communities that was the most consistent in the outputs. This was the categories for each community:

| Community Number | Community Category |
|------------------|----------------|
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

> To see a wordcloud for all the 25 different communities you can look at our [Explainer Notebook](explainer-notebook.html) under the text analysis.

This was done in order to label get an unbiased label on each community based on 100 words which that many words can be somewhat of a challenge to do for a human. Furthermore, we can quickly see what products that link communities together and what type of commmunities the products link together with a one word category. You can read more about this analysis in the [Explainer Notebook](explainer-notebook.html) under the network analysis.

<figure>
    <img src="/images/betweenness.png" width="80%" alt="Scraping">
    <figcaption style="text-align:center;font-style: italic;font-size:smaller;">  Figure. 4: A dataframe showing the top betweeness centrality products in the network and the communities they link.  </figcaption>
</figure>

The dataframe is sorted such that the products on the left, are ordered from highest betweenness centrality to lowest of the top 15 highest betweenness centrality in the entire frequently-bought-together network.
A higher betweenness centrality means that this products is likely to be a bridge between different grocery shopping categories. This means that these products are likely for a consumer to bought toether with a varity of goods. A reason why the cucumber is the highest, could be that it goes into a lot of different dishes, can be a snack and the vegetables are typically the first things a customer sees when entering a supermarket, and it's cheap. All this could explain why it is more likely to be picked up into a basket with a lot of different stuff.

Based on the dataframe, we can see that several products have high betweenness centrality, meaning they are often bought together with products from other categories. These products include:

- Cucumbers (agurk)
- Butter (smørbar)
- Organic cucumbers (agurk øko)
- Organic eggs (æg m/l øko)
- Grated oatmeal (finvalsede havregryn øko)
- Remoulade (remoulade øko)
- Wheat flour (hvedemel øko)

These products could be considered "bridge" products that connect different shopping categories. For example, organic cucumbers (agurk øko) appear in the "Healthy", "Organic", "Everyday", and "Beverages" communities. This suggests that organic cucumbers are often bought together with a variety of other products, such as healthy snacks, other organic items, everyday staples, and beverages.