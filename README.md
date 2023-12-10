# Actors Representation: Actor’s Recognition, Gender and Ethnicity throughout history and time 📆
In the enthralling world of cinema 🎥, actors play a pivotal role, shaping and being shaped by the ever-evolving tapestry of human history. Embark with us on a cinematic journey through time as we explore actor’s recognition and their evolving representation in the world of cinema across history. Has an actor's recognition and its longevity been influenced by specific attributes such as genre, ethnicity? Acting isn't an isolated art form but rather intricately connected to the tapestry of human existence, always influenced and shaped by historical events. Our objective is to decode the impact of pivotal historical events, such as the Civil Rights and Feminist Movements, on the composition of actors in terms of gender and ethnicity. This project invites you on a cinematic journey delving into the life of actors who have graced the Cinema screens, examining how they have been portrayed, known and represented over time.

EXPLAIN MORE IN DETAIL THE PLAN OF WHAT WE ARE DOING

PUT ALL USED DATASETS

We've all certainly always got into debates like: "No! This actor is more worldwide recognized than this one!" or things like: "I don't agree, I think this actor is the most known ever!" We've come to help! To mitigate any doubt, the idea would be to quantify an Actor's Recognition and study its evolution. Let's start walking you through how we do that. In our analysis, we consider that an Actor's recognition depends on the revenue, quality and popularity of the movies the corresponding Actor acts in. Indeed, if an Actor is very well-known, he would be majoritarly acting in movies of high revenue and high popularity. On the other hand, a not-so recognized Actor would be in the major part of his career in movies that are not very well-known, i.e. that do not have very high revenues and that are not very popular.


Revenue Box-office
Popularity IMDb rating, IMDb rating would not only qantify the cinematic quality of a movie but also its popularity, since IMDb rating are done by "normal movie lovers" (CHANGE) and not by professional critics.

Limitation: we know that other more subtle factors could be taken into account to improve the accuracy of the analysis, like social media influence of the actor, and (CITE OTHER FACTORS).

PUT INTERACTIVE PLOTS

PUT INTERACTIVE LIST WITH RANKED ACTORS (WHERE YOU CAN SCROLL AND FIND A SPECIFIC ACTOR NAME)

This is a list of ranked actors. ![f](https://github.com/AndreSchakkal/ada-actor-website/blob/master/index.html)

<head>
    <meta charset="utf-8">
    <meta content="width=device-width, initial-scale=1, shrink-to-fit=no" name="viewport">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <title>CSV to HTML Table</title>
    <meta name="author" content="Derek Eder">
    <meta content="Display any CSV file as a searchable, filterable, pretty HTML table">

    <!-- Bootstrap core CSS -->
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.2.1/css/bootstrap.min.css" integrity="sha384-GJzZqFGwb1QTTN6wy59ffF1BuGJpLSa9DkKMp0DgiMDm4iYMj70gZWKYbI706tWS"
        crossorigin="anonymous">
    <link rel="stylesheet" href="https://cdn.datatables.net/1.10.19/css/dataTables.bootstrap4.min.css">
</head>

<body>
    <div class="container-fluid">
        <main class="row">
            <div class="col">
                <h1>CSV to HTML Table</h1>

                <p>Display any CSV file as a searchable, filterable, pretty HTML table. Done in 100% JavaScript. <a
                        href="https://github.com/derekeder/csv-to-html-table">Code
                        on GitHub</a>.</p>

                <p> Here's a table of Health Clinics from the <a href="https://data.cityofchicago.org/browse?q=health%20clinic&sortBy=relevance&utf8=%E2%9C%93">City
                        of Chicago Data Portal</a>.
                </p>

                <div id="table-container"></div>
            </div>
        </main>
        <footer class="row">
            <div class="col">
                <hr>
                <p class="text-right"><a href="https://github.com/derekeder/csv-to-html-table">CSV to HTML Table</a> by
                    <a href="http://derekeder.com">Derek
                        Eder</a></p>
            </div>
        </footer>
    </div>
    <script src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/twitter-bootstrap/4.2.1/js/bootstrap.bundle.min.js"></script>
    <script src="js/jquery.csv.min.js"></script>
    <script src="https://cdn.datatables.net/1.10.19/js/jquery.dataTables.min.js"></script>
    <script src="https://cdn.datatables.net/1.10.19/js/dataTables.bootstrap4.min.js"></script>
    <script src="js/csv_to_html_table.js"></script>

    <script>
        function format_link(link) {
            if (link)
                return "<a href='" + link + "' target='_blank'>" + link + "</a>";
            else return "";
        }

        CsvToHtmlTable.init({
            csv_path: "data/general_recognition.csv",
            element: "table-container",
            allow_download: true,
            csv_options: {
                separator: ",",
                delimiter: '"'
            },
            datatables_options: {
                paging: false
            },
            custom_formatting: [
                [4, format_link]
            ]
        });
    </script>
</body>

</html>

