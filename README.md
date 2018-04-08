# Chip8 Octo Examples
Code examples for Chip8 using the Octo Assembly Language

## Helpful Links
To run these examples and other Octo code, there is [an online compiler](https://johnearnest.github.io/Octo/) available.

There is also a [detailed manual](https://github.com/JohnEarnest/Octo/blob/gh-pages/docs/Manual.md) for Octo.

In addition to the above manual, those looking to learn the Octo language should check out the [beginner's guide](https://github.com/JohnEarnest/Octo/blob/gh-pages/docs/BeginnersGuide.md)
and the [intermediate guide](https://github.com/JohnEarnest/Octo/blob/gh-pages/docs/IntermediateGuide.md).

# The Examples
###### The examples provided in this repository, complete with images and descriptions.

### Drawing a Sprite

```
: ball
0x18 0x3C 0x7E 0x7E 0x3C 0x18 0x00 0x00 0x00 0x00 0x00 0x00 0x00 0x00 0x00 

: main
	v0 := 8
	v1 := 10

	i := ball # Assign our ball sprite to the i register so the sprite instruction can use it

	sprite v0 v1 6 # Sprite instruction. Parameters: x, y, sprite height
```

Result:

![drawing a sprite](https://i.imgur.com/RjJebhi.png)

Additionally, you could extend this example by making use of the if statement and aliases:

```
: ball
0x18 0x3C 0x7E 0x7E 0x3C 0x18 0x00 0x00 0x00 0x00 0x00 0x00 0x00 0x00 0x00 

# Aliases are pretty straight forward.
# :alias <name> <register> assigns an alias for that register.
:alias x v0
:alias y v1

: main
	x := 8
	y := 10

	v2 := 0 # Switch this to a 1 to trigger the if statement and move your sprite
	if v2 == 1 then x += 10

	i := ball # Assign our ball sprite to the i register so the sprite instruction can use it

	sprite x y 6 # Sprite instruction. Parameters: x, y, sprite height
```
