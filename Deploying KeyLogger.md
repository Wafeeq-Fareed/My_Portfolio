# Creating and Deploying a Keylogger using Python

## Project Overview

The goal of this project is to develop a simple keylogging application that records keystrokes made on a keyboard and logs them into a text file. This can be useful for various purposes, such as monitoring input for usability studies or debugging.

### Functionality:
- Captures keystrokes made by the user.
- Logs the pressed keys into a file named log.txt.
- Handles special keys like space, Enter, Alt, Tab, and Backspace with specific representations.

### Key Features:
- Logs each keypress event.
- Differentiates between regular and special keys.
- Provides a clean and readable format for special key events.
- Continuously runs in the background to capture keystrokes.

## OBJECTIVES
- Importing Required Module
- Defining 'log-keystroke' Function
- Handling Special Keys
- Logging The Key Strokes
- Starting Key Listener

## Technologies Used

#### Python:
Role: The programming language used to write the keylogging application.
Features:
High-level and easy to read.
Extensive libraries and modules for various tasks.

##### pynput Library:
Role: Provides functionality to monitor and control input devices like keyboards.
Features:
Listener class to detect and respond to keyboard events.
Handles special keys and their events.

#### File I/O Operations:
Role: Used to write the captured keystrokes to a text file.
Features:
open function to create or append to log.txt.
write method to log keystrokes into the file.

### 1. Importing Required Modules
    
    from pynput.keyboard import Listener

This line imports the Listener class from the pynput.keyboard module. pynput is a library used to control and monitor input devices like the keyboard and mouse in Python. The Listener class allows us to monitor keyboard events such as key presses.

### 2. Defining 'log-keystroke' Function

    def log_keystroke(key):
        key = str(key).replace("'", "")

This is the beginning of a function called log_keystroke, which will handle each key press event.

<b>key = str(key).replace("'", ""):</b>

The key parameter represents the key that was pressed. It's converted to a string, and any single quotes (') are removed. This is done because keys are often represented as strings in the form "'a'", and we want to clean this up for easier reading and logging.

### 3. Handling Special Keys

    if key == 'Key.space':
        key = ' '
    if key == 'Key.shift_r':
        key = ''
    if key == "Key.enter":
        key = '\n'
    if key == 'Key.alt_l' or key == 'Key.alt_r':
        key = ''
    if key == 'Key.tab':
        key = ''
    if key == 'Key.backspace':
        key = ''

This part of the code checks if the pressed key is a special key and replaces it with a corresponding character:

<b>if key == 'Key.space': key = ' '</b>

If the pressed key is the space bar (Key.space), it replaces it with an actual space character (' ').

<b>if key == 'Key.shift_r': key = ''</b>

If the pressed key is the right Shift key (Key.shift_r), it replaces it with an empty string. The Shift key by itself does not produce any character, so it's effectively ignored.

<b>if key == "Key.enter": key = '\n'</b>

If the pressed key is the Enter key (Key.enter), it replaces it with a newline character ('\n').

<b>if key == 'Key.alt_l' or key == 'Key.alt_r': key = ''</b>

If the pressed key is the left or righ Alt key (Key.alt_r) or (Key.alt_l), it replaces it with an empty string.

<b>if key == 'Key.tab': key = ''</b>

If the pressed key is the tab key (Key.tab), it replaces it with an empty string.

<b>if key == 'Key.backspace': key = ''</b>

If the pressed key is the backspace key (Key.backspace), it replaces it with an empty string.

### 4. Logging The Keystrokes
      
      with open("log.txt", 'a') as f:
        f.write(key)
This part of the function opens a file named log.txt in append mode ('a').
<b>with open("log.txt", 'a') as f:</b>
This line writes the processed key (after any necessary replacements) to the file. Each key press is logged sequentially.

### 5. Starting the Key Listner
    with Listener(on_press=log_keystroke) as l:
    l.join()
This part of the code sets up the keyboard listener:
<b>with Listener(on_press=log_keystroke) as l:</b>
A Listener object is created, and the on_press event is tied to the log_keystroke function. This means that every time a key is pressed, the log_keystroke function will be called.
<b>l.join()</b>
The join() method is called on the listener, which makes the program wait for keyboard events indefinitely. The program will continue to run, logging all keystrokes until it is manually stopped.

## Summary

This script sets up a basic keylogger that captures every key pressed and writes it to a file named log.txt. It handles regular characters, as well as some special keys like space, shift, and enter, tab and alt. The pynput library is used to monitor the keyboard, and the listener runs indefinitely, capturing and logging each key press.


        
