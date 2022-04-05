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

## Sprite (animations)
* you can you the spirte node and select the number of Hframes from a sprite sheet
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

## Animation
* Animation Player node - basic character movement animation
> You should start running animations with the sprite already in movement, and finish it with sprite "stopped"
* Animation Tree with Blend Space 2D - gives you a grid with a graph where you add values to control the animations
> To prioritize one animation over another in Animation Tree (with grid). you can just tweak to grid, so it prioritzes one over another

## General
* the child's nodes positions are relative to the root node, the root node actually sits at the top left corner (you can move it, if you wish)
* You can set collisions shape to be visible
* You can set a grid in the editor

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
* $ (likes jQuery) let's you select a node from a scene by it's name

## Doubts
?? Difference beteween _physics_process and _process
?? is diagonal speed faster?