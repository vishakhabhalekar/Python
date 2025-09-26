# Python
AI Virtual Mouse Control
Virtual Mouse and Gesture Controller
This is a Virtual Mouse and Gesture Controller project that allows users to interact with their computer using hand gestures captured by a webcam. It uses the MediaPipe Hands solution for hand tracking and OpenCV for video processing, translating specific hand poses into mouse actions like movement, clicking, and taking screenshots.

🌟 Features
Mouse Movement Control: Control the mouse cursor position by moving the index finger (with the thumb extended).

Left Click: Performs a left-click action.

Right Click: Performs a right-click action.

Double Click: Performs a double-click action.

Screenshot: Captures the screen and saves the image to the project directory.

Real-time Feedback: Displays the detected gesture on the video feed.

🛠️ Technologies Used
Python: The core programming language.

OpenCV (cv2): Used for capturing video from the webcam and displaying the feed.

MediaPipe (mediapipe): Utilized for robust and real-time hand detection and landmark tracking.

pyautogui: Used to control mouse movement, perform double-clicks, and take screenshots.

pynput: Used for finer control over mouse clicks (left and right press/release).

🚀 Installation and Setup
Clone the repository:

Bash

git clone https://github.com/your-username/your-repo-name.git
cd your-repo-name
Install the required libraries:

Bash

pip install opencv-python mediapipe pyautogui pynput
# You will also need a separate 'util.py' file for helper functions like 
# get_angle, get_distance, etc., which is referenced in main.py.
(Note: This project requires a helper file named util.py containing get_angle and get_distance functions, which are essential for gesture detection logic.)

Run the script:

Bash

python main.py
The webcam feed will open, and you can start controlling your mouse with hand gestures!

✋ Gesture Guide
The core gesture detection relies on the angles of the fingers and the distance between the thumb and the index finger.

Action	Description	Gesture Logic (Inferred)
Move Mouse	Cursor follows the index finger tip.	Index finger extended, thumb extended (distance > 50), and angle at index-mcp (5) to index-pip (6) to index-tip (8) is flexed (angle>90).
Left Click	Single left mouse click.	Index finger flexed (angle<50), Middle finger extended (angle>90), Thumb extended (dist>50).
Right Click	Single right mouse click.	Index finger extended (angle>90), Middle finger flexed (angle<50), Thumb extended (dist>50).
Double Click	Double left mouse click.	Index and Middle fingers flexed (angle<50), Thumb extended (dist>50).
Screenshot	Takes a screenshot.	Index and Middle fingers flexed (angle<50), Thumb close to index finger (dist<50).

Export to Sheets
👨‍💻 Logic Highlights
The gesture detection functions (e.g., is_left_click, is_double_click) use the following logic, which assumes the util.py functions calculate the angle at the PIP joint and the distance between the thumb's base and the index finger's base:

Finger State: A small angle (angle<50) typically means the finger is flexed (bent), while a large angle (angle>90) means it's extended (straight).

Thumb Distance (thumb_index_dist): This is used to differentiate between click/double-click gestures (thumb extended, dist>50) and the screenshot gesture (thumb tucked in, dist<50).

Mouse Movement: The move_mouse function maps the hand's coordinates (from 0 to 1) to the screen's resolution. Note the y-coordinate is scaled by a factor of 1/2 (index_finger_tip.y / 2), which might be an intentional way to limit vertical movement range or compensate for camera perspective.
