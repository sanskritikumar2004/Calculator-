import tkinter as tk
import math

# Function to perform calculations
def click(event):
    global expression
    text = event.widget.cget("text")
    
    if text == "=":
        try:
            result = str(eval(expression))
            screen_var.set(result)
            expression = result
        except Exception as e:
            screen_var.set("Error")
            expression = ""
    elif text == "C":
        expression = ""
        screen_var.set(expression)
    elif text == "√":
        try:
            expression = str(math.sqrt(float(expression)))
            screen_var.set(expression)
        except:
            screen_var.set("Error")
            expression = ""
    elif text == "^":
        expression += "**"
        screen_var.set(expression)
    elif text == "log":
        try:
            expression = str(math.log(float(expression)))
            screen_var.set(expression)
        except:
            screen_var.set("Error")
            expression = ""
    else:
        expression += text
        screen_var.set(expression)

# Initialize main window
root = tk.Tk()
root.title("Advanced Calculator")

# Setting the window size
root.geometry("400x500")
expression = ""

# Entry widget to display expressions and results
screen_var = tk.StringVar()
screen = tk.Entry(root, textvar=screen_var, font="lucida 20 italic", bg="#E6E6FA", fg="black", borderwidth=6)
screen.pack(fill="both", ipadx=8, pady=10)

# Button layout with additional operations like log, sqrt, and power
buttons = [
    ["7", "8", "9", "/"],
    ["4", "5", "6", "*"],
    ["1", "2", "3", "-"],
    ["C", "0", "=", "+"],
    ["log", "√", "^"]  # Added log, sqrt (√), and exponentiation (^) buttons
]

# Custom color theme (light shades and vibrant accents)
button_colors = [
    ["#FFCCCB", "#FAD02E", "#98FB98", "#87CEEB"],
    ["#FFD700", "#FFB6C1", "#FFA07A", "#FF4500"],
    ["#20B2AA", "#FF6347", "#AFEEEE", "#FF69B4"],
    ["#FFD700", "#FF69B4", "#FAD02E", "#87CEFA"],
    ["#FF6347", "#AFEEEE", "#FF69B4"]  # Colors for log, sqrt, and power buttons
]

# Create and arrange buttons
for i, row in enumerate(buttons):
    button_frame = tk.Frame(root)
    button_frame.pack(fill="both", expand=True)
    for j, btn_text in enumerate(row):
        btn = tk.Button(button_frame, text=btn_text, font="lucida 15 italic", bg=button_colors[i][j], fg="black")
        btn.pack(side="left", fill="both", expand=True, padx=5, pady=5)
        btn.bind("<Button-1>", click)

# Start the main event loop
root.mainloop()
