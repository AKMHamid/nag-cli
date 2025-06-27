---

# nag-cli
A zero-dependency minimal tool in pure Bash for nagging terminal reminders, much like sticky notes. 
It's meant to annoy you into finishing urgent tasks by plaguing every new shell with reminders.


---

## Features

| Category | Details |
|----------|---------|
| Core     | **add · list · delete · clear** reminders |
| Toggle   | **mute / activate** with one command (🔔 ↔ 🔕) |
| Safety   | **3-level undo** for any mutating action |
| Hook     | Auto-installs a one-liner in&nbsp;`~/.bashrc` that prints reminders on every login shell |
| Portable | Pure Bash; works on GNU/Linux and macOS |


## Screenshot

![nag-cli](https://github.com/user-attachments/assets/cf21d19e-cba3-457e-9f7f-012b668bb008)

## Installation

```
git clone https://github.com/AKMHamid/nag-cli.git
sudo install -m755 nag-cli/nag /usr/local/bin/nag   # or move into any $PATH dir
```
**Note**: The first ```nag add …``` run appends a tiny block to ~/.bashrc so reminders show
up automatically. Remove that block to disable autoprinting (or mute it).

**Command quick-ref**
|Command|Short form|
|----------|----------|
|```nag add order PHEX mice```|```nag a "order PHEX mice"```|
|```nag list```               |```nag l```|
|```nag delete mice```        |```nag d mice```|
|```nag mute```               |```nag m```|
|```nag activate```           |```nag act```|
|```nag undo```               |```nag u   # (up to 3 steps)```|
|```nag clear```              |```nag c```|


Generated files
|File|Description|
|----------|---------|
|~/.reminders|active reminders|
|~/.reminders.muted|hidden while muted|
|\*.bak|timestamped  backups (3 max)|

Mutating commands create a timestamped backup, then prune to the newest three.
nag undo restores the latest backup and deletes it.

## Uninstallation
```
# remove the executable
sudo rm -f /usr/local/bin/nag     # or wherever you installed it

# strip the auto-print hook
# BSD / macOS sed
sed -i '' '/# >>> nag tool/,/# <<< nag tool/d' ~/.bashrc

# OR

# GNU sed (most Linux distros)
sed -i '/# >>> nag tool/,/# <<< nag tool/d' ~/.bashrc

# delete reminder data
rm -f ~/.reminders ~/.reminders.muted ~/.reminders*.bak
```

---


