Car Design & Purpose (Short Version)
🚗 Mobility System
We used a differential drive with two DC motors controlled by an L298N motor driver. The chassis is lightweight and compact for stability and easy mounting of components. A servo motor is used for smooth steering control.

💻 Why Raspberry Pi
Raspberry Pi 3 was chosen for its powerful processing and easy integration with OpenCV and GPIO. It controls the motors, reads ultrasonic sensors, and processes camera input for color and track detection.

🎯 Obstacle Handling Logic
The camera detects obstacle color using HSV filters:

🔴 Red → bypass from the right

🟢 Green → bypass from the left
Ultrasonic sensors help confirm obstacle distance before turning.

🔁 Lap Tracking & Stop
The car detects a visual marker near the start point. After passing it 3 times, it stops at the starting position, completing the task.
