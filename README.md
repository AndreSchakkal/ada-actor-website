In the enthralling world of cinema 🎥, actors play a pivotal role, shaping and being shaped by the ever-evolving tapestry of human history. Embark with us on a cinematic journey through time as we explore actor’s recognition and their evolving representation in the world of cinema across history. Has an actor's recognition and its longevity been influenced by specific attributes such as genre, ethnicity? Acting isn't an isolated art form but rather intricately connected to the tapestry of human existence, always influenced and shaped by historical events. Our objective is to decode the impact of pivotal historical events, such as the Civil Rights and Feminist Movements, on the composition of actors in terms of gender and ethnicity. This project invites you on a cinematic journey delving into the life of actors who have graced the Cinema screens, examining how they have been portrayed, known and represented over time.

[RESOURCES](example.md)

**EXPLAIN MORE IN DETAIL THE PLAN OF WHAT WE ARE DOING**

**PUT ALL USED DATASETS IN ANOTHER PAGE WITH THEIR EXPLANATION, REFER TO THIS PAGE HERE**

**A LOT OF MISSING DATA FOR EARLY YEARS THIS CAN AFFECT THE ANALYSIS**

**RESEARCH QUESTIONS?**

# Actor’s Recognition

Ever found yourself caught up in those spirited debates about which actor is the most globally recognized? Well, here's our attempt to bring some clarity to those lively discussions by quantifying an actor's recognition and exploring how it evolves over time. Let's take you behind the scenes of our recognition assessment.

Let's start walking you through how we do that. In our analysis, we assert that an actor's recognition is contingent on the revenue, quality, and popularity of the movies they star in, as well as their relative importance in these films. A highly recognized actor tends to feature predominantly in high-revenue, popular movies, often in significant roles. Conversely, a less recognized actor is likely to have a career characterized by lesser-known movies, lower revenues, and less popularity. 

We account for movie revenue using box office figures. These box office figures are normalized with yearly inflation rates to ensure a consistent monetary scale for comparison. The formula for this normalization is:

$$Normalized \_ Revenue (year,movie) = \frac{Revenue(movie)}{Cumulative \_ Inflation(year)}$$

Here, $$Cumulative \_ Inflation(year) = \prod_{i=1914}^{year} \left(1 + Inflation_i \right)$$, where $$Inflation_i$$ is the inflation rate for the $$i$$-th year.

Additionally, to gauge quality and popularity, we utilize IMDb ratings, which is a metric not just for cinematic quality but also a gauge of audience favor, as these ratings emanate from amateur movie lovers rather than professional critics. To have the Box-office and ratings on a comparable scale, we normalize them and scale them on a scale going from 0 to 1. 

To create a recognition coefficient ($$RC$$) for assessing an actor's recognition, we first introduce the concept of a a movie coefficient ($$MC$$) which is the average of the normalized movie rating and box office revenue scores:

$$MC(year,movie) = \frac{Normalized \_ Revenue(year,movie) + Normalized \_ Rating(year,movie)}{2}$$

Here, $$Normalized \_ Revenue(year, movie)$$ and $$Normalized \_ Rating(year, movie)$$ represent the normalized and scaled rating and box office revenue scores, respectively.

Considering that an actor's importance in a movie varies, we introduce an importance coefficient ($$IC$$) estimated by analyzing the plot summary and counting the actor's mentions. This coefficient is then used to calculate an actor's movie recognition coefficient ($$RC_{movie}$$) as follows:

$$RC_{movie}(actor, year, movie) = MC(year, movie) \times (1 + IC(actor, year, movie))$$

This coefficient ($$RC_{movie}$$) captures an actor's recognition in a specific year and movie

To assess an actor's overall recognition in a given year, we aggregate the movie recognition coefficients using the formula:

$$RC_{year}(actor,year) = \frac{1}{n(actor)} \sum_{i=1}^{n(actor)} RC_{movie}(actor,year,{movie}_i)$$

In this equation, $$n(actor)$$ represents the total number of movies in which the actor participated during the specific year.

