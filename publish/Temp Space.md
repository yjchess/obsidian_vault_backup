Ok, so I've decided to write these questions in order for me to finally get over this hump. Legit no idea why my brain's made it so hard but yeah:

<h2>What is a handler and how it works</h2>
In my case handler = controller and a signal manager. The idea being that the controller handles requests from other scripts and provides a response. And in this case acts as a middle man connecting level and canvas_layer.

now the end desired result is to have the level be a parent to multiple 'handler' type scripts. Each handler is a controller and they all interact with each other. I.e. if the UI_handler requires data from the map, it will connect the submit_update function of the map_handler to the \_submit_data function of the ui_handler as soon as the map_handler enters the tree.  \*1
## How does the handler receive data:

When the ui_handler first enters the tree - it triggers the \_enter_tree() function which is a function that occurs before the \_ready() function. Within this function code is written which 1. Grabs the current scene 2. connects the child entered tree signal of the current scene to it's own listen signal which in turn checks if that child has a submit_update function (and if it does - connects it to the submit data function) i.e. in regards to my own circumstance for any child of the level scene if they have a submit_ui_update function, I can connect it to my submit_data function. Thereby ensuring that whenever a variable is changed via submit_ui_update, I can ensure that the data is changed within ui_handler via it's submit_data function.
## How is the ui updated

\_update_all_ui is used for updating all the children of ui_handler which have the function update_ui via propagate call by passing in the same data to each component which has the update_ui function \*2 and then the components take the individual pieces of data that they need to update the ui with specific functionality programmed for the default cases. In the example project it is not called though.

## Specifics for my project (ui_handler).

### Signal Connections


| Signal Name       | data requested                                                        | Where the data comes from     |
| ----------------- | --------------------------------------------------------------------- | ----------------------------- |
| surrender         | achievements                                                          | achievement_handler           |
| end_turn          |                                                                       |                               |
| abillity_pressed  | unit_selected, building_selected, player_resources, map, ability_name | selection_handler, level, map |
| ability_unpressed |                                                                       |                               |
| dialogue_finished | dialogue                                                              | dialogue_handler              |

## How does the handler receive data:

When ui_handler enters tree - triggers the \_enter_tree() function. 
1. Grabs the current scene 
2. connect child entered tree signal of current scene to ui_handler listen signal:
	1. for children of level scene if have a submit_ui_update function, connect it to ui_handler's submit_data function.

In this way - I see that I need to build a submit_data function for:
1. achievement_handler
2. dialogue_handler
3. selection_handler
4. level





\*1 Does this mean that the ui_handler has to be loaded first after the current scene is loaded? Otherwise won't there be issues because all the children will have already entered the tree? Additionally, what if another handler needs to use data from the ui_handler? Or is there a way I can load all the handler scripts

\*2 Is the default value i.e. nulls etc. supposed to signify that there hasn't been a change? i.e. does each update_ui function in the canvas_layer components have a section of code like if data\["variable_key"] == default_value: return ? Is this efficient though? As it means that for each ui_update it will run this line of code multiple times?