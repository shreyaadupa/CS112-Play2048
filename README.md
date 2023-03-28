# Personal Note
Hi! 👋

This is the Play 2048 Game Assignment from the Rutgers CS112 Course. 

Note to future students: it's an overall easy assignment! Have fun with it!

Below are the assignment instructions:

# Overview
2048 is a puzzle game where you use the arrow keys to move left, right, up or down to merge tiles of the same number together. Check it out if you never played it before.

The goal of the game is to keep merging numbered (non-zero) tiles until you get one 2048 tile. If two tiles with the same number touch each other, they are merged together in the direction swiped into a new tile with twice the value. (ex: if you move up, the topmost value doubles and the bottom value becomes 0). Be careful with your moves – if the board is full at the end of a turn and there are no other valid moves, it’s game over!

In this assignment, we will represent the 2048 grid as a 4×4 array of integers, with 0’s representing empty tiles. Note that we will grade your individual operations – not your score or ability to get to 2048. 

# Implementation
Overview of files provided
We provide two drivers (text and graphic) to help you test the individual methods. We suggest that you start with the text driver but once you have a good understanding of the assignment then you may use the graphic driver.

Board: The Board class contains all methods needed to construct a functioning 2048 game. Edit the empty methods with you solution, but DO NOT edit the provided ones or the methods signatures of any method. This is the file you submit.
BoardSpot: An object used to represent a location on the board. It houses a row and a column, along with getters and setters. Don’t edit or submit to Autolab.
TextDriver: A tool to test your 2048 board interactively using only text-based boards. This driver is equivalent to AnimatedDriver and functions in the same way – you are free to use this driver to test all of your methods. Feel free to edit this class, as it is provided only to help you test. It is not submitted and/or graded.
To use this driver, pick whether you want to test individual methods or play the full game (this option requires all methods to be completed) by selecting the number that appears for each option. 
To test individual methods, first type in the full file name for an input file. Then, select a method to test by typing in the number that appears for each method in the list. Additionally, for makeMove, moves are represented by using the WASD keys like arrow keys (w is up, a is left, s is down, and d is right). Type in the letter corresponding to the move you want to test.
Playing the full game makes use of the WASD keys like arrow keys (W is up, A is left, S is down, and D is right). Press “Q” to quit.
AnimatedDriver: A tool to test your 2048 board interactively through rendered images. This driver is equivalent to TextDriver and functions in the same way – you are free to use this driver to test all of your methods. Feel free to edit this class, as it is provided only to help you test. It is not submitted and/or graded.
To use this driver, pick whether you want to test individual methods or play the full game (this option requires all methods to be completed) by selecting the number that appears for each option. 
To test individual methods, first type in the full file name for an input file. Then, select a method to test by typing in the number that appears for each method in the list. You will then see the board stored in the input file. For all methods besides makeMove, press any key to test your method. Press any key again to exit testing that method.
For makeMove, moves are represented by using the WASD keys like arrow keys (w is up, a is left, s is down, and d is right). Type in the letter corresponding to the move you want to test when you see the board stored in the input file. Once you type that letter, the move you want to test will be made. Press any key afterward to exit testing that method.
Playing the full game makes use of the WASD keys like arrow keys (w is up, a is left, s is down, and d is right). Press “q” to quit.
StdIn and StdOut: libraries to handle input and output. Do not edit these classes.
StdRandom: Provides methods for generating random numbers. Don’t edit or submit to Autolab.
Collage, Picture, StdDraw: Helper libraries to support AnimatedDriver. Don’t edit or submit to Autolab.
Input Files: Preset boards you’re able to use to test your 2048 board in the drivers (intput1.in, input2.in,…). You can use all input files to test all methods. Each input file contains 4 lines, each with 4 space separated numbers. Each number is either 0 (represents an empty space) or a power of 2 (represents a normal tile). Feel free to make your own input files, as they will not be submitted to Autolab.
Board.java
DO NOT add new import statements.
DO NOT change any of the method’s signatures.
Methods to be implemented by you:

# 1. updateOpenSpaces
This method adds a BoardSpot to the openSpaces array for every  board open spot.
A spot (i, j) is open when gameBoard[i][j] = 0.
Initialize a new ArrayList of BoardSpot objects in openSpaces.
Add to openSpaces all pairs (row, column) where gameBoard[row][column] is 0 (ie. the tile is empty). Use BoardSpot objects to represent these pairs.
Submit Board.java with this method completed under Early Submission to receive extra credit.
Note: DO NOT call updateOpenSpaces in any method. The driver/Autolab will call updateOpenSpaces and addRandomTile before making a move.

# 2. addRandomTile
Note: updateOpenSpaces must be completed before starting this method.

