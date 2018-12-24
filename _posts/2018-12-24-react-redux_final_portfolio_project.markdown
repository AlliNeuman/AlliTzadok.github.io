---
layout: post
title:      "React-Redux Final Portfolio Project"
date:       2018-12-24 06:34:54 +0000
permalink:  react-redux_final_portfolio_project
---

## YOM
#### The childcare expense tracker for all your childcare expenses that are excluded from child support payments

### Preface
Whenever I am building an app I am always trying to think => 
* What do I need in my life?
* What would someone else benefit from?
* Is there anything I could build to streamline a process in my current job?
* What is an idea that would bridge a gap and just make life a little more simple?

Going into this project I went through a variety of app ideas.  Since it was my final project and I knew I would be looking for a new job soon I thought it would be a good idea to build an app that my boss could use. That way when I had to tell him I was leaving I could gift him something great and he would still love me.  Take one was starting to build an app to streamline a process that I do at work. I know he is going to have to train someone else and I thought it would make his life easier when it came down to that training process down the road.  Building an app for an industry specific idea is pretty difficult.  I tried conceptualizing how I would build the app and discussing it with other people, I couldn't explain the complexities of it well enough for anyone else to wrap their mind around.

Then I decided to make a recipe app because I am an avid cook and I thought it could be useful.  My mom is also a professional chef and puts all her recipes on index cards and files them away. What better way to help my mom out than create an app that she can store her entire recipe database, search for recipes and have easy access from her computer or ipad once the app was hosted? Yeah, but then I looked around and recipe apps are pretty common.  I don't know about you, but I don't shoot for the common ideas.

Finally I landed on my app idea that was not only something I needed personally, but it was something that I felt like other people in my position may need as well.  During my time going through Flatiron, I was working full time, doing Flatiron, spending every day at the hospital with my sick grandma and also going through a divorce.  My life was extremely stressful and I honestly find it amazing that I am finally at the finish line.  I felt like I was crushing the program a first and then my life exploded infront of my eyes. 

Now that my divorce is final and I am off on my own taking care of my daughter, so many other areas of my life are put into perspective.  One thing that was driving me bananas was keeping track of all my daughters expenses that fell outside of what is included in child support. That being, extra curricular stuff like sports, music, art... and then school, medical, dental. All the things that are not daily necessities, the big items that as a single mom, I really needed to track diligently in order to be reimbursed for half.  There also are restrictions by law, for when and how you request reimbursement so I felt like an app that kept track of all my expenses would be very helpful and keep me organized. 

Enter YOM - the childcare expense tracker that helps you to not lose your mind when you ask your ex over and over for reimbursement and you forget what you've been paid and what you haven't. This has been my real life mental saver, for sure.

### Creating Rails API
I did this so long ago so I cannot go into all the specific details for the hurdles I had on the API end.  I feel like I am a rockstar at rails so I did not have too many issues.  To generate the rails API, enter in terminal: `rails new my-api --api` where my-api is whatever you want your app name to be.  I also set up my database with postgresql.  I had heard using postgresql, it made it easier to deploy to Heroku so I felt like it would make my life easier on the backend and I would learn some new documentation as well.

### Generating Controllers
I generated my controllers with the rails generator `rails g controller expenses --no-test-framework` and `rails g controller category --no-test-framework`.  I also generated a welcome controller the same way in order to render the one html page we needed to connect the react app front end to.

### Generating Models
I generated my models with the `rails g model expense`  and `rails g model category` creating my tables for my database and then migrating the data with each column attribute.  

### Creating Routes
I connected my routes with resources for anything I felt I would potentially build down the road. And routed my root to my Welcome controller that rendered my home.html.erb page that met my html requirement.

### Updating Gemfile
I added and removed some gems from my gemfile:
`
gem 'rails', '~> 5.2.1'

gem 'pg', '>= 0.18', '< 2.0'

gem 'puma', '~> 3.11'

gem 'sass-rails', '~> 5.0'

gem 'uglifier', '>= 1.3.0'

gem 'turbolinks', '~> 5'

gem 'jbuilder', '~> 2.5'

gem 'active_model_serializers'

gem 'jquery-rails'

gem 'rack-cors', require: 'rack/cors'

gem 'bootsnap', '>= 1.1.0', require: false

group :development, :test do

  gem 'byebug', platforms: [:mri, :mingw, :x64_mingw]
  gem 'pry'
  gem 'pry-remote'
  gem 'rspec-rails', '~> 3.5'
end

group :development do

  gem 'web-console', '>= 3.3.0'
  gem 'listen', '>= 3.0.5', '< 3.2'

  gem 'spring'
  gem 'spring-watcher-listen', '~> 2.0.0'
end

group :test do

  gem 'capybara', '>= 2.15'
  gem 'selenium-webdriver'

  gem 'chromedriver-helper'
end


gem 'tzinfo-data', platforms: [:mingw, :mswin, :x64_mingw, :jruby]
`

