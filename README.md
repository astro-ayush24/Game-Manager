# Game-Manager
//Game Manager System is a console-based C application offering Rock Paper Scissors gameplay with AI, score tracking, and game history. It features modular design, input validation, and random number generation, serving as both an entertainment tool and a learning aid for C programming.
//CODE 
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include <string.h>

// Global history array and counter
char history[100][100];
int historyCount = 0;

// ---------- Rock Paper Scissors ----------
void playRPS() {
    int user, cpu;
    const char *opt[] = {"Rock", "Paper", "Scissors"};

    printf("1. Rock\n2. Paper\n3. Scissors\nChoose: ");
    if (scanf("%d", &user) != 1 || user < 1 || user > 3) {
        printf("Invalid choice.\n");
        while (getchar() != '\n'); // Clear input buffer
        return;
    }

    srand((unsigned int)time(NULL));
    cpu = rand() % 3 + 1;

    printf("You: %s | CPU: %s\n", opt[user - 1], opt[cpu - 1]);

    if (user == cpu) {
        printf("It's a draw!\n");
        strcpy(history[historyCount++], "RPS - Draw (Score: You 0, CPU 0)");
    } else if ((user == 1 && cpu == 3) || (user == 2 && cpu == 1) || (user == 3 && cpu == 2)) {
        printf("You win!\n");
        strcpy(history[historyCount++], "RPS - You Win (Score: You 1, CPU 0)");
    } else {
        printf("CPU wins!\n");
        strcpy(history[historyCount++], "RPS - CPU Wins (Score: You 0, CPU 1)");
    }
}

// ---------- View Game History ----------
void viewHistory() {
    printf("\n--- Game History ---\n");
    if (historyCount == 0) {
        printf("No games played yet.\n");
        return;
    }
    for (int i = 0; i < historyCount; i++) {
        printf("%d. %s\n", i + 1, history[i]);
    }
}

// ---------- Game Selection ----------
void playGame() {
    int c;
    printf("\n1. Rock Paper Scissors\nChoose: ");
    if (scanf("%d", &c) != 1) {
        printf("Invalid input.\n");
        while (getchar() != '\n');
        return;
    }

    if (c == 1) {
        playRPS();
    } else {
        printf("Invalid choice.\n");
    }
}

// ---------- Main Menu ----------
int main() {
    int ch;

    while (1) {
        printf("\n=== Game Manager ===\n");
        printf("1. Play Game\n2. View History\n3. Exit\nChoice: ");
        
        if (scanf("%d", &ch) != 1) {
            printf("Invalid input.\n");
            while (getchar() != '\n'); // flush stdin
            continue;
        }

        if (ch == 1) {
            playGame();
        } else if (ch == 2) {
            viewHistory();
        } else if (ch == 3) {
            printf("Exiting Game Manager. Goodbye!\n");
            break;
        } else {
            printf("Invalid choice.\n");
        }
    }

    return 0;
}
