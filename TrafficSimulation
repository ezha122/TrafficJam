#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

#define NUM_ROWS 8
#define NUM_COLS 8

#define SPACE 0
#define WALL -1
#define EXIT -2

/***********************************************************/
/***********************************************************/
/******* ADD THE REQUIRED FUNCTIONS BELOW THIS POINT *******/
/***********************************************************/
/***********************************************************/

// Your function definitions should go here...

#include <stdio.h>

#define NUM_ROWS 8
#define NUM_COLS 8

#define SPACE 0
#define WALL -1
#define EXIT -2

void InitialiseRoad(int road[NUM_ROWS][NUM_COLS], char side, int pos);
void PrintRoad(int road[NUM_ROWS][NUM_COLS]);
double PercentUsed(int road[NUM_ROWS][NUM_COLS]);
void AddCar(int road[NUM_ROWS][NUM_COLS],int row, int col, int size);
void FindCar(int road[NUM_ROWS][NUM_COLS], char move, int *rowStart, int *colStart, int *rowEnd, int *colEnd);
int MoveCar(int road[NUM_ROWS][NUM_COLS], int r0, int c0, int r1, int c1);

// this function creates an array for the road
// inputs: road[NUM_ROWS][NUM_COLS] is the array that the road is initialised on
//         side is the side of the road that the exit is placed on out of the North,
//         South, West and East side
//         the pos value is the number of spaces from the top if on horizontal wall,
//         the pos value is the number of spaces from the left
// output: the final result produces an array that has walls and an exit set on one
//         of the walls. Everything within the wall is empty space
void InitialiseRoad(int road[NUM_ROWS][NUM_COLS], char side, int pos)
{
    int i, j;
    
    // set the top and bottom rows as the wall
    for (i = 0; i < NUM_ROWS; i++) {
        road[i][0] = WALL;
        road[i][NUM_COLS - 1] = WALL;
    }
    
    //set the two side walls
    for (j = 0; j < NUM_COLS; j++) {
        road[0][j] = WALL;
        road[NUM_ROWS - 1][j] = WALL;
    }
    
    // everything between the walls are set as space
    for (i = 1; i < NUM_ROWS - 1; i++) {
        for (j = 1; j < NUM_COLS - 1; j++) {
            road[i][j] = SPACE;
        }
    }
    
    // Exit is places in the side indicated and placed according to the position
    if (side == 'N') {
        road[0][pos] = EXIT;
    } else if (side == 'S') {
        road[NUM_ROWS - 1][pos] = EXIT;
    } else if (side == 'W') {
        road[pos][0] = EXIT;
    } else {
        road[pos][NUM_COLS - 1] = EXIT;
    }
    
}


// This function prints the road that has been initialised with the  InitialiseRoad
// function.
// inputs: road - array that has been initialised
// outputs: the road is printed with WALL being #, EXIT being O and SPACE being an
//          empty space.
void PrintRoad(int road[NUM_ROWS][NUM_COLS])
{
    int i, j;
    
    //
    
    for (i = 0; i < NUM_ROWS; i++) {
        for (j = 0; j < NUM_COLS; j++) {
            if (road[i][j] == WALL) {
                // values set as WALL are printed as "#"
                printf("#");
            } else if (road[i][j] == EXIT) {
                // value set as EXIT is printed as 'O'
                printf("O");
            } else if (road[i][j] == SPACE) {
                // values set as SPACE are printed as an empty space
                printf(" ");
            } else if (road[i][j] >= 'A' || road[i][j] <= 'Z') {
                // cars are printed as their assigned letter
                printf("%c", road[i][j]);
            }
        }
        printf("\n");
    }
    
}

// this function calculates the percentage of the road that has been used by the cars
// inputs: the array of the road
// output: final fraction of how much of the road is taken up by the cars
double PercentUsed(int road[NUM_ROWS][NUM_COLS])
{
    // total area is the product of the NUM_COLS - 2 and NUM_ROWS - 2
    int total = (NUM_COLS-2) * (NUM_ROWS-2);
    
    // initialise the veriables for the rows and columns
    int i, j;
    // count value is the number of spaces used by the cars
    int count = 0;
    
    // this is the final output
    double percentage;
    
    // scan through the road (within the walls) for spaces that are not between
    // 'A' and 'Z', when a space in the array is empty, then count will increase
    // by a value of one
    
    for (i = 1; i < NUM_ROWS-1; i++) {
        for (j = 1; j < NUM_COLS-1; j++) {
            if (road[i][j] != SPACE ) {
                count++;
            }
        }
    }
    
    // percentage is calculated by dividing the count value and the total
    // then multiplying by 100
    percentage = (double) count/total * 100;
}

// This function adds a car into the game, and ensures there are no overlaps between 
// the added car and any that already exist on the road. If a collision were to occur, 
// a car will not be added
// inputs: row - the row number the user wants the car to be placed on 
           col - the column number the user wants the car to be placed on 
