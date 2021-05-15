About
===
Take a bunch of notifications/tickers/statuses/texts you want, configure them to your own taste, stitch them together as plain old text then get it back with one single Curl request.


Description
---
Each user will have access to his own API endpoint through which he can get his preconfigured message.
My personal use case will be to show this info in my Terminal, but I am sure this could be used in IoT projects, any number of dashboards


Abstract Classes used within the project: 
---

**Section**
- imagine this as being one of the user's api endpoints. 
- Should look like: doormat.io/{username}/{sectionName}
- The project will have a MVP with one single/default section

**Set** 
- Not sure if this is totally needed. 
- I feel like this could work like a "set of info" within a Section.
- Could probably also implement as a Section within Section but that would definitely require shitloads of validations
- Example User requirements:
-- I want to have 2 inspirational quotes shown
-- I want to see the EUR value of USD, GBP and BTC all in one line
-- Same thing but on different lines.

**Capsule Type** 
- Imagine this as beeing the actual code that is needed to display one pice of information
- This will have to make use of the interface design pattern to connect with different free API's
- Examples:
-- Static message like: "Have a great day!"
-- Random Quote
-- Personal Quote: takes a json file from the db which contains the desired quotes
-- Price of {currency1}/{currency2}
-- Crypto price: takes a currency pair as configuration like BTC/USDT
-- Forex price: takes a currency pair as configuration like EUR/USD
-- Weather in {my-city}
-- Appointments for today (from my google calendar)
-- Open capsule: takes a JS file as configuration... displays the output of that JS. Dunno if hackers will be smarter than me :)
- These classes must be open for different types of input.

**Capsule** 
- A Capsule is the basic piece that is displaying information
- This will basically be the Object created from a Capsule Type Class
- Must have it's own hardcoded Capsule Type class
- Each capsule must define it's specific input by the user; user1 will use WeatherCapsule with argument "London", but user2 will use the same WeatherCapsule with argument "Berlin"

**Templating Engine** 
- A way to connect the output of the capsules, to the finished api _through_ a drag-and-drop type of configuring interface
- Each Section must have some kind of definition saved which will be interpreted by the TE
- The information in the Section will tell the TE how is the data _formatted_
- Crude example:
-- line1= capsuleId:12 &nbsp&nbsp capsuleId:22; line2:capsuleId:33


Features
---
- user/pass
- Oauth
- A User has one Default Section
- A User can have multiple Sections (in the paid version 😈)
- A Section can contain Sets and Capsules
- A Set has multiple Capsules
- A Capsule will have a predefined output which will be interpreted by the templating engine
- All this info must be open for extension to multiple channels. MVP will be optimised for CLI-like output
- Frontend will have a test output (basically... extending on the previous point, in the MVP we must consume our own API as a feature for the user)
- (OMFG implement that old terminal script thing that I have saved on the desktop for testing)
- figure out a templating engine that can then be extended; for example for collored output
- A chron job which updates all the processed info, so that it's available instantly to the user

Resources 
---
These must all have B.R.E.A.D. functionality through a RESTful API
- users
- sections
- sets
- capsules

DB Design
---
This is still WIP

|Table Name | Contains | Special notes  |
|--|--|--|
|users|  |  |
|sections| template_config, processed_result |  |
|sets|  | not sure if needed |
|capsule_type| class_name |  |
|capsules| user_id, capsule_type_id, configuration |  |


Decisions needed to make:
--
- are Section/Set/Capsule needed? or can just Section/Capsule enough?
- name of project??? Doormat (it's a welcome message like the welcome message on a lot of doormats)
- find a catchy short domain url to buy
