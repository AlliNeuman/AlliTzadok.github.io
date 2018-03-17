---
layout: post
title:      "Local Restaurant Sinatra App"
date:       2018-03-17 06:02:54 +0000
permalink:  local_restaurant_sinatra_app
---


This project is a doozy but it was fun and seriously challenging.  Long before I got to the project I was already thinking of an idea that I had wanted to do for as long as I can remember.

Years ago I started adding restaurants to a spreadsheet for all local restaurants in St Louis. I added the address and area of town plus notes about what to get there or if it was a romantic place, divebar, etc etc. What started off as a list of about 50 places I wanted to go turned into a list of over 300 restaurants with lots of details. It has since been shared with tons of my friends and they have shared with theirs. I meet people and they sometimes are like, "Oh you're the restaurant spreadsheet girl!"  So I thought it was perfect for an application!

I started this project last Monday and was working to figure out how to break things down.  I was a little overwhelmed but created my folder setup and started thinking about what capabilities I wanted and got even more overwhelmed.  Dalia gave me really great advice, along with a student who is already on jS.  They told me to start simple, work on foundation and go from there. So I did.

My project is the restaurant application. A user can create restaurants, edit them and pseudo delete them (I'll go into that more later). User has_many restaurants and restaurant belongs to user. I started there and built that up. I built my CRUD functions like normal, with a normal delete and then my project evolved from there.

I wanted to add a function where a user can bookmark another users restaurants. That added the restaurant has_many users and a user has_many restaurants which brought in the join table associations.  Since it was an actual function I wanted to name it as the function really was to differentiate between what was going on.  Naming it a Bookmark gave users that functionality. To take it up another notch, to relate it back to something I do on my spreadsheet of restaurants, I wanted to have the functionality on the Bookmarks for the user to say if they visited the restaurant or not.  All restaurants that are created are auto bookmarked to the creators home page, along with all the other bookmarks they add along the way.


##The Grit of Scope and Alias

So part of my comprehension issues stemed from the fact that I had Users and Restaurants being used for different purposes. I had difficulty wrapping my brain around what was going where so I aliased them for the purpose of the "creation" aspects. The user is a creator and then they have created_restaurants. Keeping those concepts separate helped me to work through the layers of complexity.

As for the scope aspect.. When I added the bookmark functionality, I didn't want a user to be able to bookmark something twice. I thought that was counterintuitive. I need a hard check to make sure that didn't happen. I added the ActiveRecord requirement to check for uniqueness on the Bookmark model for username. When I did that, I had been messing around with my database deleting and re-seeding things to see what happened. I noticed that only the first bookmark was pulling through for each user so I needed to dig deeper and apply a setting that would only apply that for the restaurant_id which was tied to my join table. 

##Rack Flash vs Sinatra Flash

So here's another thing that may make you hit your head against the wall... Rack Flash.  We had used that in previous projects and getting it to function was more than a mind could handle, even on the hardest days of code I've had yet.  I read the documentation on it and I placed the erb code above the layout like it says.  Because I'm a little over the top, I wanted to make the website as responsive as I could. That being said, the top margin was getting in the way of where the messages were printing and I couldn't seem to cycle through the right messages.  Everyone told me to go with Sinatra Flash but I felt the documentation was poor. I tried a few different ways to change the erb code on the layout page and couldn't get it to work. FInally today I was tagged in a post on slack which saved the day in that respect. 

So for anyone trying to use Sinatra Flash... Here is the erb code that I couldn't find until someone provided it on slack.
```
      <div class="flash-message">
      <% if !!flash[:message] %>
        <%= flash[:message] %>
        <% end %>

      </div>
```

##Road Blocks and Overcoming the Obstacles

To say I had road blocks and obstacles is an understatement.  I worked endless hours on this project for 10 days straight. I felt kind of helpless in the beginning and I can say without question that my hurdles made me so much stronger, made me think more than I literally ever have, and I was able to push through and figure out difficult code issues that I hadn't encountered before.  Don't get me wrong, I had some help too along the way. When my eyes were bugging out at 3 am, burning when I woke up every morning to only return to the computer to go at it again.  Every day I was determined to make that day the last day for this project.  And then today came. I was sure that I only had minor tweaks today. Little did I know I had all these tiny bugs and errors that I hadn't combed through to see. I had debugged countless time, on screenshares with coaches who told me I was doing great. We worked through many issues and I had come a long way with the project. But sometimes, the errors that occur or bugs are the weird little things that are difficult to notice. Here is a list of some of my errors that were a difficult catch but found with either a second set of eyes helping me or after taking a 5 minute break to walk my dog.. or even after I lay in bed at 4 am trying to fall asleep as I still think about code and how I'm going to make it work.....

* CSS
1. When building a responsive layout I recommend starting from the smallest model and up. I have found it is easier to resize items that way.
2. When styling your layouts, the outer-most div is very helpful, especially in responsive layouts. I made sure to style in percentages to make the flow from small size and up an easier process.
3. ALWAYS make sure to check if your personal browser is zoomed in or out.  I spent about 2 hours on my own time wondering why my page looked messed up. I got on with a tech coach for a 30 minute session and we spent that entire time going through the code.  At the very last second I randomly did my ctrl + and realized my screen was 45% zoomed out. When I zoomed in, all was well... I only wasted over 2 hours of my time and a 1:1 session that could have been better spent.
4. The code that's like... [col-* ] something like that... When I had that in my code it royally messed it up.  I played around with my code with a coach for a very long time trying to debug and find where the issue could be. We tried literally everything, moving divs, removing classes and ids to finally see that removing that styling fixed the issues.

* Helper Methods
1. Helper methods are great but to an extent.  I had added in a bunch and certain thinsg were getting too vague. It's good to see what's actually going on in your code sometimes. 
2. I did my helper methods in my ApplicationController class. I've seen them in modules extended to models and in the controller. The downside that I found in doing them in the controller is that I couldn't use them in the model. I had to pass them through as params instead; not a huge deal, just something to remember.

* Functionality and Layers of Complexity
1. So I started off small and added little by little. Once I built onto my initial project I realized some things I needed that I initially did not think of. Learning how to think like a programmer and what is needed for the logic to work in real world applications is something I hadn't thought about much before this week. Thinking about how and what I could do to implement things and the importance of the checks on certain things, other validations that impeded other assignments, how things interact etc.
2. One functionality I hadn't thought about was the fact that I wouldn't actually want a user to be able to delete a record from the database. They could edit it but not delete. Why not? If you were a user for a restaurant app and had bookmarked all these restaurants you wanted to go to and then all of a sudden someone removed their account or deleted their restaurants just because, you would lose all your data. Instead, I added the functionality that when the user deleted the restaurant, it only really removed them as the creator of that restaurant and set the creator alias to nil. One error I found in this process was I had set it up and then I saw restaurants I had deleted in my bookmarked section. I have since changed all that code because I added another layer of complexity with the visited restaurant vs not visited restaurant.
3. One thing I love about my app is the multi functional pages that have a variety of forms on them based on what your situation is. One example is on my restaurant show page I have 3 different forms. 1 form when the current user was the creator and could edit or delete their restaurant. The second form is visible when the person is not the creator but has bookmarked the restaurant, they can then edit or delete the bookmark. The third option is when the user isn't the creator and hasn't bookmarked the restaurant yet so they have that option. 
4. One problem I came across was with my radio buttons and what happened when I tried to edit them. Nothing was updating correctly.  I spent about 4 hours tonight working on it with not much luck.  The error was that I had my values set as words while they should have just been true or false because my table had the column as a boolean.  I was trying to style them as true and false instead of just putting them in the input as that value. Definitely something I won't forget next time!

All in all, I am so happy with my project.  I think I have some more styling to do but everything is fully functioning. I can add, edit, delete my bookmarks. I can add, edit and orphan restaurants.  I have learned a lot in the 2.5 months I have been doing Flatiron, but the amount I have learned in the past 10 days with this project is actually more than everything combined.  I learned how to actually program and do more critical thinking than I have before.

Huge shout out to all the people who worked through different processes with me. To the coaches I worked with Dakota, Bob, Tyler, Griffin, Nick.. you guys were great sorry if I missed anyone.. I know I can be a little over the top sometimes so thanks for your patience.  Huge thanks to Travis and Donnadieu. I swear these two guys should be hire by Flatiron when they are done. We worked on screenshares and their ability to ask me questions to get me to think about things in a different light is really great. 

Biggest thanks to my learning coach Mollie who is seriously awesome. She told me weeks ago when I started Sinatra to look ahead and start thinking about what I wanted to do for my project. I took her advice and did just that. I am so happy I did because as I was going through the lessons I was thinking ahead for my project.  I feel like I was much better off once I got to the final project stage than I would have been if she hadn't given me such great advice.

Learn. Love. Code... My husband says after thse 10 days I'm officially in the matrix.