This method adds a random tile into the board, following these rules:

First, pick a random BoardSpot from the openSpaces ArrayList (test cases are guaranteed to always have an open space). Use StdRandom.uniform(int a, int b) to generate a random integer between a lower bound “a” up to (but not including) an upper bound “b”. 
To randomly pick a board spot the lower bound is 0 and the upper bound is the number of items in the ArrayList.
Next, assign a value to the tile. There is a 90% chance that a 2 tile will be inserted and a 10% chance that a 4 tile will be inserted. Use StdRandom.uniform(double a, double b) to generate a random double between a lower bound “a” up to (but not including) an upper bound “b.”
To randomly pick a number between 0 and 1 the lower bound is 0 and the upper bound is 1.
If this value is less than, but not equal to, 10 percent (0.1), the tile will have a 4 value. Otherwise, the tile will have a 2 value.
Be sure to update the correct tile in the gameBoard array (as defined by the BoardSpot’s row and column values) with the proper value. 
Note: On the driver updateOpenSpaces() is called before this method to ensure that openSpaces is up to date. You do not need to remove the board spot from the openSpaces ArrayList!
Note: On the driver, the seed is set so you will get the same outputs every time when testing individual methods. Autolab uses the same seed as the driver to test this method. However, when playing the full game, the driver will not use seed values – it will use random values to generate different boards and tiles.

# 3. swipeLeft
Move all tiles as far left as possible while maintaining the same order and number of tiles.

There should be no empty spaces to the left of any tile.
Remember that 0 (gameBoard[row][col] = 0) represents an empty space. 

# 4. mergeLeft
Merge all identical nonzero, horizontal pairs in the board.

The leftmost neighbor (ex. The first 2 in “0 2 2 0”) will double its value, while the rightmost neighbor (ex. The second 2 in “0 2 2 0”) will become 0. The method will turn this row into “0 4 0 0”. 
Only pairs will merge. 3-tile neighbors and 4-tile neighbors will not merge to become one tile. For example, “2 2 2 0” becomes “4 0 2 0” and “2 2 2 2” becomes “4 0 4 0”. 

The next two methods (transpose and flipRows) can be applied in sequence to rotate the board 90 degrees clockwise. This will allow you to reuse your existing code for swipeLeft and mergeLeft for any of the four directions.

For example, we can swipe right by rotating the board twice, calling swipeLeft, then rotating the board twice to return it to its original orientation. The provided method rotateBoard calls transpose and flipRows in sequence to complete a 90 degree clockwise rotation.

# 5. transpose
Interchange the rows and columns of the board. In other words, row 1 should become column 1, row 2 becomes column 2, and so on. More formally, gameBoard[i][j] becomes gameBoard[j][i] for all 0 <= i < 4 and 0 <= j < 4. 

Transposing flips the board along its main diagonal (top left to bottom right). 

# 6. flipRows
Reverse all rows.

Columns 1, 2, 3, and 4 (in order) will have a new order of 4, 3, 2, and 1. For example, the row “2 0 4 0” would become “0 4 0 2”.
Repeat this procedure for all 4 rows.

# 7. makeMove
Putting everything together by calling previous methods to construct 2048 moves in all directions. Rotate as necessary to complete this method using different directions. Swipe left, merge neighbors, and swipe left again to re-fill blank spaces. 

The method input parameter is a character that indicates which direction to move (‘U’ = up, ‘R’ = right, ‘D’ = down, ‘L’ = left). Assume that you will only receive these characters, case-sensitive, as arguments in the makeMove method.
Be sure to have transpose, flipRows, swipeLeft, and mergeLeft completed before doing this method and all previous methods completed before testing.
As stated earlier, call rotateBoard to help with non-left directions. This allows for MUCH better code reuse than redoing your swipeLeft and mergeLeft in 3 new directions.
To test this method, select the “makeMove” option in either driver and enter a character. You can use the W, A, S, and D keys like arrow keys (w = up, a = left, s = down and d = right). Even though you will be using the WASD keys like arrow keys, these keys still map to U, L, D, and R respectively; for instance, pressing W will call makeMove with ‘U’ as the letter parameter.

# Implementation Notes
YOU MAY only update the methods updateOpenSpaces(), addRandomTile(), swipeLeft(), mergeLeft(), transpose(), flipRows(), and makeMove().
COMMENT all printing statements from Board.java
DO NOT add any instance variables to the Board class.
DO NOT add any public methods to the Board class.
DO NOT add/rename the project or package statements.
DO NOT change the class Board name.
YOU MAY add private methods to the Board class.
YOU MAY use any of the libraries provided in the zip file.
DO NOT use System.exit()


