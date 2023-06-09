### aces 
if score > 21, see the hand for any key that is an ace (14) and note their positions in a separate list which will hold the ace positions 

**possibilities of having to optimize for ace** 
1. 11 + 10 then change it to 1 + 10
2. 11 + 2 + 11 (total 24), change it to 11 + 2 + 1 (total 14)
3. 11 + 2 + 1 + 6 + 11 (total 31) change it to 11 + 2 + 1 + 6 + 1 (total 21 blackjack)
4. 11 + 2 + 1 + 6 + 1 + 1 (total 22), change it to 1 + 2 + 1 + 6 + 1 + 1 (total 12)

if in `check_score()` score > 21, check for aces and return positions if found, else return None? 