# Guild Wars 2 API (Python)
A Python 3.x wrapper for the second version of the <a href="https://wiki.guildwars2.com/wiki/API:Main" target="_blank">Guild Wars 2 API</a>.

## Installation

- Clone or download the repository
- Run `python setup.py install`

## List of currently supported endpoints

All <a href="http://wiki.guildwars2.com/wiki/API:2#Active_endpoints" target="_blank">currently available</a> /v2/ API endpoints are now supported.

Up next: backwards compatibility with /v1/ endpoints that are not in /v2/.

## Usage

    import guildwars2api
    gw = guildwars2api.GW2()
    
    # You may specify a preferred localization and a connection timeout (in seconds).
    gw = guildwars2api.GW2(language="EN", timeout=5)
    
    # Print details about your connection to the Guild Wars 2 API, e.g. the current API key.
    print(gw.get_connection_details())
    
    # Print the currently available endpoints of the second version of the Guild Wars 2 API.
    print('\n'.join(gw.get_endpoints()))
    
    # Some player account endpoints, e.g. /v2/pvp/stats, require an authenticated connection.
    # You can authenticate an entire session directly...
    gw.authenticate("REDACTED_API_KEY")
    print(gw.get_pvp_stats())
    # ...or if need be.
    print(gw.get_pvp_stats("REDACTED_API_KEY"))
    # Likewise, you can securely retrieve access token information for the session token...
    print(gw.get_tokeninfo())
    # ...or for a given API key.
    print(gw.get_tokeninfo("REDACTED_API_KEY"))
    
    # Get a list of details of respectively a world, a few worlds and all worlds.
    world = gw.get_worlds(1001)
    worlds = gw.get_worlds(1001, 1002, 1003)
    worlds = gw.get_worlds("all")
    
    # You can also grab just all the world ids.
    world_ids = gw.get_worlds_ids()
    
    # Print out all the world names of the worlds with a very high population of players.
    worlds = gw.get_worlds("all")
    for world in worlds:
        if world["population"] == "VeryHigh":
            print("{}\t{}".format(world["id"], world["name"]))

## Additional functionality

    import guildwars2api
    gw = guildwars2api.GW2()
    
    # You can easily convert any amount of coins to an amount of gold, silver and copper.
    print(gw.coins_to_gold(20000))
    # Or, you can convert any amount of gold, silver and copper to an amount of coins.
    print(gw.gold_to_coins(2, 11, 23))
    # Finally, you can calculate your profit if you were to sell an item on the trading post.
    print(gw.get_commerce_profit(21123))

## License

Code in this repository is licensed under the [MIT License](LICENSE).