Recognizing that an actor may maintain a certain level of recognition even in years with no movie releases, we incorporate a momentum effect. The yearly recognition coefficient is updated with a fraction ($$C=0.9$$) of the actor's previous year's recognition coefficient:

$$\overline{RC_{year}}(actor,year) = RC_{year}(actor,year) + C *\overline{RC_{year}}(actor,year-1)$$

It is important to note that we initialize the momentum term, $$\overline{RC_{year}}(actor, 0)$$, to zero.

Finally, to obtain an actor's overall recognition coefficient, we aggregate the yearly recognition coefficients with momentum over a span of years:

$$RC_{overall}(actor) = \frac{1}{Y} \sum_{i=1}^{Y} \overline{RC_{year}}(actor,{year}_i)$$

Here, $$Y$$ represents the total number of years considered in the analysis. This comprehensive approach provides a nuanced understanding of an actor's recognition, accounting for both individual movie performances and the temporal evolution of their career.


## Analysis of Actors' Recognition
Now that we have defined the coefficients, let's dive into the analysis of Actors' Recognition. First, we explore the mean magnitude of recognition each year, as depicted in the following plot:

{% include recognition_plot.html %}

Conducting a Pearson test on this aggregated data yields a p-value of $$10^{-31} < < 0.05$$. This strong evidence allows us to reject the null hypothesis, suggesting a correlation between the year and the Average Recognition Coefficient. Consequently, the plot supports the idea that the average "Magnitude of Recognition" of actors increases over time, indicating a rise in movie revenue and ratings. This suggests that actors become more widely recognized, signifying the growing impact of cinema on society.

Examining the graph, it's apparent that there is a significant change in the way the average recognition coefficient increases post-1970.

To validate this suspicion, a Chow test is performed, examining if the coefficients in two regression models on different data regions are equal. The obtained p-value is $$<0.05$$, leading us to reject the null hypothesis. This supports the assertion that a structural break point exists in the data, indicating a surge in actor recognition post-1970.
Consequently, we conclude that starting from 1970, actors experience even greater recognition, signaling a booming period for cinema.

This surge in recognition post-1970 can be attributed to two pivotal historical factors:

- The Blockbuster Phenomenon (Jaws, 1975): Directed by Steven Spielberg, "Jaws" is often hailed as the first blockbuster film, revolutionizing film distribution and marketing. The subsequent release of "Star Wars" in 1977, directed by George Lucas, further transformed the science fiction genre and became a cultural phenomenon, setting new standards for the movie industry and its merchandising.
- Invention of VHS (1976): The introduction of VHS (Video Home System) in 1976 allowed audiences to watch films at home, reshaping the industry's distribution model and making cinema more accessible to a wider audience.

<p align="center">
  <img src="images/STAR_WARS.jpg" width="600" alt="Image 1">
  <img src="images/JAWS.jpg" width="220" alt="Image 2">
</p>
<p align="center">
  <img src="images/VHS.png" width="400" alt="Image 1">
</p>


In the meantime we see also some decrease, which is likely attributable to the data not being as up-to-date.

Having explored the evolution of Actor Recognition over the years, let's now dive into the more thrilling aspect: evaluating the overall recognition of actors. The following list presents actors ranked from the most recognized to the least recognized. Take a moment to find your favorite actor and discover their rank. As a small game, consider all the actors you know and try to identify the less known ones in this list!



{% include Actor_table.html %}


We hope you've spotted your favorite actors among this list 😀.

 
This table offers a snapshot of the most recognized actors, ordered by their General Recognition Coefficients. Notably, the rankings feature a mix of contemporary figures like Robert De Niro and iconic actors from earlier periods, such as John Wayne and Sean Connery. Unfortunately, but not surprisingly, the representation of female actors in the rankings is minimal, underscoring the enduring dominance of well-known male actors. This ranking serves as a testament to the timeless influence of actors, encompassing both modern-day stars and those from cinematic history.

Next, armed with this list of actors, let's visualize the distribution of only the top 10% most well-recognized actors. Are modern-day actors more prevalent among this elite 10%?

