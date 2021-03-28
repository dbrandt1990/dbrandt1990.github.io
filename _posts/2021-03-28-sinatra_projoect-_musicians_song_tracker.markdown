---
layout: post
title:      "Sinatra projoect- Musician's Song Tracker"
date:       2021-03-28 10:52:47 -0400
permalink:  sinatra_projoect-_musicians_song_tracker
---

For this project a really wanted to make something that I would actually use. Both me and my partner play music and 
over the years I have found that it is very difficult for me to remember songs we have learned, what songs we are working on. I don't know how many times I learn a song in its entirety, only to stop practicing it for a month and then forget how to play it. Enter the Musician's Song Tracker app! 

With this applicantion, my aim was to help organize content to assist the user in managing songs that they had learned and songs that they are in the process of learning, as well as store content, such as tabs, lyrics, notes and a video to assist in learning or practicing a particular song.

Building this application went fairly smooth for me, and I attribute that to two things, pre-planning, and reusing code. Leading up to this project many of the labs were working on validation Active Record relationships, and sessions. Being able to look back and copy some of that code and file structure made it much easier to get the ball rolling. The pre-planning came much more naturally this time around. I felt confident in what I was designing and was able to relate the plan to my coding structure, ie. describing routes, models, and schema. This kept me on track when building the structure for the project. Setting clear MVP functionality and creating some bouns features also helped me to stay focused on my main goals and not drift off into the extra features abbys.

I had my plan and now it was time to start writing the code. First off, it was a bit intimidating for me to stare at an empty workspace, where should I start?! This is where some review of helped. I first built my file structure as shown by the diagram on the project page, then I went back to some of the other labs in this section and made sure I had the right gems in my gemfile and the right environment and config setups. Phew, that part was the most stressful of the whole build! Now it was time to get after it, create the DB, build some tables, make those models, perfect the schema. After a few migrations, I was up and running and ready to start the views. Again some labs were helpful here. I had some forms already build, some examples of Active Record validation, as well as some baseline templates for my CRUD actions! At this point, I felt like a real programmer! But I ran into a small snag. I wanted my videos to be embedded on the song show page and the URL was not sufficient to display that. So the user would need instructions to go in and grab the embed link on youtube and paste that into the form, not ideal. I wanted to solve this and immediately thought Regex! and then I looked at the embed URL compared to the watch URL... and my brain melted. I decided id take a shot in the dark and see if someone has already solved this problem, and BINGO!


	def youtube_embed(youtube_url)
          if youtube_url[/youtu\.be\/([^\?]*)/]
            youtube_id = $1
          else
            # Regex from # http://stackoverflow.com/questions/3452546/javascript-regex-how-to-get-youtube-video-id-from-url/4811367#4811367
            youtube_url[/^.*((v\/)|(embed\/)|(watch\?))\??v?=?([^\&\?]*).*/]
            youtube_id = $5
          end
          %Q{<iframe title="YouTube video player" width="640" height="390" src="http://www.youtube.com/embed/#{ youtube_id }" frameborder="0" allowfullscreen></iframe>}
        end 
				
My problem was solved in just a few minutes with this great Regex! The moral of the story here is, always check if someone else has solved the problem first! Now I was cooking with gas. I needed to make sure the songs that were created were displayed cleanly, and that the functionality for marking songs learned or not, and then organizing them based on this was there. I ran into a bit of a silly hiccup here. I had chosen to use a check box for the attribute of 'learned' for a given sone. The plan was that if the checkbox was click then the song was learned and if not then the user was still learning it. I was getting stuck on figuring out what value was returned when the box was checked vs unchecked. I did some searching and tried using true/false, and then 1 and 0, but nothing was working, so I decided to take a break and come back with a fresh brain. When I came back it was obvious! Just use a pry and see for yourself what it returns! 🤦‍Well... it returns "on".  That took longer than it needed to but I felt good that it was figured out and I was almost done with just a little bit of testing left to do.

In conclusion, when coding, plan it out, use old code, and ALWAYS see if someone else has solved the problem already! 

