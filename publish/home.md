---
title: Questions surrounding UI_HANDLER
excerpt: Create your own template or use someone else's. Changing the template is a matter of updating one line
---
Ok, so I've decided to write these questions in order for me to finally get over this hump. Legit no idea why my brain's made it so hard but yeah:

<h2>What is a handler and how it works</h2>
In my case handler = controller and a signal manager. The idea being that the controller handles requests from other scripts and provides a response. And in this case acts as a middle man connecting level and canvas_layer.

now the end desired result is to have the level be a parent to multiple 'handler' type scripts. Each handler is a controller and they all interact with each other. I.e. if the UI_handler requires data from the map, it will connect the submit_update function of the map_handler to the \_submit_data function of the ui_handler as soon as the map_handler enters the tree.  \*1
## How does the handler receive data:

When the ui_handler first enters the tree - it triggers the \_enter_tree() function which is a function that occurs before the \_ready() function. Within this function code is written which 1. Grabs the current scene 2. connects the child entered tree signal of the current scene to it's own listen signal which in turn checks if that child has a submit_update function (and if it does - connects it to the submit data function) i.e. in regards to my own circumstance for any child of the level scene if they have a submit_ui_update function, I can connect it to my submit_data function. Thereby ensuring that whenever a variable is changed via submit_ui_update, I can ensure that the data is changed within ui_handler via it's submit_data function \*2.
## How is the ui updated

\_update_all_ui is used for updating all the children of ui_handler which have the function update_ui via propagate call by passing in the same data to each component which has the update_ui function \*3 and then the components take the individual pieces of data that they need to update the ui with specific functionality programmed for the default cases. In the example project it is not called though.

# Specifics for my project (ui_handler).

## Functions

The function that goes from canvas_layer -> ui_handler:

```
@onready var squares = get_tree().get_nodes_in_group("squares")

func update_minimap_grid():
	for i in len(squares):
		change_minimap_square(squares[i].get_player(), i)
```

I believe it is ok to leave it as it is.
## Signal Connections

| Signal Name       | data requested                                                        | Where the data comes from     |
| ----------------- | --------------------------------------------------------------------- | ----------------------------- |
| surrender         | achievements                                                          | achievement_handler           |
| end_turn          |                                                                       |                               |
| abillity_pressed  | unit_selected, building_selected, player_resources, map, ability_name | selection_handler, level, map |
| ability_unpressed |                                                                       |                               |
| dialogue_finished | dialogue                                                              | dialogue_handler              |

<hr>
### Surrender:
1. create a Script for achievement_handler
2. create a submit_ui_update signal
3. Now we have an option - either:
	1. trigger submit_ui_update each time the achievements variable changes
	2. trigger submit_ui_update when the user presses the surrender button
		
		The advantages of 3.1 is easier code as 3.2 requires ui to submit it's only update to achievements to tell achievements that the surrender button has been pressed. The benefit of 3.2 though is that the achievements are only gotten when they are needed and not each time they are updated. 

### End_turn:

Because end_turn is a signal from canvas_layer to level that occurs when the end_turn button is pressed, there is no need to adapt anything just emit it as a signal to connect it to the level's end_turn_signal function.

### Ability_pressed:

1. create a node as a child of level named: selection_handler
2. selection_handler holds the variables: unit_selected, building_selected, ability_selected
3. when these are updated use submit_ui_update
4. In level create a submit_ui_update function which passes: player_resources and map

Instead of creating a selection_handler, would it make more sense to create a level_handler? And in this way place player_resources there too?

### Ability_unpressed:

Do not need to worry too much about this as it's simply a function that hides certain ui elements when a button is un-pressed.

### dialogue_finished:

This is a connection from canvas_layer to the dialogue_node (i.e. when the dialogue finishes on the canvas_layer - send a signal to dialogue)

<hr>

## How does the handler receive data:

When ui_handler enters tree - triggers the \_enter_tree() function. 
1. Grabs the current scene 
2. connect child entered tree signal of current scene to ui_handler listen signal:
	1. for children of level scene if have a submit_ui_update signal, connect it to ui_handler's submit_data function.

In this way - I see that I need to build a submit_data function for:
1. achievement_handler
2. dialogue_handler
3. selection_handler
4. level

## When is \_update_all_ui called?

Not sure - it seems to me because all the signals happen discretely and not continuously (i.e. x happens which triggers y signal once as opposed to a mouse hovers over something: triggering something multiple times) it seems like maybe \_update_all_ui is not needed?

That being said, perhaps this is because I structured my ui in the wrong way? As the continuous updates occur more in the square node (which is a child of the map node and parent of potentially a unit node or a building node). The square node detects when a mouse is hovering over the square and reacts differently depending on whether it has been clicked or not.  When a unit or building is clicked, they will also change the appearance of squares around it.



## Questions

\*1 Does this mean that the ui_handler has to be loaded first after the current scene is loaded? Otherwise won't there be issues because all the children will have already entered the tree? Additionally, what if another handler needs to use data from the ui_handler? Or is there a way I can load all the handler scripts and then have them re-enter the tree so they all trigger the enter_tree signal again?

\*2
```
var data: Dictionary:
	set(v):
		if data != v:
			data = v
			dirty = true
...

func _submit_data(key: String, value: Variant): 
	data[key] = value
```

This is my understanding of the above code: when data is submitted, the data dictionary declares its intent to get the key and changes it's value. This triggers the set(v) function. But if this is the case it checks if data is equal to value which is always false? As value is just part of a key-value pair of data and not data itself? Or does set for dictionaries apply to checking for the specific key-value pair?

i.e. in pseudocode, this is my current understanding:

if data is proposed to be changed:
	check if data is equal to the proposed change if it isn't - change data to be equal to the proposed change and set the dirty flag to be true

However, my issue w this is that data is a dictionary whereas v is the specific proposed change? i.e. if data = \{"key_1": "val_1", "key_2":"val_2"} - if key_1 is changed i.e. \_submit_data("key_1", "val_3") - wouldnt the check (if data!=v) be: if \{"key_1": "val_1", "key_2":"val_2"}  != "val_3" which is always false? Or have I misunderstood how set(v) works?

\*3 Is the default value i.e. nulls etc. supposed to signify that there hasn't been a change? i.e. does each update_ui function in the canvas_layer components have a section of code like if data\["variable_key"] == default_value: return ? Is this efficient though? As it means that for each ui_update it will run this line of code multiple times?