# Dota 2 Building Helper - Reborn

After various iterations, the dream of client-side particles is real, and Building Helper has now been fully updated for Panorama, allowing for building ghost and grid effects aswell as providing all the core features you'd expect for building and builder management.

## Contents

#### Core BH Features

* Building placement with a building grid preview on the world
* Queueing multiple buildings for individual workers
* Basic Support for an additional resource (Lumber)
* Building cancel process, continuing the queue
* Various construction behaviours: Self-Building, Builder-Inside, Repair-Required, Consumes-Builder.
* Repairing buildings, with multiple builders being able to assist the process
* Support for left/right click mouse callbacks and orders

#### Tech Tree Upgrades, Building Queue system, and more!

In addition to the construction related features, you'll find a couple of systems to do very common things in RTS & TD games, which is unlocking different upgrades/researches and automatically enable them when the requirements are met. 

Whenever a building starts channeling an ability with certain research time, a queue will be created using the item slots of the building, without any extra UI, and just requires that every ability also gets an item copy to be able to cancel at will any point of the queue.

**Note:** The following 2 systems were excluded from the basic library:
- Unit Production
- Gather Gold/Lumber

If you are interested in said features, you can take a look at the [DotaCraft repository](https://github.com/MNoya/DotaCraft)

## Installation

There are 2 ways to use this library, starting by [downloading the latest release](https://github.com/stephenfournier/Dota-2-Building-Helper/releases), you can either get the samplerts addon to see the features ingame, or if you have a preexisting addon which you'd like to utilize BuildignHelper, I'll explain the necessary files and configuration for it.

### SampleRTS sandbox addon

1. Copy the entire **content** and **game** folders in your dota folder `\Steam\SteamApps\common\dota 2 beta\`.
2. Start the workshop tools, you'll see a **samplerts** in your list of addons.
3. Launch the samplerts map, either through Hammer or copying `dota_launch_custom_game samplerts samplerts` in your console.

### Adding BuildingHelper scripts to your game mode

There are multiple elements you'll need to incorporate for a successfull implementation of this library. 

1. Panorama Content.
  - Merge the Panorama folder `content\dota_addons\samplerts\panorama` with the panorama folder in your addon.
  - If you already have a <custom_ui_manifest.xml>, you'll have to add these lines to it:
  ```
   <CustomUIElement type="Hud" 	layoutfile="file://{resources}/layout/custom_game/scripts.xml" />
   <CustomUIElement type="Hud"  layoutfile="file://{resources}/layout/custom_game/resource.xml" />
   <CustomUIElement type="Hud"  layoutfile="file://{resources}/layout/custom_game/notifications.xml" />
  ```

2. Lua Scripts
  - Go inside the `\game\dota_addons\samplerts\scripts\vscripts` folder and copy all the files excluding:
    - addon_game_mode.lua (**Require** all files and precache lines)
    - gamemode.lua (This contains necessary events and table initializations)

3. DataDriven ability examples.
  - BH abilities come already split to conveniently combine with [Dota-2-ModKit](https://github.com/stephenfournier/Dota-2-ModKit). In `game\dota_addons\samplerts\scripts\npc` folder there are both essential abilities and ability examples. 
  - Copy the sub folders **abilities**, **items**. 
  - The other 2 folders (heroes and units) aren't necessary but contain important keys which will be explained later
  
4. Particles
  - Copy the buildinghelper compiled particles (vpcf_c) from `game\dota_addons\samplerts\particles` into your addons game particle folder. You can also get the sources at the same directory under content.
 

## [Usage](https://github.com/stephenfournier/Dota-2-Building-Helper/wiki)

### Grid and Model Ghost options

In buildinghelper.lua, you will find these variables to control the properties of the ghost particles.

* GRID_ALPHA: Defines the transparency of the ghost squares in Panorama
* MODEL_ALPHA: Defines the transparency of both the ghost model in Panorama and Building Placed in Lua
* RECOLOR_GHOST_MODEL: Whether to recolor the ghost model green/red or not
* RECOLOR_BUILDING_PLACED: Whether to recolor the queue of buildings placed in Lua
  
## Help, Bug Reports and Feature Requests

We can be reached through various ways:

*[Create an issue on GitHub](https://github.com/Myll/Dota-2-Building-Helper/issues/new)
* At irc.gamesurge.net [#dota2mods & #dota2modhelpdesk](https://kiwiirc.com/client/irc.gamesurge.net/?#dota2mods,#dota2modhelpdesk)
* At [moddota.com](https://moddota.com/forums/), throught the dedicated [Tools subforum](https://moddota.com/forums/categories/tools)

## Contributing

Contributing to this repo is absolutely welcomed. Building Helper's goal is to make Dota 2 a more compatible platform to create RTS-style and Tower Defense mods. It will take a community effort to achieve this goal.

If you implement any fix or feature you'd like to see it included in this library, make a pull request or make an issue with the necessary script changes.

## Credits

* [Myll](https://github.com/stephenfournier), original dev
* [BMD](https://github.com/bmddota), helped figure out how to get mouse clicks in Flash. Made the particles in BH.
* [Perry](https://github.com/perryvw), contributed to the old scaleform version
* [zed](https://github.com/zedor), contributed with old scaleform
* [snipplets](https://github.com/snipplets/), first panorama implementation and queue system
* [Noya](https://github.com/MNoya), new release, updates and maintenance

## Notes

If you're a new modder we highly recommend forking a new starter addon using [D2ModKit](https://github.com/Myll/Dota-2-ModKit) program.

## License

Building Helper is licensed under the GNU General Public license. If you use Building Helper in your mod, please state so in your credits.
