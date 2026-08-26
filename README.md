# UNOFFICIAL OoTMM for Archipelago

Play OoTMM, which merges Ocarina of Time and Majora's Mask into one game, as
an Archipelago multiworld. Roughly 3,500 checks depending on settings, and
nearly every OoTMM setting is available.

apworld v1.1.4, generation kit v1.1.0.

## What you need

Archipelago 0.6.7 or later. RetroArch with the mupen64plus-next core. Clean
OoT (NTSC 1.0) and MM (US) ROMs. No ROM data is included here.

In RetroArch, set `network_cmd_enable = "true"` and turn cheevos hardcore mode
off, since it blocks the memory writes the client needs.

## Setup

Put `ootmm.apworld` in your Archipelago `custom_worlds` folder. Unzip the
generation kit, then put your two ROMs in its `roms/` folder as `oot.z64` and
`mm.z64`. The kit's SETUP.md has the longer walkthrough.

## Playing a seed

Generate as normal and download your `.apootmm` from the room page. Drag it
onto `Generate-From-AP-Export.bat` to get your ROM. Load that in RetroArch,
then open the OoTMM Client from the Archipelago launcher and connect. Load a
save file and items start flowing.

Generation takes a few minutes. The last step compresses the ROM and prints
nothing while it works, so give it time before assuming it hung.

## Client commands

`/breakables [text]` lists breakable checks the server says you are missing.

`/repair confirm` makes lost breakable checks respawn.

`/regrant_keys confirm` re-sends dungeon keys, maps and compasses.

`/resync` reattaches to the ROM and rebuilds the item list.

`/victory` reports goal completion by hand.

The first two exist because of bugs that could lose checks. Both are fixed
now, but neither fix recovers what was already lost. Back up your save before
running either one.

## Known issues

Entrance rando is not supported. All 44 `er_*` settings are unavailable. The
wiring works, but only about one seed in three places successfully, so it
stays out until that improves.

A few settings can hit OoTMM's own limits and fail with "more items than
places". Plentiful item pool, both soul categories at once, and song notes on
a normal sized seed are the usual causes. Add more checks or turn one off.

Dungeon maps and compasses from other players may still land wrong. Keys are
fixed. Maps and compasses share the same bug, and the fix does not reach them
yet because Archipelago names them differently than OoTMM does.

## How it works

The apworld builds the logic and picks the placements, then writes a
`.apootmm` file. The kit hands those placements to OoTMM's own generator and
patches your ROMs. The client watches a mailbox in the game's memory. The game
writes there when you find something, and the client writes there when someone
sends you something.

Both games' logic comes from OoTMM's own data, so seeds play the way OoTMM
says they should.

## One ROM, not two

The kit builds a single ROM. Older versions built two, because offworld checks
needed a second player to belong to. That dummy world is gone and offworld
checks are marked as another player's directly, which halves generation time
and removes the item limits the second world caused.
`Generate-TwoWorld-Legacy.bat` is still there, but it cannot handle large
asyncs.

## Reporting a bug

Send the client log and the kit version, which prints on every run as
something like `OoTMM AP kit v1.1.0 (single-world)`. If a check went missing,
say which one and how you broke it.

## Credits

OoTMM by Nax and contributors: https://github.com/OoTMM/OoTMM

Archipelago integration by LUGAWI. (discord: @drlugawi7001)
