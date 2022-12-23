# Tactically-Decompiled

![Image](https://raw.githubusercontent.com/Tsuey/Tactically-Decompiled/main/documentation/images/game_intermission_01.png)

The files on this repo are strictly for educational use.

This repo contains very lossy Ghidra decompiles that are useless beyond the scope of this repo. Map decompiles, and fixes of map decompiles, are common and expected when it comes to Source games.

Tactical Intervention was free to play and, outside of those who had claimed it on Steam, is no longer officially distributed. Those who did not have the chance to claim the game, have no choice but to launch it independent from Steam.

Most of the modder's toolset, such as simple things like `nav_edit`, can only be used if its binaries are edited.

While the map encryption is no problem for BSPSource, TI devs erroneously (or deliberately) have extra nulls in the entity lump which causes BSPSource to miss 100's of critical entites per map.

Each folder has a unique README.md with additional context.

	documentation	images for README.md's to use and user-friendly lists
	game		Decompiled game binaries that hold crucial CVAR information
	game_mods	Edited binaries to forcefully enable modder CVAR's
	maps		Decompiled maps that have had 12k+ entities repaired
	maps_mods	Edited maps (beyond the scope of simply repairing entities)