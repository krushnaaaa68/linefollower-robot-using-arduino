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
WORKING CODE :
// ----------------------------------------------------------
// Line Follower Robot (BO Motor + L298N + IR Array)
// Made for Armageddon 2025 – by Krishna Bule
// ----------------------------------------------------------

/* ----- PIN CONFIGURATION ----- */
#define ENA 9       // L298N Enable A (Left motor speed)
#define ENB 10      // L298N Enable B (Right motor speed)

#define IN1 2       // Left motor forward
#define IN2 3       // Left motor backward
#define IN3 4       // Right motor forward
#define IN4 5       // Right motor backward

// IR Sensor Inputs (5-sensor array)
#define S1 A0       // Left-most
#define S2 A1
#define S3 A2       // Center
#define S4 A3
#define S5 A4       // Right-most

/* ----- BASE SPEEDS ----- */
int baseSpeed = 130;     // Normal forward speed
int turnSpeed = 180;     // Speed used during turns

/* ----- THRESHOLD ----- */
int threshold = 500;     // IR value to detect black/white

/* ---------------------------------------------------------- */

void setup() {
  pinMode(ENA, OUTPUT);
  pinMode(ENB, OUTPUT);
  pinMode(IN1, OUTPUT);
  pinMode(IN2, OUTPUT);
  pinMode(IN3, OUTPUT);
  pinMode(IN4, OUTPUT);

  pinMode(S1, INPUT);
  pinMode(S2, INPUT);
  pinMode(S3, INPUT);
  pinMode(S4, INPUT);
  pinMode(S5, INPUT);

  Serial.begin(9600);
}

/* ---------------------------------------------------------- */

void loop() {
  int s1 = analogRead(S1);
  int s2 = analogRead(S2);
  int s3 = analogRead(S3);
  int s4 = analogRead(S4);
  int s5 = analogRead(S5);

  // Convert to digital (0 = white, 1 = black)
  s1 = s1 > threshold ? 1 : 0;
  s2 = s2 > threshold ? 1 : 0;
  s3 = s3 > threshold ? 1 : 0;
  s4 = s4 > threshold ? 1 : 0;
  s5 = s5 > threshold ? 1 : 0;

  // FORWARD
  if (s3 == 1 && s2 == 0 && s4 == 0) {
    forward();
  }

  // SLIGHT LEFT
  else if (s2 == 1 && s3 == 1) {
    slightLeft();
  }

  // SLIGHT RIGHT
  else if (s4 == 1 && s3 == 1) {
    slightRight();
  }

  // HARD LEFT
  else if (s1 == 1) {
    hardLeft();
  }

  // HARD RIGHT
  else if (s5 == 1) {
    hardRight();
  }

  // STOP if nothing is detected (lost line)
  else {
    stopRobot();
  }
}

/* ---------------------------------------------------------- */
/*               MOTOR CONTROL FUNCTIONS                      */
/* ---------------------------------------------------------- */

void forward() {
  analogWrite(ENA, baseSpeed);
  analogWrite(ENB, baseSpeed);

  digitalWrite(IN1, HIGH);
  digitalWrite(IN2, LOW);

  digitalWrite(IN3, HIGH);
  digitalWrite(IN4, LOW);
}

void slightLeft() {
  analogWrite(ENA, baseSpeed - 40);
  analogWrite(ENB, baseSpeed + 20);

  digitalWrite(IN1, HIGH);
  digitalWrite(IN2, LOW);

  digitalWrite(IN3, HIGH);
  digitalWrite(IN4, LOW);
}

void slightRight() {
  analogWrite(ENA, baseSpeed + 20);
  analogWrite(ENB, baseSpeed - 40);

  digitalWrite(IN1, HIGH);
  digitalWrite(IN2, LOW);

  digitalWrite(IN3, HIGH);
  digitalWrite(IN4, LOW);
}

void hardLeft() {
  analogWrite(ENA, 0);
  analogWrite(ENB, turnSpeed);

  digitalWrite(IN1, LOW);
  digitalWrite(IN2, HIGH);

  digitalWrite(IN3, HIGH);
  digitalWrite(IN4, LOW);
}

void hardRight() {
  analogWrite(ENA, turnSpeed);
  analogWrite(ENB, 0);

  digitalWrite(IN1, HIGH);
  digitalWrite(IN2, LOW);

  digitalWrite(IN3, LOW);
  digitalWrite(IN4, HIGH);
}

void stopRobot() {
  analogWrite(ENA, 0);
  analogWrite(ENB, 0);

  digitalWrite(IN1, LOW);
  digitalWrite(IN2, LOW);

  digitalWrite(IN3, LOW);
  digitalWrite(IN4, LOW);
}

