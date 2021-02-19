<p align="center"><img src="https://github.com/musurca/IKE/raw/main/ike_logo.png" /></p>

## PBEM/hotseat multiplayer for *Command: Modern Operations* scenarios
FOR PLAYERS: [**DOWNLOAD LATEST SCENARIO PACK HERE (v1.2)**](https://github.com/musurca/IKE/releases/download/v1.2-scenarios/IKE_Scenario_Pack_v1.2.zip)

FOR SCENARIO AUTHORS: [**DOWNLOAD LATEST RELEASE HERE (v1.2)**](https://github.com/musurca/IKE/releases/download/v1.2/IKE_v1.2.zip)

If you're a scenario author or player looking to convert a new or existing scenario for multiplayer use, you only need to download either the latest release or scenario pack using the links above. 

This code repository is intended only for those who are curious about how **IKE** works internally, want to add more features, or want to localize the text for a language other than English. In other words, **if you just want to create a PBEM scenario, you can just download the latest release and skip everything below.**

If you're interested in localizing text: you don't have to build the system. You can just add your translations to [the localization source file](https://github.com/musurca/IKE/blob/main/src/00_localize.lua) and submit the changes via pull request or by [creating a new Issue](https://github.com/musurca/IKE/issues/new) and attaching the file.

For all others interested: welcome! Pull requests and bug reports are greatly appreciated.

(Please note that **IKE** is licensed under [GNU GPL v3](https://www.gnu.org/licenses/gpl-3.0-standalone.html), so if you intend to make and distribute changes, please make the source freely available or submit a pull request to this repository promptly.)

### Build prerequisites
* A Bash shell (on Windows 10, install the [WSL](https://www.howtogeek.com/249966/how-to-install-and-use-the-linux-bash-shell-on-windows-10/))
* [luamin](https://github.com/mathiasbynens/luamin)
* [Python 3](https://www.python.org/downloads/)

#### Quick prerequisite install instructions on Windows 10

Assuming you've installed the [WSL](https://www.howtogeek.com/249966/how-to-install-and-use-the-linux-bash-shell-on-windows-10/) and Ubuntu, run the following commands from the shell:
```
sudo apt-get install npm
sudo npm install -g luamin
```

### How to compile

#### Release
```
./build.sh
```

The compiled, minified Lua code will be placed in `release/ike_min.lua`. This is suitable for converting scenarios for PBEM play by pasting it into the Lua Code Editor and clicking RUN as the final step in the scenario creation process.
 
#### Debug
```
./build.sh debug
```

This will produce compiled but unminified Lua code in `debug/ike_debug.lua`. _Do not use this in a released scenario._ This is mostly useful to observe how the final released Lua is composed from the source files.

#### Why is the build process so complicated?
**IKE** works by injecting its own code into a *CMO* LuaScript event action which is executed upon every scenario load. The build process converts the **IKE** source into a minified, escaped string which is then re-embedded into its own code. (IKE-ception!)

### What is IKE?
**IKE** adds PBEM (Play by E-Mail) or Hotseat play to any *Command: Modern Operations* scenario, allowing you to engage in a turn-based multiplayer game with one or more opponents by exchanging .save files.

### What does it do?
**IKE**...
* keeps track of turn order and length, and stops the scenario automatically when a player’s turn is over.
* provides a summary of any losses sustained or messages received during the last turn.
* adds an (optional) Setup Phase, allowing players to configure loadouts, missions, and orders before the game begins.
* supports either Unlimited Orders (traditional CMO play) or Limited Orders to simulate command delay and friction.
* provides password protection for each player’s turn.
* allows players to either use the scenario’s recommended PBEM settings, or customize them at game start.
* maintains a consistent random seed, to discourage replaying turns for more advantageous results.
* prevents players from cheating by (optionally) disabling the Editor until the scenario has ended.

### Who is it for?
**IKE** is designed primarily for scenario authors who want to create a multiplayer version of their existing scenario, but it may also be used productively by players who want to convert their favorite scenario for use with a friend.

### How do I use it?
For detailed instructions, please refer to the manual included with the [latest official release](https://github.com/musurca/IKE/releases/download/v1.2/IKE_v1.2.zip).

### VERSION HISTORY
v1.2 (2/18/2021):
* added: limited order mode
* added: players can customize scenario settings
* added: option to prevent editor mode
* added: losses marked with RPs
* added: missed messages delivered next turn
* added: special action to change side posture
* added: localization support
* fix: end of setup phase message
* fix: API replacements clean themselves up
* fix: workaround for broken ScenEnded trigger
* fix: set clock precisely to turn boundaries
* fix: special message order hiding IKE messages
* fix: coop kills not reported as losses
* fix: observed losses not reported next turn
* fix: ScenEdit_PlayerSide() in limited order mode
* fix: better random seed

v1.1 (2/1/2021):
* fix: edge case for ScenEdit_SetTime() 
* fix: use os.date("!") to format scenario times

v1.0 (1/25/2021):
* Initial release.