{% include well_recognized_actors_plot.html %}

As anticipated, we observe that the majority of actors in this top 10% are from modern times. Once again, we note the final decrease, likely due to the data not being very up-to-date in the most recent years until 2012. Additionally, the sudden increase in the number of actors post-1970 aligns with the previously explained reasons.

# Actor Recognition Longevity

Shifting to a more longitudinal perspective on Actors' Recognition, let's examine how this recognition lasts over time. The goal is to explore the span of actors' recognition through different periods. Specifically, we aim to identify the years when an actor began to be well-recognized and when this recognition "ended". This involves selecting the range of years where the Actor Yearly Recognition Coefficient exceeds a designated threshold. This threshold is set at 50% of the actor's highest recognition coefficient, providing a concise measure of the actor's sustained recognition over time. The plot below illustrates the average span of recognition through the years.

{% include average_span_recognition_plot.html %}

We observe that actors starting to be well-recognized after 1970 have decreasingly small spans of recognition. This is attributed to the data ending in 2012, implying that these actors likely continued their careers post-2012, but corresponding data is unavailable. Hence, the Last Year of Recognition for these actors is considered around 2012, as depicted in the following histogram.

{% include last_year_recognition_histogram.html %}

To evaluate the correlation between the average recognition span and the first year of recognition, we use only the data before 1970, as the decrease in recognition span after 1970 is not reflective of the reality. Therefore, we fit a linear regression on spans starting before 1970.

{% include fitted_average_span_recognition_plot.html %}

Based on the above graph and a Pearson test (yielding a p-value $$<0.05$$), we observe a trend of an increase in the average span of recognition for actors before 1970. This result suggests that, over time, actors tend to enjoy longer periods of recognition. This could be attributed to various factors such as improvements in health and later retirements.

## Recognition coefficient of specific actors
As an interesting step, we can also inspect the evolution of the recognition coefficient of different actors:

{% include specific_actors.html %}

From the graphs above, let's inspect the evolution of the recognition coefficient for different actors:

- Michael Caine: The recognition coefficient for Michael Caine exhibits a remarkable longevity, starting to be well-recognized around 1960 and continuing beyond 2012. Notably, there is a dip in recognition during the 1990-2000 period, possibly linked to his involvement in less successful movies during that time. However, his recognition rebounds in subsequent years.
- John Wayne: The second plot featuring John Wayne provides a unique perspective as it visualizes the recognition of an actor who ceased to be well-recognized. We witness a sharp decline in his recognition coefficient after 1979, aligning with the year of his death.

Now, it's your turn! Explore the plot showcasing the evolution of the recognition of your favorite actor. Try the following interesting example:

**INTERESTING EXAMPLES**

{% include Actor_recognition_graph.html %}

**HOVER ON ACTOR NAME TO KNOW HIS STORY**

**SCANDALS**
**DEATH**
**BLOCKBUSTERS**
**PREGRANCIES**


# Gender representation in Cinema over time

To start our analysis, let's examine the proportion of female and male actors over time.


{% include male_female_proportion.html %}

As evident from the chart, the proportion of male actors is significantly higher, almost double that of female actors throughout the years. However, are there discernible trends that have evolved over time? Have major historical events, such as the Feminist Movement, influenced the representation of females in cinema?

## Impact of the Feminist movement on female representation in Cinema
The second wave feminist movement, prominent in the 1960s and 1970s, advocated for gender equality and reproductive rights. It gained momentum in the early 1960s, notably sparked by the publication of Betty Friedan's "The Feminine Mystique" in 1963. Its influence gradually decreased by the early 1980s. The Feminist movement had a profound impact on decreasing gender-based discrimination, exemplified by the Equal Pay Act of 1963 and Title IX of 1972—an Education Amendment prohibiting gender-based discrimination in educational programs and activities.

In this section, we aim to explore the impact of this movement on female representation in cinema and observe the evolution of female representation during and after this period. This analysis can provide insights into societal shifts and progress made toward gender parity in cinema. We divide the data into three segments for analysis:

- Before the Feminist Movement (1914-1963): Examining the early years leading up to the Feminist Movement.
- During the Feminist Movement (1963-1980): Analyzing the period when the movement was at its peak.
- After the Feminist Movement (1980-2012): Investigating the years following the peak of the movement.
- 
Following this, we fit a regression line to the proportion of female actors for each of these periods.
{% include female_actors.html %}

We observe a decrease in female representation between 1914 and 1963 and an increase in female representation between 1980 and 2012. The very small p-value (p−value$$<0.05$$) associated with the regression line after the feminist movement indicate a significant correlation between the dates after the feminist movement and the observed increase. On the other hand, during the feminist movement, the p-value exceeds 0.05, suggesting no substantial correlation during this period.

Conducting a Chow test on the proportion of female actors during and after the feminist movement yields a p−value $$<0.05$$. This result leads us to reject the null hypothesis, providing compelling evidence of a structural break point between the periods during and after the feminist movement.

Moving beyond overall trends, we shift our focus to the top 10% most well-recognized actors to ascertain if the trends among this subset mirror those of the entire female actor population. The plot below illustrates the proportion of female actors among the 10% most recognized actors over time:

{% include female_actors_10perc.html %}

The plot suggests a consistent increase in the proportion of female actors among well-known actors, independent of the feminist movement. A subsequent Chow test on the proportion of well-known female actors during and after the feminist movement yields a p−value>0.05. Consequently, we lack sufficient evidence to suggest any structural breakpoint in this subset.

In summary, while the proportion of female actors among all females increases, likely due to the feminist movement, the proportion of female actors among well-known actors follows a distinct pattern, steadily rising over time independent of the feminist movement.


## Distribution of Recognition among genders
To assess the distribution of overall recognition coefficients among female and male actors, we've compiled histograms illustrating the recognition coefficients for each gender:

{% include male_female_recognition.html %}

While the number of female and male actors differs, there are apparent similarities in the trends. To compare the recognition distributions, density functions for each gender are plotted. The integral of the density function from 0 to a given value represents the probability of having a recognition coefficient below that value, i.e. for each density, $$\int_{0}^{x} f(t) dt$$ represents the probability to have a recognition coefficient below $$x$$.

**OR CCDF**

{% include recognition_densities.html %}

From the density plot above, it's evident that the density peak for female actors is higher, indicating a greater likelihood of having lower recognition coefficients, especially below 0.04. This suggests that a larger proportion of female actors tend to have lower recognition amplitudes compared to their male counterparts. In essence, there are more male actors with higher recognition amplitudes.

To assess the statistical significance of these differences, we conduct a Kolmogorov–Smirnov test. The test yielded a p-value less than 0.05, providing sufficient evidence to reject the null hypothesis. This result indicates that the two density distributions (for male and female actors) are not sampled from the same distribution. In simpler terms, there is a statistically significant difference between the recognition coefficient distributions for male and female actors.

## Actor first-appearance among genders

Another intriguing facet to explore is the debut age of actors and whether there is a significant difference in the age at which male and female actors commence their careers. To investigate this, we present a histogram visualizing the distribution of ages at which actors make their first appearances.

{% include 1st_appearance_hist.html %}

The histogram suggests a noticeable difference in the debut ages of male and female actors. Specifically, it indicates that female actors tend to start their careers at an earlier age compared to their male counterparts. This observation is further supported by a t-test, which yields an extremely small p-value (p−value<<0.05). This compelling result provides strong evidence to assert a significant difference between the mean first-appearance ages for female and male actors.

The subsequent plot highlights this difference, showing a mean first appearance age of 24.2 years for female actors and 29.0 years for male actors:

{% include 1st_appearance_ci.html %}

# Ethnic representation in Cinema over time

Among the significant repercussions of the Feminist movement was the enactment of the Civil Rights Act of 1964, a groundbreaking law designed to combat discrimination based on gender, race, color, religion, or national origin. Simultaneously, the Civil Rights movement, advocating for racial equality, played an instrumental role in the realization of this transformative Act. Spanning from 1954 to 1968 in the United States, the civil rights movement stood as a nonviolent social campaign, striving to eradicate legalized racial segregation, discrimination, and disenfranchisement. 

