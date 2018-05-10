---
layout: post
title:      "Rails Portfolio Project - Socially Organized"
date:       2018-05-10 04:38:04 +0000
permalink:  rails_portfolio_project_-_socially_organized
---


I set out to finish my Rails project weeks ago and I struggled from the beginning.  As I was going through the lessons I understood what I was learning, but it became apparent that building my app from scratch was going to take a TON more digging in. In digging in is exactly what I've been doing the past few weeks.

When I initially was brain storming ideas for my project I reflected back on my previous projects. My CLI was just a "for fun" app that dealt with scraping a horoscope page. My Sinatra project was a "consumer" type app for creating a database for local restaurants. I wanted my Flatiron projects to be all encompassing, and to expand my skills on what people may be looking for in different areas of their life.

I decided to build an app called Socially Organized.  The bud to fruition stemmed from a struggle I was having at my regular job.  I had recently taken on a marketing position for a guy I work with.  I had to plan out his entire marketing calendar for a 2 year time frame, and then create templates and populate the CRM with campaigns.  As I sat at the office churning out a calendar on a simple excel sheet, I was frustrated building it out and thought, I wish I had an app for this.  I wanted an app not only for planning his marketing campaigns (which in a sense is a calendar), but also all the social media marketing we may do throughout the year.  

I have this issue where when I want to do something, I have to do it. It may be considered a negative, or a positive. In this case, it was simply an upward hill learning experience.  I knew exactly what I wanted and would not deviate from it, regardless of the many join tables it required.  Wrapping my brain around the relationships and getting the code to work the way I envisioned was sometimes painful. BUT I did it! I wanted to finish this 2 weeks ago, but because I'm stubborn and have to do, what I have to do, it took me a bit longer than expected.

So here goes....

Users has_many Posts... Posts belong_to User -- easy 
Users has_many Calendars.  Calendars has_many Users -- creating a join table with through association
Calendars has_many Posts. Posts has_many calendars --another join table fun!.... Also with the user subittable attributes.
Posts has_many Platforms --uh oh it continues
Platforms has_many Posts --the final join table relationship

## Why so many join tables?
In the real world, if you are working for a marketing company and on different teams, you may be working with different colleagues on different brands, etc. I felt it was essential to set up my app with this has_many to has_many relationship to offer that functionality.  I also felt like it was important to give the user the opportunity to assign a post to many calendars and platforms as they chose. This is highly likely if a person is posting content on different social media platforms. It is also likely if you are running email marketing campaigns.  In my real life example, I was setting up campaigns for Referral Partners we work with where we rate their relationship by how close they are and how many "touches" we want them to get per year. A's get them ever 10 days, B's get them every 20, C's get them every 45 and so on through D getting something quarterly. All the campaigns are going to get the same emails, the spacing of time is just different.  I felt like this is probably a commonality across many business and sales structures.

## Real Struggles
My thoughts when planning out my app - 
* How do my models work together
* Am I going to start messing with time and timezone, the craziness they call UTC and the adjustments ?
* What authorization and authentication do I want to utilize?
* Scope? What a what? What is the best concept to scope down in my model?
* Best user submittable attribute idea?
* Where do I want partials?
* Where do I want more thorough information?

The list goes on...

## Setting Up The App
1. First I ran `rails new socially_organized` from my console. Then I created my repo on github and went to connect my local app with the repo.  I had some issues with this because when I went to add the app the code snippet did not show up. So with a quick google I knew I needed to connect the local repo with the upstream repo. Something wasnt working though. I kept getting errors that I coudln't push my app to github. After adding and deleting repos multiple times, it worked.  One thing I've learned from creating an app on my new local Linux system is that it is quirky! I literally ran the same code multiple times, because I knew it was the right code per several recomendations on google and stackoverflow, and it eventually took? Why? I have no idea why it didn't take in the first place. I attribute that to quirky Linux.

I added my .gitignore and found a very useful site: https://www.gitignore.io/ that provides tons of information based on the machine or language you choose. 

