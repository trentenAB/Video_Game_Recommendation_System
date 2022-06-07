![Banner](https://user-images.githubusercontent.com/89433717/170891205-463af589-40b0-4135-9141-66b115c70c7b.png)
# [Collection](https://github.com/trentenAB/Video_Game_Recommendation_System/blob/main/notebooks/scraping_meta.ipynb)
The data was scraped off of MetaCritic's [Best Games of All Time](https://www.metacritic.com/browse/games/score/metascore/all/all/filtered) List<br><br>
<ins>__Libraries__</ins> 
- requests: For making HTTP requests. Turns the HTML of each page into a string for parsing.  
- BeautifulSoup: For parsing through the HTML.
- pandas: For Data Management
- playsound: For playing a notification sound after interruption or completion of scraping
- yagmail: For sending an email after interruption or completion of scraping
- concurrent.futures: For greatly reducing scraping time. It utilizes at most 32 CPU cores for executing calls asynchronously. 
__________________________________________________________________________________________
# [Data](https://www.kaggle.com/datasets/trentenberam/metacritic-games-all-time)
### Game Set
- `title` = Game Title
- `release_date` = Release Date (Games on multiple platforms will have a seperate row per release date)
- `genre` = Genres
- `platform` = Platform (Games on multiple platforms will have a seperate row per platform)
- `developer` = Developer
- `esrb_rating` = __E__ (Everyone), __E10+__ (Everyone 10 and Up), __T__ (Teen 13 and Up), __M__ (Mature 17 and Up), 
                  <br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; __K-A__ (Kids to Adults changed to Everyone in 1998), __AO__ (Adults Only)       
- `ESRBs` = Specific content descriptions that could be of interest (Check out the [Ratings Guide](https://www.esrb.org/ratings-guide/) for more details)
- `metascore` = Weighted average of critic scores. Weights are determined by critic fame ([Here](https://www.metacritic.com/about-metascores) for more info)
- `userscore` = Average of user scores
- `critic_reviews` = Number of critic reviews
- `user_reviews` = Number of user reviews 
- `num_players` = Description of how many players allowed on game
- `summary` = Summary of game

### Review Set
- `ids` = User id
- `game` = Game Title
- `rating` = User's score of game
- `review` = User's review
__________________________________________________________________________________________
# [Wrangling](https://github.com/trentenAB/Video_Game_Recommendation_System/blob/main/notebooks/Wrangling.ipynb)
There wasn't too much permanent cleaning done to either dataset. For the Game Set, there were 11 entries where the `release_date` value was not a date. Some of them also happened to be the summary of that game. Because there were 11 instances, I manually searched the release date of each game, inserted it, and updated the summaries as needed. I was then able to convert `release_date` to a datetime column. 

![Game Set](https://user-images.githubusercontent.com/89433717/170890214-e72c1d23-f225-42a5-928b-1dad096db551.png)

Based off the abundance of null values for some of the columns, I made subsets of the data with the non-null values to use for visualizations. This can be seen more clearly in the [EDA](https://github.com/trentenAB/Video_Game_Recommendation_System/tree/main/notebooks/VGR%20EDA) notebook.  

[//]: # (Put pictures of this process)

For the Review Set, there were 10 entries where the user name was null. These happened to be pairs of duplicates and somehow pandas was able to distinguish between the different null-values.

![negative ids](https://user-images.githubusercontent.com/89433717/170890328-bb1610a9-0ccf-4223-ac77-849c0a49e3f0.png)

The duplicates were dropped, as well as for the rest of the dataset, and the ids were used in lieu of the user_names. 

![Reviews.info()](https://user-images.githubusercontent.com/89433717/170890380-5cb4f4b0-7790-4be2-b814-a049d2fbebdf.png)
__________________________________________________________________________________________
# [EDA](https://github.com/trentenAB/Video_Game_Recommendation_System/tree/main/notebooks/VGR%20EDA)
The Game Set was mainly used for the visualizations. As mentioned before, because of the large percentage of null-values for columns like `ESRBs`, subsets were created for each visual. Here is a visualization I thought to be the most interesting. 

![Critic and User Ratings 1999-2022](https://github.com/trentenAB/Video_Game_Recommendation_System/blob/main/notebooks/VGR%20EDA/CriticScores%20vs%20UserScores.png)

Here we can see the obvious decline in game ratings throughout the 2000s. Then sometime during 2012, we can see a fairly large diverge begin between user and critic scores. One could speculate that these trends were signs of cultural shifts within and outside the gaming community.   
__________________________________________________________________________________________
# [Pre-Processing/Modeling](https://github.com/trentenAB/Video_Game_Recommendation_System/blob/main/notebooks/Preprocess%20and%20Modeling.ipynb)

Both Content and Collaborative filtering were attempted.

__<ins>Content Filtering:</ins>__
- <ins>Genre Similarities</ins>: Using the `genre` feature of the [Game Set](https://user-images.githubusercontent.com/89433717/170890214-e72c1d23-f225-42a5-928b-1dad096db551.png), a dummy matrix was made for the all the titles and the respective genres. This is a matrix that only has 0 or 1 as values depending on if the game title contains the particular genre.    

![genre dummy matrix](https://user-images.githubusercontent.com/89433717/172474691-673d65d1-7d49-412a-91e7-7affab0de030.png)


[//]: # (Put pic of the dummy matrix)

Using the dummy matrix, another matrix was created containing the [jaccard similarity](https://en.wikipedia.org/wiki/Jaccard_index) coefficients for each game to every other game. This was made using scipy's [pdist](https://docs.scipy.org/doc/scipy/reference/generated/scipy.spatial.distance.pdist.html) and [squareform](https://docs.scipy.org/doc/scipy/reference/generated/scipy.spatial.distance.squareform.html?highlight=squareform#scipy.spatial.distance.squareform) packages. With this matrix, one could look up the titles with the most similar genres. 

![elden ring genre similarities](https://user-images.githubusercontent.com/89433717/172476244-f4045164-427e-41cb-8b96-f257783e2e59.png)<br>
*The scores of 1 mean all these games have the same exact genres as Elden Ring*

But as we can see, due to the abundance of games and the lack of genres associated to each game, there will be many pairings where games have the exact same genres.



__<ins>Collaborative Filtering:</ins>__

