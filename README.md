# FE8U_SoundRoomBG
For displaying different backgrounds in the sound room. FE8U only.

# Install
This patch is for FE8U! I don't recommend using the patch if you're using FEBuilder, although you can still.

- Buildfile users: Install by using Event Assembler to apply "SoundRoomBG.event" to your ROM, or include "SoundRoomBG.event" in your buildfile.
  
- FEBuilder users: "Advanced Editors"->"Insert EA"->"Select File". Pick "SoundRoomBG.event" and press "Load Script".

# Whatitdo?
This patch adds the option to display different backgrounds in the sound room based on which song is currently playing. It's possible to have multiple backgrounds display consecutively (with 5 second pauses before transitioning to the next background) or a single background only. Whilst in the soundroom, press L to hide the UI. Press any button to display the UI again.

# Customization
## songBGStructs
In [Structs/Structs.event](https://github.com/Huichelaar/SoundRoomBG/blob/main/Structs/Structs.event) you'll find two macros:
  - SBG_SongBGListEntry(songID, songBGStruct) where songBGStruct is a pointer to an instance of the other macro. There's a list of these called songBGList. An instance of this macro indicates which backgrounds should be displayed for a given songID. If a songID is not in the songBGList (terminated by two "0" words) the default scrolling relief will be displayed.
  - SBG_SongBGStructEntry(label, BGTiles, BGPalette, next). These indicate which background to display and are used as entries to a linked list. After the background has been displayed for five seconds, the next songBGStruct is used by following the "next" pointer. You can use the label argument of a songBGStruct as an argument to a (possibly different) songBGStruct's "next" argument.

As an example I've made a songBGStruct looping through two screenshots I made of FE7U used for songID 1 and 3, and another songBGStruct displaying one screenshot of FE6 used for song 2.

## Adding backgrounds
Backgrounds are displayed in 256-colour mode. The first two background palettes are used by BG0-BG2 so you can't use those in your backgrounds, leaving you with 224 colours. If you want to add more backgrounds and you're using Png2Dmp, keep in mind you need to feed it a 480x160 representation of a 240x160 image as each 256-colour pixel is represented by two 16-colour pixels. You can use FEBuilder and a clean FEGBA ROM to convert a 256-colour 240x160 image to an 8bpp 480x160 representation. The final image needs to be LZ77-compressed.

# Concluding
12/9/2021
This was a fun and quick project. It's a shame it's the type of feature that'll eat a lot of ROM. Gotta have them nostalgic backgrounds though.

~Huichelaar