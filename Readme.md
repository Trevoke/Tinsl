#Tinsl

###Fantasy baseball, but for movies.
**login**: guest@guest.com

**password**: password

*go nuts!*

![Tinsl Screenshot](/screenshots/TinslScreenshot.gif)

Everyone loves movies.  Tinsl is an addictive game that allows you to become a bigtime movie producer.  See if you can cast a movie that grosses in the the top ten movies of all time.  After registering for an account and logging in you can create a movie.  You get to write your own title or have the app come up with one for you (these are hilarious), then write a tagline.  Next you get to cast your movie.  Search for Hollywood's top actors and actresses and see who'd available. Once you're finished with the casting process, click on "what's the bottom line" to see the total gross of your movie and how it stacks up with the classics.  Not satisfied?  Click on "make unreasonable demands" to fire and hire actors, earn more money, and beat out previous hits.


##Under the hood

The soul of the app is the database of movies and actors.  Automatically getting the grosses of the top movies through an API is impossible (most likely for legal reasons).  So I scraped a list of the top 200 movies of all time and their inflation-adjusted grosses from http://www.boxofficemojo.com/alltime/adjusted.htm.  I used the app at https://www.kimonolabs.com/ and some search-and-replacing to generate a list of movies and grosses in the following format:

	 [
	...
	 {
      title: {
        text: "The Twilight Saga: Breaking Dawn - Part 2",
        href: "http://www.boxofficemojo.com/movies/?id=breakingdawn2.htm"
      },
      gross: "$289,056,500"
    },
    {
      title: {
        text: "The Love Bug",
        href: "http://www.boxofficemojo.com/movies/?id=lovebug.htm"
      },
      gross: "$287,367,200"
    },
    {
      title: {
        text: "The Twilight Saga: Breaking Dawn - Part 1",
        href: "http://www.boxofficemojo.com/movies/?id=breakingdawn.htm"
      },
      gross: "$285,867,000"
    },
    ...
    ]

Then I passed each movie title to the API at http://www.omdbapi.com/ to get a list of actors for each movie.  The app calculates a value for each actor based on the grosses of films they have been in, and stores it in the actors table.

In addition to Box Office Mojo and OMDB, I used and API at https://www.wordnik.com/ to generate the automatic movie titles, and one at http://www.themoviedb.org/ to get images of the actors.  Everytime a new actor image is acquired I store in in the actors table to avoid having to make multiple API calls for the same image.)

