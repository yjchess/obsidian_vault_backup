---

kanban-plugin: board

---

## Ideas

- [ ] Refactoring:
	1. Use Encapsulation to reduce overuse of GameData.gd (singleton)
	2. The encapsulation should work such that level.gd receives signals from other scripts and instructs those scripts to perform functions. No one script should be able to access information from another script.
	3. Use composition to reduce amount of code per script + increase readability + reduce variance (i.e. the variable parts of certain nodes will be held in other parts)
	4. Allow for easier scaling - make it easier to add new features
- [ ] <ol>
		<li>instead of showing square uis from selected square, show from map</li>
	</ol>
- [ ] Human
	
	Barracks
	- warrior
	- axeman 
		- T2 Castle
	- elite swordsman 
		- T3 Castle
	- paladin 
		- T3 Castle, church, armory
	
	Archery Range
	- archer
	- crossbowman 
		- T2 Castle
	- ranged_specialist
		- T3 Castle
	- assassin 
		- T3 Castle, library up, armory 
	
	Stables
	- cav warrior
	- cav archer
		- T2 Castle
	- knight / ranged knight
		- T3 Castle
	- Griffin
		- T3 Castle, library up, armory
	
	Castle
	- Peasant
	- Wizard
		- T2 Castle, library
	- Heros
	
	Church
	- priest
	- priest upgrades
	
	Library
	- upgrades
- [ ] Undead
	
	Lich King
	- Necromancer
	- Death knight
	- Vampire Assasin
	
	Necromancer
	- ghoul
	- gargoyle
	- evil wizard
	
	Evil wizard
	- skeleton_warrior
	- skeleton_archer
	- goblin_slave
	
	Undead Stables
	- undead cav warrior
	- undead cav archer
	- wolf raider
	- wolf archer
	
	Creature Prison
	- Goblin Slave
	- Troll Slave
	- Mind-Controlled Brute
	
	Wizard Tower
	- upgrades(flat)
	- upgrades(skills)


## Planned

- [ ] ## bugs
	
	- description sometimes not showing full message
- [ ] <b><font size = 4>Refactor level Two.gd</font></b>
	<font size = 3 color = aqua>
	<ol>
		<li>Add Dialogue for endings + Choices</li> 
		<li>Fix Achievements</li>
		<li>Allow Dialogue to delay the computer's turn</li> 
		<li>Store Resources in autoload </li>
	</ol>
- [ ] Small TODOs
	
	1. Evil Wizard Unit
- [ ] <b><font size = 4>Refactor level Two.gd</font></b>
	<font size = 3 color = aqua>
	<ol>
		<li>
			<b>Ending 1a: </b>Saved the old man - killed grinkle via choice
		</li>
		<li>
			<b color = red>Ending 1b:</b> Saved the old man - killed grinkle via action
		</li>
	</ol>


## In Progress



## Completed

- [ ] <b><font size = 4>Refactor square.gd</font></b>
	<font size = 3 color = aqua>
	<ol>
		<li>Remove references to GameData.gd <input type="checkbox">
		<font size = 2 color = yellow>	
		<ol>
			<li>Use signals to indicate selected square <input type="checkbox"></li>
			<li>Use Signals to indicate an action to be performed on a square <input type="checkbox"></li>
		<ol>
		</li>
	</ol>
- [ ] <b><font size = 4>Refactor generic map.gd</font></b>
	<font size = 3 color = aqua>
	<ol>
		<li>Remove references to GameData.gd <input type="checkbox"></li>
	</ol>
- [ ] Potentially:
	
	Move signals from level.gd to map.gd
