# Introduction
CommunityDragon (also referred to as cdragon) is an open-source organization which provides tools for scraping data from riot's content delivery network, as well as provide services around hosting scraped data.

### Services
If you're only looking for access to assets, CommunityDragon provides two main services for accessing those assets, that being [RAW](https://raw.communitydragon.org) and [CDN](https://cdn.communitydragon.org). 

**raw.communitydragon.org**\
The RAW service provides all data directly scraped from both the game client and the LCU (League Client Update), up until patch 7.1. Although providing all data available in both clients, the data might be more difficult to access, since Riot's client data is slightly unstructured, and you'll have to fetch some JSON files beforehand in order to get the correct paths to certain assets. You can find commonly used paths in the [assets page](https://github.com/CommunityDragon/Docs/blob/master/assets.md).

**cdn.communitydragon.org**\
The CDN service provides assets in a more structured manner. It proxies the data directly from RAW. Beware that CDN will be deprecated in the future, in order to allow for versioning of the endpoints, improving uptime, and allowing multiple games from Riot (Valorant, Legends of Runeterra, Wild Rift) to be hosted through CDN. CommunityDragon will drop an announcement about the deprecation through both the blog and in discord announcements.

### Tooling
Currently, all scraping tools are located on GitHub under the name of [CDTB](https://github.com/communitydragon/CDTB) (short for CommunityDragon ToolBox). This toolbox is primarily focused on scraping and unpacking League of Legends data specifically. The toolbox does however also contain python scripts that allow for the scraping other games made by Riot, as Riot uses the same patcher for all of it's IPs.

### Bugs & Suggestions
If you find any bugs, the community would appreciate reporting these bugs either through Discord or GitHub Issues. Issues found on the provided services should be reported through [Discord](https://discord.gg/rZQwuek) and pinging an online member of management. As for the tooling, issues can both be reported through the Discord community, or through GitHub Issues.

CommunityDragon is also open for suggestions. If you have any interesting suggestions or ideas, feel free to join the [Discord](https://discord.gg/rZQwuek) community and write it in *#suggestions*.

### Legal
First and foremost, **CommunityDragon was created under Riot Games' ["Legal Jibber Jabber"](https://www.riotgames.com/en/legal) policy using assets owned by Riot Games. Riot Games does not endorse or sponsor this project.** While CommunityDragon functions within a gray area, this project has been acknowledged by Riot through the Riot Developer Portal. The usage of CommunityDragon does not pose a risk to your API key.

**CommunityDragon does not endorse, condone or support the usage of Riot's assets provided through CommunityDragon's services with the purpose of ill intent, such as scripting or hacking.** CommunityDragon operates on good faith, with the intention of providing developers assets and static data that Riot does not provide themselves.
