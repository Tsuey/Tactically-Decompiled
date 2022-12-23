It's suspected the game was built off Portal 2's branch, but CVAR's do expose a "L4D2C5" reference.

For binaries relevant to the study of strings and CVAR flags, this repo contains very lossy Ghidra decompiles under the following setup:

	1. CodeBrowser -> Edit -> Tool Options -> Decompiler -> Analysis -> UNCHECK "Eliminate Unreachable Code" (we want everything)

	2. Used AutoHotkey with "Next Non-Function Ctrl+Alt+N" to recover 5000+ UndefinedFunctions that contain crucial CVAR data

		Also known as "Go To Next Instruction Not In a Function". Bind "F" is "Create External Function".

		https://ghidra.re/ghidra_docs/api/ghidra/util/UndefinedFunction.html

		https://github.com/NationalSecurityAgency/ghidra/issues/2507

	3. Headers created for each with "Function Tags" included

Ghidra decompiles align pretty nicely to the open Source SDK code:

![Image](https://raw.githubusercontent.com/Tsuey/Tactically-Decompiled/main/documentation/images/study_02_cvarflags.png)

Note that the error "The Navigation Mesh was built using a different version of this map" should be ignored -- it doesn't prevent the NAV file from working, even if the game's jank sometimes feels like it didn't load. It is not necessary or helpful to make a DLL edit that ignores outdated NAV files, and while the Source SDK does define and set "m_isOutOfDate", it doesn't appear to ever be used.

To snugly fit "client_mapkit.dll.c.txt" under the 25 MB Github limit, all lines containing "this + " (50574 lines total) were deleted -- this is a decompile, all of those lines didn't provide any useful CVAR information even with their context.