void AddCar(int road[NUM_ROWS][NUM_COLS],int row, int col, int size)
{
    int i, j;
    
    int count = 0;
    
    // set car to be initially A
    int car = 'A';
    
    // scan through the road to see what cars are already present, if the value
    // is found in the array, then the value increases by one and becomes the
    // next letter in the alphabet - this repeats until the entire array is scanned
    for (i = 1; i < NUM_ROWS - 1; i++) {
        for (j = 1; j < NUM_COLS - 1; j++) {
            if (road[i][j] >= car) {
                car = road[i][j];
                car++;
            }
        }
    }
    
    // positive value for size means the car will be places horizontally
    if (size > 0) {
        //[row][col] is the left most value
        
        // check if all positions in the array needed are empty and that no
        // collisions will occur
        for (j = col; j < col + size; j++) {
            // if none of the spaces are occupied, then count will remain 0
            if (road[row][j] != SPACE) {
                count++;
            }
        }
        
        // if all spaces are not occupied, then the car will be placed in the
        // positions that were just scanned
        if (count == 0) {
            for (j = col; j < col + size; j++) {
                road[row][j] = car;
            }
        }
    // positive value for size means the car will be places horizontally
    } else {
        //vertical, [row][col] is uppermost value
        // check if all positions in the array needed are empty and that no
        // collisions will occur
        for (i = row; i < row - size; i++) {
            if (road[i][col] != SPACE) {
                count++;
            }
        }
        
        // if all spaces are not occupied, then the car will be placed in the
        // positions that were just scanned
        if (count == 0) {
            for (i = row; i < row - size; i++) {
                road[i][col] = car;
            }
        }

    }

}


// this function finds the row and column value for the start and end of the car given 
// inputs: move - the car to be found
//         road - the array which has already been initialised 
// outputs: rowStart/colStart/rowEnd/colEnd - these are where the found values will be stored 
void FindCar(int road[NUM_ROWS][NUM_COLS], char move, int *rowStart, int *colStart, int *rowEnd, int *colEnd)
{
    int i, j;
    int count = 0;
    
    // set arrays to store values for the car's positions
    int car_row[NUM_ROWS-2];
    int car_col[NUM_COLS-2];
    
    // scan through the array
    for (i = 0; i < NUM_ROWS; i++) {
        for (j = 0; j < NUM_COLS; j++) {
            // if array position equals the car letter, then the row and column
            // value are stored in the respective arrays. the arrays size should
            // not exceed NUM_ROWS-2 or NUM_COLS-2
            if (road[i][j] == move) {
                if (count <= NUM_ROWS-2) {
                    car_row[count] = i;
                }
                if (count <= NUM_COLS-2) {
                    car_col[count] = j;
                }
                // count tracks the array position, increasing with every loop
                // making sure that the first values in the array are the left
                // most and going towards the right or the top most and going
                // down
                count++;
            }
        }
    }
    
    if (car_col[0] == car_col[1]) {
        //the car is horizontal
        
        *colStart = car_col[0];
        *rowStart = car_row[0];
        // first value in each array becomes the start row and column value
        *colEnd = car_col[0];
        *rowEnd = car_row[count-1];
    } else {
        // the car is vertical
        
        // first value in each array becomes the start row and column value
        *colStart = car_col[0];
        *colEnd = car_col[count-1];
        *rowStart = car_row[0];
        *rowEnd = car_row[0];
    }
}

// this function moves the car to 
// inputs: r0, c0 - the coordinates of either the leftmost or uppermost block the car occupies, depending on whether it is horizontal or vertical, respectively
           r1, c0 - the coordinates of either the rightmost or lowermost block the car occupies, depending on whether it is horizontal or vertical, respectively