The main one of importance to note was active_model_serializers.  When I was building this app it had been so long since I did that unit and I forgot all about using the generator to build the serializer, and adding in the gem.  So When I got to the front end, I was seeing errors about my serializers not existing.  I was looking at my files and saying, yes they exist, yes I have the code right.... But I hadn't used the generator or added the gem.  I deleted my .rb files and started those over again and everything worked out fixing that error.

### Adding Controller Methods
Then it was time to add all my CRUD methods to the controllers. 

Some key things to note: 
I ran into issues on my front end when I was submitting my data from `http://localhost:3001` because my backend did not know where the info was coming from.  I looked all over and found that I needed to add the `cors gem` and add some additional coding to get back end to accept my code.  Main changes happened in my controller and then the cors_initializer.

In my application controller I added this line of code: `  protect_from_forgery unless: -> {request.format.json?}`  and then cors.rb in my initializers folder looked like this:
`Rails.application.config.middleware.insert_before 0, Rack::Cors, :debug => true, :logger => ( -> { Rails.logger }) do
  allow do
    origins '*'

    resource '*',
      headers: :any,
      methods: [:get, :post, :put, :patch, :delete, :options, :head]
  end
end`

This allowed my front end to send my data to the backend, accepted the headers and all json data that was being sent back.  I got this information from the rack-cors documentation on github. https://github.com/cyu/rack-cors

One thing note as well is to make sure what params you are accepting in your backend.  The params have to be exactly what you are sending back in your create methods on the react side.  At the beginning I was getting state and attributes confused.  I was thinking I could name state anything I wanted, and when I created the new instances on the frontend, that it would be accepted.  What I realized was that because I have expenses that belong to categories, even though I had everything linked up correctly on the back end, and I had an input field for category, I needed to be passing back my category.id because that was the data point in the backend.  I can say with absolute certainty that I sat staring at my screen debugging, shaking my head, saying why is categoryid null, why is everything passing back but not the category when I cleary am.  Moving throug the obstacles I encountered definitely made me more inquisitive and helped me to better understand the dataflow of how the backend and frontend talk to each other.

## Creating the Front End 
Enter `create-react-app client`.   I followed the official documentation on github: https://github.com/facebook/create-react-app

I knew I needed my `src` file, and then in there I was going to need `actions` `components` `containers` `reducers`.  When you generate the create-react-app a lot of things are automatically created.  

### Setting Up Store 
With the recent React update there are some issues with setting up the store. From all the previous code I had seen for labs, or online I kept seeing the documentation showing: `const store = createStore(
  rootReducer,
  window.__REDUX_DEVTOOLS_EXTENSION__ &&
  window.__REDUX_DEVTOOLS_EXTENSION__(),
  applyMiddleware(thunk)
);`

This did not work though.  I was having an error because you cannot have more than 2 argments inside of the createStore function anymore.  I read a lot about this issue because it was a recent issue that was very prevalent on the internet.  The solution to this was to change the code around and add additional parts from redux. I additionally imported `{ compose }` from redux...  and setting up the rest of my store looked like this.. which is found in recent documentation updates: 
`const composeEnhancers =
  typeof window === 'object' &&
  window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__ ?
    window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__({
      // Specify extension’s options like name, actionsBlacklist, actionsCreators, serialize...
    }) : compose;

const enhancer = composeEnhancers(
  applyMiddleware(thunk),
  // other store enhancers if any
);
const store = createStore(rootReducer, enhancer);`

### Setting Up Index and App with Store
My index file held the code for provider store and rendered my app component into the DOM.  It rendered it into my html home page that was my  `<div id="root">`. Adding some basic code to my app.js I just wanted to make sure I could get something to render and badabing, it did. Sweet. We were up and running.

