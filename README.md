# TDA's Single File HTML Quake 1 Random Map Generator

This is it! A single-file, browser-based procedural map generator for the original Quake that lets you crank out solid, playable deathboxes with the click of a button. No installation, no servers, no dependencies. Just pure map-making chaos.

This project was forged in the fires of "vibe coding" by **TDA317** over a month of intense collaboration with AI models from across the grid (ChatGPT, Qwen, and Gemini). The critical, show-stopping bugs in the geometry pipeline were finally stomped out by Google's Gemini 1.5 Pro, channeling the combined might of John Carmack and John Romero to make the damn thing *work*.

You may think "Vibe coding? Oh, he just put in a couple prompts and the AI spit it out." 
If you think it is that easy, try!

There is well over 40hrs of actual work with multiple false starts and ventures down wrong baths trying to fix bugs and get it workiing this well. Tons of creating maps, opening them in Trenchbroom, wandering around looking for what is broken, explaining the issues to the AI, trying again, repeating, over and over. Tens of millions of tokens used (glad I'm not paying for it) filling up Gemini's 1million token context window dozens of times as well as ChatGPT's 'memory' and hitting it's daily free limits. Qwen's coder is good but still seems to lag behind the paid models. 

## Current Status: ALPHA

This is an early, alpha release. The machine is stable, but it's not finished. Here's the deal:

*   **It Makes Solid Maps!** The generator creates simple but architecturally sound levels that, with one major exception, seal properly and are ready to compile.
*   **The SKY is the VOID!** The big caveat: The generator does not currently create skyboxes. Courtyard areas will have openings straight to the void. This is the top priority for the next major feature update. For now, you can either enjoy the brutalist, open-roof aesthetic or build your own skybox around the level in an editor to get it to properly VIZ.
*   **Single Player Focused:** Light and entity placement is functional but very basic. There are no `trigger_changelevel` entities to end a map and no deathmatch starts have been implemented, though adding them is trivial.
*   **Lots of Knobs to Turn:** The GUI provides a ton of options for controlling the map's dimensions, room count, verticality, and entity population. Go wild.

## How to Use

1.  Download the `.html` file and open it in any modern web browser.
2.  Tweak the settings in the left-hand panel.
3.  Click **"Generate New Layout"** to create the architecture.
4.  Click **"Place Entities"** to populate it with monsters and items.
5.  Click **"Download .map File"** and save it.
6.  Compile your map with your favorite Quake tools!

### **IMPORTANT: Texture Dependency**

This generator is hard-coded to use textures from **Aleksander "Mar-san" Marshall's Prototype WAD**. It's a fantastic toolkit for getting a clean, readable look.

*   **You can download it here:** [Prototype WAD on Slipseer](https://www.slipseer.com/index.php?resources/prototype-wad.263/)

After downloading the `.map` file, you MUST open it in a text editor (like Notepad++) and edit the `worldspawn` entity to point to the location of your WAD file. Change this line:
"wad" "QUAKE.WAD"
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

*   **The Generator:** Do whatever you want with this `.html` file for any non-commercial purpose. If you modify it and release your own version, giving credit is appreciated!
*   **The .map Files:** Any `.map` you generate is **100% yours**. Do anything you want with it. If you build something amazing and release it commercially, that's AWESOME! Let me know, I'd love to see it.
