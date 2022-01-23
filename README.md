# Conway-s-Game-of-Life
An exercise to practice lists and loops


import random
import time 
import copy
WIDTH = 20
HEIGHT = 10

# Create a list of lists for the cells:
nextCells = []
for x in range(WIDTH):
    column = []    # create a new column
    for y in range(HEIGHT):
        if random.randint(0,1) == 0:
            column.append('#')  # add a living cell
        else:
            column.append(' ')  # add a dead cell
    nextCells.append(column)  # nextCells is a list of column lists

# Main game loop 
while True:
    print('\n\n\n\n\n')  # Seperate each step with new lines
    currentCells = copy.deepcopy(nextCells)

    # Print currentCells on the sceen:
    for y in range(HEIGHT):
        for x in range(WIDTH):
            print(currentCells[x][y], end=' ')
        print()  # prints a new line at the end of the row

    # Calculate the next step's cells based on current step's cells:
    for x in range(WIDTH):
        for y in range(HEIGHT):
            leftCoord = (x - 1) % WIDTH
            rightCoord = (x + 1) % WIDTH
            aboveCoord = (y - 1) % HEIGHT
            belowCoord = (y + 1) % HEIGHT

            numNeighbors = 0
            if currentCells[leftCoord][aboveCoord] == '#':
                numNeighbors += 1  # Top-left neighbor is alive
            if currentCells[x][aboveCoord] == '#':
                numNeighbors += 1  # Top neighbor is alive
            if currentCells[rightCoord][aboveCoord] == '#':
                numNeighbors += 1  # Top-right neighbor is alive
            if currentCells[leftCoord][y] == '#':
                numNeighbors += 1  # Left neighbor is alive
            if currentCells[rightCoord][y] == '#':
                numNeighbors += 1  # Right neighbor is alive
            if currentCells[leftCoord][belowCoord] == '#':
                numNeighbors += 1  # Bottom-left neighbor is alive
            if currentCells[x][belowCoord] == '#':
                numNeighbors += 1  # Bottom neighbor is alive
            if currentCells[rightCoord][belowCoord] == '#':
                numNeighbors += 1  # Bottom-right neighbor is alive
                
            if currentCells[x][y] == '#' and (numNeighbors == 2 or numNeighbors == 3):
                nextCells[x][y] = '#'
            elif currentCells[x][y] == ' ' and numNeighbors == 3:
                nextCells[x][y] = '#'
            else:
                nextCells[x][y] = ' '
    
    time.sleep(10)  # Add a 10 second pause to reduce flickering and to examine the new patterns.
