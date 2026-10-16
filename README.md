
import random

def print_board(board):
    print()
    for i in range(0, 9, 3):
        print(" " + " | ".join(board[i:i+3]))
        if i < 6:
            print("---+---+---")
    print()

def check_winner(board, player):
    winning_lines = [
        (0, 1, 2), (3, 4, 5), (6, 7, 8),
        (0, 3, 6), (1, 4, 7), (2, 5, 8),
        (0, 4, 8), (2, 4, 6)
    ]
    return any(
        board[a] == board[b] == board[c] == player
        for a, b, c in winning_lines
    )

def play_game():
    board = [str(i) for i in range(1, 10)]
    print("TIC-TAC-TOE: YOU (X) vs COMPUTER (O)")
    print("Choose a position from 1 to 9.")
    print_board(board)

    while True:
        move = input("Choose your position (1-9): ").strip()

        if move not in [str(i) for i in range(1, 10)]:
            print("Please enter a number from 1 to 9.")
            continue

        position = int(move) - 1

        if board[position] in ["X", "O"]:
            print("That position is occupied. Try another.")
            continue

        board[position] = "X"

        if check_winner(board, "X"):
            print_board(board)
            print("Congratulations! You win!")
            break

        if all(cell in ["X", "O"] for cell in board):
            print_board(board)
            print("It's a draw!")
            break

        available = [
            i for i, cell in enumerate(board)
            if cell not in ["X", "O"]
        ]
        computer_move = random.choice(available)
        board[computer_move] = "O"

        print("Computer chose position", computer_move + 1)
        print_board(board)

        if check_winner(board, "O"):
            print("Computer wins! Try again.")
            break

        if all(cell in ["X", "O"] for cell in board):
            print("It's a draw!")
            break

play_game()
