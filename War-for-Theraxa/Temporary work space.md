<h2>Issues for abilties:</h2>

abilities getting too messy:
- no consistent structure,
- signals all over the place
- ui_handler match statement should not be concerned about handling abilities - only how they appear
- Repeated functions, data and properties between unit and building class.
- Some abilities are instantiated as their own node whilst others are not
- Repeated information such as resource costs for building and training units
- Issues with scalability - adding a new ability becomes a nightmare

<h2>Potential Solutions</h2>
1. Design a consistent system of expected behaviours:
	1. Each ability will create it's own node
	2. Improved signal connections
	3. abilities will have a function to determine which squares are usable: Takes viable squares as an input and outputs the usable squares
	4. Combine Summon type abilities and Train type abilities?
	5. Write a blueprint for how to 
		1. add an ability with an already defined ability type
		2. add an ability with a new ability type

<h2>Old System</h2>

When an ability button is pressed:
1. emit the ability_pressed signal which passes the ability_name to ui
2. ui re-emits the signal to ui_handler
3. ui_handler tells the level what ability is selected via the ability_selected signal
4. ui_handler uses a match statement to manually find the corresponding squares via functions such as unit.get_buildable_squares() and unit.get_unit_possible_moves() and decide whether they are abilitable, movable, attackable etc. type squares

5. In the square node. It checks if the square clicked is attackable / movable / abilitable and emits the relevant signal
6. Map re-emits entity_ablilty to level which then gets the currently selected entity and uses the ability.
7. The building / unit selected has a use_ability function which gets the ability and tells it to use it's own use_ability function
8. the ability's use_ability function determines what kind of ability it is and emit's signal based off the typing.


<h2>New System </h2>
1. use the \_listen function in ui_handler to listen to ability_button_pressed from ability_button
2. ability_button_pressed_signal in ui_handler determines if the last pressed entity is a unit or building
3. The signal also determines whether to show movable, attackable or abilitaable (or change the abilities panel) depending on the ability_ui_type passed in through ability_button to the signal

4. In the square node. It checks if the square clicked is attackable / movable / abilitable and emits the relevant signal
5. Map re-emits entity_ablilty to level which then gets the currently selected entity and uses the ability.
6. The building / unit selected has a use_ability function which gets the ability and tells it to use it's own use_ability function
7. the ability's use_ability function determines what kind of ability it is and emit's signal based off the typing.



	emit_signal("ability_button_pressed", ability_name, ability_ui_type)


[https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/monitor_estimated_charges_with_cloudwatch.html](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/monitor_estimated_charges_with_cloudwatch.html "https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/monitor_estimated_charges_with_cloudwatch.html")

[https://neon.com/](https://neon.com/ "https://neon.com/") (postgres)

[https://aws.amazon.com/startups/credits#hero](https://aws.amazon.com/startups/credits#hero "https://aws.amazon.com/startups/credits#hero")

[https://upstash.com/pricing](https://upstash.com/pricing "https://upstash.com/pricing") redis

![[Pasted image 20250908192654.png]]