# TDA's Single File HTML Quake 1 Random Map Generator

This is it! A single-file, browser-based procedural map generator for the original Quake that lets you crank out solid, playable deathboxes with the click of a button. No installation, no servers, no dependencies. Just pure map-making chaos.

This project was forged in the fires of "vibe coding" by **TDA317** over a month of intense collaboration with AI models from across the grid (ChatGPT, Qwen, and Gemini). The critical, show-stopping bugs in the geometry pipeline were finally stomped out by Google's Gemini 2.5 Pro, channeling the combined might of John Carmack and John Romero to make the damn thing *work*.

You may think "Vibe coding? Oh, he just put in a couple prompts and the AI spit it out." 
If you think it is that easy, try!

There is well over 40hrs of actual work with multiple false starts and ventures down wrong baths trying to fix bugs and get it workiing this well. And that was just the first Alpha. Tons of creating maps, opening them in Trenchbroom, wandering around looking for what is broken, explaining the issues to the AI, trying again, repeating, over and over. Tens of millions of tokens used (glad I'm not paying for it) filling up Gemini's 1million token context window dozens of times as well as ChatGPT's 'memory' and hitting it's daily free limits. Qwen's coder is good but still seems to lag behind the paid models. 

## Current Status: ALPHA

This is an early, alpha release. The machine is stable, but it's not finished. Here's the deal:

*   **It Makes Solid Maps!** The generator creates simple but architecturally sound levels that, with one major exception, seal properly and are ready to compile.
*   ~~**The SKY is the VOID!** The big caveat: The generator does not currently create skyboxes. Courtyard areas will have openings straight to the void. This is the top priority for the next major feature update. For now, you can either enjoy the brutalist, open-roof aesthetic or build your own skybox around the level in an editor to get it to properly VIZ.~~
*   **Single Player Focused:** Light and entity placement is functional but very basic. ~~There are no `trigger_changelevel` entities to end a map and no deathmatch starts have been implemented, though adding them is trivial.~~
*   **Lots of Knobs to Turn:** The GUI provides a ton of options for controlling the map's dimensions, room count, verticality, and entity population. Go wild.

Issues:
*   **Z-Fighting:** Textures overlap places. Occasionally you'll see a little bit of sky peaking through places it shouldn't because of this. I had worked on it for this version but rolled back due to some repeated issues. Will address again later
*   ~~**Lighting:** Lighting is place holder at best. Next thing to be addressed.~~
*   **Entities:** Sometimes entities/spawn points will clip into walls or stairs. Its much improved but still not perfect. **Fixed again, again, again**
*   **Geometry:** Being that this is random, some impossible geometry and architecture is made. Large rooms next to a courtyard where you'd definitely see the large room's outside walls over the courtyard wall, etc. and sometimes impassible obstacles. If you go beyond the default vertical variation, the ability to go from room to room quickly falls apart. Can be helped by making the minimum ceiling heights larger too, but there are limits.

## Alpha v 1.085 notes:
*   **Improved item and enemy placement**
* Major overhall of entity placement, stairs placement is much improved. Still edge case errors but they are much more edge case than ever before. 
* Smarter spot-finding with bounding box and checks of what is under feet.
* "Fixed" the "End Alter" and item podiums to not be floating if placed on stairs.
* Better info_intermission and _sun light handling
* Texture Z-Fighting issues greatly reduced by a few architectural tweaks. Main remaining issue are direct room to courtyard indoor/outdoor wall joints.

## Alpha v 1.080 notes:
*   **Improved item and enemy placement**
* Last version more logically placed things in the space. But, items and enemies would get stuck in stairs sometimes. This brute force fixes that by dropping them from higher up. 
*   **LIGHTS**
* Place holder "one light per room" lighting is gone. Now, we have some lighting themes to choose from. Normal, Murky, Dramatic (more flashing lights), and Blackout (very dark has some very low level lights scattered around)
* Early theme support added with light improvements. Normal, Murky, Dynamic, and Blackout for indoor, Normal, Bright Sun, and Dim Night themes for outdoor/skybox areas. 
* Outdoor lights set with a light with the added _sun property and target suntar. An info_null with targetname : suntar placed randomly below it.
*   **Architecture and world sealing**
* Some architectural elements removed. Drop ceilings and ceiling openings over liquid pools being most notable. Both started as bugs and were left in for architectural interest. But, lead to issues sealing the world and with player 'head clearance'
* Improved checking for player's 'head clearance' when moving to rooms of different elevations. Stairs and clearance issues still quickly become issues as you increase vertical variation values beyond default.
* More often than not, the world will actually be sealed. Almost always at default settings.

## Alpha v1.064 notes:
*   **Improved item and enemy placement**
* The last version left a lot of room for improvement. Lots of things clipped in walls and floors. It is much improved but still not perfect.
* Fish are ACTUALLY in the water. 
* Check box in GUI to enable "major items on pedistals" places a brush under armor, power ups, and a few weapons as well as a light at the center of the object. Adds a bit of focus and specialness to these otherwise randomly placed items.
*   **Skyboxes**
* Not perfect, but skyboxes are actually implemented and working. At default settings, it will produce properly sealed maps.
*   **Single player**
* There is a proper functional end of map for single player. Points at start.bsp 
* Randomly placed intermission camera. Supposed to pick one of the larger rooms and place it there. But, currently has no real focus of interest otherwise.


## Alpha v1.051 notes:
*   **Improved item and enemy placement**
* Before, things were simply placed inside the map. Now, health and ammo boxes are placed along walls. You'd never believe the trouble I had getting the .bsp model items to be properly spaced from the walls (The AI just wasn't getting it)
* Fish in water, other enemies on land. Shamblers shouldn't get stuck in walls or low ceilings. Its not 100% but it is MUCH improved. 
*   **Game modes** 
* Single player actually has an end. A start room is forced to be placed in the first 5% of the X axis. An end room with an alter containing a trigger_changelevel going nowhere is on the opposite 5% of the map. The rest of the map is built between.
* Co-op spawns are right there with Single Player.
* Deathmatch spawns are spread out as much as logically possible.
*  **More Textures**
*   Added a few more wads from **Aleksander "Mar-san" Marshall's Prototype WAD** It's recommended you add all his textures to the wad because I plan to add more as features creep.
*   **GUI Improvements**
*   Proper seeds. "Forge World" randomizes geometry. "Place Entities" randomizes entities. Two user input seed spaces (one for each) and a "Forge From Seeds" button to build from the current/user's seeds.
*   Simple key with status indicator added to right. Preview resizes to browser window.
*   Too many changes to list. Lots of default values tweaked. And much more you may never notice.

