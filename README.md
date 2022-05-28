![Banner](https://github.com/trentenAB/Video_Game_Recommendation_System/blob/main/VGR%20Banner.png)
# Collection
The data was scraped off of MetaCritic's [Games of All Time](https://www.metacritic.com/browse/games/score/metascore/all/all/filtered) List<br><br>
__Libraries__: requests, BeautifulSoup, pandas, numpy, playsound, yagmail, concurrent.futures

# Data
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
- `user` = User id
- `game` = Game Title
- `rating` = User's score of game
- `review` = User's review

# EDA
# Pre-Processing/Modeling