This historical context lays the foundation for the second part of our exploration into the dynamic representation of diverse ethnicities in cinema. Our objective is to trace the evolution of ethnic representation over time, with a specific emphasis on examining the impact of movements like the Civil Rights Movement on the portrayal of black actors in the film industry.

To delve into this investigation, comprehensive data on actors' ethnicities is imperative. The [CMU dataset](https://www.cs.cmu.edu/~ark/personas/) offers ethnicities in the form of Freebase IDs. To translate these IDs into actual ethnicities, we utilize a mapping system. Acknowledging the scarcity of ethnicity information for many actors, we try to bridge gaps by extracting data from various [Wikipedia](https://en.wikipedia.org/wiki/Main_Page) pages, including [List of African-American actors](https://en.wikipedia.org/wiki/List_of_African-American_actors), [List of Hispanic and Latino American actors](https://en.wikipedia.org/wiki/List_of_Hispanic_and_Latino_American_actors), and [List of Italian-American actors](https://en.wikipedia.org/wiki/List_of_Italian-American_actors). Despite these efforts to mitigate missing data, a significant portion remains incomplete.


However, the prevalence of missing values should not impede our exploration of ethnicities. Operating under the assumption that these gaps occur randomly, akin to a randomized control experiment, we can reasonably exclude them as confounding factors that might influence our analysis outcomes. This perspective empowers us to proceed with our study on ethnic representation in cinema, acknowledging and addressing the challenges posed by missing data.

Moreover, the Freebase IDs correspond to 263 different ethnicity names. To streamline and focus our analysis, we employ a mapping system to categorize these 263 ethnicities into six distinct groups based on ancestral origin: Africans, Arabs, Asians, Europeans, Hispanics, and Natives.


Moving on, let us examine the number of actors per ethnicity in the data we have.

{% include Ethnicity_Distribution.html %}

As we can see, with the exception of missing ethnicity entries, European actors significantly outnumber actors from other ethnicities. Here, European actors encompass individuals of European descent, including both native European actors and American actors of European descent.

Let's now examine how the number of actors from the three most represented ethnicities varies over time.

{% include total_actors_ethnicity.html %}

{% include actors_ethnicity.html %}

Since we are interested in the representation of African actors in Cinema, let us take a look at the third plot. Similar to the other plots, we observe a consistent increase in the number of African actors over time. However, a notable surge in their representation around 1970 catches our attention, and this sudden uptick may be attributed to the influence of the Civil Rights Movement, which started in 1954 and ended in 1968.

It's essential to note that the total number of actors, regardless of ethnicity, also shows a continuous increase over time. Consequently, the sudden spike in the number of African actors could be a byproduct of this overall rise. To eliminate the potential bias from the increasing number of actors, we pivot our analysis to examine the proportion of actors from each ethnicity rather than their count. This shift allows us to better understand the impact of the Civil Rights Movement on the representation of African actors in cinema.


{% include actors_ethnicity_proportion.html %}


In contrast to the count plots, where we observed a consistent increase in the number of actors for all ethnicities, the proportion plots reveal intriguing patterns. Specifically, for African actors, a distinctive pattern emerges, showcasing a discernible decrease in their proportion until around 1970, coinciding with the sudden increase that aligns with the Civil Rights Movement.

To substantiate the hypothesis of a significant increase in the proportion of African-American actors, we apply linear regression to analyze the proportion of African-American actors during three distinct time intervals:

- Before the Civil Rights Movement (Before 1954)
- During the Civil Rights Movement (After 1954 and before 1968)
- After the Civil Rights Movement (After 1968)

{% include african_actors_perc.html %}


From the analysis presented in the plot above, several key insights emerge. Before the Civil Rights Movement, there is a discernible decrease in the proportion of African actors. During the Civil Rights Movement, there is a transition period characterized by a nearly-horizontal trend.

