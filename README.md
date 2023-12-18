In the enthralling world of cinema 🎥, actors play a pivotal role, shaping and being shaped by the ever-evolving tapestry of human history. Embark with us on a cinematic journey through time as we explore actor’s recognition and their evolving representation in the world of cinema across history. Has an actor's recognition and its longevity been influenced by specific attributes such as genre, ethnicity? Acting isn't an isolated art form but rather intricately connected to the tapestry of human existence, always influenced and shaped by historical events. Our objective is to decode the impact of pivotal historical events, such as the Civil Rights and Feminist Movements, on the composition of actors in terms of gender and ethnicity. This project invites you on a cinematic journey delving into the life of actors who have graced the Cinema screens, examining how they have been portrayed, known and represented over time.

**EXPLAIN MORE IN DETAIL THE PLAN OF WHAT WE ARE DOING**

**PUT ALL USED DATASETS IN ANOTHER PAGE WITH THEIR EXPLANATION, REFER TO THIS PAGE HERE**

**A LOT OF MISSING DATA FOR EARLY YEARS THIS CAN AFFECT THE ANALYSIS**

**RESEARCH QUESTIONS?**

# Actor’s Recognition

We've all certainly always got into debates like: "No! This actor is more worldwide recognized than this one!" or things like: "I don't agree, I think this actor is the most known ever!" We've come to help! To mitigate any doubt, the idea would be to quantify an Actor's Recognition and study its evolution. Let's start walking you through how we do that. In our analysis, we consider that an Actor's recognition depends on the revenue, quality and popularity of the movies the corresponding Actor acts in. Indeed, if an Actor is very well-known, he would be majoritarly acting in movies of high revenue and high popularity. On the other hand, a not-so recognized Actor would be in the major part of his career in movies that are not very well-known, i.e. that do not have very high revenues and that are not very popular. To account for movie revenue we use the movie Box-office while adapting its value with yearly inflation rates to have the same monetary scale for comparison. Furthermore to account for quality and popularity, we use IMDb ratings, IMDb rating would not only qantify the cinematic quality of a movie but also its popularity, since IMDb rating are done by "normal movie lovers" (CHANGE) and not by professional critics. To have the Box-office and ratings on a comparable scale, we normalize them and scale them on a scale going from 0 to 1. What is necessary now is that we define a recognition coefficient ($$RC$$)  to asses the recognition of an actor. Let us now define some coefficients that will be relevant to our analysis.

In our methodology for assessing an actor's recognition over time, we introduce the concept of a movie recognition coefficient ($$RC_{movie}$$). This coefficient captures an actor's recognition in a specific year and movie. To calculate this coefficient, we calculate a movie coefficient ($$MC$$) as the average of the normalized movie rating and box office revenue scores:

$$MC(actor,year,movie) = \frac{Normalized \_ Revenue(actor,year,movie) + Normalized \_ Rating(actor,year,movie)}{2}$$

Here, $$Normalized \_ Revenue(actor, year, movie)$$ and $$Normalized \_ Rating(actor, year, movie)$$ represent the normalized rating and box office revenue scores, respectively.

Since the importance of every actor is not the same in the same movie, we estimate the actor's importance in a given movie by analysing the plot summary of the movie and counting the number of times this actor is mentioned or referenced in the summary. We divide that value by the highest number of mentions to give an estimate between 0 and 1 of how important the character is important in the movie, having then an importance coefficient ($$IC$$). We then use this actor importance in a movie to calculate an actor's movie recognition coefficient ($$RC_{movie}$$) as follows:

$$RC_{movie}(actor, year, movie) = MC(actor, year, movie) \times (1 + IC(actor, year, movie))$$

To gauge an actor's overall recognition in a given year, we aggregate the movie recognition coefficients using the formula:

$$RC_{year}(actor,year) = \frac{1}{n(actor)} \sum_{i=1}^{n(actor)} RC_{movie}(actor,year,{movie}_i)$$

In this equation, $$n(actor)$$ represents the total number of movies in which the actor participated during the specific year.

Recognizing that an actor may maintain a certain level of recognition even in years with no movie releases, we incorporate a momentum effect. The yearly recognition coefficient is updated with a fraction ($$C=0.9$$) of the actor's previous year's recognition coefficient:

$$\overline{RC_{year}}(actor,year) = RC_{year}(actor,year) + C *\overline{RC_{year}}(actor,year-1)$$

It is important to note that we initialize the momentum term, $$\overline{RC_{year}}(actor, 0)$$, to zero.

Finally, to obtain an actor's overall recognition coefficient, we aggregate the yearly recognition coefficients with momentum over a span of years:

