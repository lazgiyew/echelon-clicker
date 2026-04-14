import tkinter as tk
from tkinter import messagebox
import threading
import pyautogui
import keyboard
import time


RUNNING = False
HOLD_TIME = 2
TOGGLE_KEY = "F6"


def click_loop():
    global RUNNING
    while True:
        if RUNNING:
            pyautogui.mouseDown()
            status_label.config(text="Status: HOLDING", fg="#00ff00")
            time.sleep(HOLD_TIME)
            pyautogui.mouseUp()
            status_label.config(text="Status: RELEASED", fg="#ff0000")
            time.sleep(0.05)
        else:
            time.sleep(0.05)


def start_stop():
    global RUNNING
    RUNNING = not RUNNING
    if RUNNING:
        status_label.config(text=f"Status: RUNNING ({TOGGLE_KEY})", fg="#00ff00")
    else:
        status_label.config(text="Status: STOPPED", fg="#ffffff")


def update_hotkey():
    global TOGGLE_KEY
    key = hotkey_entry.get()
    if key.strip() == "":
        messagebox.showwarning("Warning", "Hotkey cannot be empty!")
        return
    try:
        keyboard.remove_hotkey(TOGGLE_KEY)
    except:
        pass
    TOGGLE_KEY = key
    keyboard.add_hotkey(TOGGLE_KEY, start_stop)
    hotkey_label.config(text=f"Current Hotkey: {TOGGLE_KEY}")
    messagebox.showinfo("Info", f"Hotkey updated to {TOGGLE_KEY}")


root = tk.Tk()
root.title("🖱️ Echelon Clicker")
root.geometry("400x450")
root.configure(bg="#1a1a1a")
root.resizable(False, False)

title_label = tk.Label(root, text="Echelon Clicker", font=("Segoe UI", 22, "bold"),
                       bg="#1a1a1a", fg="#8000ff")
title_label.pack(pady=20)

status_label = tk.Label(root, text="Status: STOPPED", font=("Segoe UI", 14),
                        bg="#1a1a1a", fg="#ffffff")
status_label.pack(pady=10)


button_frame = tk.Frame(root, bg="#1a1a1a")
button_frame.pack(pady=20)


def on_enter_start(e):
    start_button['bg'] = "#6600cc"
def on_leave_start(e):
    start_button['bg'] = "#8000ff"

start_button = tk.Button(button_frame, text="Start / Stop", font=("Segoe UI", 14, "bold"),
                         bg="#8000ff", fg="#ffffff", width=20, height=2,
                         bd=0, relief="flat", command=start_stop, activebackground="#6600cc", activeforeground="#ffffff")
start_button.pack(pady=10)
start_button.bind("<Enter>", on_enter_start)
start_button.bind("<Leave>", on_leave_start)


hotkey_label = tk.Label(button_frame, text=f"Current Hotkey: {TOGGLE_KEY}", font=("Segoe UI", 12),
                        bg="#1a1a1a", fg="#ffffff")
hotkey_label.pack(pady=5)

hotkey_entry = tk.Entry(button_frame, font=("Segoe UI", 12), width=10, bg="#2b2b2b", fg="#ffffff",
                        insertbackground="#ffffff", justify="center")
hotkey_entry.pack(pady=5)
hotkey_entry.insert(0, TOGGLE_KEY)

def on_enter_hotkey(e):
    hotkey_button['bg'] = "#6600cc"
def on_leave_hotkey(e):
    hotkey_button['bg'] = "#8000ff"

hotkey_button = tk.Button(button_frame, text="Update Hotkey", font=("Segoe UI", 12, "bold"),
                          bg="#8000ff", fg="#ffffff", width=20, height=2, bd=0, relief="flat",
                          command=update_hotkey, activebackground="#6600cc", activeforeground="#ffffff")
hotkey_button.pack(pady=10)
hotkey_button.bind("<Enter>", on_enter_hotkey)
hotkey_button.bind("<Leave>", on_leave_hotkey)


t = threading.Thread(target=click_loop)
t.daemon = True
t.start()

# Add initial hotkey
keyboard.add_hotkey(TOGGLE_KEY, start_stop)

root.mainloop()
