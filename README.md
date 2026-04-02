```
 ▄▄▄▄▄  ▄▄▄▄  ▄  ▄▄▄
   ▄▄▀  █▄▄▄  █   █
 ▄▀▀    █▄▄▄  █   █
 ▀▀▀▀▀  ▀▀▀▀  ▀   ▀
```

Simple time logger for the terminal. No timers, no start/stop — just log how many hours you worked and move on. Built for people who eyeball their time or keep forgetting to stop timers.

## Install

### Quick install (curl)

```bash
curl -fsSL https://raw.githubusercontent.com/moritzpflueger/zeit/main/zeit -o ~/.local/bin/zeit && chmod +x ~/.local/bin/zeit
zeit init
```

### Git clone (recommended)

```bash
git clone https://github.com/moritzpflueger/zeit.git
cd zeit
./zeit init
```

Cloning makes updates easy with `git pull`.

### Update

```bash
zeit update              # curl installs — checks for new version
cd <your-zeit-dir> && git pull  # git installs
```

`zeit init` walks you through first-time setup:
- Creates a `~/.zeit/` data directory for your logs
- Optionally sets your billing currency and connects a private GitHub repo for sync
- Symlinks `zeit` into your PATH

## Usage

### Log hours

```bash
zeit 8                          # 8h today
zeit 5 yesterday                # 5h yesterday
zeit 6 monday                   # 6h last Monday
zeit 3 03-28                    # 3h on March 28
zeit 7 2026-03-28               # 7h on explicit date
zeit 8 yesterday client call    # 8h with description
zeit 0 04-14..04-18 vacation    # 0h for a date range
```

The project is auto-detected from your current directory. First time in an unmapped directory, you'll be asked to pick or create a project.

### View hours

```bash
zeit sum march           # Current project, March
zeit sum april all       # All projects, April
zeit sum 2026-04         # Explicit year-month
zeit sum slidesgpt       # Specific project, all time
zeit sum all             # All time, current project
zeit sum all all         # Everything
```

Shows all entries with weekday, daily earnings (if currency is set), gap markers for missing days, and copies the total hours to your clipboard.

### Fix mistakes

```bash
zeit undo                # Remove last entry
zeit rm yesterday        # Remove entries on a specific date
zeit rm 2026-04-01       # Same with explicit date
zeit edit                # Open zeit.csv in $EDITOR
```

### Other commands

```bash
zeit status              # Activity overview for the current month
zeit last                # Last 10 entries
zeit last 20             # Last 20 entries
zeit list                # Show projects, directories, rates
zeit sync                # Manual GitHub sync
zeit config              # Change settings (currency, sync, symlink)
zeit -h                  # Help
zeit --version           # Version
```

## How it works

- **Data:** `~/.zeit/zeit.csv` — one row per entry (date, hours, project, description)
- **Config:** `~/.zeit/config.json` — maps directory prefixes to project labels, optional hourly rates and currency
- **Sync:** Auto-commits and pushes to your private GitHub repo after every write (if configured)

Your data lives in `~/.zeit/`, separate from the tool itself. This keeps your logs private even if the tool repo is public.

## Project detection

Directory prefixes map to project labels. `/Users/you/Projects/slidesgpt` matches any subdirectory underneath it. When you're in an unmapped directory, zeit offers to map it to an existing project or create a new one.

## License

MIT
