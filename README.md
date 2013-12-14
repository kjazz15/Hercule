Hercule 0.1.0
=============

Hercule is a robust Python wrapper for Riot Games League of Legends API

Making Calls
------------

It's simple! To start, from hercule, import Request - this is the class you'll use to make API calls

	from hercule import Request

Hercule uses the requests module - if you're getting module errors, pip install it -

	pip install requests

Then, initialize your class - you'll need to have your API key, which you can get at https://developer.riotgames.com/sign-in

	r = Request(api_key)

From this object, you can call any of Hercule's methods and receive your information as a string or a Python dict 

Here are a few examples - 

### Getting a summoner ID

	player_id = r.get_id_from_name('Greedoid')

What this method returns is simply the player's summoner ID - useful for other methods that take it as an argument

As a note, any methods that return player information default to the North American server - if you wish to query EU-West or EU-Northeast players, just pass the server in after the player name 

	player_id = r.get_id_from_name('Froggen', 'euw')

### Getting many summoner names from a list of IDs

	bunch_of_ids = [1, 2, 3, ... 140]
	list_of_ids = r.get_names_from_ids(bunch_of_ids)

This method returns a list of names corresponding to the list of summoner IDs passed to it.

**NOTE**: This API call takes in a max of 40 IDs per call. You can pass in as many IDs as you want to the method, but you may be rate-limited if you use very large lists of IDs

### Getting the rune/mastery pages from a player

	my_runes = r.get_runes_from_name('Trick2g')
	
This returns a list of rune pages from the particular player

**NOTE**: Due to the way the Riot Games API is set up, most player information-based calls take the player's summoner ID as the argument. As such, the above method technically takes 2 API calls to Riot to make - one to convert the player name to a summoner ID, and then one, using the summoner ID, to get the player information. If you're making a lot of calls in a short period of time, it may be wise to use the functions that take summoner IDs as arguments, in order to cut down on API calls made.

	my_current_masteries = r.get_current_masteries_from_name('Trick2g')

This function goes one step further and returns only the current mastery page that the player has equipped. There is a similar function for rune pages.

 


