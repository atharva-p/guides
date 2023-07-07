# basic structure 

```python 
import pygame 
import sys

pygame.init()

screen = pygame.display.set_mode((800, 450))
pygame.display.set_caption("Your window caption here")

clock = pygame.time.Clock()

while True: 
	for event in pygame.event.get(): 
		if event.type == pygame.QUIT: 
			pygame.quit()
			sys.exit()

	pygame.display.update()
	clock.tick(60)

```

1. `pygame.init()` will initialize all pygame modules and is required to be called
2. `display.set_mode()` expects a tuple with the screen size (best set according to your screen resolution) and can also take additional arguments (if not passed will use the default ones) 
3. `time.Clock()` creates a clock object
4. `while True:` holds the main interface 
5. `pygame.event.get()` will give all the event classes that have occurred in a list. Every event class has an `type` class attribute which is an `int`. This can be compared with `pygame.QUIT` which is also an `int`. [`pygame.quit()`](https://www.pygame.org/docs/ref/pygame.html?highlight=quit#pygame.quit) is optional, uninitialises all the pygame modules. `sys.exit()` will stop program execution
6. `pygame.display.update()` updates the screen 
7. `clock.tick(60)` will limit the framerate to 60 fps (which means it will stop the `while True:` from running more than 60 times a second). Also returns time in milliseconds that has passed since the last frame. 

Updating the display and the clock tick should happen at the end (my theory) 

# Surface

pygame object for representing images 

`Surface((width, height), flags=0, depth=0, masks=None) -> Surface`

The first tuple sets the size of the surface. Surfaces need to be bind to the main display surface for them to actually be displayed. 

## binding a surface to the main display 

This is done using the `Surface.blit()` function 

`blit(source, dest, area=None, special_flags=0) -> Rect` 

`source` denotes the display that will be bound to the display from which this function is being called (for example, `screen.blit(test_surface, (w, h))` will bind `test_surface` to main display)

`dest` can be a tuple(width, height) representing the position of the upper left corner of the `source` surface that will be bound. 

## converting surfaces for fast blitting

surfaces are recommended to be converted to optimize the blitting performance 

`Surface.convert()` - this will convert the surface to the most optimized pixel format for blitting. this method will remove any alpha values from the original image (opacity values). 

`Surface.convert_alpha()` - same function as the above method but preserves alpha values of the images. 

# Text 

There are two steps in inserting text into the game 
1. create a font object using `font.Font(file_path, size)`, use `None` instead of the path to use the default pygame font 
2. render the font object using `font.render(text, anti_alias, color)`

# Rectangles 

Rectangles allow you to place at positions much precisely compared to positioning with surfaces. Rectangles also provide basic collision detection 


![[Pasted image 20230705152859.png]]

1. create a surface with the imported image 
2. get a rectangle from that surface, you can also pass positional keyword arguments  `test_rect = test_surface.get_rect(bottomleft=(0, 300))`
3. you can change the position of the rect by accessing the rect attributes `test_rect.left += 10`
4. blit the rectangle in the main loop `screen.blit(test_surface, test_rect)`  

# detecting key presses 

there are two methods 

1. using `key.get_pressed()` this will return an object containing bool values of all keys. Pass the key constant to get the bool for the desired key (for example `keys_pressed[pygame.K_SPACE]`). Note that this method will generate bool values for the duration of the key press. Not ideal if you only want one bool per key stroke
2. using the event loop. check if `event.type == pygame.KEYDOWN`  or keyup. To check for a specific key, check for `if event.key == pygame.K_SPACE` 
