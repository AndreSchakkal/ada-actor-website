# Actors Representation: Actor’s Recognition, Gender and Ethnicity throughout history and time 📆
In the enthralling world of cinema 🎥, actors play a pivotal role, shaping and being shaped by the ever-evolving tapestry of human history. Embark with us on a cinematic journey through time as we explore actor’s recognition and their evolving representation in the world of cinema across history. Has an actor's recognition and its longevity been influenced by specific attributes such as genre, ethnicity? Acting isn't an isolated art form but rather intricately connected to the tapestry of human existence, always influenced and shaped by historical events. Our objective is to decode the impact of pivotal historical events, such as the Civil Rights and Feminist Movements, on the composition of actors in terms of gender and ethnicity. This project invites you on a cinematic journey delving into the life of actors who have graced the Cinema screens, examining how they have been portrayed, known and represented over time.

EXPLAIN MORE IN DETAIL THE PLAN OF WHAT WE ARE DOING

PUT ALL USED DATASETS

We've all certainly always got into debates like: "No! This actor is more worldwide recognized than this one!" or things like: "I don't agree, I think this actor is the most known ever!" We've come to help! To mitigate any doubt, the idea would be to quantify an Actor's Recognition and study its evolution. Let's start walking you through how we do that. In our analysis, we consider that an Actor's recognition depends on the revenue, quality and popularity of the movies the corresponding Actor acts in. Indeed, if an Actor is very well-known, he would be majoritarly acting in movies of high revenue and high popularity. On the other hand, a not-so recognized Actor would be in the major part of his career in movies that are not very well-known, i.e. that do not have very high revenues and that are not very popular. To account for movie revenue we use the movie Box-office while adapting its value with yearly inflation rates to have the same monetary scale for comparison. Furthermore to account for quality and popularity, we use IMDb ratings, IMDb rating would not only qantify the cinematic quality of a movie but also its popularity, since IMDb rating are done by "normal movie lovers" (CHANGE) and not by professional critics. To have the Box-office and ratings on a comparable scale, we normalize them and scale them on a scale going from 0 to 1. What is necessary now is that we define a recognition coefficient ($RC$)  to asses the recognition of an actor. Let us explain how we define it.
We start by defining a movie recognition coefficient, which represents the recognition coefficient of an actor in a specific year in a specific movie:
$$RC_{movie}(actor,year,movie) = \frac{Normalized \textunderscore Revenue(actor,year,movie) + Normalized \textunderscore Rating(actor,year,movie)}{2}$$
Where:
- $Recognition(actor,year,movie)$ is the actor's recognition coefficient in a specific year in a specific movie.
- $Normalized \textunderscore Revenue(actor,year,movie)$ is the normalized movie's rating score.
- $Normalized \textunderscore Rating(actor,year,movie)$ is the normalized movie's box office revenue score.

We aggregate this coefficient to find a yearly recognition coefficient, which represents an actor's recognition coefficient in a specific year:

$$RC_{year}(actor,year) = \frac{1}{n(actor)} \sum_{i=1}^{n(actor)} RC_{movie}(actor,year,{movie}_i)$$

Where:
- $Recognition(actor,year,{movie}_i)$ represents the Recognition Coefficient for the i-th movie that actor has played in a specific year.
- $ n(actor)$ is the total number of movies the actor has participated in during a specific year.

Since even if a certain actor does not play in any movie in a certain year, an actor would remain well-recognized to a certain extent during this year. To account for this effect, we add a certain fraction of the actor past year's Recognition Coefficient to the the current year's Recognition Coefficient.

We update the yearly Recognition Coefficient with momentum with the following formula:

$$  \overline{RC_{year}}(actor,year) = RC_{year}(actor,year) + C *\overline{RC_{year}}(actor,year-1) $$

Where:
- $C$ is the previous year contribution, here we use $C=0.9$

Finally, in order to have an overall recognition coefficient for each actor, we aggregate the yearly Recognition Coefficient with momentum in the following way:

$$RC_{overall}(actor) = \frac{1}{Y} \sum_{i=1}^{Y} \overline{RC_{year}}(actor,{year}_i)$$
Where:
- $Y$ is the total number of years.




In our methodology for assessing an actor's recognition over time, we introduce the concept of a movie recognition coefficient ($RC_{movie}$). This coefficient captures an actor's recognition in a specific year and movie, calculated as the average of the normalized movie rating and box office revenue scores:
$$RC_{movie}(actor,year,movie) = \frac{Normalized \textunderscore Revenue(actor,year,movie) + Normalized \textunderscore Rating(actor,year,movie)}{2}$$
Here, $Normalized_Revenue(actor, year, movie)$ and $Normalized_Rating(actor, year, movie)$ represent the normalized rating and box office revenue scores, respectively.

To gauge an actor's overall recognition in a given year, we aggregate the movie recognition coefficients using the formula:

$$RC_{year}(actor,year) = \frac{1}{n(actor)} \sum_{i=1}^{n(actor)} RC_{movie}(actor,year,{movie}_i)$$

In this equation, $n(actor)$ represents the total number of movies in which the actor participated during the specific year.



Recognizing that an actor may maintain a certain level of recognition even in years with no movie releases, we incorporate a momentum effect. The yearly recognition coefficient is updated with a fraction ($C=0.9$) of the actor's previous year's recognition coefficient:

$$  \overline{RC_{year}}(actor,year) = RC_{year}(actor,year) + C *\overline{RC_{year}}(actor,year-1) $$

Finally, to obtain an actor's overall recognition coefficient, we aggregate the yearly recognition coefficients with momentum over a span of years:

$$RC_{overall}(actor) = \frac{1}{Y} \sum_{i=1}^{Y} \overline{RC_{year}}(actor,{year}_i)$$
Here, $Y$ represents the total number of years considered in the analysis. This comprehensive approach provides a nuanced understanding of an actor's recognition, accounting for both individual movie performances and the temporal evolution of their career.







Limitation: we know that other more subtle factors could be taken into account to improve the accuracy of the analysis, like social media influence of the actor, and (CITE OTHER FACTORS).

PUT INTERACTIVE PLOTS

PUT INTERACTIVE LIST WITH RANKED ACTORS (WHERE YOU CAN SCROLL AND FIND A SPECIFIC ACTOR NAME)
https://www.convertcsv.com/csv-to-html.htm

{% include Actor_table.html %}
 