### Adding Routes and All App Components 
I added my routes for my home page, expenses page, and the pages that would hold my NEW forms.  I used exact paths for my routes to not run into any route issues.  I also felt like `app.js` was the perfect place to add in my components that I wanted to render on every page (i.e. navbar and footer).

### Stateless Functional Components + Class Components vs. Containers
I do like to start small and only bite off what I can chew, making sure I can wrap my mind about what is going on with my app before moving on too much.  I have issues sometimes pulling the reigns back though.  I get excited when I'm building and I just want to build.  I get ahead of myself and then stuff doesn't work and then I'm working backwards to get things to render properly.  I tried to stay in check with this app though and work in tiny pieces before things got out of hand.  Making sure a component will render first and then build on from there is the approach I have come to love to take.  I added my home, navbar and footer components that I planned to just be purely text returned.  My container components are what holds the state of my app.  I knew my forms and my overall expenses page would hold the state.  I would then fetch my data from the API and dispatch to the store for the state to be updated and mapped to props to be rendered and/or passed to the child components.  At the beginning of the project I still kind of felt like a novice debugger (3 months ago).  I struggled with building this app and overcame every obstacle.  Some of it has become second nature and I understand the data flow more than I thought I would by the time I reached the finish line.  

### Refactoring 
I refactored my project so many times, my head could explode.  Moving things from single container components and piecing them out to smaller components, to then refactor them back as a whole for better formatting with bootstrap.  There are some obstacles and formatting issues when you have several smaller components for tables with bootstrap and react.  I could not get certain classes to style the way they should when I had small components for the tiny pieces in the expenses table I was making.  I worked on the formatting several days trying to figure out why the classes would not work.  It appeared that with the JSX Fragment tags the tables were not picking up the classes like they should.  It was easier for me to map through the list of expenses and build out the table in one entire component.  I also wanted to add collapsable forms on my expenses page.  When I initially made the app I had the expense form and category form showing on the expenses page.  To me, it seemed too cumbersome and I felt like it was not information that always needed to be there.  I added the bootstrap collapse functionality with a toggle toolbar for the forms.  This made the presentational aspect much better, in my opinion. 

### Working with Numbers and Dates
One amazing thing React has built in is for input fields, if you set the type to date, it has a nifty date picker that pops out.  I had spent almost an entire week trying to utilize the react-day-picker package.  I could get the input to update in the form, but on submit, nothing wasn't being sent over.  After more research I found changing the input type to date instead of string gave me the result I was looking for.

I wanted certain fields to not be able to be pure input fields.  I wanted the person to select categories from a drop down because I wanted to fetch the categories from the API. No need to have duplicates and it's nice to just be able to browse and select an option. 

Some of my data from the backend had to be slightly manipulated for things I wanted to display in the frontend.  I had some issues with parsing the data and getting it to render the way I wanted.  I read all about parseFloat but even still you can run into unexpected issues. No matter what I did for a few days, I kept getting NaN or it would concat my numbers together. For example, if I had 2 expenses with amounts of $194 and $65 (which are 2 of my real monthly expenses), my totals component would render 19465.  This issue had to do with needing to parse each one separately and add them together. Also, I have an update expense where the person can choose paid or not. When they click the button, I needed a function that filtered through the expenses.paid and then updated the outstanding total. 

### Cannot Render React Child Found Object
This error really got me.  My expenses are objects and then nested within I had my category for each.  I needed to be able to access the category but I also needed to map through the expenses to render and return the data I wanted.  Enter this snazzy line of code that I found after reading endless amounts of responses on Stackoverflow.  Inside my mapping function I had this line of code for the category I wanted to pass down to the child component. `const category = ((expense || {}).category || {}).name;` 
		
I wanted to be able to pass the category as a prop into my ExpenseListItem component.  I was getting the error because initially when it checks, expense does not show up as a prop..  I was getting undefined the first pass through until it loads.  So this line of code checks for the expense or an empty object and then the category or an empty category... then I chained the name onto it because that is what I wanted to pass through to the child.  
		
### Wrap Up
All in all, I am pretty stoked about my project.  I needed it for my own life. I learned so much more about bootstrap.  I built a much deeper understanding of React and Redux which I was very afraid about in the beginning.  I have now also bought a few other courses to further my knowledge after I pass my assessment! Cheers!
