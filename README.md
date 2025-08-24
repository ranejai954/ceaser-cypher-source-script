# ceaser-cypher-source-script
import tkinter as tk
from tkinter import messagebox

def caesar_cipher(text, shift, mode):
    result = ""
    for char in text:
        if char.isalpha():
            base = ord('A') if char.isupper() else ord('a')
            shift_val = shift if mode == "encrypt" else -shift
            result += chr((ord(char) - base + shift_val) % 26 + base)
        else:
            result += char
    return result

def process_text():
    text = entry_text.get()
    shift = entry_shift.get()
    if not shift.isdigit():
        messagebox.showerror("Error", "Shift must be a number")
        return
    shift = int(shift)
    mode = var.get()
    result = caesar_cipher(text, shift, mode)
    output_label.config(text="Result: " + result)

# GUI setup
root = tk.Tk()
root.title("Caesar Cipher App")

tk.Label(root, text="Enter Text:").pack()
entry_text = tk.Entry(root, width=40)
entry_text.pack()

tk.Label(root, text="Enter Shift (1-25):").pack()
entry_shift = tk.Entry(root, width=10)
entry_shift.pack()

var = tk.StringVar(value="encrypt")
tk.Radiobutton(root, text="Encrypt", variable=var, value="encrypt").pack()
tk.Radiobutton(root, text="Decrypt", variable=var, value="decrypt").pack()

tk.Button(root, text="Process", command=process_text).pack(pady=5)

output_label = tk.Label(root, text="Result: ", fg="blue")
output_label.pack()

root.mainloop()
