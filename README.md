Line Follower Robot – Rmageddon 2025 (Tech Event Project)
🚀 A fast and stable Line Follower Robot built for the rmageddon 2025 college tech event.

This robot uses an IR sensor array for line detection and controls two BO motors via an L298N motor driver, powered by a Li-Po battery.

🔥 Features

Smooth line following on black track

IR sensor array for accurate detection

BO motors for fast and lightweight motion

L298N motor driver for bidirectional control

Li-Po battery for high current output

Simple, low-cost, and easy to build

🧰 Technologies & Components
# Components List

1. Arduino uno
2. BO Gear Motors x 2
3. L298N Motor Driver
4. IR Sensor Array (5-line / 6-line / 8-line)
5. Li-Po Battery (7.4V 2S recommended)
6. Acrylic 2-wheel chassis
7. Wheels x 2
8. Jumper Wires (Male-Male, Male-Female)
9. Switch for power control
10. Battery holder / Velcro mount
11. Screws, spacers, nuts
s
🧠 Working Principle

The IR sensor array continuously detects the position of the black line beneath the robot.
Based on this, the microcontroller identifies:

Robot is on track

Robot is moving left

Robot is moving right

It then adjusts the motor speeds using a simple error-control algorithm (Basic or PID).
