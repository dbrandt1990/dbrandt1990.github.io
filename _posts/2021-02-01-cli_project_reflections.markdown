---
layout: post
title:      "CLI project reflections"
date:       2021-02-01 23:07:45 +0000
permalink:  cli_project_reflections
---


Turns out, objects are a big part of object-oriented programing. I think they do a good job making code read like 'things' rather than just processes. It makes the code feel more relatable to me. The relationships you can create between objects open up a myriad of options to build larger infrastructures that really make sense syntactically! These objects also allow for different levels of encapsulation, through class and instance variables. This is pretty powerful stuff!


So for my CLI project, I had a hard time not going overboard with things. The project called for; gathering data online using scraping techniques or an API, building objects with that data, displaying those objects via the command-line interface, and finally offering the user to move at least one layer deeper into the object's data.

I am a big fan of board games and thought it would be fun to create a way to find and list the most popular board games and give the user some more information on a game they choose. My first idea was to scrape the BoardGameGeek(BGG) as it seems to be the golden standard for boardgame rankings, but they were not so keen on being scraped, so I found an API called BoardGameAtlas that worked great. They have so many stats on these board games consolidated into an array of game objects. Most of the games had image links and rule book pdfs, as well as stats for how many times the game has been mentioned on Reddit! I thought, these were great, and a little overwhelming. 

So for my project I took this info and listed the games by rank, name, year published, number of players, playtime, and minimum age. I wanted to display the games in order of rank, allow the user to choose one of the games from the list, and display its information. From the game's specific info the user is prompted to get 'more', which returns a rule book link and game description. 


When I started to build this application I  thought that it needed more functionality, something cooler than just pulling up a list. So I built a separate filter menu that would allow games to be filtered by any of the attributes they display. This was a lot of back and forth to get it up and running. The main issue that I ran into was not defining the filter in my mind as a separate list. When the filter was applied to the normal games list, you could see the games that met the parameters of the filter, but you couldn't select the game from that list.... it defaulted back to the original list and gave you a game from there. this was because the menu method I built had no access to the filter method and vice versa. I opted out of using the filter or my final build because the solution I came up with, though it worked, compromised the readability of the code, and was outside of the requirements for this project. I figured it would be better to have a clean solution that did what was asked of it, instead of an app with a bunch of messy bells and whistles that weren't even asked for.

If I did it again, I would definitely separate the methods to display the menu and interact with the menu. I could have a filter menu display, and a standard menu display and both would be affected by the same menu interaction method. I believe this is getting into the Model View Controller concept. Overall I was happy with what I built, and as always there is plenty of room to grow!
