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
   
4. Run Coding tersebut dan lihat outputnya.
   ![image](https://github.com/rizkyrizaldim/tugas/assets/148876602/1c0b6a4b-d44a-46a7-89cb-90a290316f8d)
   ![image](https://github.com/rizkyrizaldim/tugas/assets/148876602/6f38d9fc-3586-4cc4-98ef-740de33938e0)
   ![image](https://github.com/rizkyrizaldim/tugas/assets/148876602/2de76eac-a2a8-4356-8de0-f0ad930f29a9)


# Penjelasan Coding
Kode tersebut adalah implementasi dari permainan Tic Tac Toe menggunakan antarmuka grafis (GUI) dengan modul `tkinter` di Python. Saya akan memberikan penjelasan untuk setiap bagian dari kode tersebut:

1. Import Modul Tkinter:
   ```python
   import tkinter as tk
   from tkinter import messagebox
   ```
   - Baris pertama mengimpor modul `tkinter` dan menamainya sebagai `tk`.
   - Baris kedua mengimpor fungsi `messagebox` dari modul `tkinter`.

2. Definisi Kelas `TicTacToeGUI`:
   ```python
   class TicTacToeGUI:
   ```
   - Membuat kelas `TicTacToeGUI`.

3. Metode `__init__`:
   ```python
   def __init__(self):
   ```
   - Metode khusus yang dipanggil saat objek kelas dibuat.
   - Inisialisasi antarmuka pengguna.

4. Inisialisasi Frame Tkinter:
   ```python
   self.frame = tk.Tk()
   self.frame.title("Tic Tac Toe")
   self.frame.geometry("300x380")
   ```
   - Membuat frame utama menggunakan `tk.Tk()`.
   - Mengatur judul jendela menjadi "Tic Tac Toe".
   - Menetapkan ukuran jendela menjadi 300x380 piksel.

5. Matriks Tombol (`self.buttons`):
   ```python
   self.buttons = [[None for _ in range(3)] for _ in range(3)]
   ```
   - Membuat matriks 3x3 untuk menyimpan tombol permainan.

6. Menyimpan Pemain Aktif:
   ```python
   self.current_player = "X"
   ```
   - Menyimpan pemain saat ini (awalnya "X").

7. Label untuk Gantian Pemain:
   ```python
   self.turn_label = tk.Label(self.frame, text=f"Player {self.current_player}'s turn", font=("Arial", 12))
   self.turn_label.grid(row=0, columnspan=3)
   ```
   - Membuat label yang menunjukkan giliran pemain saat ini.
   - Menyimpannya dalam `self.turn_label`.
   - Menempatkannya di baris 0 dan menempati tiga kolom.

8. Metode `create_board`:
   ```python
   def create_board(self):
   ```
   - Membuat tombol-tombol pada papan permainan.

9. Metode `create_reset_button`:
   ```python
   def create_reset_button(self):
   ```
   - Membuat tombol untuk mereset papan permainan.

10. Metode `reset_board`:
   ```python
   def reset_board(self):
   ```
   - Mengatur ulang papan permainan.

11. Metode `on_click`:
   ```python
   def on_click(self, row, col):
   ```
   - Dipanggil saat tombol pada papan permainan ditekan.

12. Metode `switch_player`:
   ```python
   def switch_player(self):
   ```
   - Mengganti pemain aktif.

13. Metode `update_turn_label`:
   ```python
   def update_turn_label(self):
   ```
   - Memperbarui label yang menunjukkan giliran pemain.

14. Metode `check_winner`:
   ```python
   def check_winner(self):
   ```
   - Memeriksa apakah ada pemenang.

15. Metode `is_board_full`:
   ```python
   def is_board_full(self):
   ```
   - Memeriksa apakah papan permainan sudah penuh.

16. Metode `start_game`:
   ```python
   def start_game(self):
   ```
   - Memulai permainan dan menampilkan jendela Tkinter.

17. Memeriksa Apakah Ini Pemanggilan Utama:
   ```python
   if __name__ == "__main__":
       game_gui = TicTacToeGUI()
       game_gui.start_game()
   ```
   - Memastikan bahwa permainan dimulai hanya jika skrip ini dijalankan sebagai skrip utama (bukan sebagai modul). Membuat objek `TicTacToeGUI` dan memulai permainan.

Dengan kode ini, Anda dapat menjalankan permainan Tic Tac Toe dengan GUI Tkinter. Pemain dapat mengklik tombol pada papan permainan untuk menempatkan tanda mereka, dan permainan akan berlanjut hingga ada pemenang atau papan permainan penuh (seri).