$$RC_{overall}(actor) = \frac{1}{Y} \sum_{i=1}^{Y} \overline{RC_{year}}(actor,{year}_i)$$

Here, $$Y$$ represents the total number of years considered in the analysis. This comprehensive approach provides a nuanced understanding of an actor's recognition, accounting for both individual movie performances and the temporal evolution of their career.


After defining these coefficients, we can now delve into our analysis of Actors' Recognition. First, since we have a yearly $$RC$$ for every actor, it would be interesting to examine the mean-magnitude of recognition every year, here's a plot showing this.

{% include recognition_plot.html %}

RESULTS:
Doing a Pearson test on this aggregated data, we find a $$p-value=10^{-31} < < 0.05$$. This means that we have strong evidence to reject the null-Hypothesis that suggests that there is no correlation between the Year and the Average Recognition Coefficient. This would suggest that with time the average "Magnitude of Recognition" of actors increases, i.e. the revenue and rating of movies increases with time, suggesting that actors become more and more well-recognized and Cinema is taking a bigger part in society. That is indeed what we see in the plot, where we see that thr average recognition coefficient is increasing with time.



Looking at the graph, we suspect that there is a strong change in the way the average recognition coefficient increases post-1970. 

To be sure of that, we can perform a Chow test, which tests if the coefficients in two different regression models on different regions of the data are equal. Performing the test, we get a $$p-value=  < < 0.05$$. Since the p-value is smaller than 0.05, we can reject the null hypothesis of the test. This means we have sufficient evidence to say that a structural break point is present in the data. We can say that starting 19770, actors are getting even more recognized and the Cinema is booming, this is boom can be caused by two important historical factors:

- The Blockbuster Phenomenon, "Jaws" (1975): Directed by Steven Spielberg, is often considered the first blockbuster film, changing the landscape of film distribution and marketing. Furthermore the release of "Star Wars" in 1977 (directed by George Luca) revolutionized the science fiction genre and became a cultural phenomenon, setting new standards for the movie industry and how to merchandise it.
- The second reason could be the invention of VHS (short for Video Home System) in 1976, which allowed audiences to watch films at home, transforming the industry's distribution model and making Cinema more accessible.

<p align="center">
  <img src="images/STAR_WARS.jpg" width="600" alt="Image 1">
  <img src="images/JAWS.jpg" width="220" alt="Image 2">
</p>
<p align="center">
  <img src="images/VHS.png" width="400" alt="Image 1">
</p>


In the meantime we see also some decrease, this likely due to the fact that in the most recent years (until 2012), the data is not very much up to date.

After checking the Actor Recognition through the years, let us move on to the more exciting part: Evaluating the overall recognition of actors. We present here a list of Actors ranked by most recognized to less recognized. You can try to find your favorite actor and see how is he ranked. Also, as a small game, considering all the actors you know, try to find the less known of them in this list!


{% include Actor_table.html %}


We hope that you found your favorite actors among this list 😀.
 
The above table provides a glimpse into the top well-recognized actors, showcasing their General Recognition Coefficients. Notably, in the first rankings the list features both contemporary figures like Robert De Niro and iconic actors from earlier periods, such as John Wayne and Sean Connery. Also, sadly but intuitivly, we see that the number of female actors is very minorr. Showcasing the still existing dominace of well-known male actors.
This ranking highlights the timeless influence of actors, encompassing both modern-day stars and those from cinematic history.

Moving on, having this list of actors, we can try to visualize the distribution of only the top 10% Well-recognized of these actors. Are the modern-day actors more present among these 10%?

{% include well_recognized_actors_plot.html %}

Indeed as we can imagine, we see that among these 10% of actors, their majority is present in modern-days. Once again, we see this final decrease we saw before, likely due to the fact that in the most recent years (until 2012), the data is not very much up to date. Moreover, we can also see this sudden increase in number of actors post-1970, which is likely to be due to the reasons we explained before.


# Actor Recognition Longevity

Now that we had a timely approach to Actors' Recognition, let's now see how this Recognition lasts over time. The idea is to examine the span of the actors' Recognition through time. In other words, we are trying to find the year in which the actor started to be well-recognized and the year this recognition "ended". The criteria for determining these periods involve selecting the range of years in which the Actor Yearly Recognition Coefficient surpasses a defined threshold. This threshold is set at 50% of the actor's highest recognition coefficient score, providing a concise measure of the actor's sustained impact over time. We can see below the plot showing the average span of recognition through the years.

{% include average_span_recognition_plot.html %}

