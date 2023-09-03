import tkinter as tk
import subprocess  # For opening applications

def update_shortcut():
    shortcut_text.set(shortcut_entry.get())

# Create a main application window
root = tk.Tk()
root.title("Shortcut Key App")

# Create a Canvas widget for the gradient background
canvas = tk.Canvas(root, width=400, height=300)
canvas.pack()

# Define the gradient colors (dark blue to light blue)
gradient_colors = ["#00008B", "#1E90FF", "#87CEEB", "#E0FFFF"]

# Create the gradient background by drawing rectangles
for i in range(len(gradient_colors)):
    color = gradient_colors[i]
    y0 = (i * 300) // len(gradient_colors)
    y1 = ((i + 1) * 300) // len(gradient_colors)
    canvas.create_rectangle(0, y0, 400, y1, fill=color, outline="")

# Create and place a label widget for Shortcut Key
label = tk.Label(root, text="Shortcut Key:", fg="blue", bg=gradient_colors[-1], font=("Arial", 12, "bold"))
label.pack()

# Create an entry widget for shortcut input
shortcut_text = tk.StringVar()
shortcut_entry = tk.Entry(root, textvariable=shortcut_text, fg="black", bg="white", font=("Arial", 10))
shortcut_entry.pack()

# Create and place a button to update the shortcut
update_button = tk.Button(root, text="Update Shortcut", command=update_shortcut, fg="white", bg="green", font=("Arial", 12, "bold"))
update_button.pack()

# Create and place a label to display the current shortcut
display_label = tk.Label(root, text="Current Shortcut: None", fg="red", bg=gradient_colors[-1], font=("Arial", 12))
display_label.pack()

# Function to open an application when the shortcut is pressed
def open_application():
    # Replace 'your_application_path' with the path to the application you want to open
    application_path = 'your_application_path'
    try:
        subprocess.Popen(application_path, shell=True)
    except Exception as e:
        print(f"Error opening application: {e}")

# Bind the open_application function to the shortcut key
root.bind('<Control-Alt-a>', lambda e: open_application())  # Change 'a' to your desired key

# Start the main event loop
root.mainloop()
