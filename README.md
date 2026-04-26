# Arduino-Bluetooth-Control-Car
An Arduino Bluetooth Control Car represents a shift from the systems we just discussed. The humidity, light, and temperature projects were closed-loop feedback systems—they ran automatically based on sensor data. A Bluetooth car is typically an open-loop system (also called direct teleoperation). It doesn't think for itself; it just listens for your commands and executes them directly.

Here is how the hardware and logic map out for a classic remote-control rover:

The Core Components
The Controller (The Remote): A smartphone app connected via Bluetooth. When you press a button on the app's screen, it sends a simple text character over the air (e.g., 'F' for forward, 'B' for back).

The Communicator (The Ear): A Bluetooth module (like the popular HC-05 or HC-06) wired to the Arduino. It receives the wireless signal and sends the text character to the Arduino using Serial communication (RX/TX pins).

The Brain (The Microcontroller): Your Arduino (or ESP8266/ESP32). It constantly reads the Serial port. When it sees an 'F', it triggers a specific block of code to move forward.

The Muscle (Motor Driver): Just like your line-following car, an L298N or similar motor driver takes the low-power logic signals from the Arduino and uses them to switch high-power battery voltage to the motors.

The Actuators: Two or four DC motors attached to the wheels.

How the Logic Works (Differential Steering)
To steer a standard two-wheel-drive (or tank-tread) robot, you don't use a steering wheel. You use "differential steering"—changing the direction of the left and right wheels relative to each other:

Forward ('F'): Left Motor Forward + Right Motor Forward

Backward ('B'): Left Motor Reverse + Right Motor Reverse

Left Turn ('L'): Left Motor Reverse + Right Motor Forward (This causes the car to spin in place to the left)

Right Turn ('R'): Left Motor Forward + Right Motor Reverse (Spins in place to the right)

Stop ('S'): Both motors off.
