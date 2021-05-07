---
layout: post
title:      "Rails Project "
date:       2021-05-06 14:13:29 -0400
permalink:  rails_project
---


This project held the most weight for me thus far. Not only was it putting all of my skills to the test, building a full-stack web application from scratch, but also carried an opportunity. A client of mine, who works as a rails developer, said the company will have an opening for a new dev soon and sent me their API with some project ideas. What a great opportunity! I felt so motivated to get my project going, so I jumped right in.

The API has info for all of the alternative fuel stations in the US and Canada. Initially, I was going to do an admin dashboard/data management app, but after looking at the project requirements I realized that wouldn't work. I started to think in terms of a basic user profile model, like a blog. I thought that if I could give the user info relevant to their area that I could make that model work. I decided to build user profiles that would have the ability to filter the stations by zip code,  save stations to their profile, and add notes to stations that all users could see. I then added a search feature that I had hoped could allow the users to search by state, but the amount of data returned was too much to handle so I stuck with searching by zip code. Finally, I needed to give the user the ability to create a new object. 

Considering that the information in the app is coming from an API of real fuel stations, I was unsure of what the users could create without it being arbitrary. Then it hit me. Wouldn't it be great if these users could put their residential address into the database as a station!? My thought was similar to Air BnB, people could post their station to be found and used by travelers. There are a lot of other moving pieces to this to make it a working feature, but for now, I have just allowed the user to create the station and marked it as flagged; the idea being that an admin could then review and verify the address and do any of the necessary onboarding before updating the API with the address and making it available for public use. 
This all came together as I worked through the project, but I must say that the preparation I did before writing any code was very helpful. I built diagrams for my models, views, and controllers, and even though they changed throughout the project, it felt fantastic to go into writing code with solid ideas and a plan from start to finish.

> "The only way to make sense out of change is to plunge into it, move with it, and join the dance."
> -Alan Watts

The biggest headaches came from managing the API and database as separate entities, and Omniauth. I needed the user to have a populated table of stations after they signed up, but those stations should not be associated with that user yet (the user would be able to choose what they wanted to be saved to their profile). The stations are gathered by the zip code set by the user upon signing up. If the zip code exists in my database then we should grab them from there, if not we should query the API and create the stations and add them to the database. 

`def self.create_station_objects(zip, method)
        #ONLY make api call if user and DB don't have station already
        if Station.find_by(zip: zip).nil?
            method.each do |station|
                ApiController.create_station(station)
            end 
            stations = Station.where(zip: zip)
        #add station from DB if user doesn't have
        else 
            stations = Station.where(zip: zip)
        end
        stations
    end`
		
Simple enough now that it is done, but getting there took some trial and error. Omniauth on the other hand was a bear for different reasons. I had an issue getting it to work initially, but didn't worry about it because I was going to use the Devise gem and the Oauth implementation is a bit different. Once I had Devise working, I ran into similar problems with Omniauth, getting 

`request.env['omiauth.auth']`

to return anything but nil was maddneing. I worked and worked to find a solution, and then ended up in a study group where the consensus was to drop Devise, and implement Omniauth on its own. So I tried, and still got the same errors. After many StackOverflow 'fixes', trying several Oauth providers, and starting a whole new application I was at a loss. Luckily there was another study group. The instructor walked through it with me and dissected the Omniauth control flow. What we came to was that the URL that was used for the link to sign in with a third party was incorrect

`<%= button_to "Login with GitHub", omniauth_path('github')%>`

after changing it so that it was not referencing my own route, pointing to my own controller everything worked great

`<%= button_to "Login with GitHub", '/auth/github' %>`


![](https://media.giphy.com/media/d3YHKs8wwYfce0PS/giphy.gif)

The moral of the story here is, look at what you know before looking at things you don't. If I would have looked at the control flow of omniauth and all of the code that I wrote and knew what it was supposed to do I may have run across this, but since I thought I had it all correct I looked eslwhere. I got into config stuff and enviroment things, modifying permissions and bypassing crsf protections, I had no clue what I was doing, I was just trying anything I could. I do understand routes.... I should have looked at those first. I hope this helps someone avoid this pitfall I ran inot. 

In conclusion this project felt like the real thing. It held some extra weight becuase of the interview opportunity, and the challange of implementing the API, but I enjoyed the process and know, with all of the doing and redoing I will be better next time.

![](https://media.giphy.com/media/WUHo4B8DsFny1PPzC6/giphy.gif)
		
