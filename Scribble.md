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