2. Next it was time to generate all my models, build the associations, add then bootstrap and other gem dependencies I knew I needed. 

3. Once I got my associations all linked up the way I needed them I started writing "generic" code for all the CRUD functions.  I like to do this so it gives me a foundation to start playing with and build off of.

4. I added Devise with Facebook omniauth... BIG mistake. Facebook has change a lot because of everything going on with the app privacy and settings right now. HTTPS is required for Facebook Omniauth and so you have to use the gem Thin. For some reason I never had a problem with Thin during the Omniauth lab, but for whatever reason while building my app it kept throwing me weird errors. No matter where I googled, nothing came up. The issues other people had encountered were not like what I was experiencing. I had followed the directions in setup, and stupidly did not verify everything was ok. I figured everything would be good to go with Thin because I had used it before on the lab, wrong.  Devise tutorial on Github was an easy setup with following the directions. There are so many people who use Devise and tons of amazing resources out there. A favorite resource I have come cross several times during this project is [RichOnRails.com](http://richonrails.com) ! That site is a wealth of information if you are stuck at any point in Devise or Omniauth setup.

5. Now that I had everything linked behind the scenes I needed to set up my routes so that I can see what is actually going on visually.  I created my basic resources and then decided what I wanted to be nested, and what I didn't need at all. 

6. Routes done, controllers done with basic methods, models done, time to work on views.  I knew from the start that my basic new and update forms would be partials. That was an easy first step.  Working through the more complex forms with nested attributes, custom setter/getter methods, strong params and much more were where the complexity came in.  One major take away from setting up the forms was that placement is EVERYTHING. If you have a div just outside of your form vs. the line below a form_for you are going to have issues. My submit button didn't work for over a day on one of my forms and finally with a second pair of eyes Dakota pointed that out. I never would have even thought of it but now that I know these things I'm constantly on the lookout for those "little things" that are not so little.

7. Having the basic app set up, it's time to focus on all the things that break the code... and there are so many.  I think I said every day, multiple times, for over a week, "I think I'm on my final 3 issues". It wasn't until last night at 1 am (or this morning), that i was like... I think I may actually almost be within my 3 issues, for real. Searching for typos, routing issues, and the final issue last night at 1 am was Omniauthath with Facebook.... That was an ouch. I had been coding since 1 pm, trying to work through Facebook issues... I was emotional, tired, worn out, and felt beat down because I coudn't get it to work.  I even paused and cried at my kitchen table for a good 5 minutes and then decided it was time to shut it down and start fresh with new eyes in the morning.  This morning I woke up super early before work and started at it again. I decided to switch Facebook over to Github... WIN! I had a few initial errors but figured it out. The main issue I had was due to a very weird situation. Somehow my computer created a second User folder. I had one for my facebook omniauth (which was hidden for some reason), and the one I was trying to use for Github.  I couldn't see the folder for Users/OmniauthController that had my Facebook code in it but in my repo on Github it existed. After opened through my folder directory on my actual computer, not on Atom, I deleted the extra folder and everything worked as planned.  SO If you are going to pick an omniauth provider ... GO WITH GITHUB!!  Piece of cake... Cake walk... Walk in the park... whatever route you want to go, Github is the least stressful route.  When doing your setup, make sure to put your key and secret in a .env file, or something else hidden. 

8. Now that everything was working, and all my spec.md boxes were checked off I went through the functionality to verify everything was ok.  I removed excess code that I didn't use. I added more logic and authorizations to user actions based on their role. I added some checks and stop points for errors and reroutes.

My app definitely does not look the way I want it to look. Building it was a doozy, and I decided that done was better than "perfect". This was EXTREMELY hard for me to accept but after several weeks on this project I needed to move on.  Knowing that the next project builds on this was the one saving grace because I knew I would continue to make this better. I am so excited about starting Javascript and JQuery and adding even more awesome functionality to my app!

Do you want to get Socially Organized?  Looking for testers once I update with API in my next project!  Contact me on Slack: Allit

8.




