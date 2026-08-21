# Tictactoe
from tkinter import *
import random

root = Tk()
root.title("Tic Tac Toe")

board = [""] * 9
currentPlayer = "X"

buttons = []


def checkWinner():
    wins = [
        [0,1,2], [3,4,5], [6,7,8],
        [0,3,6], [1,4,7], [2,5,8],
        [0,4,8], [2,4,6]
    ]

    for a, b, c in wins:
        if board[a] == board[b] == board[c] and board[a] != "":
            status.config(text=f"{board[a]} wins!")
            disableButtons()
            return True

    if "" not in board:
        status.config(text="It's a tie!")
        return True

    return False


def disableButtons():
    for button in buttons:
        button.config(state=DISABLED)


def computerMove():
    empty = [i for i in range(9) if board[i] == ""]

    if empty:
        move = random.choice(empty)
        board[move] = "O"
        buttons[move].config(text="O")

        checkWinner()


def buttonClick(index):
    global currentPlayer

    if board[index] == "":
        board[index] = "X"
        buttons[index].config(text="X")

        if not checkWinner():
            computerMove()


for i in range(9):
    button = Button(root,
                    text="",
                    font=("Arial", 25),
                    width=5,
                    height=2,
                    command=lambda i=i: buttonClick(i))

    button.grid(row=i//3, column=i%3)
    buttons.append(button)

status = Label(root, text="Player X", font=("Arial", 15))
status.grid(row=3, column=0, columnspan=3)

root.mainloop()
