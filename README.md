# GameJolt API plugin for Godot Engine
## How to install/setup
Just download the repository and drop the **gamejolt_api** folder into your addons folder. Open the add node dialog and locate **GameJoltAPI** under the HTTPRequest node. A demo project showing some of the functions is next to the plugin folder. **Don't forget to fill the private key and your game id in the inspector**


## How to use/methods description
### Authentication/users
Before doing any calls to the API you must authenticate a user first so the system knows what user to work with.
A method to do it is provided:

`auth_user(token, username)`
* token - your gamejolt token (NOT your password)
* username - your gamejolt username, duh

Now you can use other api methods. The api allows you to fetch user's information like their username, description and so on. You can use on of two provided methods:

`fetch_user_by_name(username)`
* username - name of the user you want to fetch

`fetch_user_by_id(user_id)`
* user_id - id of the user you want to fetch. Multiple ids allowed, comma-separated 1,2,3,4

### Sessions
Sessions are used to tell the system that someone's playing the game and to collect stats about the average game time, number of sessions... To open a session use the respective method:

`open_session()`

A session is closed within 120 seconds if not pinged. Ping your session to prevent the system from cleaning it up with the following method:

`ping_session()`

If the player wants to quit the game you might want to close the current session. Use this method to close the active session:

`close_session()`

BTW if you look at the official API docs you'll see that some calls to the api require to pass a username and a token and the plugin methods don't. The plugin caches them so you don't need to pass them everytime. No worries!

### Trophies aka achievements

GameJolt has their achievements system so you can add trophies and players can achieve them! To fetch the list of trophies for a game, call:

`fetch_trophies(achieved="", trophy_ids="")`
* achieved - if you leave this blank, all throphies will be fetched, passing true will return only the achieved trophies while passing false return only unachieved trophies
* trophy_ids - if you pass this, only trophies with the specified ids will be fetched. You can pass multiple ids separated by a comma 1,2,3,4. If this option is passed, the first one is ignored

To set a trophy as achieved, call this:

`add_trophy(trophy_id)`
* trophy_id - the id of the trophy. Found on the game's trophies section

### Scores

GameJolt also features the scoreboards system. To fetch the scores use this method:

`fetch_scores(limit="", table_id="")`
* limit - how many scores to return. Default is 10, max is 100
* table_id - pass this if you want scores from a specified table. Scores from the primary scoreboard are returned otherwise.

To fetch scores only of the currently logged in user use this method:

`fetch_scores_for_user(limit="", table_id="")`
* limit - how many scores to return. Default is 10, max is 100
* table_id - pass this if you want scores from a specified table. Scores from the primary scoreboard are returned otherwise.

To add a score for the user use this method:

`add_score_for_user(score, sort, table_id="")`
* score - a string value associated with the score. Example: "234 Jumps".
* sort - a numerical sorting value associated with the score. All sorting will work off of this number. Example: "234". 
* table_id - The id of the high score table that you want to submit to. If left blank the score will be submitted to the primary high score table.

Scores can be added as guest:

`add_score_for_guest(score, sort, guest, table_id="")`
* score - a string value associated with the score. Example: "234 Jumps".
* sort - a numerical sorting value associated with the score. All sorting will work off of this number. Example: "234".
* guest - name of the guest
* table_id - The id of the high score table that you want to submit to. If left blank the score will be submitted to the primary high score table.

A list of the scoreboards can be fetched with this method:

`fetch_tables()`

### Data store

Right now I haven't implemented these features yet, they will be available very soon.

### How to parse the API responses?

API responses use the json format and are not pre-parsed or modified before sending them with the signals so the Dictionary class can be used to parse them.