## How to Use

1.  Download the `.html` file and open it in any modern web browser.
2.  Tweak the settings in the left-hand panel.
3.  Click **"Generate New Layout"** to create the architecture.
4.  Click **"Place Entities"** to populate it with monsters and items.
5.  Click **"Download .map File"** and save it.
6.  Compile your map with your favorite Quake tools!

### **IMPORTANT: Texture Dependency**

This generator is currently hard-coded to use textures from **Aleksander "Mar-san" Marshall's Prototype WAD**. It's a fantastic toolkit for getting a clean, readable look.

*   **You can download it here:** [Prototype WAD on Slipseer](https://www.slipseer.com/index.php?resources/prototype-wad.263/)

After downloading the `.map` file, you MUST edit the `worldspawn` entity to point to the location of your WAD file. Change this line:
"wad" " "
To this:
"wad" "C:\path\to\your\wads\prototype_basic_1_3.wad; C:\path\to\your\wads\prototype_liquids_1_3.wad; C:\path\to\your\wads\prototype_Skies_1_3.wad"


### Under the Hood

This generator is **100% vanilla JavaScript**. There are no external frameworks or libraries like `p5.js` or `jQuery`. It's a completely self-contained tool, designed to be lean, fast, and portable.

## Designer Notes from TDA317

*   `Vertical Variation` is the secret sauce. It's a 2D generator faking a 3D feel by shifting rooms up and down. Keep it reasonable; extreme settings can create cool-looking but unplayable maps.
*   My preferred settings for a big, classic-feeling map:
    *   Map Width/Height: `4096`
    *   Cell Size: `64`
    *   Room Count: `~20-25`
    *   Max Room Size: `~15`

## The Roadmap

The goal is to make this thing even better. The future holds:

*   More detailed and interesting architectural variations.
*   A proper theming system to support texture sets for **Base**, **Castle**, and **Runic** styles.
*   Potential support for community texture WADs (like `ikbase`).
*   Smarter, more deliberate entity and light placement.

## License

This is for the community.

*   **The Generator:** Do whatever you want with this `.html` file. If you modify it and release your own version, giving credit is required!
*   **The .map Files:** Any `.map` you generate is **100% yours**. Do anything you want with it. If you build something amazing and release it commercially, that's AWESOME! Let me know, I'd love to see it.