- [ ] <b><font size = 4>Implement Abilities UI Answers</font></b>
	<font size = 3 color = aqua>
	<ol>
		<li>When the user clicks on a button:  The UI sends a signal to the level which: using the selected unit,
		<ol>
			<li>Removes all UI square effects i.e. movable, attackable and abilitable</li>
			<li>obtains the squares related to the button from the selected_entity</li>
			<li>uses the corresponding function in the ui to show the squares (in the right colour)</li>
		</ol>
		</li>
		<li>Understand how the current system works:
		<ol>
		<li>When a square is selected, if it has a unit, it automatically displays all the unit movement and attack options.</li>
		</ol>
		</li>
		<li>Refactor if needed:<ol>
			<li>No need to change as intended behaviour when selecting a square</li>	
		</ol>
		</li> 
		<li>Implement updates <input type="checkbox"></li> 
	</ol>
- [ ] <b><font size = 4>Refactor level one ai.gd</font></b>
	<font size = 3 color = aqua>
	<ol>
		<li>Remove references to GameData.gd <input type="checkbox"></li>
		<li>Redefine how information is obtained by using signals to tell level.gd what is requested and then handle the output as input for the rest of the function<input type="checkbox"></li>
	</ol>
- [ ] <b><font size = 4>Implement Abilities UI</font></b>
	<font size = 3 color = aqua>
	<ol>
		<li>Decide on the desired behaviour<input type="checkbox"></li>
		<li>Understand how the current system works <input type="checkbox"></li>
		<li>Refactor if needed <input type="checkbox"></li> 
		<li>Implement updates <input type="checkbox"></li> 
	</ol>
- [ ] <b><font size = 4>Refactor level one.gd</font></b>
	<font size = 3 color = aqua>
	<ol>
		<li>Remove references to GameData.gd <input type="checkbox"></li>
		<li>Handle user clicking squares <input type="checkbox"></li>
		<li>Fix Dialogue <input type="checkbox"></li> 
		<li>Handle Loading and Saving <input type="checkbox"></li> 
	</ol>
- [ ] <b><font size = 4>Make Art for Undead Race</font></b>
	<font size = 3 color = aqua>
	<ol>
		<li>Goblin Slave</li>
		<li>Skeleton Warrior</li>
		<li>Skeleton Archer </li> 
	</ol>
- [ ] <b><font size = 4>Allow Undead Units to be initialised</font></b>
	<font size = 3 color = aqua>
	<ol>
		<li>Find out how human units are initialised</li>
		<li>Update information for undead units</li>
		<li>Link up undead units </li> 
	</ol>
- [ ] <b><font size = 4>Reorganize file directories</font></b>
	<font size = 3 color = aqua>
	<ol>
		<li>Youtube how to organise file directories for godot</li>
		<li>Implement</li>
	</ol>
- [ ] <b><font size = 4>Investigate Classes for Godot</font></b>
	<font size = 3 color = aqua>
	<ol>
		<li>Youtube Classes Godot</li>
		<li>Implement</li>
	</ol>
- [ ] <b><font size = 4>Refactor level Two.gd</font></b>
	<font size = 3 color = aqua>
	<ol>
		<li>extend Level</li>
		<li>in init() replace buildings + units</li>
		<li>Fix Dialogue </li> 
		<li>Fix Grinkle Behaviour (no spells)</li>
		<li>Fix Ghoul Behaviour - Line up at forest entrance behind Lord Montague</li>
	</ol>
- [ ] ## Finish Randomized Maps for PvE
	
	1. Add PvE to Campaign Menu
	2. Add Portraits for:
		1. King
		2. Queen
		3. Golem
		4. Cavlary_warrior
	3. Fix Description Error
	4. Fix Minimap Error
	5. Improve square_selection for randomized troops
	6. Implement Golem Damage Absorption Ability


***

## Archive

- [ ] <b><font size = 4>Refactor ability.gd</font></b>
	<font size = 3 color = aqua>
	<ol>
		<li>Remove references to GameData.gd <input type="checkbox">
			<font size = 2 color = yellow>	
			<ol>
				
				<li>Use signals to request viable squares inside ability range <input type="checkbox"></li>
				<li>Use Signals to 'summon' / 'status_effect' / 'damage' selected squares <input type="checkbox"></li>
			<ol>
		</li>
		 
	</ol>

%% kanban:settings
```
{"kanban-plugin":"board","list-collapse":[false,false,false,false]}
```
%%