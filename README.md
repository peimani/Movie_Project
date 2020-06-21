# Getting into the Film Industry:

For this project we are exploring how Microsoft can best enter the movie production business.  As multiple different streaming services have popped up recently (Amazon Prime movies, Disney +, etc. . .), we’ve been tasked with using data analysis for helping guide decisions on how to most effectively enter the market.

Our methods and findings are summarized below:

## Data Cleaning:

For the data, we were investigating a series of nine csv files, ranging from roughly five thousand rows to well over 100 thousand.  Some of these files had matching columns names, and some didn’t.  That said, we needed a little bit from all of these sheets though, and subsequently had to clean them.

To accomplish this task, we did some light initial cleaning (getting rid of duplicates, filling in title data, removing outliers, etc. . .) and then created a SQL database so we could pull up dataframes using Pandas for different purposes at will.  

For cleanest results, we most often chose the primary factor we were investigating (example: directors), then did a left join to add less essential explanatory data (example: average budget or birth year).  After that, we searched for null values, missing data, outliers, and dealt with the issues at hand.

## Question 1 - How to Time Releases by Genre:

We explored genre first.  We were curious as to how the different genres behaved during different months in terms of gross revenue they brought in. For the data behind this exploration, we used Pandas to do various left and inner joins, cleaning as we went along.  We started with the title basics file as it had a variable called tconst, some basic information on the movie, and a couple different versions of the title name, for example, foreign release name and original name.  

To start cleaning, we removed missing original titles with the primary titles, and missing runtimes (there weren’t many missing) with the mean runtime.  This seemed like a better decision than dropping other valuable data in a given row.  We then split the grouped genres into three.  For example, “Action,Crime,Drama” would now become three columns, “Action”, “Crime”, and “Drama”.

After a few more rounds of joins and cleanings (mostly left joins so the starting information was the core of our dataframe), we had a new file, that had title, title id, primary genre, runtime, month of release (another value I had separated out), a few other less important variables, but most importantly, foreign and domestic gross revenue.  From here, I was able to compile the following chart:
 
