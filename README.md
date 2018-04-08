# Chip8 Octo Examples
Code examples for Chip8 using the Octo Assembly Language

Displayed below, you will see the examples ordered by complexity and displayed with a description, an image, and comments to help you learn the language. Some examples will include a tutorial to guide you through each part of the example in greater detail.

## Helpful Links
To run these examples and other Octo code, there is [an online compiler](https://johnearnest.github.io/Octo/) available.

There is also a [detailed manual](https://github.com/JohnEarnest/Octo/blob/gh-pages/docs/Manual.md) for Octo.

In addition to the above manual, those looking to learn the Octo language should check out the [beginner's guide](https://github.com/JohnEarnest/Octo/blob/gh-pages/docs/BeginnersGuide.md)
and the [intermediate guide](https://github.com/JohnEarnest/Octo/blob/gh-pages/docs/IntermediateGuide.md).

# The Examples
###### The examples provided in this repository, complete with images and descriptions.

### Drawing a Sprite

<details> 
  <summary>Detailed tutorial for this example</summary>
   <p> </p>
   The beginning of a program is defined with the main label as seen below.
   <p> </p> 
   Chip8 provides a screen which is 64x32 pixels. 
   <p> </p>
   There are 16 registers available: v0-v9 and va-vf (v0, v1, v2, v3, v4, v5, v6, v7, v8, v9, va, vb, vc, vd, ve, vf).
   These registers can hold a number value from 0 to 255.
   <p> </p>
   There is also a special register called i which can store an address. In this example, it will be storing the address
   for the ball sprite so it can be used by the sprite instruction when drawing.
   <p> </p>
   Sprites are drawn by providing the address of a sprite ("ball" in this example) to the i register 
   and calling the sprite instruction with 3 parameters: x position, y position, and sprite height.
   Sprites can have a maximum height of 15 pixels. They are always 8 pixels wide.
   <p> </p>
   In this example, the ball sprite is made up of hexadecimal numbers (denoted by 0x at the start of each).
   
   You can also define a sprite with binary numbers (started with 0b).	
   Sprites can be made up of rows of binary numbers. Keeping in mind the fact that sprites are always 8 pixels
   wide, you could represent a sprite with a height of 1 like this:
   
   0b01010101
   
   This would place a pixel at every other horizontal position.
   
   Now if we wanted a straight verticle line, we would use multiple rows like so:
   
   0b00010000
   0b00010000
   0b00010000
   0b00010000
   0b00010000
   
   This would create a verticle line down the middle of your sprite which is now 5 pixels tall (5 rows).
   <p> </p>
   Additionally, when drawing a sprite you will invert the pixels occupying that space. Drawing a sprite over
   another will erase what was there as if no pixels were drawn in that space by your program. Likewise, drawing where
   a sprite is not already being drawn will switch the pixels for that area and allow your sprite to be seen.
   <p> </p>
</details>

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
