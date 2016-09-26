# GameJolt API plugin for Godot Engine
## How to install
Just download the repository and drop the **gamejolt_api** folder into your addons folder. Open the add node dialog and locate **GameJoltAPI** under the HTTPRequest node. A demo project showing some of the functions is next to the plugin folder.

## How to use/methods description
### Authentication/users
Before doing any calls to the API you must authenticate a user first so the system knows what user to work with.
A method to do it is provided:

**auth_user(token, username)**

*token - your gamejolt user token(NOT your password)
username - your username*
