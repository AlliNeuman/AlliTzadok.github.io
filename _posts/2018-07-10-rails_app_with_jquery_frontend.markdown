---
layout: post
title:      "Rails App with jQuery Frontend"
date:       2018-07-10 19:45:34 +0000
permalink:  rails_app_with_jquery_frontend
---

Socially Organized is a social media marketing app for planning social media posts. There is added functionality for adding team members to calendars and scheduling posts to specific team or brand calendars once you are ready.  The app is something I have needed in my current job and I wanted to create an app for functionality that I thought would help me, and potentially help others.  It could be used in marketing companies for different brands or teams, it could be used by individuals for building their own brand on social media, or collaboration for small teams.  It is diverse and can fit a variety of needs.

Buliding the jQuery frontend for Socially Organized was something I had outlined with my initial ideas of creating the app.  I had several features I wanted to add and this API project gave me the opportunity to add some additional functionality to the dashboard view. 

I swapped out links for button features for the user to be able to view the calendar index, create a new calendar, post index and create a new post.  I have on click functions that are loaded on document load, and secondary functions that are add on submit and secondary clicks once the jQuery loads the elements in the page. 

I initially wrote code for my listeners to be on my user.js and call functions in each the calendar.js and post.js.  I didn't like the way the code was. I had so many different functions and I wanted to have my listeners tied in specifically for each js file.  I refactored the code so that each appropriate listener was in it's own .js file and within a bindlistener function.  Prior to refactoring all my functions worked the way I had intended.  As you may know, when you refactor code your elements and data objects may end up changing so I started running into bugs.  Going back through debugging each line and piecing the functions together the way javascript jumps around, made the debugging process a huge learning experience.  I am glad I refactored my code because I hadn't come to the realization before that those data elements change once you change your code into different functions. That was a big learning experience for me.

Another big piece of the project is differentiating your backend issues that arise, from the frontend issues.  I had a 404 issue and I was thinking it had to be within my controller, but it was actually a matter of something being retrieved incorrectly in the frontend. 

Initially my code was using all es5 functions.  I had watched several videos throughout the past week and when I refactored I decided to switch to es6 functions.  What I wasn't 100% sure about was when regular functions are needed vs. arrow functions.  I had an issue with this where my scope was incorrect because I was using an arrow function within my callback.  My ${this} was calling on the window instead of the data object I was trying to retrieve information from.  Through delving in deeper I came to understand that if you need your ${this} inside your function to look up to the next level then you would use the arrow, otherwise you would use a normal function.

All in all, I am pretty happy with my progress on this project.  I was consumed when I started it and I feel accomplished with the mental progress I've made through the process of creating it.  Check back at my app for additional features I will be adding!
