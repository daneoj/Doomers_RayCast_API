# Raycaster API
### Team Doomers: Pavel Peev and Dane Ojala
### UWB CSS452 with Prof. Kelvin Sung
### Winter 2022

[Home](https://daneoj.github.io/Doomers_RayCast_API/)  [Tutorial](https://daneoj.github.io/Doomers_RayCast_API/Tutorial)  [Demos And Conclusion](https://daneoj.github.io/Doomers_RayCast_API/DemosAndConclusion)

## Module Description:
Our API implements several classes that will be used together to allow users of the game engine to create 3D gameplay using a Raycasting engine.
This API allows users of the game engine to quickly implement a retro-3D look, complete with texture support, camera movement, and more.
Users can use a RCCamera in conjunction with a GridMap object of textured Tiles to implement basic games with raycast graphics. RCSpriteRenderable objects allow the user to add enemies, pickups, etc. that are rendered by the RCCamera as well.

## API Classes Overview:

## RCCamera
- Performs Raycasts and displays the result (Creating a 3D effect)
- Extends from Camera, but includes a RCrotation element for tracking the rotation of the RC_Camera (since we can rotate our view left and right)
- Stores the most recent RayCast data so we can determine which RCSpriteRenderable objects need to be drawn
## GridMap
- 2D Grid that defines the world that will be raycasted.
- Consists of textured tiles
- Grid system allows RCCamera to perform optimization when Raycasting
## Tile
- Simple object that can hold 4 textures, one for each side. Used by GridMap to implement textured worlds.
## RCSpriteRenderable
- Defines a sprite that can be rendered by the RCCamera
- Allows the user to implement enemies, pickups, etc.

# API Functions

## RCCamera API:
RCCamera(wcPos, viewPortArray)
setViewPort(viewPortArray)
- Sets viewport of the RC_Camera (same as the Camera class)

getViewPort()
- Returns viewport array.

setRayCast(fov, resolution)
- Sets total angle that raycasts will be performed between (higher number = wider FOV)
- Sets the number of raycasts that will be performed (we do X raycasts from left to right, along the horizon line (Raycasting method does not support height)

setRCrot(rot)
- Sets the direction that the camera is facing. (the direction raycasts will originate from)

getRCrot()
- Returns the current rotation of the camera.

setRCpos(pos)
- Sets current position of the camera in WC (location that raycasts originate)

getRCpos()
- Returns current position of the camera in WC.

rayCast(GridMap)
- Returns an array of raycasts
- Provides information about hit/no hit, distance of hit, which object was hit.
- This function will be called by GridMap.draw() to determine what parts of the map should actually be drawn

getRayCasts()
- Returns most recent Raycast
- (used by RC_RenderableSprite.draw() to determine whether the sprite is visible)

DrawRays()
- Draws the most recent Raycasts that have been stored by the RCCamera after raycasting onto a GridMap.

getHorizonLine()
setHorizonLine(height)
moveHorizonLine(d)
- Getter/Setter/Mover for the horizon line the raycaster renders with.

getFishEye()
setFishEye(b)
- Getter/Setter for whether to use FishEye effect


## GridMap API:

RC_GridMap(2DArrayOfTiles, xWidth, yWidth, xPos, yPos)
setTile(Tile, xIndex, yIndex)
- Function for modifying one element of the gridmap

setTiles(2DArrayOfTiles)
- Function for setting the elements of the gridmap

setPosition(xPos, yPos)
- This allows us to change where the gridmap is located in world coordinates (WC)

setSize(x, y)
- Increases the width and height of the gridmap.

setTile(xIndex, yIndex)
- Returns the Tile at the specified coordinates in the gridmap.

setPosition()
- Returns WC offset of the gridmap (as set by SetPosition)

setSize()
- Returns width and height of the gridmap

getTileAtIndex(x,y)
- Returns the Tile at the specified index within the Gridmap


## Tile API:

Tile(topTexture, bottomTexture, leftTexture, rightTexture)
getTopTexture()
setTopTexture(tex)
getBottomTexture()
setBottomTexture(tex)
getLeftTexture()
setLeftTexture(tex)
getRightTexture()
setRightTexture(tex)
- Setters and getters for the textures of each side of a tile (getters utilized by RCCamera when determining which texture to render onto a tile)

## RCSpriteRenderable API:

RC_RenderableSprite(spriteRef)
- Constructor, sets the sprite reference associated with the class instance

getScaleX()
setScaleX(x)
- Getter and setter for X scale that the RCSpriteRenderable is rendered with.

getScaleY()
setScaleY(y)
- Getter and setter for Y scale that the RCSpriteRenderable is rendered with.

getYOffset()
setYOffset(y)
- Getter and setter for Y offset (allows the user to control how high on the screen the RCSpriteRenderable should be rendered.

draw(RC_Camera, position)
- Draws the sprite if visible (RC_Camera’s current raycasts + position + the sprite’s position are both taken into account)

