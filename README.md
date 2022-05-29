![Banner](https://github.com/trentenAB/Video_Game_Recommendation_System/blob/main/VGR%20Banner.png)
# [Collection](https://github.com/trentenAB/Video_Game_Recommendation_System/blob/main/notebooks/scraping_meta.ipynb)
The data was scraped off of MetaCritic's [Best Games of All Time](https://www.metacritic.com/browse/games/score/metascore/all/all/filtered) List<br><br>
<ins>__Libraries__</ins> 
- requests: For making HTTP requests. Turns the HTML of each page into a string for parsing.  
- BeautifulSoup: For parsing through the HTML.
- pandas: For Data Management
- playsound: For playing a notification sound after interruption or completion of scraping
- yagmail: For sending an email after interruption or completion of scraping
- concurrent.futures: For greatly reducing scraping time. It utilizes at most 32 CPU cores for executing calls asynchronously. 

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
__________________________________________________________________________________
### Review Set
- `ids` = User id
- `game` = Game Title
- `rating` = User's score of game
- `review` = User's review

# [Wrangling](https://github.com/trentenAB/Video_Game_Recommendation_System/blob/main/notebooks/Wrangling.ipynb)
There wasn't too much permanent cleaning done to either dataset. For the Game Set, there was 11 entries where the `release_date` was not a date. 
[//]: <(Put pictures of this process)>
For the Review Set, there were 10 entries where the user name was null. These happened to be pairs of duplicates. 
[//]: <(Put pictures of this process)>
Based off the abundance of null values for some of the columns, I made subsets of the data with the non-null values to use for visualizations. 

# [EDA](https://github.com/trentenAB/Video_Game_Recommendation_System/tree/main/notebooks/VGR%20EDA)

# [Pre-Processing/Modeling](https://github.com/trentenAB/Video_Game_Recommendation_System/blob/main/notebooks/Preprocess%20and%20Modeling.ipynb)

