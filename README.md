# downloads-organiser

File `~/Downloads` into topic folders on macOS.
Apply regular expression rules first, then ask Claude to place the files that no rule matched.
Claude only reads files. The script does every move and logs it.

## Setup

1. Install Python 3.11 or later and [Claude Code](https://claude.com/claude-code).
2. Copy `rules.example.toml` to `rules.toml` and edit it.
3. To run it weekly, copy `launchd.example.plist` to `~/Library/LaunchAgents`, set the paths, and load it with `launchctl bootstrap gui/$(id -u) <file>`.

## Use

- `python3 organise.py plan` prints the moves of the next run and changes nothing.
- `python3 organise.py run --claude` applies `rules.toml`, then asks Claude to place the rest.
- `python3 organise.py log` shows the most recent run. Add `--all` for every run.
- `python3 organise.py undo` reverses the most recent run.

Skip files newer than one day unless you pass `--min-age 0`.
The first matching rule wins.
Pictures with camera data go to `camera_photos`, and other images go to `other_images`.
Every move goes to `moves.log`.

Git ignores `rules.toml` and `moves.log`, because both contain personal file names.
