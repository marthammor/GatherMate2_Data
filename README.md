# Anatomy of the datafile

Sample FishData.lua

```lua
GatherMateData2FishDB = {
    [ZONE_ID] = {
        [COORDINATES] = NODE_ID,
    }
}
```

`ZONE_ID` - can be found in-game by typing `/dump C_Map.GetBestMapForUnit("player")` in the chat.  This is the same zone id that the TomTom addon uses with their `/way` command.

`COORDINATES` - In `XXXXYYYY00` format.  Always 10-digits long.  Use zeros as a buffer.  Example: If you have a coordinate of 64.3 59.8, the coordinate value would be `6430598000`.  If you have a coordinate of 58.39 31.41, the coordinate value would be `5839314100`

`NODE_ID` - As defined by the [GatherMate2](https://www.curseforge.com/wow/addons/gathermate2) addon in the `GatherMate2\Constants.lua` file.

## Example

There's a `Prismatic Leaper` node in `Ohn'ahran Plains` at location 64.3, 59.8.

```lua
GatherMateData2FishDB = {
    [2023] = {
        [6430598000] = 1117,
    }
}
```

There's also `Prismatic Leaper` node in `The Azure Span` at 30.4, 25.0.

```lua
GatherMateData2FishDB = {
    [2023] = {
        [6430598000] = 1117,
    },
    [2024] = {
        [3040250000] = 1117,
    }
}
```

## Tips for populating data from WoWHead

1. Lookup the object/node you care about on wowhead and has the map indicating where to find it.

    [Prismatic Leaper](https://www.wowhead.com/item=200061/prismatic-leaper) on WoWHead

2. Click the pin on the map, and then click `Copy All -> TomTom Command`

    When you paste, you'll get something that looks like this:

    ``` text
    /way #2023 56.4 80.4 Prismatic Leaper
    /way #2023 56.4 80.5 Prismatic Leaper
    /way #2023 56.5 80.4 Prismatic Leaper
    /way #2023 56.5 80.5 Prismatic Leaper
    /way #2023 58.3 31.7 Prismatic Leaper
    /way #2023 58.4 31.4 Prismatic Leaper
    /way #2023 58.5 31.4 Prismatic Leaper
    /way #2023 58.5 31.5 Prismatic Leaper
    /way #2023 61.5 82.3 Prismatic Leaper
    /way #2023 64.3 38.5 Prismatic Leaper
    /way #2023 64.4 38.2 Prismatic Leaper
    /way #2023 64.6 38.3 Prismatic Leaper
    /way #2023 64.6 38.7 Prismatic Leaper
    /way #2023 86.2 51.9 Prismatic Leaper
    ```

3. Then use your preferred method to then translate those coordinates into entries to include in FishData.lua.  Don't forget to look up the constant for "Prismatic Leaper" in the `GatherMate2\Constants.lua` file.