int MoveCar(int road[NUM_ROWS][NUM_COLS], int r0, int c0, int r1, int c1)
{
    int i, j;
    int count = 0;
    int car = road[r0][c0];
    
    //
    if (c0 == c1) {
        //vertical car
        
        // count the number of empty spaces above the car and store into the count integer
        for (i = r0 - 1; i > 0; i--) {
            if (road[i][c0] == SPACE) {
                count++;
            } else {
                break;
            }
        }
        
        // no spaces above the car means count will remain 0, this means that
        // the car cannot be moved up
        if (count == 0) {
            // the values below the car will now be scanned to find empty
            // spots to move to
            for (i = r1 + 1; i < NUM_ROWS; i++) {
                if (road[i][c0] == SPACE) {
                    count++;
                } else {
                    break;
                }
            }
            
            // if count is larger than 0 in this instance then the car will be
            // moved down
            if (count > 0) {
                // make all the the spaces the car originally occupied empty
                for (i = r0; i <= r1; i++) {
                    road[i][c0] = SPACE;
                }
                
                // place the car count number of spaces below the original position
                for (i = r0 + count; i <= r1 + count; i++) {
                    road[i][c0] = car;
                }
                
            // set the new values of the upper most and lower most positions of
            // the car
            r0 -= count;
            r1 -= count;
            }
        } else {
            // there are empty spaces above the car
            // make all the the spaces the car originally occupied empty
            for (i = r0; i <= r1; i++) {
                road[i][c0] = SPACE;
            }
            
            // place the car count number of spaces above the original position
            for (i = r0 - count; i <= r1 - count; i++) {
                    road[i][c0] = car;
                }
                
            // set the new values of the upper most and lower most positions of
            // the car
            r0 -= count;
            r1 -= count;
        }
        
        //car is next to exit = return 1
        // if car is not by the exit then return 0
        if (road[r1 + 1][c0] == EXIT || road[r0 - 1][c0] == EXIT) {
            return 1;
        } else {
            return 0;
        }
        
        
    } else {
        //horizontal car
        
        // count the number of empty spaces to the left of the car and store
        // into the count integer
        for (j = c0 - 1; j > 0; j--) {
            if (road[r1][j] == SPACE) {
                count++;
            } else {
                break;
            }
        }
        
        // no spaces to the left of the car means count will remain 0, this
        // means that the car cannot be moved to the left
        if (count == 0) {
            // count the number of empty spaces to the right of the car
            for (j = c1 + 1; j < NUM_COLS; j++) {
                if (road[r1][j] == SPACE) {
                    count++;
                } else {
                    break;
                }
            }
            
            // there are empty spaces to the right of the car
            // make all the the spaces the car originally occupied empty
            if (count > 0) {
                for (j = c0; j <= c1; j++) {
                    road[r1][j] = SPACE;
                } 
                
                // place the car count number of spaces to the right of the
                // original position
                for (j = c0 + count; j <= c1 + count; j++) {
                    road[r1][j] = car;
                }
            }
            
            // set the new values of the left most and right most positions of
            // the car
            c0 += count;
            c1 += count;
        } else {
            // there are empty spaces to the left of the car
            
            // make all the the spaces the car originally occupied empty
            for (j = c0; j <= c1; j++) {
                road[r1][j] = SPACE;
            } 
            
            // place the car count number of spaces to the right of the
            // original position
            for (j = c0 - count; j <= c1 - count; j++) {
                    road[r1][j] = car;
                }
            
            // set the new values of the left most and right most positions of
            // the car
            c0 -= count;
            c1 -= count ;
        }
        
    //car is next to exit = return 1
    // if car is not by the exit then return 0
        
    if (road[r0][c1 + 1] == EXIT || road[r0][c0 - 1] == EXIT) {
        return 1;
    } else {
        return 0;
    }
   
    }
}


/***********************************************************/
/***********************************************************/
/********* DO NOT MODIFY ANY CODE BELOW THIS POINT *********/
/***********************************************************/
/***********************************************************/

/* Function to obtain capital letter as input */
char GetMove(void)
{
	char move;
	printf("\nMove car: ");
	scanf("%c", &move);
	// Ignore non-capital letter inputs
	while ((move < 'A') || (move > 'Z')) {
		scanf("%c", &move);
	}
	return move;
}

/* The main Traffic Jam simulation */
int main(void)
{
	int gameOver = 0;
	int road[NUM_ROWS][NUM_COLS];
	int rowStart, colStart, rowEnd, colEnd;
	char input;

	/* Print banner */
	printf(" _____           __  __ _            _                                        \n");
	printf("|_   _| __ __ _ / _|/ _(_) ___      | | __ _ _ __ ___           ____          \n");
	printf("  | || '__/ _` | |_| |_| |/ __|  _  | |/ _` | '_ ` _ \\  --   __/  |_\\_      \n");
	printf("  | || | | (_| |  _|  _| | (__  | |_| | (_| | | | | | | --- |  _     _``-.    \n");
	printf("  |_||_|  \\__,_|_| |_| |_|\\___|  \\___/ \\__,_|_| |_| |_| --  '-(_)---(_)--'\n\n");

	/* Initialise the road and add cars */
	InitialiseRoad(road, 'E', 3);
	AddCar(road, 3, 3, 2);
	AddCar(road, 1, 1, 2);
	AddCar(road, 2, 1, 3);
	AddCar(road, 3, 2, -2);
	AddCar(road, 5, 2, -2);
	AddCar(road, 4, 4, -2);
	AddCar(road, 6, 3, 3);
	AddCar(road, 1, 5, -3);
	AddCar(road, 2, 6, -2);

	/* Print status */
	printf("ENGGEN131 2020 - C Project\nTraffic Jam!  There is a lot of traffic on the road!\n");
	printf("In fact, %.2f%% of the road is cars!\n\n", PercentUsed(road));

	/* Main simulation loop */
	while (!gameOver) {
		PrintRoad(road);
		input = GetMove();
		FindCar(road, input, &rowStart, &colStart, &rowEnd, &colEnd);
		gameOver = MoveCar(road, rowStart, colStart, rowEnd, colEnd);
	}

	/* A car has exited - the simulation is over */
	PrintRoad(road);
	printf("\nCongratulations, you're on your way again!");

	return 0;
}
