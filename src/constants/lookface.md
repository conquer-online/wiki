# Look Face

The look face of a player or monster is the mesh calculation for the 3D role. While the monster look face is rather simple (just the monster type), the look face of a player is more complicated and follows this equation: 

```
Look = Body + (Avatar x 10000) + (Transformation x 10000000)
```