Crucially, after the end of the Civil Rights Movement, a distinct and significant increase in the proportion of African actors becomes apparent. It is noteworthy that the Pearson Coefficient, specifically calculated for values after the Civil Rights Movement, indicates a statistically significant correlation, with a p-value less than 0.05.

Furthermore, a substantial increase is observed from the intercept of the regression line during the Civil Rights Movement to the intercept of the regression line after the Civil Rights Movement. This difference is highlighted at the extremities of the interval, where there is an approximate 5% increase on the different regression lines when transitioning from the last point during the Civil Rights Movement (year=1968) to the first point after the Civil Rights Movement (year=1969). This statistical evidence supports the proposition of a noteworthy and statistically significant rise in the proportion of African actors in cinema following the Civil Rights Movement.


The bar plot below illustrates the evolution of the proportion of different ethnicities in 10-year intervals. In addition to the already observed increase in African actors, there is a notable surge in the proportion of Asian actors over time. Native actors also show a relative increase in their representation, and even for Arab actors, a modest uptick is noticeable. All these trends are juxtaposed against the proportion of European actors, indicating a transformative shift in world cinema towards greater inclusivity. This evolution reflects a positive trajectory, embracing actors with diverse ethnic backgrounds and contributing to a more representative and inclusive landscape in the realm of cinema.

{% include Ethnicities_Over_Decades.html %}

## Ethnicities of most-recognized actors

Building upon our previous analysis, let's delve into the ethnicities of the top 10% most recognized actors.

{% include ethnicity_10perc_hist.html %}

While European actors still dominate among the most recognized, with the exception of missing ethnicity entries, a noteworthy shift emerges. African actors now claim the second spot, signaling a growing presence among the top 10% most recognized actors.


Examining the distribution of the top 10% most recognized actors across ethnicities over the years provides further insights.

{% include recognized_Ethnicities_Over_Decades.html %}

As we can see, similarly to the previous plot, in early years European actors are the most present among the 10%-most recognized actors, i.e. the majority of the most recognized actors are European actors. However, with time, we see am increase in the proportion of actors of other ethnicities. In other words, the number of actors of other ethnicities among this elite 10% is increasing and it starts to be more common to have well-known actors of ethnicities different than European. Specifically, we can also see that following the Civil Rights movement (after 1970), the proportion of African actors among the most recognized is considerably increasing. Furthermore, it is interesting to note that the proportion of the European actors among the 10% most recognized actors goes from 77.8% in the first decade available to 51.4% in the last available decade, a considerable decrease of 26.4% highlighting the positive shift of public opinion for well-known actors towards a more inclusive opinion, blabla.


As we can see, similarly to the previous plot, in the early years, European actors overwhelmingly dominated the top 10% most recognized actors. Put simply, the majority of the most recognized actors were of European descent. However, over time, a transformative trend unfolds, showing an important increase in the proportion of actors from diverse ethnicities. In essence, the exclusive club of the most recognized actors is becoming more inclusive. It's becoming increasingly common to find well-known actors representing ethnicities beyond the European spectrum.

Specifically, we notice that Post-Civil Rights movement (after 1970), the proportion of African actors among the most recognized experiences a substantial increase. Furthermore, a particularly interesting facet is the diminishing proportion of European actors among the top 10% most recognized. This proportion shrinks from a commanding 77.8% in the earliest available decade to a more balanced 51.4% in the latest available decade. This significant decrease of 26.4% underscores a positive evolution in public opinion. The shift reflects a growing acceptance and appreciation for well-known actors of diverse ethnicities, marking a positive step towards a more inclusive and representative entertainment industry.

# Remarks 

Limitation: we know that other more subtle factors could be taken into account to improve the accuracy of the analysis, like social media influence of the actor, and (CITE OTHER FACTORS).

PUT INTERACTIVE PLOTS

PUT INTERACTIVE LIST WITH RANKED ACTORS (WHERE YOU CAN SCROLL AND FIND A SPECIFIC ACTOR NAME)
https://www.convertcsv.com/csv-to-html.htm
