# LEARN GODOT
## scope of the learning project: action rpg

## Importing
* For importing items you can simply drag them to the godot editor

* For pixel art, go to the IMPORT tab and delect 2d pixel then select use as default

## Display settings
width and heigth is the "viewport" it can be zoomed in depending on the window size
> for a pixel art game, set it to 320x180
> **set strech mode to 2D** - this will strech the viewport to the window size 

test width and height is the actual window sizes
> for testing is good 1280x720

## Animations
* you can you the sprite node and select the number of Hframes from a sprite sheet
* Animation Player node - basic character movement animation
> You should start running animations with the sprite already in movement, and finish it with sprite "stopped"
* Animation Tree with Blend Space 2D - gives you a grid with a graph where you add values to control the animations
> To prioritize one animation over another in Animation Tree (with grid). you can just tweak to grid, so it prioritzes one over another
* A simple solution for controlling animations is creating a enum to control the state like ATTACK, MOVE, ROLL
* In Animation Player you can call a function for example when the animaiton finishes
### State Machine
* space will trigger to roll 
* move will have it's own function
> match functions like a switch

    match state:
        MOVE:
            function_move(delta)
### AnimatedSprite(For simple animations)
* when an object is constantly animated
* for example the destruction of some terrain/object
> something that will just play

## Backgrounds
* You can just use the same 2D sprite node, but using some tweaks, like on the import tab selecting repeat, also on the sprite right most options, selecting region enabled
> you can fill up the room pretty easily like this
> There are other ways of doing this, for example using a TextureRect node, is actually easier, however it was meant to be a UI node, so it might have some drawbacks. This is something to be researched about
## TileMap
* This should be below the main 2D Sprite (if you have one) background node
* There are three main options with tile sets in TileMap node. Single (for a single tile), auto tile, and tile atlas (if you have multiple different tiles in one texture pack)
* For configuring how to set a single Tile go on the bitmask property of the TileSet property from TileMap node
* There is collisions and a whole of other properties in tilemaps

## Physics
* multiply delta, so if it's lagging it will move faster
> actually this can make the player frustrated, since he won't have time to react, if it lags, so it's something you should consider
* normalizing movement vectors, so it has the length of 1, so it doesn't move faster at diagonals
* to add something like acceleration do += to the input_vector so it adds the amount every frame, to do constant speed just do input_vector = input_vector * speed
* Vector2.move_towards sets a value to which the vector will get updated to every frame
* Vector2.clamped caps the vector to a specific value
* move and slide will make the character slide on the walls/collisions

## Collisions
* It's a good idea to have one collision shape for interacting with scenario, and another for hitboxes
* You can actually draw collisions, like whole walls at a time (Collision Polygon)

## Hitbox & Hurtbox
* one way of doing it is with Area2D with CollisionShape with no collision shape
> and in the scene you're adding it to, change the shape to fit the object

* For controlling attack hithox one way is adding a Position2D node as a center position and adjusting the hitbox relative to it
> and keying it in the AnimationPlayer and in it adjusting the rotation and positioning of the hitbox
> and also keying the disable property of the collision shape at the start and end of the animation

## Instancing
* you can instance a scene by code by using something lke:
    
    GrassEffect = load(""res://"")
    grassEffect = GrassEffect.instance()
    main = get_tree().current_scene
    main.add_child(grassEffect)
    grassEffect.global_position = global_position
> the last global_position is from the node owner of the script (in this case all grasses)
## General
* the child's nodes positions are relative to the root node, the root node actually sits at the top left corner (you can move it, if you wish)
* You can set collisions shape to be visible
* You can set a grid in the editor
* You can switch in the Scene tab to Remote which will show you real time data from the running game

* **Layers** > controlling the layers of collisions so not all collisions happen the same way, for exaple, triggering only when a hitbox enters a hurtbox
> the Layer is the one the object should be, the mask is the one it should interact/collide with

## Reusable
### Inhenritence
* one object can inherit funcionst for example from another object

### Composition
* you compose it from reusable assets like ""hurtbox** reusable scene
* **stats**  scene
> you can export variables so you can change it when instancing in other objects

## Signal
* nodes have specifc signals, for example animation finished, that you can hook with some function to handle it
* you can create a signal to tell for example that your enemy has no health, then you can emit_signal
* **you can connect signals trhough code** and also you can pass parameters with it

## Set & Get
* it will trigger whenever that varible is benig updated/set

## Camera
* Camera2D node as a child of the player and enabling current will follow the root node
> you can instead of making the Camera2D a child of the Player's node, make it an independent node and adding to the player a RemoteTranform2D, and setting it to the Camera which will make the camera follow the player, but won't destroy the camera's node when the player is destroyed
> you can enable smoothing to make to following a little batter
> there's a lot of tweaking you can do with the camera, like pixel snap, making it run in the physics proccess
* Adding a CanvasLayer Node and the UI elements as childs of it will make it also follow the camera

## Tips
* You can just right click some node to change it's type
* on the error tab of the editor, Godot sometimes points out things that might be very helpfull, such as move_slide function is retuning a value but it's never used
> this will make movement smoother after colliding with something
* You can just right click a node and export it as a scene (to instance it later)
> you will have to use transform to fix it's positioning beacuse when it's created it will be relative to the one that you've created previously
* You can/should use Node2D as the main root not for the world 
> since you can move the root and all it's children will also move
* you can lock positioning of nodes
* Ysort object as a root node but not as the root one of the scene, but the root of interactable objects like player and boxes for example
> will automatically sort the Y layer for you, but it's important to have it's instances with it's poistioning at the "feet" properly, so you run into any sorting "bugs"
> If you wanna group like bushes into a single node, make the root of it also a YSort node, because it will know how to sort
* $ (likes jQuery) let's you select a node from a scene by it's name
* Ctrl + D will duplicate a node
* **when you're going down the scene tree you may want to update something in the scrpt, if you're going up like your stats node is telling you root object somehitng you may want to use a sginal**
* you can preload resources
* YSort can fix a lot of problem when you have for example animations player over the player, even though it shouldn't
### Performance
* While running the game you can check frame rate in the bottom tabs, Monitor one
> in Profiler tab you can actually see which functions are causing problems in performance, like how many calls function is having

## UI
* most of the Controls nodes are related to UI elements

## Polishing
* you can just set a variable as an export variable and update it while the game is running to tweak it's values

## Doubts
?? Difference beteween _physics_process and _process
> main difference is that physics process actually waits for the physics to stop processing. So it's good if you want to use stuff like a node's positioning

?? is diagonal speed faster?

## BUGS
* if you're using area_entered for trigerring hits, what if the are never actually leaves? Like when the player is hugging a wall...
> a possible fix for it is twearking with the monitoring and monitorable properties of collisionShape
### Overlap
* Area2D get_overlapping_areas will return an array with all bodies that are overlapping
## TODO
* ??export collision shape and got into tool node??