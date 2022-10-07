# Tactically-Decompiled

The files on this repo are strictly for educational use.

Tactical Intervention was free to play and, outside of those who had claimed it on Steam, is no longer officially distributed. Those who did not have the chance to claim the game, have no choice but to launch it independent from Steam.

It's suspected the game was built off Portal 2's branch, but CVAR_LIST.TXT does show a "L4D2C5" reference.

Most of the modder's toolset, such as simple things like nav_edit, can only be used if its binaries are edited.

While the map encryption is no problem for BSPSource, TI devs erroneously (or deliberately) have extra nulls in the entity lump which causes BSPSource to miss 100's of critical entites per map.

For binaries relevant to the study of strings and CVAR flags, this repo contains very lossy Ghidra decompiles under the following setup:

	1. CodeBrowser -> Edit -> Tool Options -> Decompiler -> Analysis -> UNCHECK "Eliminate unreachable code"

	2. Used AutoHotkey with "Next Non-Function Ctrl+Alt+N" to recover 1000's of functions that weren't in earlier exports

	3. Headers created for each with "Function Tags" included

And the map decompiles have been fixed so every single map entity is now present.
