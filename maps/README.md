All the entities BSPSource missed were manually recovered from each entity lump.

All have been tested for VBSP to successfully compile, just note that a couple may take a while at the "Building Physics collision data..." stage.

Most have been confirmed working with VVIS, but note that they may take a long time or stall at 99% -- but will eventually finish.

Beyond automated or batch-processed fixes, some edits were applied manually. Several gamebreaking bugs that restrict movement throughout the maps were fixed, such as broken ladders or clips that failed to decompile well.

The "cross-section grid planes" are the only mystery -- but ALL have been deleted to allow free movement around each of the maps. As for why they wre present is anyone's guess. Maybe they were reference markers for the mapper to assess space or scale. Or, similar to how the ladders decompiled with all sides as toolsinvisible, maybe it was some TI-only tool brush that had a collision property, or some other special tool that was compiled into the BSP but never meant to be interpreted in a decompile.

Checksums for the Official Originals that were decompiled with BSPSource v1.4.1, in case your build of TI differs.

Over 12k entities fixed, non-destructive, and objective.

	Bytes		CRC32		Mapname			Number of repaired entities

	184356		BA3B3D66	game_intermission.bsp	nothing
	48300336	4DE2EF9A	int_uprising.bsp	153
	73812340	865AAA5E	mis_airport.bsp		196
	97076976	B7DA9400	mis_castalla.bsp	303
	42010104	681E4F8C	mis_classicmall.bsp	706 + changed areadoor6
	57306144	26846BE8	mis_construction.bsp	605
	139164132	A3C5AA76	mis_highway.bsp		1582
	125517444	C41D92F0	mis_innercity.bsp	994
	84716468	B38C3670	mis_mall.bsp		892
	96393152	A2622F79	mis_milan.bsp		276
	31176228	E34A7A6A	mis_monaco.bsp		1606
	20732892	3C4AB5AE	mis_monaco_2014.bsp	nothing
	87304196	7E0440DB	mis_morningcalm.bsp	199
	43989328	A11EEEEA	mis_office.bsp		499
	123472708	B39AB16E	mis_skyrise.bsp		1215
	59642704	5CED27CE	mis_skytrain.bsp	771
	47898568	0F60260A	mis_uprising.bsp	162
	72151588	70FE4D3B	mis_villa.bsp		832
	43492448	33325E49	ti_tdm_01.bsp		232
	41885452	0B5802AB	ti_tdm_02.bsp		60
	62992012	399D3238	ti_tdm_03.bsp		nothing
	43462032	132ED002	ti_tdm_04.bsp		58
	80241540	4188E809	ti_tdm_05.bsp		825
	52824112	99D43734	ti_tdm_06.bsp		nothing

Test embed:

![Image](https://raw.githubusercontent.com/Tsuey/Tactically-Decompiled/main/documentation/images/game_intermission_01.png)

Tested.