#include <stdio.h>
#include <stdlib.h>
#include <time.h>

#define BOARD_SIZE 100

int rollDice() {
    return (rand() % 6) + 1;
}

int checkSnakeOrLadder(int position) {
    // Define snakes and ladders
    int snakes[10][2] = {{99, 54}, {70, 55}, {52, 42}, {25, 2}, {95, 72}};
    int ladders[10][2] = {{6, 25}, {11, 40}, {60, 85}, {46, 90}, {17, 69}};

    for (int i = 0; i < 5; i++) {
        if (position == snakes[i][0]) {
            printf("Oh no! You landed on a snake at %d. Go down to %d.\n", snakes[i][0], snakes[i][1]);
            return snakes[i][1];
        }
        if (position == ladders[i][0]) {
            printf("Great! You landed on a ladder at %d. Climb up to %d.\n", ladders[i][0], ladders[i][1]);
            return ladders[i][1];
        }
    }
    return position;
}

void playGame() {
    int player1Pos = 0, player2Pos = 0;
    int currentPlayer = 1;
    srand(time(0));

    while (player1Pos < BOARD_SIZE && player2Pos < BOARD_SIZE) {
        int diceRoll = rollDice();
        printf("Player %d rolled a %d.\n", currentPlayer, diceRoll);

        if (currentPlayer == 1) {
            player1Pos += diceRoll;
            if (player1Pos > BOARD_SIZE) player1Pos = BOARD_SIZE;
            player1Pos = checkSnakeOrLadder(player1Pos);
            printf("Player 1 is now at position %d.\n", player1Pos);
            if (player1Pos == BOARD_SIZE) {
                printf("Player 1 wins!\n");
                break;
            }
            currentPlayer = 2;
        } else {
            player2Pos += diceRoll;
            if (player2Pos > BOARD_SIZE) player2Pos = BOARD_SIZE;
            player2Pos = checkSnakeOrLadder(player2Pos);
            printf("Player 2 is now at position %d.\n", player2Pos);
            if (player2Pos == BOARD_SIZE) {
                printf("Player
