# Tutorial

[Home](https://daneoj.github.io/Doomers_RayCast_API/)  [Tutorial](https://daneoj.github.io/Doomers_RayCast_API/Tutorial)  [Demos And Conclusion](https://daneoj.github.io/Doomers_RayCast_API/DemosAndConclusion)

## Part 1: Setting up GridMap

First, we need to make some tiles to use with the gridmap.
Here, we input 4 textures into the Tile constructor, one for each side of the tile (top, bottom, left, and right).
We then make a tile array, to pass into the gridmap later.

```
. . .
This.tile1 = new engine.Tile(this.kWall1, . . . );
This.tile2 = new eTile(this.kWall2, . . . );
this.tileArray = [
[this.tile1, this.tile1, this.tile2, this.tile1, this.tile2],
[this.tile1, this.tile1, this.tile2, this.tile1, this.tile2],
. . .
];
. . .
```

Next, let’s set up our GridMap, and populate it with tiles.
```
This.mGridMap = new engine.GridMap();
this.mGridMap.setTiles(tileArray);

```

## Part 2: Creating a RCCamera and RCSpriteRenderable

Our Raycaster API uses a special camera called a RCCamera to do all of the raycasting and rendering. We can set one up like this:
```
. . .
this.mCamera = new engine.RCCamera(
	vec2.fromValues(50,37.5),
	100,
	[0,0,640,480]
);
. . .
```

Just like a normal camera, a RCCamera takes in a vec2 for its position, a value for its width, and then an array of 4 numbers showing the starting x/y positions of the viewport, as well as its width and height.
Now, we can focus on creating a RCSpriteRenderable.

```
. . .
this.mSpriteRenderable = new engine.RCSpriteRenderable(this.kSprite);
. . .
```

Pretty simple! Just like a normal sprite renderable, all we need to do is pass a sprite into the constructor. If we’d like, we can adjust the scale and y offset of this renderable, like so:
```
. . .
this.mSpriteRenderable.setScaleX(1.5);
this.mSpriteRenderable.setScaleY(0.9);

this.mSpriteRenderable.setYOffset(0.5);
. . .
```
Now we have a RCSpriteRenderable, a GridMap, and a RCCamera to render them with!

# Part 3: Rendering

In your game’s draw function, we only have to do a few simple tasks.
First, we need to perform a raycast upon the GridMap. This sets up some crucial information within the camera, and allows us to then draw the result later.

Then, we setViewAndCameraMatrix(), just like a normal camera, before we draw.

From there, we call RCCamera’s DrawRays() function to render what we have calculated.

```
. . .
this.mCamera.Raycast(this.mGridMap);

this.mCamera.setViewAndCameraMatrix();

this.mCamera.DrawRays()
. . .
```

Now, we can render our RCSpriteRenderable very similarly to any SpriteRenderable.
We simply call the draw function of our RCSpriteRenderable, as well as the position (in grid map coordinates) that we want the RCSpriteRenderable to be rendered (if visible).

```
. . .
this.mSpriteRenderable.draw(this.mCamera, posToBeRendered);
. . .
```
With this, our RCCamera will determine if the RCSpriteRenderable should be rendered. By implementing these tools in conjunction with existing engine tools, and some custom classes, you should be able to get up and running with a raycast-style game in no time!


