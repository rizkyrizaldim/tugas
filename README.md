# Rizky Rizaldi Mastiyanto (5311421085)
# Praktek Best First Search
# Permainan Tic-Tac-Toe 3x3
Tujuan Praktikum untuk meningkatkan pemahaman mahasiswa terhadap code permainan tic tac toe. Selain itu, modul 6
memberikan pengetahuan tentang Object Oriented Programming menggunakan bahasa pemrograman Python di Visual Studio Code.

Berikut adalah langkah-langkahnya:
1. Buka Visual Studio Code, lalu buat file baru dengan format .py.
2. Masukkan coding berikut.

       import tkinter as tk
       from tkinter import messagebox

       class TicTacToeGUI:
       def __init__(self):
            self.frame = tk.Tk()
            self.frame.title("Tic Tac Toe")
            self.frame.geometry("300x380")

            self.buttons = [[None for _ in range(3)] for _ in range(3)]
            self.current_player = "X"

            self.turn_label = tk.Label(self.frame, text=f"Player {self.current_player}'s turn", font=("Arial", 12))
            self.turn_label.grid(row=0, columnspan=3)

            self.create_board()
            self.create_reset_button()

       def create_board(self):
           for i in range(3):
               for j in range(3):
                   self.buttons[i][j] = tk.Button(self.frame, text="", font=("Arial", 20), width=5, height=2, command=lambda i=i, j=j: self.on_click(i, j))
                   self.buttons[i][j].grid(row=i + 1, column=j)

       def create_reset_button(self):
           reset_button = tk.Button(self.frame, text="Reset", font=("Arial", 16), command=self.reset_board)
           reset_button.grid(row=4, columnspan=3)

       def reset_board(self):
           for i in range(3):
               for j in range(3):
                   self.buttons[i][j]["text"] = ""
                   self.buttons[i][j]["state"] = "normal"
        self.current_player = "X"
        self.update_turn_label()

       def on_click(self, row, col):
           if self.buttons[row][col]["text"] == "":
               self.buttons[row][col]["text"] = self.current_player
               self.buttons[row][col]["state"] = "disabled"
               if self.check_winner():
                  messagebox.showinfo("Game Over", f"Player {self.current_player} Wins!")
                  self.reset_board()
           elif self.is_board_full():
                messagebox.showinfo("Game Over", "It's a Tie!")
                self.reset_board()
           else:
                self.switch_player()

       def switch_player(self):
           self.current_player = "O" if self.current_player == "X" else "X"
           self.update_turn_label()

       def update_turn_label(self):
           self.turn_label["text"] = f"Player {self.current_player}'s turn"

       def check_winner(self):
           for i in range(3):
               if all(self.buttons[i][j]["text"] == self.current_player for j in range(3)) or all(self.buttons[j][i]["text"] == self.current_player for j in range(3)):
                return True

               if all(self.buttons[i][i]["text"] == self.current_player for i in range(3)) or all(self.buttons[i][2 - i]["text"] == self.current_player for i in range(3)):
            return True

               return False

       def is_board_full(self):
           return all(self.buttons[i][j]["text"] != "" for i in range(3) for j in range(3))

       def start_game(self):
           self.frame.mainloop()

       if __name__ == "__main__":
           game_gui = TicTacToeGUI()
           game_gui.start_game()