![Imgur](https://i.imgur.com/REe0rRv.png)

From there, I gathered the top six genres by revenue.  Listed from most to least revenue, they are Action, Adventure, Drama, Comedy, Documentary, and Biography.  Next I started looking at when revenue spiked (both worldwide and domestic) for each genre.  Below is the final chart.  As you can see, each genre has 2-3 months where revenue spikes significantly.  This is likely when the market and demand for these movies is highest.  Using this information, Microsoft can create a release schedule for its top movies in each genre!  The gross revenue figures (Y axis) are shown in billions of dollars, and the pink signifies worldwide gross, while the blue signifies domestic gross.

![Imgur](https://i.imgur.com/VroLKBt.png)


## Question 2 - Do We Need To Spend A Lot To Make A Lot?

To help assess this question we started importing and analyzing the dataframe called movie budgets. After our analysis we realized that we would need to clean up this file by converting the columns that had monetary input into integers. This was done with the following code:

![Imgur](https://i.imgur.com/cXQ0WPm.png)

After the conversion was verified we dropped the column labeled ‘worldwide_gross’.  This was because it was agreed that we are looking at entering the domestic market as an initial rollout. Looking at the world market would require consideration of many factors which would be country dependent. Once we have a better understanding of the domestic market we could develop foreign strategies based on the country of expansion.

![Imgur](https://i.imgur.com/sToYeCa.png)

After cleaning this dataframe we plotted a Scatter Plot using Seaborn that would help us best visualize any correlations or trends between Production Budget and Domestic Gross. While we saw a positive correlation between the two variables, our interest focused on movies with a budget of $200 million.  At this mark we saw films with high gross profits.  

![Imgur](https://i.imgur.com/OVmYRiU.png)

Identifying the area where we could maximize our profit, we identified the top 10 films.



## Question 3 - What Are The Top 10 Money Making Movies?
In order to isolate the films with a production budget of $200 million we picked only those rows. Once these rows were picked the data was sorted by domestic_gross in a descending order to highlight the highest domestic gross first and sequentially go lower from that point.

![Imgur](https://i.imgur.com/5PAAvC8.png)


At this point we created a new column to display the percentage of profit each film made (percent_profit). To accomplish this, the columns for domestic_gross was divided by the productions_budget and multiplied by 100. Then a line of code was added to make sure this new columns data type was an integer.
![Imgur](https://i.imgur.com/WRT3eMF.png)


This set up our data frame to graph the top 10 movies by the percentage of profit.
![Imgur](https://i.imgur.com/KzaRybj.png)




The results led us to hypothesize that movies that use lots of special effects and animation have a good return on investment.  This data can lead to further research and discussions with Microsoft regarding what technology and/or infrastructure they have that may cut the costs of production for these types of movies.


## Question 4 - Improving Ratings:

Now that we know that an enormous budget isn’t necessary to gain revenue success, I looked for ways to improve ratings.  While revenue and profit are important, ratings keep customer loyalty.  If your movies are badly rated, it hurts publicity and will lead to customers dropping your platform.  

For this questions, I explored the data through a SQL database I had put together with the various CSV files.  The reason I did it this way is because I was exploring several different variables.  Since I was answering several different smaller questions, it was easier to use SQL queries suited to the question at hand, rather than creating a dataframe for all the questions using Pandas alone.  

For example, when talking about studios, I had to use SQL to start with the cleaned dataframe I had from my first question, left join studio data so I had the studio names, drop the null values, and I was left with valuable clean data on 71 distinct studios.  This is something that would have been much more complicated using Pandas alone.

I explored the following variables as these items are variables that microsoft can control directly:
* Budget
* Runtime
* Studio
* Genre
* Director
I was curious which of these factors correlate with better ratings or in a simpler sense, which of these microsoft could manipulate to improve ratings:

**Budget**:

Surprisingly, there’s not much correlation between budget and ratings.  This is likely due to small Art House studios making shoestring budget films that rate highly.  The tradeoff here is that the small Art House studios don’t often generate that much revenue.  That said, I would advise Microsoft to work with these studios as well as the larger ones as these smaller, more artistically focused studios can lead to better ratings. 

![Imgur](https://i.imgur.com/75txSps.png)

**Runtime**:

Runtime correlates fairly highly with ratings success.  While it’s not always appropriate to drag out your films, an extra half hour on a high quality film certainly can’t hurt!

![Imgur](https://i.imgur.com/KmCqIM4.png)

**Studio**:

This is where some of the more serious analysis started.  As we noted above, a high budget does not equal a stellar rating.  As such, if we’re looking for studios to work with or acquire, we should be searching for studios with experience (not one hit wonders) that are able to put out high quality films on a reasonable budget.  With the data I collected, I had a clean list of 71 studios to go through.  

I created a scatter plot showing average rating on the y axis, average budget on the x axis, average domestic gross as dot size, and number of movies on the color scale (high number being lighter).  We identified the following studios as promising partners due to their modest budgets, experience with multiple highly regarded films, and reasonable high revenue potential.

![Imgur](https://i.imgur.com/TLTgzMw.png)

The following studios (with some of their more well known movies) stood out: 
* **MBox** - *Girl with Dragon Tattoo and Ida*
* **Neon** - *I, Tonya*
* **Lantern Entertainment** (previously known as Weinstein company) - *The King’s Speech, Django Unchained*
* **TriS** - *John Wick, Looper*

**Genre**:

Next we took a look at genres.  From the boxplot below, it seems that a small emphasis on putting out dramas and biography films may be to our advantage in terms of ratings.  As we discovered in previous questions, though, these two genres are not huge moneymakers, so it would be wise to not lean on them too heavily.  That said, these are the only two genres with average ratings above 7.

![Imgur](https://i.imgur.com/7eDxCyQ.png)

**Director**:

Lastly we looked at directors.  Here, we took a similar approach to the studio question.  Who has experience?  Who brings in above average revenue?  Who can create well rated movies on below average budgets?  I created a scatterplot tracking the following:
* Average Rating on the Y axis
* Total Domestic Gross on the X axis
* Average Budget on the color scale

With these criteria, we can identify which directors create excellent movies on medium/low budgets (while still bringing in high revenue).  For this chart, I only pulled in the top 100 directors in terms of total domestic gross.  I think we can afford to be a bit selective here!

![Imgur](https://i.imgur.com/GQV4A4e.png)

With the above chart, we identified the following directors with one of their most well known movies:
* **Marilyn Barnes** - *Beauty and the Beast*
* **Tim Miller** - *Deadpool*
* **Martin Scoresese** - *The Wolf of Wall Street*


## Further Work To Do

- One of the areas that will need more research will be to identify if there is any correlation with these movies and the production staff. 
- We would also be interested in identifying the costs of computer graphics and the studios involved. This would allow us to figure out if it may be more cost effective to use Microsoft technology or have Microsoft invest in a special effects studio.
- Another area of research would be to see how much money these movies can make when released straight to a streaming service like Netflix.  With the COVID-19 pandemic, movie theaters may not be as profitable so it would be a good idea to look at investing in movies made for a streaming audience.

## Conclusion:

There are many factors involved in making a successful film. In order to make a good decision it is important to ask many questions and look at many variables. We can try and minimize this risk by releasing certain genres corresponding to certain dates when the genres are popular.  

Budgeting for a movie project is also crucial in the development of a film. It is important to strike a balance for the production budget and break down those costs to prioritize those costs. 
Along with identifying monetary considerations, the crew that makes the movie can also be vital to their success.  People like, Producers, Directors, Actors and Writers of screenplays can help in choosing what movie project is put into production.

While it is very possible to gather data for many factors and still make a movie that does not do well in the box office, we can minimize this risk. By using reliable data, organizing and cleaning it properly, we can provide the information needed for Microsoft to make its decision.


