import random
import tkinter as tk
from tkinter import messagebox

# Create the main window
root = tk.Tk()
root.title("Number Guessing Game")
root.geometry("400x500")

# Select a random number
secret_number = random.randint(1, 100)
attempts = 0

# Function to check the guess
def check_guess():
    global attempts
    try:
        guess = int(entry.get())
        if guess < 1 or guess > 100:
            messagebox.showerror("Invalid Input", "Please enter a number between 1 and 100.")
            return
        attempts += 1
        if guess < secret_number:
            result_label.config(text="Too low! Try again.", fg="red")
        elif guess > secret_number:
            result_label.config(text="Too high! Try again.", fg="red")
        else:
            result_label.config(text=f"Congratulations! You guessed it in {attempts} attempts.", fg="green")
            entry.config(state="disabled")  # Disable the input field after winning
            check_button.config(state="disabled")  # Disable the button after winning
    except ValueError:
        messagebox.showerror("Invalid Input", "Please enter a valid number.")

# Function to restart the game
def restart_game():
    global secret_number, attempts
    secret_number = random.randint(1, 100)
    attempts = 0
    result_label.config(text="Guess a number between 1 and 100.", fg="black")
    entry.config(state="normal")
    check_button.config(state="normal")
    entry.delete(0, tk.END)

# Set up the GUI
title_label = tk.Label(root, text="Number Guessing Game", font=("Helvetica", 18, "bold"))
title_label.pack(pady=10)

image_label = tk.Label(root)
image_label.pack(pady=10)

instruction_label = tk.Label(root, text="Enter a number (1-100):", font=("Helvetica", 12))
instruction_label.pack(pady=5)

entry = tk.Entry(root, font=("Helvetica", 12), width=10)
entry.pack(pady=5)

check_button = tk.Button(root, text="Check Guess", font=("Helvetica", 12), command=check_guess)
check_button.pack(pady=10)

result_label = tk.Label(root, text="Guess a number between 1 and 100.", font=("Helvetica", 12), wraplength=350)
result_label.pack(pady=10)

restart_button = tk.Button(root, text="Restart Game", font=("Helvetica", 12), command=restart_game)
restart_button.pack(pady=10)

# Run the GUI
root.mainloop()
