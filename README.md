# Actors Representation: Actor’s Recognition, Gender and Ethnicity throughout history and time 📆
In the enthralling world of cinema 🎥, actors play a pivotal role, shaping and being shaped by the ever-evolving tapestry of human history. Embark with us on a cinematic journey through time as we explore actor’s recognition and their evolving representation in the world of cinema across history. Has an actor's recognition and its longevity been influenced by specific attributes such as genre, ethnicity? Acting isn't an isolated art form but rather intricately connected to the tapestry of human existence, always influenced and shaped by historical events. Our objective is to decode the impact of pivotal historical events, such as the Civil Rights and Feminist Movements, on the composition of actors in terms of gender and ethnicity. This project invites you on a cinematic journey delving into the life of actors who have graced the Cinema screens, examining how they have been portrayed, known and represented over time.

EXPLAIN MORE IN DETAIL THE PLAN OF WHAT WE ARE DOING

PUT ALL USED DATASETS

We've all certainly always got into debates like: "No! This actor is more worldwide recognized than this one!" or things like: "I don't agree, I think this actor is the most known ever!" We've come to help! To mitigate any doubt, the idea would be to quantify an Actor's Recognition and study its evolution. Let's start walking you through how we do that. In our analysis, we consider that an Actor's recognition depends on the revenue, quality and popularity of the movies the corresponding Actor acts in. Indeed, if an Actor is very well-known, he would be majoritarly acting in movies of high revenue and high popularity. On the other hand, a not-so recognized Actor would be in the major part of his career in movies that are not very well-known, i.e. that do not have very high revenues and that are not very popular. To account for movie revenue we use the movie Box-office while adapting its value with yearly inflation rates to have the same monetary scale for comparison. Furthermore to account for quality and popularity, we use IMDb ratings, IMDb rating would not only qantify the cinematic quality of a movie but also its popularity, since IMDb rating are done by "normal movie lovers" (CHANGE) and not by professional critics. To have the Box-office and ratings on a comparable scale, we normalize them and scale them on a scale going from 0 to 1. What is necessary now is that we define a recognition coefficient ($RC$)  to asses the recognition of an actor. Let us explain how we define it.
We start by defining a movie recognition coefficient, which represents the recognition coefficient of an actor in a specific year in a specific movie:
$$RC_{movie}(actor,year,movie) = \frac{Normalized\_Revenue(actor,year,movie) + Normalized\_Rating(actor,year,movie)}{2}$$
Where:
- $Recognition(actor,year,movie)$ is the actor's recognition coefficient in a specific year in a specific movie.
- $Normalized_Revenue(actor,year,movie)$ is the normalized movie's rating score.
- $Normalized_Rating(actor,year,movie)$ is the normalized movie's box office revenue score.

We aggregate this coefficient to find a yearly recognition coefficient, which represents an actor's recognition coefficient in a specific year.:
$$  RC_{year}(actor,year) = \frac{1}{n(actor)} \sum_{i=1}^{n(actor)} Recognition(actor,year,{movie}_i) $$
Where:
- $Recognition(actor,year,{movie}_i)$ represents the Recognition Coefficient for the i-th movie that actor has played in a specific year.
- $ n(actor)$ is the total number of movies the actor has participated in during a specific year.

$$dd$$



Limitation: we know that other more subtle factors could be taken into account to improve the accuracy of the analysis, like social media influence of the actor, and (CITE OTHER FACTORS).

PUT INTERACTIVE PLOTS

PUT INTERACTIVE LIST WITH RANKED ACTORS (WHERE YOU CAN SCROLL AND FIND A SPECIFIC ACTOR NAME)
https://www.convertcsv.com/csv-to-html.htm

{% include Actor_table.html %}
 
