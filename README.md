# dsda-doom v0.6.0
This is a fork of prboom+ with extra tooling for dsda.
This is based on the unstable branch of PRBoom+, so there could be bugs - please keep this in mind. :^)

### New Stuff
- Use `-analysis` to write an analysis.txt file with run details.
- Use `-track_pacifist` to enable a "Not pacifist!" message to appear when breaking the category rules.
- Use `-track_100k` to enable a "100K achieved!" message to appear when reaching 100% kills on a map.
- Use `-time_keys` to show a split when you pick up a key.
- Use `-time_use` to show a split when you press the use key.
- Use `-time_secrets` to show a split when you find a secret.
- Use `-time_all` to enable all the split options.
- Use `-export_ghost xyz` to write a ghost file (xyz.gst).
- Use `-import_ghost xyz` to import a ghost file (xyz.gst).

### Ghosts
A ghost follows the life of the player recorded in the ghost file. This can be useful to compare two demos, or to compete against a specific demo while you play. Movies are supported in the sense that they don't cause an error, but a ghost that is "on the next map" will still show up on your current map. Only one ghost is supported for now. Ghosts most likely don't work under conditions where you skip time (warping during demo playback, skipsec, etc). In the future, we will have better handling for movies, multiple ghosts, display options, etc.

### Analysis File
This file contains summary data about a run in key-value pairs.
Current contents:

- `skill`, `1` to `5`.
- `nomonsters`, `1` or `0` (-nomonsters parameter).
- `respawn`, `1` or `0` (-respawn parameter).
- `fast`, `1` or `0` (-fast parameter).
- `pacifist`, `1` or `0`.
- `stroller`, `1` or `0`.
- `reality`, `1` or `0` (no damage taken).
- `almost_reality`, `1` or `0` (only nukage damage taken).
- `100k`, `1` or `0` (100% kills as seen on intermission).
- `100s`, `1` or `0` (100% secrets as seen on intermission).
- `missed_monsters`, monsters left alive (not including icon spawns).
- `missed_secrets`, secrets left uncollected.
- `weapon_collector`, `1` or `0` (`0` if no weapons).
- `tyson_weapons`, `1` or `0` (only pistol, chainsaw, and fist used).
- `turbo`, `1` or `0`.
- `category`, `UV Max`, `NoMo`, etc.

### Category Detection
If multiple categories are detected, the first match in this list is chosen:
UV Max, UV Tyson, Stroller, Pacifist, UV Speed

Example: if you complete UV Tyson on a map and collect all the secrets, the analysis will show UV Max.

Use the extra flags (`pacifist`, `stroller`, `tyson_weapons`) to check the details.

Irrelevant categories for a run are ignored. E.g., you won't see `NM 100S` if a map has no secrets and you won't see `Pacifist` if a map has no monsters.

### PRBoom+ Stuff (since 2.5.1.5 - heavily abridged)
- Fix boom autoswitch behaviour (in some cases running out of ammo forced a specific weapon swap)
- Add mouse code option (classic prboom+ vs chocolate doom)
- Forbid 180 while strafe is on (previously could produce sr50 on turns)
- Add configurable quick start window (simulates different hardware speed)
- Include secret exit format in levelstat (E1M3s instead of E1M3)
- Use `-stroller` to prevent strafing and limit speed (-turbo 50)
- Fix boom rng seed (previously this was hardware dependent and not random)
- Add mouse strafe divisor setting - limit horizontal mouse strafe.