We observe that actors starting to be well-recognized after 1970 have decreasingly small spans of recognition. This is due to the fact the data we have ends in 2012, this means that these actors are probably still acting after 2012 but we don't have the corresponding data. Therefore the Last Year of recognition of these actors is considered to be around 2012 as we can see in the following histogram

{% include last_year_recognition_histogram.html %}

In order to evaluate the correlation between the average recognition span and first year of recognition, we use only the data before 1970, since the decrease of recognition span after 1970 is not reflective of the reality. Therefore, we fit a linear regression on spans starting before 1970.

{% include fitted_average_span_recognition_plot.html %}

Based on the above graph and the Pearson test we do (which gives us a $$p-value= 0.0008<0.05$$ ), we observe a trend of increase in the average span of recognition for actors (before 1970). This result suggests that with time actors tend to have longer periods of recognition. This could be attributed to several factors like increase in quality of health and more late retirements.

## Recognition coefficient of specific actors
As an interesting step, we can also inspect the evolution of the recognition coefficient of different actors:

{% include specific_actors.html %}

From the graphs above, we can see how the Recognition of different actors varies with time:
- Michael Caine: We can see that Michael Caine has a very long span of recognition, starting to be well-recognized around 1960 until after 2012. It is also interesting to notice that for the period 1990-2000, he acted in less-succesful movies, but then he had his recognition increase again.
- John Wayne: The second plot with John Wayne is also very interesting since it allows to visualize the Recognition of an actor that stopped to be well-recognized. We can see how his recognition coefficient decreases with time abruptly after 1979, which is in fact the date of his death

Now, your turn! You can see the plot of the evolution of the recognition of your favorite actor. Try 

**INTERESTING EXAMPLES**

{% include Actor_recognition_graph.html %}

# Gender representation in Cinema over time

As a first step to our analysis, let us inspect the proportion of female and male actors over time.

{% include male_female_proportion.html %}

As we can see, the proportion of male actors is predominant and is equal nearly to the double of the proportion of female actors throughout time. However, are there some interesting trends that changed throughout time? Did big historical events, like the Feminist Movement, have an impact on female representation in Cinema?

## Impact of the Feminist movement on female representation in Cinema
The second wave feminist movement, prominent in the 1960s and 1970s, advocated for gender equality and reproductive rights. It gained momentum in the early 1960s, notably sparked by the publication of Betty Friedan's "The Feminine Mystique" in 1963, while its influence gradually waned by the early 1980s. As we know the Feminist movement had a great impact on decreasing gender-based discrimination, like by the Equal Pay Act of 1963, and, Title IX of 1972, an Education Amendment which prohibits gender-based discrimination in educational programs and activities. In this section, we try to explore the impact of this movement on female representation in Cinema and to observe the evolution of female representation during and after this period as it can provide insights into societal shifts and the progress made toward gender parity in cinema.. In order to do that, we divide the data into three parts that are interesting to analyze:
- Before the feminist movement: from 1914 to 1963.
- During the feminist movement: from 1963 to 1980.
- After the feminist movement: from 1980 to 2012.
- 
After that, we fit a regression line on the proportion of female actors for each one of these periods.

{% include female_actors.html %}

We observe a decrease in female representation between 1914 and 1963 and an increase in female representation between 1980 and 2012. Very small p-values ($$p-value << 0.05$$) corresponding to the regression line **before** and **after** the feminist movement suggest that there is indeed a correlation between the dates of the feminist movement and the observed increase. On the other hand, for the regression **during** the feminist movement, we get a $$p-value>0.05$$ suggesting that there is no significant correlation during the movement itself. Furthermore, performing a Chow test on the proportion of female actors during the feminist movement and after the feminist movement yields a $$p-value < 0.05$$ suggesting that we can reject the null hypothesis of the test, meaning we have sufficient evidence to say that a structural break point is present in the between during the feminist movement and after the feminist

Furthermore, it would be interesting to examine the proportion of female actors among the 10% most well recognized actors. Does the trend of well-known female actors follow the one of all female actors? Or, are well-known female actor representation follow different trends through time?

To examine that, we select the top 10% well-known actors from the list shown above and plot the proportion of females among those actors through time.

{% include female_actors_10perc.html %}

As we can see, the plot suggests that there is a permenent increase of the proportion of female actors among well-known actors, independent of the feminist movement. We perform once again a Chow test on the proportion of **well-known** female actors **during** the feminist movement and **after** the feminist movement, which yields a $$p-value>0.05$$. Therefore, we don't have enough evidence to suggest any structural breakpoint.

As a small summary, it is interesting to note that we observe that among all female actors we observe an increase of proportion of female actors thanks to the feminist movement. On the other hand, we observe that the proportion of female actors among well-known actors follows another behaviour, this proportion seems to increase through time independently from the feminist movement. 

