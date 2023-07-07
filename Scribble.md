# obstacles

video solution 
1. make a obstacle rect list 
2. add a new obstacle rect to the list when the obstacle event runs 
3. for every rect in that list, move it to the left
4. delete it from the list when it goes out of the screen 

my solution 
1. create a rect obstacle list 
2. have `random.choice()` choose a rect (with more bias towards snails) on every OBSTACLE_EVENT and blit that to the screen, at a randomly chosen position 
3. move it to the left, snails should move slower than flys, flys should be faster 
4. delete the blitted rect from the screen when it goes outside the screen (just don't draw it again)

solution 2 
1. create rects from surfaces of snail and fly and store in separate lists 
2. blit them separately in 80-20 prob 
3. control speed separately 
4. delete rects when they go outside screen 

code used to make snail move 

```python
# outside main loop 
snail_rect = snail_surface.get_rect(bottomleft=(800, 300))

# inside main loop 
screen.blit(snail_surface, snail_rect)  
  
snail_rect.x -= 5  
if snail_rect.right < 0:  
snail_rect.left = 800
```
