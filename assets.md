# Asset paths

A lot of assets are available in client and game files. This describes how
they are organized and where to find frequently requested files.

**Note:** Files are sometimes reorganized by Riot. This page applies to the latest version.

On [raw.communitydragon.org](http://raw.communitydragon.org/latest/), LCU files
are exported at the root and game client hashes are exported in the `game/`
subdirectory.

Files with unknown path are put in `unknown/` subdirectories.


## Client paths

Most paths from client use the following format: `plugins/<plugin>/<region>/<lang>/...`
Where:
 - `<plugin>` is the client plugin name
 - `<region>` is a region name (e.g. `euw`), or `global`
 - `<lang>` is a language code (e.g. `en_gb`), or `default`

The plugin name matches the directory name in which a WAD can be found. For
instance, for `.../plugins/rcp-fe-lol-missions/assets.wad`, the plugin is
`rcp-fe-lol-missions`.

With the exception of the `rcp-be-lol-game-data` plugin which contains a lot of
common assets, only the `fe` (frontend) plugins contain assets; the `be`
(backend) can be ignored.

The region/lang pair allows the client to use different files depending on the
region and/or language. It is notably used for translations and censorship of
some visuals (e.g. Grave's cigar).
When retrieving an asset, the client starts by looking for a match with its
specific region and/or language, then falls back to `global/default`.


## JSON data files

Various data are available [as JSON files](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/v1/).
They cover a large set of game objects (champions, skins, missions, TFT, ...) and are a good start point.

### Mapping paths from JSON files

In those JSON files, asset paths can be mapped to URLs: `/lol-game-data/assets/<path>` is mapped to `plugins/rcp-be-lol-game-data/global/default/<lowercased-path>`.

For instance:
 - `/lol-game-data/assets/ASSETS/Items/Icons2D/TeleportHome.png` maps to [plugins/rcp-be-lol-game-data/global/default/assets/items/icons2d/teleporthome.png](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/assets/items/icons2d/teleporthome.png)
 - `/lol-game-data/assets/v1/champion-icons/-1.png` maps to [plugins/rcp-be-lol-game-data/global/default/v1/champion-icons/-1.png](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/v1/champion-icons/-1.png)


## Champion assets

**Note:** layout have changed and not all champions have been updated yet. For
the actual path, always check the champion's JSON file from
[champion basic data](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/v1/champions/).

**Note:** most assets from `rcp-be-lol-game-data` can be found in both LCU files and game client files.

 - [Basic data](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/v1/champions/), also includes paths to champion assets
 - [Square portraits (base skin)](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/v1/champion-icons/)
 - [Square portraits (all skins)](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/v1/champion-tiles/), as seen on shop and hextech-crafting
 - Round portraits (all skins): `game/assets/characters/{name}/hud/` ([example](https://raw.communitydragon.org/latest/game/assets/characters/lux/hud/))
 - [Skin backgrounds (centered)](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/v1/champion-splashes/), as seen on profile page
 - [Skin backgrounds (uncentered)](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/v1/champion-splashes/uncentered/), as seen on collection tab
 - [Ultimate skin backgrounds](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/v1/summoner-backdrops/), as displayed on profile page, also animated
 - [Chroma appearances](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/v1/champion-chroma-images/), as seen on champion select
 - Loading screen champion backgrounds: `plugins/rcp-be-lol-game-data/global/default/assets/characters/{name}/skins/` or `game/assets/characters/{name}/skins/`
   ([example](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/assets/characters/akali/skins/)),
   also include limited edition borders ([example](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/assets/characters/riven/skins/skin16/rivenloadscreen_16_le.jpg))
 - Spell icons (all forms): `game/assets/characters/{name}/hud/icons2d` ([example](https://raw.communitydragon.org/latest/game/assets/characters/khazix/hud/icons2d/))

## Event assets
Some event assets aren't exported on raw.communitydragon.org. These event assets (like images and videos) are sorted by year and event on [universe.communitydragon.org](https://universe.communitydragon.org)

## Other assets

 - [Summoner icons](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/v1/profile-icons/)
 - [Rune icons](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/v1/perk-images/styles/), [stats icons](https://raw.communitydragon.org/pbe/plugins/rcp-be-lol-game-data/global/default/v1/perk-images/statmods/)
 - [Ward skins](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/content/src/leagueclient/wardskinimages/)
 - [Emotes](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/assets/loadouts/summoneremotes/), also [here](https://raw.communitydragon.org/latest/game/assets/loadouts/summoneremotes/)
 - Game modes: [icons and lobby](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/content/src/leagueclient/gamemodeassets/), [loading screen backgrounds](https://raw.communitydragon.org/latest/game/assets/ux/loadingscreen/)
 - [Item icons](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/assets/items/icons2d/)
 - Hextech crafting and loot:
   [here](https://raw.communitydragon.org/latest/plugins/rcp-fe-lol-loot/global/default/assets/loot_item_icons/)
   [and](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/assets/loot/)
   [there](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/v1/hextech-images/)
 - Role icons: [PNG](https://raw.communitydragon.org/latest/plugins/rcp-fe-lol-clash/global/default/assets/images/position-selector/positions/), [SVG](https://raw.communitydragon.org/pbe/plugins/rcp-fe-lol-static-assets/global/default/svg/) (multiple colors available for both)
 - [Clash banner flags](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/assets/loadouts/summonerbanners/flags/)
 - [Nexus Blitz event icons](http://raw.communitydragon.org/pbe/game/assets/ux/gamemodes/slime_atlas.png) (texture map), also [some here](http://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/content/src/leagueclient/gamemodeassets/gamemodex/img/eventicons/)
 - [Profile and friend-list circles based on summoner level](https://raw.communitydragon.org/latest/plugins/rcp-fe-lol-static-assets/global/default/images/uikit/themed-borders/) (look for `theme-*-border.png` files), old ones [here](https://raw.communitydragon.org/latest/plugins/rcp-fe-lol-static-assets/global/default/images/uikit/themed-level-ring/)
 - [League ranked crests](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/content/src/leagueclient/rankedcrests/) (various parts for each tier, look into `images/` subdirectory for each tier)
 - [League ranked icons](https://raw.communitydragon.org/latest/plugins/rcp-fe-lol-shared-components/global/default/)
 - [League ranked mini icons](https://raw.communitydragon.org/latest/plugins/rcp-fe-lol-static-assets/global/default/images/ranked-mini-crests/)
 - [Tier promotion animations](https://raw.communitydragon.org/pbe/plugins/rcp-fe-lol-static-assets/global/default/videos/)
 - [Mission icons](https://raw.communitydragon.org/latest/plugins/rcp-fe-lol-missions/global/default/events/images/missions/) (note: some are still [unknown](https://raw.communitydragon.org/latest/plugins/rcp-fe-lol-missions/unknown/))
 - [Loading screen tier borders](https://raw.communitydragon.org/pbe/game/assets/ux/loadingscreen/)
 - In-game announcements: [champion borders, multi-kill banners](https://raw.communitydragon.org/latest/game/assets/ux/announcements/announcementicons.png), [non-champion portraits](http://raw.communitydragon.org/latest/game/data/images/ui/momentstimelineportraits/), [dragon portraits](https://raw.communitydragon.org/latest/game/assets/ux/announcements/)
 - [Match history icons](https://raw.communitydragon.org/latest/plugins/rcp-fe-lol-match-history/global/default/), including [gold](https://raw.communitydragon.org/latest/plugins/rcp-fe-lol-match-history/global/default/icon_gold.png) and [CS](https://raw.communitydragon.org/latest/plugins/rcp-fe-lol-match-history/global/default/icon_minions.png) icons from scoreboard
 - [Buff/debuf icons](http://raw.communitydragon.org/latest/game/data/spells/icons2d/)
 - [In-game cursors](http://raw.communitydragon.org/pbe/game/assets/ux/cursors/) (also [Qiyana's ones](http://raw.communitydragon.org/pbe/game/assets/characters/qiyana/cursors/))
 - [Mastery icons](https://raw.communitydragon.org/latest/game/assets/ux/mastery/)
 - [Challenge assets](https://raw.communitydragon.org/latest/plugins/rcp-fe-lol-static-assets/global/default/images/challenges-shared/) like crystal and category icons

## Teamfight Tactics (TFT)

 - [Most icons](http://raw.communitydragon.org/pbe/game/assets/ux/fonts/texticons.png) (small versions)
 - [Trait icons](http://raw.communitydragon.org/latest/game/assets/ux/traiticons/)
 - [Champion images](http://raw.communitydragon.org/latest/game/assets/ux/tft/championsplashes/) (as displayed in in-game shop)
 - [Companions](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/assets/loadouts/companions/) (as displayed in lobby)
 - [Map skins](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/assets/loadouts/tftmapskins/) (as displayed in lobby)
 - [UI assets](http://raw.communitydragon.org/pbe/game/assets/ux/tft/) (look in subdirectories for more)

## Obsolete assets

 - [Old league tier images](https://raw.communitydragon.org/8.23/plugins/rcp-fe-lol-league-tier-names/global/default/assets/images/ranked-crests/)
 - [Old tier promotion animations](https://raw.communitydragon.org/8.23/plugins/rcp-fe-lol-leagues/global/default/videos/)