## Distribution of Recognition among genders
Having an overall Recognition coefficient for every actor, we can inspect the distribution of these overall Recognition coefficients among female and male actors. This could be done to explore if recognition is evenly distributed between female and male actors. 

{% include male_female_recognition.html %}

As we can see, the number of female actors and male actors is not the same, however we observe that the two histograms could have similar trends. In order to compare the distribution of recognition, we plot the density function for each gender. We have that for each density, $$\int_{0}^{x} f(t) dt$$ represents the probability to have a recognition coefficient below $$x$$.

**OR CCDF**

{% include recognition_densities.html %}

From the plot above, we see that, since the density of female actors has a higher peak, the probability to have low recognition coefficients (below 0.04, for example) is larger for female than for male actors. In other words, male actors that have higher recognition amplitudes are more numerous than female actors. Moreover, to compare if the two density distributions are alike, if they can be sampled from the same distribution, we perform a Kolmogorov–Smirnov test that yields a $$p-value<0.05$$. This means that we have enough evidence to say that the two density distributions are not sampled from the same distribution and that there is a significant difference in these density distributions.

## Actor first-appearance among genders

Another intersting aspect we can inspect is the debut age of the different actors. It would be interesting to find out wether there is a significant difference between the age at which male and female actors start acting. To do the following, we visualize a histogram with the different ages at which male and female actors start acting

{% include 1st_appearance_hist.html %}

As we can see, this plot suggests, that is a difference in means. In other words, female actors seem to start acting earlier than males. Performing a t-test confirms this hypothesis having a very small p-value ($$p-value <<0.05$$), this suggests that there is enough evidence to say there is a significant difference between the mean first appearance age for female actors and for male actors. The plot below highlights this significant difference, showing a mean first appearance age of 24.2 years for female actors anf 29.0 years for male actors.

{% include 1st_appearance_ci.html %}

# Ethnic representation in Cinema over time

Among the significant repercussions of the Feminist movement was the enactment of the Civil Rights Act of 1964, a groundbreaking law designed to combat discrimination based on gender, race, color, religion, or national origin. Simultaneously, the Civil Rights movement, advocating for racial equality, played a pivotal role in shaping the legislative landscape. This lays the foundation for our exploration into the dynamic representation of diverse ethnicities in cinema, tracing its evolution over time and specifically examining the profound impact of movements such as the Civil Rights Movement on the portrayal of black actors in the film industry. 


To delve into this investigation, comprehensive data on actors' ethnicities is imperative. The [CMU dataset](https://www.cs.cmu.edu/~ark/personas/) offers ethnicities in the form of Freebase IDs. To translate these IDs into actual ethnicities, we utilize a mapping system. Acknowledging the scarcity of ethnicity information for many actors, we try to bridge gaps by extracting data from various [Wikipedia](https://en.wikipedia.org/wiki/Main_Page) pages, including [List of African-American actors](https://en.wikipedia.org/wiki/List_of_African-American_actors), [List of Hispanic and Latino American actors](https://en.wikipedia.org/wiki/List_of_Hispanic_and_Latino_American_actors), and [List of Italian-American actors](https://en.wikipedia.org/wiki/List_of_Italian-American_actors). Despite these efforts to mitigate missing data, a significant portion remains incomplete.


However, the prevalence of missing values should not impede our exploration of ethnicities. Operating under the assumption that these gaps occur randomly, akin to a randomized control experiment, we can reasonably exclude them as confounding factors that might influence our analysis outcomes. This perspective empowers us to proceed with our study on ethnic representation in cinema, acknowledging and addressing the challenges posed by missing data.

Moreover, the Freebase IDs correspond to 263 different ethnicity names. To streamline and focus our analysis, we employ a mapping system to categorize these 263 ethnicities into six distinct groups : Africans, Arabs, Asians, Europeans, Hispanics, and Natives.


Moving on, let us examine the number of actors per ethnicity in the data we have.

{% include Ethnicity_Distribution.html %}

As we can see, after missing ehtnicities, european actors are dominating the number of actors of a certain ethnicity


# Remarks

Limitation: we know that other more subtle factors could be taken into account to improve the accuracy of the analysis, like social media influence of the actor, and (CITE OTHER FACTORS).

PUT INTERACTIVE PLOTS

PUT INTERACTIVE LIST WITH RANKED ACTORS (WHERE YOU CAN SCROLL AND FIND A SPECIFIC ACTOR NAME)
https://www.convertcsv.com/csv-to-html.htm
