 Car Design and Purpose: Explanation
🚗 1. Mobility System: Wheels, Chassis Design, Motor Types
Our autonomous car uses a differential drive system with two DC geared motors connected via an L298N motor driver, enabling it to move forward, backward, and turn smoothly. This type of mobility system was chosen for its simplicity, efficiency, and ease of control via GPIO.

The chassis is a lightweight, low-profile acrylic frame that provides:

Good balance between durability and speed

Enough space to mount all components (Raspberry Pi, camera, sensors, motor driver, etc.)

Proper center of gravity to maintain stability during curves and obstacle avoidance

We use a servo motor for steering adjustments during turns or obstacle bypassing, giving us finer control compared to fixed-angle turns.

💻 2. Why Raspberry Pi? Sensor and Camera Integration
We chose the Raspberry Pi 3 as our main controller because:

It offers a powerful CPU capable of handling real-time image processing using OpenCV

Has built-in GPIO pins for sensor and motor control

Supports USB and CSI camera modules for high-quality video input

Easily programmable using Python, which integrates well with GPIO and OpenCV libraries

Sensor Integration:

4× HC-SR04 ultrasonic sensors are placed on the front, left, right, and slightly tilted angles to detect nearby obstacles and assist in precise navigation.

Camera Integration:

A Raspberry Pi Camera is mounted facing forward to continuously analyze the track and detect:

The black track line for path following

Red and green obstacles for side-based avoidance

The camera captures video frames processed using OpenCV, and the ultrasonic sensors confirm proximity to ensure smooth and safe movement.

🎯 3. Color-Based Obstacle Handling Logic
The vehicle must handle obstacles according to their color:

🔴 Red Obstacle → Always bypass from the right side

🟢 Green Obstacle → Always bypass from the left side

Using OpenCV, we convert camera input to the HSV color space to make color detection more robust against lighting changes. The obstacle detection pipeline is:

Frame captured from the camera

Apply Gaussian blur and convert to HSV

Mask the image using defined HSV ranges for red and green

If an obstacle is detected:

Use ultrasonic sensors to measure the distance

Initiate obstacle avoidance routine by steering and moving in the correct direction (left or right)

After bypassing, the vehicle re-centers itself on the black track using line-following logic.

🔁 4. Lap Tracking Logic and Stop Mechanism
To track laps and stop the vehicle after 3 full laps, we implemented a lap-counting system:

A distinct marker (e.g., a specific color patch or visual cue near the starting point) is placed on the track

The camera checks for this marker every time the car passes that section

A lap counter variable is incremented each time the marker is detected after a full loop

Once the counter reaches 3, the car:

Slows down

Moves to the start position

Stops all motors

We ensure the detection is only valid once per lap using time or position thresholding to avoid false positives.

✅ Summary
This autonomous car is designed for:

Efficient navigation using a simple but effective wheel and motor layout

Smart decision-making through camera and ultrasonic sensor fusion

Rule-based obstacle handling (color + direction logic)

Accurate lap tracking and self-stop after completing the task

Our solution is modular, scalable, and designed with real-world robotic challenges in mind, aligning perfectly with the spirit of WRO Future Engineers.
