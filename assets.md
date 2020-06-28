# Asset paths

A lot of assets are available in LCU and game client files. This describes how
they are organized and where to find frequently requested files.

**Note:** Files are sometimes reorganized by Riot. This page applies to the latest version.

On [raw.communitydragon.org](http://raw.communitydragon.org/latest/), LCU files
are exported at the root and game client hashes are exported in the `game/`
subdirectory.

Files with unknown path are put in `unknown/` subdirectories.


## LCU paths

Most paths from LCU use the following format: `plugins/<plugin>/<region>/<lang>/...`
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
 - [Ultimate skin backgrounds](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/v1/summoner-backdrops/), as displayed on profile page
 - [Animated ultimate skin backgrounds](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/v1/champion-splash-videos/), full animation, centered
 - [Chroma appearances](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/v1/champion-chroma-images/), as seen on champion select
 - Loading screen champion backgrounds: `plugins/rcp-be-lol-game-data/global/default/assets/characters/{name}/skins/` or `game/assets/characters/{name}/skins/`
   ([example](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/assets/characters/akali/skins/)),
   also include limited edition borders ([example](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/assets/characters/riven/skins/skin16/rivenloadscreen_16_le.jpg))
 - Spell icons (all forms): `game/assets/characters/{name}/hud/icons2d` ([example](https://raw.communitydragon.org/latest/game/assets/characters/khazix/hud/icons2d/))

## Other assets

 - [Summoner icons](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/v1/profile-icons/)
 - [Rune icons](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/v1/perk-images/styles/), [variants (including black and white)](https://raw.communitydragon.org/latest/plugins/rcp-fe-lol-perks/global/default/images/), [stats icons](https://raw.communitydragon.org/pbe/plugins/rcp-be-lol-game-data/global/default/v1/perk-images/)
 - [Ward skins](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/content/src/leagueclient/wardskinimages/)
 - [Emotes](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/assets/loadouts/summoneremotes/), also [here](https://raw.communitydragon.org/latest/game/assets/loadouts/summoneremotes/)
 - Game modes: [icons and lobby](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/content/src/leagueclient/gamemodeassets/), [loading screen backgrounds](https://raw.communitydragon.org/latest/game/assets/loadingscreen/)
 - [Item icons](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/data/items/icons2d/)
 - Hextech crafting and loot:
   [here](https://raw.communitydragon.org/latest/plugins/rcp-fe-lol-loot/global/default/assets/loot_item_icons/)
   [and](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/assets/loot/)
   [there](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/v1/hextech-images/)
 - Role icons: [PNG](https://raw.communitydragon.org/latest/plugins/rcp-fe-lol-clash/global/default/assets/images/position-selector/positions/), [SVG](https://raw.communitydragon.org/latest/plugins/rcp-fe-lol-leagues/global/default/svg/) (multiple colors available for both), [for each league tier](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/assets/ranked/positions/)
 - [Clash banner flags](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/assets/loadouts/summonerbanners/flags/)
 - [Odyssey augments](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/assets/loadouts/odysseyaugments/)
 - [Nexus Blitz event icons](https://raw.communitydragon.org/pbe/game/data/menu/textures/slime_atlas.png) (texture map), also [some here](http://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/content/src/leagueclient/gamemodeassets/gamemodex/img/eventicons/)
 - [Profile and friend-list circles based on summoner level](https://raw.communitydragon.org/latest/plugins/rcp-fe-lol-uikit/global/default/images/) (look for `theme-*-border.png` files)
 - [League tier crests](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/content/src/leagueclient/rankedcrests/) (various parts for each tier, look into `images/` subdirectory for each tier)
 - [League tier icons](https://raw.communitydragon.org/latest/plugins/rcp-fe-lol-league-tier-names/global/default/assets/images/ranked-mini-regalia/)
 - [Tier promotion animations](https://raw.communitydragon.org/latest/plugins/rcp-fe-lol-leagues/global/default/lottie/videos/)
 - [Mission icons](https://raw.communitydragon.org/latest/plugins/rcp-fe-lol-missions/global/default/events/images/missions/) (note: some are still [unknown](https://raw.communitydragon.org/latest/plugins/rcp-fe-lol-missions/unknown/))
 - [Loading screen game mode backgrounds](https://raw.communitydragon.org/latest/game/data/loadingscreen/)
 - Loading screen tier borders: [season 9](https://raw.communitydragon.org/pbe/game/data/menu/textures/loadingscreen_frames_atlas.png), [seasons 5-8](https://raw.communitydragon.org/latest/game/data/loadingscreen/season_5_borders.png)
 - [Minimap icons](https://raw.communitydragon.org/latest/game/data/menu/minimapicons/): towers, Nashor, wards, Kindred passive, ...
 - In-game announcements: [champion borders, multi-kill banners](https://raw.communitydragon.org/latest/game/data/menu_sc4/announcements/), [non-champion portraits](http://raw.communitydragon.org/latest/game/data/images/ui/momentstimelineportraits/)
 - [Match history icons](https://raw.communitydragon.org/latest/plugins/rcp-fe-lol-match-history/global/default/), including [gold](https://raw.communitydragon.org/latest/plugins/rcp-fe-lol-match-history/global/default/icon_gold.png) and [CS](https://raw.communitydragon.org/latest/plugins/rcp-fe-lol-match-history/global/default/icon_minions.png) icons from scoreboard
 - [Buff/debuf icons](http://raw.communitydragon.org/latest/game/data/spells/icons2d/)
 - [In-game cursors](http://raw.communitydragon.org/latest/game/data/images/ui/cursors/)
 - [Login screen (background, animation, music)](https://raw.communitydragon.org/latest/plugins/rcp-fe-lol-splash/global/default/splash-assets/), check older patches for older themes
 - [Mastery icons](https://raw.communitydragon.org/latest/game/assets/ux/mastery/)

## Teamfight Tactics (TFT)

 - [Most icons](http://raw.communitydragon.org/pbe/game/assets/ux/fonts/texticons.png) (small versions)
 - [Trait icons](http://raw.communitydragon.org/latest/game/assets/ux/traiticons/)
 - [Champion images](http://raw.communitydragon.org/latest/game/assets/ux/tft/championsplashes/) (as displayed in in-game shop)
 - [Companions](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/assets/loadouts/companions/) (as displayed in lobby)
 - [Map skins](https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/assets/loadouts/tftmapskins/) (as displayed in lobby)
 - UI assets: [one](http://raw.communitydragon.org/latest/game/data/menu/textures/tft_hud_texture_atlas.png), [two](http://raw.communitydragon.org/latest/game/data/menu/textures/tft_traits_texture_atlas.png), [three](http://raw.communitydragon.org/latest/game/data/menu/textures/tfthealthbaratlas.png)

## Obsolete assets

 - [Old league tier images](https://raw.communitydragon.org/8.23/plugins/rcp-fe-lol-league-tier-names/global/default/assets/images/ranked-crests/)
 - [Old tier promotion animations](https://raw.communitydragon.org/8.23/plugins/rcp-fe-lol-leagues/global/default/videos/)

