# Wraith ARS 2X
The **Wraith ARS 2X** (Wraith Advanced Radar System) is a realistic police radar that takes heavy inspiration from the real Stalker DSR 2X radar system. It includes a plethora of features from the DSR 2X such as the new operator menu, to improve the realism and experience whilst using the newest instalment from the collection of Wraith radar systems. Previously with WraithRS, vehicle speeds were only displayed in the target window, with no priority to certain vehicles (such as large and slower vehicles, or smaller and faster vehicles). The Wraith ARS 2X tracks both large and faster, smaller targets and displays the speeds of both in the target windows, meaning the radar can track 4 different speeds with both antennas turned on and transmitting. Alongside the new radar system is also a plate reader that scans in front and behind the patrol vehicle, a BOLO plate can also be set, but developers can also hook into the scanner to link it into other resources. 

## Installation
Installing the Wraith ARS 2X into your FiveM can be done by following the listed steps below. 
1. Download the latest version of the resource from [here](https://github.com/WolfKnight98/wk_wars2x/releases)
2. Open the zip file and place the `wk_wars2x` folder into your server's resource folder
3. Open up your server configuration file and add `ensure wk_wars2x` to your resource start list 

It's now installed! When you boot your server you should see a Wraith ARS 2X message as well as the version check message. 

## Default key binds
Although these can be viewed ingame through the operator manual, the default key binds are listed below. 
| Action              | Key                         |
| ------------------- | --------------------------- |
| Open remote         | F5                          |
| Close remote        | ESC or right mouse button   |
| Lock front antenna  | Numpad 8 (full) / 1 (small) |
| Lock rear antenna   | Numpad 5 (full) / 2 (small) |
| Lock front plate    | Numpad 9 (full) / 3 (small) |
| Lock rear plate     | Numpad 6 (full) / 4 (small) |
| Toggle keylock      | L                           |
| Toggle key bind set | K                           |

## Changing the UI file save type
As the UI can be moved and scaled, the system also saves the UI data as it is set by the user. By default, this identifier type uses `license` to name the JSON files saved in the `saves` folder. This can easily be changed by opening the `sv_saving.lua` file, then looking for the following line of code at the top:
```lua
DATASAVE.idType = "license"
```
All you need to do is change the value, so for example, if I wanted the save files to be saved using Steam IDs, I would change the code to look like this:
```lua
DATASAVE.idType = "steam"
```

## Script configuration
All of the configuration for the Wraith ARS 2X is done inside the `config.lua` file, below is a copy of the configuration file. All of the options have comments to describe what they do, along with the available options you can set. You have the ability to change the key binds for the large and small key set, the default operator menu options, and the default UI element scale and safezone. 
```lua
-- Radar fast limit locking
-- When enabled, the player will be able to define a fast limit within the radar's menu, when a vehicle 
-- exceeds the fast limit, it will be locked into the fast box. Default setting is disabled to maintain realism
CONFIG.allow_fast_limit = true 

-- Sets all of the controls
CONFIG.keys =
{
	-- Remote control key 
	-- The default key to open the remote control is 166 (F5 - INPUT_SELECT_CHARACTER_MICHAEL)
	remote_control = 166,

	-- Radar key lock key 
	-- The default key to enable/disable the radar key lock is 182 (L - INPUT_CELLPHONE_CAMERA_FOCUS_LOCK)
	key_lock = 182,

	-- Radar keybinds switch 
	-- The default key to switch the bind set is (K - INPUT_REPLAY_SHOWHOTKEY)
	switch_keys = 311, 

	-- Keys for a full size keyboard
	[ "full" ] = {
		-- Radar front antenna lock/unlock Key 
		-- The default full keyboard key to lock/unlock the front antenna is 111 (Numpad 8 - INPUT_VEH_FLY_PITCH_UP_ONLY)
		front_lock = 111,

		-- Radar rear antenna lock/unlock Key 
		-- The default full keyboard key to lock/unlock the rear antenna is 112 (Numpad 5 - INPUT_VEH_FLY_PITCH_DOWN_ONLY)
		rear_lock = 112,

		-- Plate reader front lock/unlock Key 
		-- The default full keyboard key to lock/unlock the front plate reader is 118 (Numpad 9 - INPUT_VEH_FLY_SELECT_TARGET_RIGHT)
		plate_front_lock = 118,

		-- Plate reader rear lock/unlock Key 
		-- The default full keyboard key to lock/unlock the rear plate reader is 109 (Numpad 6 - INPUT_VEH_FLY_ROLL_RIGHT_ONLY)
		plate_rear_lock = 109
	}, 

	-- Keys for smaller keyboards 
	[ "small" ] = {
		-- Radar front antenna lock/unlock Key 
		-- The default small keyboard key to lock/unlock the front antenna is 157 (1 - INPUT_SELECT_WEAPON_UNARMED)
		front_lock = 157,

		-- Radar rear antenna lock/unlock Key 
		-- The default small keyboard key to lock/unlock the rear antenna is 158 (2 - INPUT_SELECT_WEAPON_MELEE)
		rear_lock = 158,

		-- Plate reader front lock/unlock Key 
		-- The default small keyboard key to lock/unlock the front plate reader is 160 (3 - INPUT_SELECT_WEAPON_SHOTGUN)
		plate_front_lock = 160,

		-- Plate reader rear lock/unlock Key 
		-- The default small keyboard key to lock/unlock the rear plate reader is 164 (4 - INPUT_SELECT_WEAPON_HEAVY)
		plate_rear_lock = 164
	}
}

-- Here you can change the default values for the operator menu, do note, if any of these values are not
-- one of the options listed, the script will not work. 
CONFIG.menuDefaults = 
{
	-- Should the system calculate and display faster targets
	-- Options: true or false
	["fastDisplay"] = true, 

	-- Sensitivity for each radar mode, this changes how far the antennas will detect vehicles
	-- Options: 0.2, 0.4, 0.6, 0.8, 1.0
	["same"] = 0.6, 
	["opp"] = 0.6, 

	-- The volume of the audible beep 
	-- Options: 0.0, 0.2, 0.4, 0.6, 0.8, 1.0 
	["beep"] = 0.6,
	
	-- The volume of the verbal lock confirmation 
	-- Options: 0.0, 0.2, 0.4, 0.6, 0.8, 1.0 
	["voice"] = 0.6,
	
	-- The volume of the plate reader audio 
	-- Options: 0.0, 0.2, 0.4, 0.6, 0.8, 1.0 
	["plateAudio"] = 0.6, 

	-- The speed unit used in conversions
	-- Options: mph or kmh 
	["speedType"] = "mph"
}

-- Here you can change the default scale of the UI elements, as well as the safezone size
CONFIG.uiDefaults =
{
	-- The default scale of the UI elements.
	-- Options: 0.25 - 2.5
	scale =
	{
		radar = 1.0, 
		remote = 1.0, 
		plateReader = 1.0
	}, 

	-- The safezone size, must be a multiple of 5.
	-- Options: 0 - 100
	safezone = 20 
}
```

## Suggestions
If there is an improvement that you think should be made, open a pull request with your modified code, I will then review your request and either accept/deny it. Code in a pull request should be well formatted and commented, it will make it much easier for others to read and understand. In the event that you want to suggest something, but don't know how to code, open an issue with the enhancement tag and then fully describe your suggestion. 

## Reporting issues/bugs
Open an issue if you encounter any problems with the resource, if applicable, try to include detailed information on the issue and how to reproduce it. This will make it much easier to find and fix. 