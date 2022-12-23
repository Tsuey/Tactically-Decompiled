File "CVAR_LIST_CONDEBUG.TXT" is all CVAR's dumped through official means, while "CVAR_LIST_DECOMPILED.TXT" is directly from the binaries with additional information that's useful so they can be identified and edited in hexadecimal.

"DUMPENTITYFACTORIES.TXT" contains all the entity classes that exist. "STRINGS_ONLY_SORTED.TXT" is just a lazy collection of all strings in those same binaries.

Version:

	Engine Version: Tactical Intervention - STEAM (MAPKIT)
	Engine Build: 14:42:54 Aug 29 2017 Build Number: 3174
	Fix Game API: 17039616

"cvarlist cvars.txt" doesn't work in TI:

	https://old.reddit.com/r/SourceEngine/comments/3mu4ym/how_do_i_export_a_games_cvar_list_to_a_file_from/

Used launch parameter -condebug which saved "console.log" (changeable with "con_logfile") to:

	C:\Users\Username\Documents\TacticalIntervention\steam

All were dumped by doing "find a" through "find z", then several kinds of different space indentations had newlines removed, everything was Sorted with Duplicate Lines Deleted, and newlines restored with uniform tabs for everything.

Note that in some cases the descriptions cut off which seemed unavoidable and you can see it happening by doing "find cvar" yourself -- other descriptions were never completed by the developer, and any typos such as "preftech" were left as is, and trailing spaces kept just in case they'd someday be useful to further flesh out descriptions for what each of these do.