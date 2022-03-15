[Home](https://daneoj.github.io/Doomers_RayCast_API/)  [Tutorial](https://daneoj.github.io/Doomers_RayCast_API/Tutorial)  [Demos And Conclusion](https://daneoj.github.io/Doomers_RayCast_API/DemosAndConclusion)

## Demos

[Pick-up Demo](https://daneoj.github.io/452_Pickup_Demo/)

[Bubble Shooter Demo](https://thesquashedman.github.io/RayCast-Project/)

## Conclusion

### Strengths:
Robust support for Raycasting, including a GridMap object + tiles for easy map design, a RCCamera for easy raycasting + rendering, and a RCSpriteRenderable for implementing other objects within the gameworld that need to be rendered.
### Weaknesses:
Perhaps it could have tighter implementation that fits within existing API calls more cleanly.
Certain tasks require making custom classes (I.e., modifying GameObject class to use a RCSpriteRenderable)
### Thoughts:
If we had more time, we would like to add better support for default engine items such as GameObjects to allow them to be used more seamlessly within our Raycasting API. This task is somewhat difficult since raycasting requires certain optimizations and special fields that many of these objects do not support by default.
