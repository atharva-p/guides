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

# Surface

pygame object for representing images 

`Surface((width, height), flags=0, depth=0, masks=None) -> Surface`

The first tuple sets the size of the surface. Surfaces need to be bind to the main display surface for them to actually be displayed. 

## binding a surface to the main display 

This is done using the `Surface.blit()` function 

`blit(source, dest, area=None, special_flags=0) -> Rect` 

`source` denotes the display that will be bound to the display from which this function is being called (for example, `screen.blit(test_surface, (w, h))` will bind `test_surface` to main display)

`dest` can be a tuple(width, height) representing the position of the upper left corner of the `source` surface that will be bound. 