# passwordgenerator
python
import string
import tkinter as tk
from tkinter import messagebox
def generate_password():
    try:
        length = int(length_entry.get())
        use_letters = letters_var.get()
        use_numbers = numbers_var.get()
        use_symbols = symbols_var.get()

        character_pool = ""
        if use_letters:
            character_pool += string.ascii_letters
        if use_numbers:
            character_pool += string.digits
        if use_symbols:
            character_pool += string.punctuation

        if not character_pool:
            raise ValueError("No character types selected!")

        password = ''.join(random.choice(character_pool) for _ in range(length))
        password_output.config(text=password)
        root.clipboard_clear()
        root.clipboard_append(password)
        root.update()  # Copy to clipboard
        messagebox.showinfo("Success", "Password copied to clipboard!")
    except ValueError as e:
        messagebox.showerror("Input Error", str(e))

# GUI setup
root = tk.Tk()
root.title("Password Generator")

tk.Label(root, text="Password Length:").grid(row=0, column=0, padx=10, pady=10)
length_entry = tk.Entry(root)
length_entry.grid(row=0, column=1, padx=10, pady=10)

letters_var = tk.BooleanVar(value=True)
numbers_var = tk.BooleanVar(value=True)
symbols_var = tk.BooleanVar(value=True)

tk.Checkbutton(root, text="Include Letters", variable=letters_var).grid(row=1, column=0, columnspan=2)
tk.Checkbutton(root, text="Include Numbers", variable=numbers_var).grid(row=2, column=0, columnspan=2)
tk.Checkbutton(root, text="Include Symbols", variable=symbols_var).grid(row=3, column=0, columnspan=2)

tk.Button(root, text="Generate Password", command=generate_password).grid(row=4, column=0, columnspan=2, pady=10)

password_output = tk.Label(root, text="", font=("Bold", 12))
password_output.grid(row=5, column=0, columnspan=2, pady=10)
root.mainloop()
