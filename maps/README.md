Folder "MANUAL_REPAIRS" is the one you want -- a fixed and proper modder pack. VBSP and VVIS compiles are guaranteed, with VRAD quickly tested for most.

Note that the "Clips -> Player" VisGroup needs to be UNCHECKED for a successful compile on both "mis_highway" and "ti_tdm_02" -- the fixed 12k entities were all objective and non-destructive, so things still aren't flawless since large amounts of clipping is corrupt on just these 2 maps:

![Image](https://raw.githubusercontent.com/Tsuey/Tactically-Decompiled/main/documentation/images/mis_highway_02.png)
![Image](https://raw.githubusercontent.com/Tsuey/Tactically-Decompiled/main/documentation/images/ti_tdm_02.png)

The BSP inputs for all the BSPSource 1.4.1 "RAW_DECOMPILES" have these file sizes and CRC32's:

	Bytes		CRC32		Mapname			Number of repaired entities

	184356		BA3B3D66	game_intermission.bsp	nothing (flawless)
	48300336	4DE2EF9A	int_uprising.bsp	153
	73812340	865AAA5E	mis_airport.bsp		196
	97076976	B7DA9400	mis_castalla.bsp	303
	42010104	681E4F8C	mis_classicmall.bsp	706 + changed areadoor6
	57306144	26846BE8	mis_construction.bsp	605
	139164132	A3C5AA76	mis_highway.bsp		1582 (UNCHECK "Clips -> Player" VisGroup)
	125517444	C41D92F0	mis_innercity.bsp	994
	84716468	B38C3670	mis_mall.bsp		892
	96393152	A2622F79	mis_milan.bsp		276
	31176228	E34A7A6A	mis_monaco.bsp		1606
	20732892	3C4AB5AE	mis_monaco_2014.bsp	nothing (flawless)
	87304196	7E0440DB	mis_morningcalm.bsp	199
	43989328	A11EEEEA	mis_office.bsp		499
	123472708	B39AB16E	mis_skyrise.bsp		1215
	59642704	5CED27CE	mis_skytrain.bsp	771
	47898568	0F60260A	mis_uprising.bsp	162
	72151588	70FE4D3B	mis_villa.bsp		832
	43492448	33325E49	ti_tdm_01.bsp		232
	41885452	0B5802AB	ti_tdm_02.bsp		60 (UNCHECK "Clips -> Player" VisGroup)
	62992012	399D3238	ti_tdm_03.bsp		nothing (flawless)
	43462032	132ED002	ti_tdm_04.bsp		58
	80241540	4188E809	ti_tdm_05.bsp		825
	52824112	99D43734	ti_tdm_06.bsp		nothing (flawless, except "water_lod_control")

"MISSING_AND_FIXED_ENTITIES_PASTED_INTO_RAW_DECOMPILES.TXT":

	Final file before everything was carefully copied into the VMF's.

"MISSING_AND_FIXED_ENTITIES_SORTED_REPORT.TXT":

	Report of missing entities that was used to isolate them from the BSP.

"REPORT_OF_ALL_MAP_ENTITIES_FROM_MANUAL_REPAIRS.TXT":

	Every single entity (including the missing ones) in the repaired VMF's.

"REPORT_OF_ALL_MAP_ENTITIES_FROM_RAW_DECOMPILES.TXT":

	Every single entity (excluding the missing ones) in the decompiled VMF's.

BSPSource settings for World, Entities, Entity mapping, and Textures were all left at defaults. Debug mode isn't going to be informative here as it's largely just redundant brush info. Loaded from *.LMP files (even though there aren't any), and created VisGroups and Cameras. Set "BSP format" explicitly to "Tactical Intervention" and left "VMF format" at Automatic (Source 2004-2009 is old so probably auto's to 2010+). Yes to "Extract embedded files". No to "Smart extracting".

# Overview

In order to fix the BSPSource decompiles, I originally suspected that the null character in lump 0 entities was to blame:

![Image](https://raw.githubusercontent.com/Tsuey/Tactically-Decompiled/main/documentation/images/study_01_nullfail.png)

While the null character feels like decompile protection, it's very consistent that the entities after the null are client-side or TI-specific, as if they were "tacked on" with an unknown in-house tool.

To be absolutely sure, I took all BSPSource VMF decompiles and created a report of all entities within, then removed all prop_static, env_cubemap, func_detail, func_ladder, info_lighting, and info_overlay from those reports -- because all of those are compiled fully or partially into independent lumps 1-63. I knew that the raw BSP files had all the correct lump 0 entities, so I manually extracted exclusively that section of the BSP file to yield only plaintext -- then I created a report of those entities, too. Finally, the VMF report was compared to the BSP report to find all entities that were missing.

A total of 12,159 entities were missing because of the null character, plus an unrelated 7 "info_overlay_accessor" that I would've missed if I had saved time and acted only on my original suspicion.

For purposes of easily identifying all 7 "info_overlay_accessor" (all "material overlays/bomb_site-1"):

	int_uprising

	"origin" "610 2330 -76"		"targetname" "alleymarker"	"hammerid" "825201"
	"origin" "-165.798 344.154 24"	"targetname" "compressormarker"	"hammerid" "729351"

	mis_morningcalm

	"origin" "2523.55 -299.979 -81"	"targetname" "stage2marker"	"hammerid" "6849868"

	mis_uprising

	"origin" "610 2330 -76"		"targetname" "alleymarker"	"hammerid" "825201"
	"origin" "-165.798 344.154 24"	"targetname" "compressormarker"	"hammerid" "729351"
	"origin" "-1833 1098 32"	"targetname" "portmarker"	"hammerid" "729321"
	"origin" "-1766 3905 39"	"targetname" "towermarker"	"hammerid" "729398"

While the final count of missing entities is 12,166 (12,167 if counting the below portal), all decompiled func_ladder were broken (they need to be func_detail with all non-climbable sides invisible), some brushes became bugged that made it impossible to compile or navigate, and "areadoor6" modified. So, the final count of total fixes is much higher, and will continue to grow with `maps_mods` updates.

![Image](https://raw.githubusercontent.com/Tsuey/Tactically-Decompiled/main/documentation/images/study_04_ladderlads.png)

Map's "mis_classicmall" case of "areadoor6" involves a missing "func_areaportal" with ID "1433568", and out of all decompiles is an isolated occurrence of a brush being missed completely:

	"portalnumber" "31"
	"target" "areadoor6"
	"StartOpen" "0"
	"PortalVersion" "1"

Which belongs to this "prop_door_rotating" (ID "1136556"):

	"origin" "-1150 -411.66 912"
	"targetname" "areadoor6"
	"skin" "0"
	"model" "models/props_doors/door-4.mdl"

Instead of building 2 replacement brushes and dealing with nearby HINT/SKIP conflicts, it felt like the best solution was to add a window to the door itself ("door-5.mdl") and change from red ("skin 0") to gray ("skin 1") to match a nearby identical door.

Lastly, the second biggest issue was the "cross-section grid planes" cordoning off most maps. Several per-map screenshots are provided below. These are all the tool brushes that ship with the game:

![Image](https://raw.githubusercontent.com/Tsuey/Tactically-Decompiled/main/documentation/images/study_05_toolsa.png)
![Image](https://raw.githubusercontent.com/Tsuey/Tactically-Decompiled/main/documentation/images/study_06_toolsb.png)

While it is possible that BSPSource failed to convert the geometry into some un-heard-of brush, they don't follow the logic of HINT/SKIP or any other brush, and seem arbitrary and inconsistent dependent on the map. They often decompiled into CLIP brushes, but often one side had a different material, and in any case these planes were always solid. This made the majority of maps unwalkable since you'd spontaneously run or drive into a solid wall, usually invisible but not always. All of them were deleted, as the only necessary destructive step to fix the maps.

# Details

8 maps have "water_lod_control" entities with no "hammerid", thus automatically compiled in since the mapper missed them:

	mis_castalla
	mis_highway
	mis_mall
	mis_skytrain
	mis_villa
	ti_tdm_02
	ti_tdm_04
	ti_tdm_06

Absolutely every single other entity has a "hammerid" and they match across BSP lump 0 and VMF decompile.

All 46 (technically 45 since "func_areaportal" is a fluke) entity classnames that BSPSource ALWAYS misses, most of them client-side or TI-specific:

	env_sprite_clientside
	func_areaportal
	info_ammo_box_spawn
	info_car_spawn
	info_heli_CT_spawn
	info_heli_TER_spawn
	info_heli_supply_drop
	info_hostage_spawn_1
	info_hostage_spawn_2
	info_hostage_spawn_3
	info_hostage_waypoint_1
	info_hostage_waypoint_2
	info_hostage_waypoint_3
	info_oozpoint
	info_overlay_accessor
	info_player_ctstart_1A
	info_player_ctstart_1B
	info_player_ctstart_1C
	info_player_ctstart_2A
	info_player_ctstart_2B
	info_player_ctstart_2C
	info_player_ctstart_3A
	info_player_ctstart_3B
	info_player_ctstart_3C
	info_player_ctstart_A1
	info_player_ctstart_A2
	info_player_ctstart_B1
	info_player_ctstart_C1
	info_player_terroriststart_1A
	info_player_terroriststart_1B
	info_player_terroriststart_1C
	info_player_terroriststart_2A
	info_player_terroriststart_2B
	info_player_terroriststart_2C
	info_player_terroriststart_3A
	info_player_terroriststart_3B
	info_player_terroriststart_3C
	info_player_terroriststart_A1
	info_player_terroriststart_A2
	info_player_terroriststart_B1
	info_portable_blockade
	info_supply_crate_spawn
	info_vehicle_wp
	info_vip_wp
	prop_hitzone
	prop_ragdoll_clientside

Usually the decompile is perfect if the map doesn't have any of these entities.

There is nothing to note or fix regarding "game_intermission".

Both "mis_monaco" and "mis_monaco_2014" don't have any "cross-section grid planes". They are also among the most unfinished maps, and it seems odd that the planes would be added for scale/reference later on in development... so there's still no answer for them.

![Image](https://raw.githubusercontent.com/Tsuey/Tactically-Decompiled/main/documentation/images/both_monaco_01.png)

Both "int_uprising" and "mis_uprising" had the same errors with clips corrupted enough to completely block movement, so those were deleted.

![Image](https://raw.githubusercontent.com/Tsuey/Tactically-Decompiled/main/documentation/images/both_uprising_01.png)
![Image](https://raw.githubusercontent.com/Tsuey/Tactically-Decompiled/main/documentation/images/both_uprising_02.png)

Map "mis_airport" shows the failed ladder decompiles (as func_ladder with toolsinvisible on all sides) and "cross-section grid planes".

![Image](https://raw.githubusercontent.com/Tsuey/Tactically-Decompiled/main/documentation/images/mis_airport_01.png)
![Image](https://raw.githubusercontent.com/Tsuey/Tactically-Decompiled/main/documentation/images/mis_airport_02.png)

Map "mis_castalla" had the grid planes.

![Image](https://raw.githubusercontent.com/Tsuey/Tactically-Decompiled/main/documentation/images/mis_castalla_01.png)

Map "mis_classicmall" also had them, which blocked passage through hallways.

![Image](https://raw.githubusercontent.com/Tsuey/Tactically-Decompiled/main/documentation/images/mis_classicmall_01.png)

Map "mis_construction" has dynamic "func_brush" ladders that were duplicated at the origin, luckily outside of the map so I simply left the duplicates in. The grid planes were textured on one side, and CLIP on the other.

![Image](https://raw.githubusercontent.com/Tsuey/Tactically-Decompiled/main/documentation/images/mis_construction_01.png)
![Image](https://raw.githubusercontent.com/Tsuey/Tactically-Decompiled/main/documentation/images/mis_construction_02.png)

Map "mis_highway" has a memey ladder up to nowhere that could've been artistic vision for all I know considering the game's other jank, so that was left in. "Bad detail brush side" requires that the "Clips -> Player" VisGroup be UNCHECKED or else the compile will fail. Grid planes were by far the worst on this map. Also corrupted clipping was deleted, its purpose very unclear and allowed one to walk in the air.

![Image](https://raw.githubusercontent.com/Tsuey/Tactically-Decompiled/main/documentation/images/mis_highway_01.png)
![Image](https://raw.githubusercontent.com/Tsuey/Tactically-Decompiled/main/documentation/images/mis_highway_02.png)
![Image](https://raw.githubusercontent.com/Tsuey/Tactically-Decompiled/main/documentation/images/mis_highway_03.png)

Map "mis_innercity" will, unlike other maps, take 3++ minutes at the "Building Physics collision data..." compile stage. Grid planes blocking random roads.

![Image](https://raw.githubusercontent.com/Tsuey/Tactically-Decompiled/main/documentation/images/mis_innercity_01.png)

Map "mis_mall" has grid planes, but this is what I meant by them feeling arbitrary and inconsistent.

![Image](https://raw.githubusercontent.com/Tsuey/Tactically-Decompiled/main/documentation/images/mis_mall_01.png)

Map "mis_milan", again, just begs the question "why?" when it comes to these "grid planes".

![Image](https://raw.githubusercontent.com/Tsuey/Tactically-Decompiled/main/documentation/images/mis_milan_01.png)

Map "mis_morningcalm" has no grid plane in the way of movement, but all were deleted anyway.

![Image](https://raw.githubusercontent.com/Tsuey/Tactically-Decompiled/main/documentation/images/mis_morningcalm_01.png)
![Image](https://raw.githubusercontent.com/Tsuey/Tactically-Decompiled/main/documentation/images/mis_morningcalm_02.png)

Map "mis_office" was mostly clean.

![Image](https://raw.githubusercontent.com/Tsuey/Tactically-Decompiled/main/documentation/images/mis_office_01.png)

Map "mis_skyrise" features one dynamic "func_brush" ladders that was duplicated at the origin, a playable space that needed to be fixed.

![Image](https://raw.githubusercontent.com/Tsuey/Tactically-Decompiled/main/documentation/images/mis_skyrise_01.png)
![Image](https://raw.githubusercontent.com/Tsuey/Tactically-Decompiled/main/documentation/images/mis_skyrise_02.png)

Map "mis_skytrain" has more grid planes.

![Image](https://raw.githubusercontent.com/Tsuey/Tactically-Decompiled/main/documentation/images/mis_skytrain_01.png)

Map "mis_villa" has more dynamic ladders duplicated but they're outside of the map. Grid planes uniquely blue.

![Image](https://raw.githubusercontent.com/Tsuey/Tactically-Decompiled/main/documentation/images/mis_villa_01.png)
![Image](https://raw.githubusercontent.com/Tsuey/Tactically-Decompiled/main/documentation/images/mis_villa_02.png)
![Image](https://raw.githubusercontent.com/Tsuey/Tactically-Decompiled/main/documentation/images/mis_villa_03.png)

Map "ti_tdm_01" is more grid planes.

![Image](https://raw.githubusercontent.com/Tsuey/Tactically-Decompiled/main/documentation/images/ti_tdm_01.png)

Map "ti_tdm_02" throws "Bad detail brush side" and requires that the "Clips -> Player" VisGroup be UNCHECKED or else the compile will fail.

![Image](https://raw.githubusercontent.com/Tsuey/Tactically-Decompiled/main/documentation/images/ti_tdm_02.png)

Map "ti_tdm_03" is normal -- TDM maps are mostly just earlier versions of the main maps.

![Image](https://raw.githubusercontent.com/Tsuey/Tactically-Decompiled/main/documentation/images/ti_tdm_03.png)

Map "ti_tdm_04" is normal.

![Image](https://raw.githubusercontent.com/Tsuey/Tactically-Decompiled/main/documentation/images/ti_tdm_04.png)

Map "ti_tdm_05" had grid planes.

![Image](https://raw.githubusercontent.com/Tsuey/Tactically-Decompiled/main/documentation/images/ti_tdm_05.png)

Map "ti_tdm_06" had bad grid planes.

![Image](https://raw.githubusercontent.com/Tsuey/Tactically-Decompiled/main/documentation/images/ti_tdm_06.png)