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
	
	Archery Range
	- archer
	
	Stables
	- cav warrior
	- cav archerr
	
	Castle
	- Peasant
	- Wizard
	- Hero
	
	Library
	- upgrades
- [ ] Undead
	
	Necromancer
	- skeleton warrior
	- skeleton archer
	
	Undead Stables
	- undead cav warrior
	- undead cav archer
	
	Creature Prison
	- Goblin Slave
	- Troll
	
	Lich King
	- Necromancer
	- Goblin Slave
	- Evil Wizard


## Planned

- [ ] <b><font size = 4>Refactor level Two.gd</font></b>
	<font size = 3 color = aqua>
	<ol>
		<li>extend Level</li>
		<li>in init() replace buildings + units</li>
		<li>Fix Dialogue </li> 
		<li>Fix Achievements</li> 
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
		<li>Fix Achievements</li> 
	</ol>


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