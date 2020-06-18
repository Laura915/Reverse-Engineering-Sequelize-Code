# Code Break Down and Explanation

 ## Description 
  A breakdown of the folder structure and all its contained files, a detailed explanation of each file, and instructions for a new feature.  

  ## Table of Contents

  * [server](#server)
  
  * [config](#config)

  * [db](#db)
  
  * [models](#models)

  * [routes](#routes)

  * [public](#public)

  * [Feature](#Feature)
    
  * [Questions](#questions)

  
  ## server

  ### server.js :

  Require express npm package to create an express server that will render http/api requests and parse data.

  Require express-session npm package to keep track of user login info. Session ID is used and will save last session ID stored.

  Require passport.js file to export configuration with middleware. Use initialize method to configure passport to express server. In order to use persistant login session, apply session method to passport. 

  Require models directory to import sequilize database .Sync database to run once server is run.

  Require html-routes.js file so that express app can render html pages.

  Require api-routes.js file so express app can work with api requests.

  ## db

  ### schema.sql :
  Schema sequel file is used simply for the creation of the database and to establish usage. This is important because, in order for sequelize to create tables, the database needs to be created.

  ## config

  ### ./middleware/ isAuthenticated.js :
  exports middleware that restricts a in-valid user access to unrestricted areas, and re-routes to signup page. Otherwise if a valid user is loged in, continue to next route. 

  ### cong.json :
  Json file with our connection to my sequel database. This file is need in order to connect to mysql database and edit tables with sequilize. Database passport_demo is created in schema.sql file. 

  ### passport.js :
  Require passport npm package that serves as express authentication middleware. Passport authticates credentials with use of a specified strategy from passport-local npm package. 

  Require passport-local package and create a new LocalStrategy that authenticates passport through a callback function. This stratgy authticates email and password. 

  Require models directory so that the passport authinticator can acess the new User values ceated from models/user.js.

  Serialize and deserialize the user to keep authtication across app when http request. 

  Export passport to be used in server.

  ## models

  ### user.js :
  Export User function, that defines new User with sequelize npm package. Defines Users' emails value to be a string, cannot be null, must be unique, and must be formated as an email. the password value is defined as a string value and cannot be null.  

  Require bcryptjs npm package to allow hashing of passwords before their created. The Hook added specifies beforeCreate so that it executes that when new user is being created.

  ### index.js :
  This file is part of using the sequelize package, this file is pre-made and is used to controll all created models. In our case we only have one model user.js.

  Require config.json file to connect to the correct database.

  Require fs and path node packages to read all the models in models directory

  All models created will then be added to an db object 

  db is then is exported

  ## routes

  ### api-routes.js :
  Require models so that we can work with database table User

  Require passport file to use passport.authenticate middleware and local strategy to check if user inputs valid credentials. 
  
  First post route, posts login information to server. Then a request is sent to be validated with passport middleware . If a current user, then members page is rendered.

  Second post route will sign up new users. This post route will create new user. If sign up is sucessful user will be routed to login page else they will get a error.

  first get route logs user out. and re-routes to to sign up page

  Second get route qet User data. If user isn't logged in send empty object else send user's email and id to designed url path. 

  Export api routes function    

  ### html-routes.js :
  Require path node package in order to find correct html file in our directory.

  Require isAuthenticated.js file to check wether a user is logged in or not.

  First get route, home or sign in route , checks if an existing user and if so directs user to members page. Otherwise send user to sign up page.

  Second get route, login page route, checks if an existing user. If valid user, then directed to members page. Otherwise sent login page.

  Third get route, members page route. Applies isAuthenticated function to direct authenticated members to members page.

  Export differenent html routes function

  ## public

  ### js

  ### signup.js :
  Added jquery .ready function to the document so that this function is applied to the html document once all html is loaded.

  Get all variables w'ell need, such as user email, password and the sign up form.

  Add an event listerner to listen to all submits on sign up form. Inside the listerner, prevent default form behavior and create an object with input values. Use sinUpUser function and handelLoginError function to take care or submisson.

  SignUpUser function will post the new User data to post route "/api/signup" and load members page. Otherwise execute handelLoginError function. 

  handelLoginError function will handel error message.   

  ### login.js :
  Very similar to the sign up page. A .ready function is applied to the document.

  Get all variables w'ell need, user email, password and the login form.

  Add event listerner to login form. Same as sign up form, prevent form behavior, create object with input values and check wether a valid user and if so execute loginUser function.

  LoginUser function posts User's data to post route "/api/login" and direct to members page or console err message.  

  ### members.js :
  Added jquery .ready function to the document so that this function is applied to the html document once all html is loaded.

  Gets user email and sends to "/api/user_data" route. And sets user email to the class member-name

  ### stylesheets
  
  ### signup.html :
  Sign up page is created with bootstrap stlying. This page consist of a basic sign up page, input fields for both user email and password. A submit button to initiate event listener. 
  
  A block of code for the err message with spam tags

  A link to the login page in case they're a registered user. 

  ### login.html :
  Very similar to singup.html the only difference would be the title page and the link to the sign up page.

  ### members.html :
  This is the members page, provides a logout route link in the nav bar and a welcome message as the body.  

  ## Feature :

  ### Strong Password Feature
  1. Add hook method for after user is created,hook will check if password is strong and secure   

  2. Add function to hook that will specify the password has minimum of at least one of the following:
  - Capital letter
  - Lower case letter
  - Number
  - Special character

  3. If password is weak, user will be pomted to try again
  
  ## Questions
  If you have a question about this repo, open a issue or contact Laura915 

  